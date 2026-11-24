# DeepCrossAttention (DCA) — 트랜스포머의 층 간 정보 재사용

DeepCrossAttention은 트랜스포머 각 층에서 이전 층의 출력을 토큰별로 다르게 섞어 쓰는 구조다. Heddes 외가 ICML 2025에서 발표했고, Google Research가 2026년 11월 23일 블로그에서 구조와 실험 결과를 소개했다. [ICML 2025 논문](https://proceedings.mlr.press/v267/heddes25a.html) · [Google Research 블로그](https://research.google/blog/supercharging-transformer-residual-connections/)

## 동작 원리

1. **표준 잔차 연결**은 현재 입력 `x`에 층의 출력 `F(x)`를 더한다. 층을 거칠수록 이전 출력이 하나의 잔차 스트림에 합쳐지므로, 뒤쪽 층에서 특정 층의 표현에 개별적으로 가중치를 주기 어렵다.
2. **DCA의 층별 가중합**은 모델 입력과 앞선 층의 출력을 모은 뒤, 학습된 기본 가중치에 현재 토큰의 표현에서 계산한 값을 더해 섞는다. 토큰마다 어떤 층의 정보를 얼마나 가져오는지가 달라진다.
3. **Q·K·V 분리**는 같은 층 출력 묶음에 세 개의 독립적인 가중합 모듈을 적용해 Query, Key, Value의 입력을 각각 만든다. 이렇게 만든 Q·K·V로 시퀀스 안에서 기존 masked multi-head attention을 수행한다. [논문 §3 및 그림 4](https://raw.githubusercontent.com/mlresearch/v267/main/assets/heddes25a/heddes25a.pdf#page=4)

이전 층 출력을 개별적으로 보관하고 읽으면 메모리 대역폭 부담이 커진다. 논문의 `k-DCA`는 모델 입력과 최근 `k`개 층의 출력을 개별 항으로 두고, 그 사이의 층 출력은 하나의 합으로 묶는다. [논문 §3.1](https://raw.githubusercontent.com/mlresearch/v267/main/assets/heddes25a/heddes25a.pdf#page=4)

## 실험 결과 읽기

언어 모델 실험의 기준은 검증 perplexity(PPL)다. 낮을수록 평가 데이터에서 실제 다음 토큰에 더 높은 확률을 부여했다는 뜻이다.

| 항목 | 보고된 결과 | 실험 조건·출처 |
| --- | --- | --- |
| 목표 PPL까지 학습 스텝 | 최대 **80% 감소** | C4·LM1B에서 표준 트랜스포머가 도달한 PPL을 최대 약 1/5의 스텝으로 달성했다. [Google Research](https://research.google/blog/supercharging-transformer-residual-connections/) |
| 목표 PPL까지 실제 학습 시간 | 약 **1/3** | LM1B 24층 실험에서 2-DCA는 기준 모델 시간의 0.33배에 기준 PPL 15.14에 도달했다. 초당 처리량은 표준 모델 8.14배치, 2-DCA 5.39배치였다. [논문 표 1](https://raw.githubusercontent.com/mlresearch/v267/main/assets/heddes25a/heddes25a.pdf#page=7) |
| 목표 품질에 필요한 모델 크기 | 공개 글 요약 **30~40% 감소**, LM1B 사례 **약 29% 감소** | 같은 폭에서 PPL 14 미만을 달성한 30층 DCA가 42층 표준 모델보다 더 낮은 PPL을 기록했다. [Google Research](https://research.google/blog/supercharging-transformer-residual-connections/) · [논문 그림 6](https://raw.githubusercontent.com/mlresearch/v267/main/assets/heddes25a/heddes25a.pdf#page=6) |
| DCA 모듈의 추가 파라미터 | LM1B 6층 예시에서 **약 0.16%** | 표준 모델 49.65M, DCA 49.73M으로 약 8만 개가 증가했다. [논문 표 5](https://raw.githubusercontent.com/mlresearch/v267/main/assets/heddes25a/heddes25a.pdf#page=8) |
| 사전학습 모델에 적용 | 추가 학습 후 PPL **0.19 개선** | LM1B 6층 모델에 DCA를 끼운 직후 두 모델의 PPL은 18.98이었다. 6만 스텝을 더 학습한 뒤 DCA는 18.79, 기존 구조를 이어 학습한 모델은 18.96이었다. [논문 표 4](https://raw.githubusercontent.com/mlresearch/v267/main/assets/heddes25a/heddes25a.pdf#page=7) |

학습 스텝 80% 감소와 실제 시간 약 3배 단축은 각 실험에서 목표 PPL에 도달할 때까지의 수치다. 같은 모델에 DCA를 붙였을 때 늘어나는 파라미터와, 층 수를 줄여 목표 품질을 맞췄을 때 절약하는 파라미터도 각각 다른 비교에서 나온다. C4 규모 실험은 최대 약 449M 파라미터까지 평가했으며, 실제 학습 시간과 메모리 비용은 모델 크기와 보관하는 층 출력 수에 따라 달라진다. [논문 §5](https://raw.githubusercontent.com/mlresearch/v267/main/assets/heddes25a/heddes25a.pdf#page=7)
