# RAG (Retrieval-Augmented Generation) 정리

## 개요

- 대형 언어 모델(LLM)이 외부 지식 기반에서 관련 정보를 검색, 활용(기존에는 학습 데이터만 이용)
- 별도 구축한 외부 데이터베이스나 문서에서 검색 후, 해당 정보를 포함한 증강된 입력을 바탕으로 답변을 생성
- 장점 : 최신 정보 반영, 도메인 특화 지식 활용, 환각 현상 감소
- 이용 사례 : 고객 지원 챗봇, 기업 내부 문서 검색, 의료/법률 도메인 지식 기반 Q\&A, 콘텐츠 생성 보조

## 주요 구성 및 동작 과정

1. **외부 데이터 생성 및 인덱싱**
    - 외부 문서, 데이터, API 등 다양한 데이터 소스를 숫자 벡터(임베딩)로 변환해 벡터 DB에 저장
2. **정보 검색(Retrieval)**
    - 사용자 질문을 벡터화하여 벡터 DB에서 관련도가 높은 문서를 검색
3. **프롬프트 증강(Augmentation)**
    - LLM에 사용자 질문과 함께 검색된 문서 내용을 포함한 증강된 입력을 구성
4. **응답 생성(Generation)**
    - 증강된 입력을 바탕으로 LLM이 더욱 정확하고 최신의 답변 생성
5. **외부 데이터 갱신**
    - 외부 데이터가 오래되면 주기적으로 임베딩 및 데이터 갱신 진행

## 장점

- LLM 단독 사용 대비 최신 정보 반영 가능
- 도메인 전문 지식 적용 용이
- AI 허위정보(환각 현상) 생성 감소
- 빈번한 모델 재학습 불필요로 비용 절감
- 투명성 제고(참고 문서 출처 제공 가능)

***

# 참고 링크

- AWS: [What is RAG (Retrieval-Augmented Generation)](https://aws.amazon.com/what-is/retrieval-augmented-generation)
- Google Cloud: [What is Retrieval-Augmented Generation (RAG)](https://cloud.google.com/use-cases/retrieval-augmented-generation)
- Wikipedia: [Retrieval-augmented generation](https://en.wikipedia.org/wiki/Retrieval-augmented_generation)
- NVIDIA Blog: [What Is Retrieval-Augmented Generation aka RAG](https://blogs.nvidia.com/blog/what-is-retrieval-augmented-generation)
- IBM: [What is RAG (Retrieval Augmented Generation)](https://www.ibm.com/think/topics/retrieval-augmented-generation)
- Weaviate Blog: [Introduction to Retrieval Augmented Generation (RAG)](https://weaviate.io/blog/introduction-to-rag)
- [DeepLearning.AI RAG Course](https://www.deeplearning.ai/courses/retrieval-augmented-generation-rag)
