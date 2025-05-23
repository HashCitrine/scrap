# Multimodal RAG
- Multimodal : 여러 타입의 데이터를 이해하는 기술
- Reasoning : 추론
- Optimization : 최적화
  1. Math : 수학적
  2. Rationale : 인지적

- RAG(Retrieval Augmented Generation) : 
  1. Embedding : 서로 다른 차원의 데이터를 통합하여 모델이 이용할 수 있도록 변환 및 저장
  

- VLM : Vision-Language Model

# Vision
- Classification
- Object Detection
- Segmentation   
  -> `Prompt Focusing`(Detail) 의 단계가 될 수 있음 : 수위 조절 (`with more detailed captions and grounding.`)
  ![image](https://github.com/user-attachments/assets/48180923-b739-4885-921d-dc26d993b81d)

# LLM
- Top P : 대상의 추천 확률의 커트라인 (0.3이면 30% 추천도 이상인 값을 대상으로 함)
- Temperature : 대상이 될 수 있는 값 중, 대상으로 이용할 값의 선정에 랜덤성을 줌
  -> 값이 낮을 수록 확률(추천)이 높은 대상을 선택 (즉, 응답도 거의 일정해짐)
- ChatGPT, gemini 등의 서비스를 통해 직접적으로 설정하여 이용할 수는 없음 (API 이용하면 가능)


# Model
- [VILA](https://nvlabs.github.io/VILA/)
- YOLO V5 이후에 Classification + Localization(비전 내 대상 분리) 가능해짐 -> 2019년
- [COSMOS](https://www.nvidia.com/en-us/ai/cosmos/)
