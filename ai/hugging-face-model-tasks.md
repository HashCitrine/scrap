# 개요
hugging face의 model tasks 정리


## Multimodal Task
![multimodal](https://github.com/user-attachments/assets/bd9ffe92-4ab1-4955-81f8-efb78515c3b7)

- **Visual Question Answering (VQA)**  
  이미지와 자연어 질문을 입력으로 받아, 이미지에 대한 질문에 대한 답변을 생성합니다. (예: "이 사진에 고양이가 몇 마리 있나요?".​)
- **Image Captioning**  
  이미지를 입력으로 받아, 이미지의 내용을 설명하는 자연어 문장을 생성합니다.​
- **Image-Text Retrieval**  
   이미지와 텍스트를 입력으로 받아, 서로 관련된 이미지-텍스트 쌍을 찾거나, 텍스트에 가장 잘 맞는 이미지를 검색합니다.​
- **Visual Grounding**  
  이미지와 자연어 문장을 입력으로 받아, 문장에서 언급된 객체나 영역을 이미지 내에서 박스로 표시합니다.​
- **Multimodal Emotion Recognition (MER)**  
  오디오와 텍스트, 또는 이미지와 텍스트 등 여러 모달리티를 결합해 감정을 인식합니다.​
- **Text-to-Speech / Speech-to-Text**  
  텍스트와 오디오를 결합해 음성 생성 또는 음성 인식을 수행합니다.​
- **Multimodal Chat**  
  이미지, 오디오, 비디오 등 다양한 입력을 텍스트와 함께 받아 대화를 생성하거나 응답합니다.​
- **Image Generation from Text**  
  텍스트 설명을 입력으로 받아, 해당 설명에 맞는 이미지를 생성합니다.​

### 주요 모델 예시
- **BLIP, BLIP-VQA**
  이미지와 텍스트를 결합해 질문에 답변하거나 캡션을 생성합니다.​
- **CLIP**
  이미지와 텍스트를 같은 임베딩 공간에 매핑해, 이미지-텍스트 검색이나 분류에 활용합니다.​
- **ViLT (Vision-and-Language Transformer)**
  이미지와 텍스트를 결합해 다양한 vision-language task를 수행합니다.​
- **IDEFICS, IDEFICS 2**
  이미지와 텍스트를 결합해 질문에 답변하거나 이미지 설명을 생성합니다.​
- **Phi-4-multimodal**
  음성과 텍스트를 결합해 multimodal task를 수행합니다.​

### 활용 예시
- 이미지와 질문을 입력해 답변을 받는 VQA 시스템
- 이미지에 대한 설명을 자동으로 생성하는 캡션 생성기
- 이미지와 텍스트를 결합해 감정을 인식하는 시스템
- 음성과 텍스트를 결합해 음성 인식 또는 생성하는 시스템

### 참고
- https://huggingface.co/learn/computer-vision-course/unit4/multimodal-models/tasks-models-part1

## Computer Vision
![Computer Vision](https://github.com/user-attachments/assets/078dcb87-af94-40a1-9cb0-23d9c02b6962)

### 주요 컴퓨터 비전 작업
- **이미지 분류 (Image Classification)**  
  이미지 전체에 대해 하나의 레이블(카테고리)을 할당합니다. 예를 들어, 사진이 강아지인지 고양이인지 분류하는 작업이며, ViT, DeiT, ConvNeXt 같은 모델들이 종종 사용됩니다.

- **객체 탐지 (Object Detection)**  
  이미지 내 여러 객체들의 위치(바운딩 박스)와 종류를 찾습니다. 대표적인 모델로는 DETR, YOLOv8 등이 있습니다.

- **이미지 분할 (Image Segmentation)**  
  이미지 내 각 픽셀 단위로 의미 있는 영역을 분할하는 작업입니다. 즉, 객체를 정확한 형태로 분리하는 것으로, Mask2Former, SegFormer 같은 모델이 사용됩니다.

- **포즈 추정 (Pose Estimation)**  
  사람이나 물체의 주요 관절 및 위치를 키포인트로 추정하는 작업입니다. 예를 들어 사람의 자세를 분석하는 데 사용됩니다.

- **시각적 질문응답 (Visual Question Answering, VQA)**  
  이미지에 대한 자연어 질문에 답하는 작업으로, 이미지와 텍스트를 함께 분석해야 합니다.

- **이상 탐지 (Anomaly Detection)**  
  정상적인 패턴과 다르게 보이는 이미지 내 이상징후를 탐지합니다.

- **장면 이해 (Scene Understanding)**  
  3D 공간 구조나 이미지 내 객체 간 관계 등을 인지하는 고급 작업입니다.

- **3D 재구성 (3D Reconstruction)**  
  여러 뷰로부터 3D 모델을 생성합니다.

- **비디오 이해 (Video Understanding)**  
  비디오의 행동 인식이나 분류 작업을 수행합니다.

- **광학 문자 인식 (OCR, Optical Character Recognition)**  
  이미지에서 문자 영역을 인식하고 텍스트로 변환하는 작업입니다.

- **이미지 태그 및 속성 예측 (Image Tagging & Attribute Prediction)**  
  이미지에 대해 키워드 태그를 붙이거나 특정 속성을 추론합니다.

- **이미지 생성 (Image Generation)**  
  텍스트 설명을 기반으로 이미지를 생성하거나 이미지 변환을 수행합니다.


### 주요 모델 예시 
- **Vision Transformer(ViT)**

### 참고
- https://huggingface.co/blog/CongPTIT/cv


## Natural Language Processing

### 주요 NLP 작업

- **텍스트 분류 (Text Classification)**  
  주어진 문장이 어떤 카테고리에 속하는지를 판단하는 작업입니다. 예를 들어, 감정 분석(Sentiment Analysis)은 긍정, 부정, 중립 등으로 텍스트 감정을 분류합니다.

- **질문 응답 (Question Answering)**  
  주어진 문서나 문맥에서 사용자의 질문에 대해 답변을 찾아주는 작업입니다.

- **언어 모델링 및 텍스트 생성 (Language Modeling / Text Generation)**  
  주어진 텍스트 기반으로 다음에 올 단어나 문장을 예측하고, 자연스러운 텍스트를 생성합니다. 대표적으로 GPT 계열이 여기에 속합니다.

- **개체명 인식 (Named Entity Recognition, NER)**  
  텍스트에서 사람, 장소, 날짜, 조직명 등 특정 개체를 인식하여 추출합니다.

- **요약 (Text Summarization)**  
  긴 텍스트를 간결하게 요약한 짧은 텍스트로 변환하는 작업입니다.

- **기계 번역 (Machine Translation)**  
  한 언어로 된 텍스트를 다른 언어로 자동 번역합니다.

- **자연어 추론 (Natural Language Inference, NLI)**  
  두 문장의 관계를 판단하는 작업으로, 전제와 가설 간에 참, 거짓, 중립 관계를 분류합니다.

- **토큰화 및 문장 단위 처리 (Tokenization & Sentence Parsing)**  
  텍스트를 단어 혹은 토큰 단위로 분할하고, 문장 구조를 분석하는 작업입니다.

- **코어퍼런스 해소 (Coreference Resolution)**  
  텍스트에서 동일한 대상을 가리키는 여러 표현을 연결하는 작업입니다.

- **제로샷 학습 (Zero-shot Learning)**  
  학습하지 않은 새로운 태스크에도 사전 학습된 모델이 직접 일반화하여 수행하는 작업입니다.

### 주요 모델 예시
- **BERT**
- **RoBERTa**
- **GPT**
- **T5**
