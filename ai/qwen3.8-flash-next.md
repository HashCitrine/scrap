# Qwen3.8-Flash-Next — 모델 구조와 로컬 추론 벤치마크

Qwen3.8-Flash-Next는 Alibaba Qwen 팀이 차세대 Qwen 아키텍처를 미리 공개한 멀티모달 MoE 모델이다. Locally 영상에서 소개한 **193.2 tok/s**는 RTX 5080 16GB 한 장과 시스템 RAM 64GB를 사용해, Basalt에서 2비트급 가중치와 MTP를 켠 코딩 벤치마크의 디코딩 속도다. [원본 영상 2:46](https://youtu.be/LkLgzSLD844?t=166) · [RTX 5080 원본 벤치마크](https://www.reddit.com/r/LocalLLM/comments/1y0pydt/basalt_05_vs_strata_0155_qwen_38_fn_on_single/) · [Qwen 모델 카드](https://huggingface.co/Qwen/Qwen3.8-Flash-Next)

## 모델 구조

- **희소 MoE**는 본체 파라미터 125B 중 토큰당 6B를 활성화한다. 별도로 N-gram 임베딩 51B와 MTP 모듈 4B가 있다. 6B는 토큰당 연산에 참여하는 규모이며, 메모리를 산정할 때는 전체 가중치의 양자화 크기와 RAM·VRAM 배치를 봐야 한다. [모델 카드](https://huggingface.co/Qwen/Qwen3.8-Flash-Next#model-overview) · [기술 보고서](https://arxiv.org/abs/2608.30320)
- **Gated DeltaNet(GDN)과 Qwen Sparse Attention(QSA)**을 3:1로 배치한다. GDN은 과거 토큰 정보를 고정 크기 상태에 누적한다. QSA는 긴 입력을 블록 단위로 탐색해 관련 위치를 고르고, 선택한 위치에 어텐션을 적용한다. [공식 발표](https://www.alibabacloud.com/blog/qwen3-8-flash-next-a-new-architecture-towardsultimate-cost-efficiency_603501)
- **N-gram 임베딩**은 인접한 토큰 조합의 표현을 테이블에서 조회한다. 조회할 행을 미리 알 수 있어 테이블을 호스트 RAM에 두고 필요한 부분을 비동기로 가져올 수 있다. **Gated Residual**은 잔차 경로를 네 갈래로 확장하고 입력에 따라 각 경로에서 읽고 쓸 정보를 조절한다. [기술 보고서](https://arxiv.org/abs/2608.30320)
- 공개 가중치 **Qwen3.8-Flash-Next**의 기본 컨텍스트는 262,144토큰이며 최대 100만 토큰까지 확장할 수 있다. 관리형 API **Qwen3.8-Flash**는 기본 100만 토큰과 내장 도구를 제공한다. 공개 가중치에는 Qwen Community License 1.0이 적용된다. [모델 카드](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) · [공식 라이선스](https://huggingface.co/Qwen/Qwen3.8-Flash-Next/blob/main/LICENSE)

## RTX 5080에서 193.2 tok/s가 나온 조건

같은 PC에서 Basalt 0.5.0과 Strata 0.1.55에 동일한 코딩 프롬프트를 넣은 비교다. Ryzen 9900X, RTX 5080 16GB, 시스템 RAM 64GB에서 `IQ2_XS` 가중치와 MTP 드래프터, int8 KV 캐시를 사용했다. 아래는 프롬프트 캐시를 재사용하지 않고 **입력 65,536토큰과 출력 1,024토큰**으로 실행한 3회 중앙값이다. 런타임에 설정한 컨텍스트 창은 131,072토큰이었다. [원본 측정표](https://www.reddit.com/r/LocalLLM/comments/1y0pydt/basalt_05_vs_strata_0155_qwen_38_fn_on_single/)

| 지표 | Basalt 0.5.0 | Strata 0.1.55 |
| --- | ---: | ---: |
| 프리필 (입력 처리) | 4,589 tok/s | 3,785 tok/s |
| 디코딩 (출력 생성) | **193.2 tok/s** | 155.6 tok/s |
| 첫 토큰까지 (TTFT) | 14.36초 | 17.36초 |
| 전체 요청 시간 | 19.59초 | 23.94초 |

이 조건에서 Basalt는 출력 생성 속도가 약 24% 높았고, 전체 요청 시간은 약 18% 짧았다. 영상의 153 tok/s와 VRAM 15.7GB·시스템 RAM 54.1GB는 RTX 5080에서 `IQ3_S`로 돌린 별도의 코딩 세션에서 나온 수치다. [원본 측정표](https://www.reddit.com/r/LocalLLM/comments/1y0pydt/basalt_05_vs_strata_0155_qwen_38_fn_on_single/) · [영상 4:36](https://youtu.be/LkLgzSLD844?t=276) · [제작자 출처 목록](https://locallyexplains.site/qwen-3-8-flash-next-fastest-way-to-run/)

## 다른 로컬 실행 사례

영상에서 인용한 결과다. 런타임, 양자화, 프롬프트 길이가 서로 달라 GPU 간 성능 차이를 이 표만으로 판단하기 어렵다. [제작자 출처 목록](https://locallyexplains.site/qwen-3-8-flash-next-fastest-way-to-run/)

| 구성 | 런타임과 조건 | 디코딩 |
| --- | --- | ---: |
| RTX 3060 12GB + RAM 64GB | Strata, `Q2_0`, 입력 4,096토큰 | 42.9 tok/s |
| RTX 5060 Ti 16GB × 2 + RAM 64GB | Basalt, 4비트 NVFP4 | 102.4 tok/s |
| RTX 3090 24GB × 2 + RAM 256GB | Strata, 6비트, 약 120K 컨텍스트 | 72~86 tok/s |
| RTX 5090 32GB | Strata, `UD-Q5_K_XL`, MTP 활성화 | 79.1 tok/s |
| Mac Studio M5 Max 128GB | MTPLX, 코딩 작업, MTP 활성화 | 73.5 tok/s |
| AMD Strix Halo 128GB | Halogen, 짧은 단일 요청 | 94.3 tok/s |
| CPU 16 vCPU + RAM 128GB | llama.cpp, 1비트급 가중치 | 4.8 tok/s |

## 로컬에서 비교할 때 볼 항목

- **양자화와 메모리 배치.** 가중치 비트 수를 낮추면 가중치가 차지하는 공간과 읽기 대역폭이 줄어든다. 품질도 달라질 수 있으므로 실제 작업으로 확인한다. 가중치와 KV 캐시가 VRAM, 시스템 RAM, SSD 중 어디에 놓이는지도 함께 기록한다. [Basalt 문서](https://github.com/jesdga95/basalt) · [영상 6:50](https://youtu.be/LkLgzSLD844?t=410)
- **MTP(Multi-Token Prediction).** 드래프터가 다음 토큰 후보를 여러 개 만들고 본체가 한 번에 검증한다. 후보가 많이 채택될수록 디코딩에 필요한 본체 실행 횟수가 줄어든다. 영상의 M5 Max 코딩 사례는 같은 작업에서 MTP를 끄면 43.8 tok/s, 켜면 73.5 tok/s였다. [기술 보고서](https://arxiv.org/abs/2608.30320) · [영상 5:41](https://youtu.be/LkLgzSLD844?t=341)
- **비교 조건.** 같은 입력·출력 길이와 캐시 상태를 맞춘 뒤, 프리필·디코딩 속도와 함께 첫 토큰까지 걸린 시간, 전체 요청 시간, VRAM·RAM 사용량을 본다. 공식 가중치의 서버 배포 설정은 vLLM 레시피에서 하드웨어와 양자화 형식별로 확인할 수 있다. [원본 벤치마크](https://www.reddit.com/r/LocalLLM/comments/1y0pydt/basalt_05_vs_strata_0155_qwen_38_fn_on_single/) · [vLLM 배포 레시피](https://recipes.vllm.ai/Qwen/Qwen3.8-Flash-Next)
