# ElasticsearchAlternatives
ElasticSearch와 유사한 기능을 제공하는 대안 방안 정리

# Algolia
![image](https://github.com/user-attachments/assets/db1c83d8-d51b-4204-916e-fe1c529e8402)
- [site](https://www.algolia.com/)
- E-Commerce 분야에서 주로 활용
- SaaS 형태로 서비스 제공
- 검색에 AI를 활용하여 연관 데이터를 추천, 연결하고 개인화 기능 제공  
  ![image](https://github.com/user-attachments/assets/1c6c1ce7-d01f-4a42-a9ed-247639744ac2) 
- 기타
  - Pinecone([site](https://www.pinecone.io/)라는 vector database 를 붙혀 사용하는 경우가 있는 것 같음(확인 필요)

# Typesense
![image](https://github.com/user-attachments/assets/105a2b73-d299-445e-a208-3b96697df268)
- [site](https://typesense.org/)
- 오픈 소스이지만 [typesense cloud](https://cloud.typesense.org/?_gl=1*15mey6n*_gcl_au*MTk1NDAxMzk0MC4xNzM5MTYwNDkw*_ga*NjU5NDUwOTk0LjE3MzkxNjA0OTA.*_ga_XWJNP9CSY7*MTczOTE2MjkwNC4yLjAuMTczOTE2MjkwNC42MC4wLjA.&_ga=2.174811746.1523168302.1739160490-659450994.1739160490)를 통해 SaaS 서비스도 제공
- 공식 사이트에서 경쟁 서비스들과 비교한 데이터를 메인 페이지에서 제공하는 부분이 인상 깊음([ref](https://typesense.org/typesense-vs-algolia-vs-elasticsearch-vs-meilisearch/))
- 오타 허용, 이미지/ 음성 검색, 사용자 정의 필드 기준 필터링, 자체적인 서비스 클러스터링 지원 등등의 기능 제공(상세 내용 확인 필요, [ref](https://typesense.org/docs/overview/features.html))

# Meilisearch
![image](https://github.com/user-attachments/assets/f0d12cac-2b98-46d5-92cf-37ab30d9ec06)
- [site](https://www.meilisearch.com/)
- 오픈 소스이지만 typesense 처럼 SaaS 서비스도 제공
- Algolia처럼 AI를 활용하여 서비스 제공
- 여러 가지 키워드를 이용한 검색, 언어 자동 감지 등등의 기능

# Apache Solr
![image](https://github.com/user-attachments/assets/98043695-37a3-4210-a65f-87b13f8f909f)
- [site](https://solr.apache.org/)
- 오픈 소스
- 실시간 인덱싱, 전체 텍스트 검색 기능, 대용량 트레픽에 대한 최적화, Docker/K8S 연계성 등등의 기능 제공

# ParadeDB
![image](https://github.com/user-attachments/assets/e0f4a1b9-5fb0-4b0a-9b0b-26b9020555ca)
- [site](https://www.paradedb.com/)
- Postgresql 기반으로 검색 및 집계 기능(쿼리)을 이용할 수 있도록 만들어진 서비스
- 원하는 데이터 저장을 위한 DB로 Postgresql를 이용할 경우에만 사용할 수 있는 대안이지만, 별도의 서비스를 구성할 필요 없이 기존의 Postgresql을 이용 방법을 그대로 유지하면서 필요한 기능을 추가로 이용할 수 있는 장점으로 예상됨
- [이용 가이드](https://docs.paradedb.com/documentation/overview) 

# 참고
- [2025년 최고의 Elasticsearch 대안 10가지](https://clickup.com/ko/blog/119350/elasticsearch-alternatives)
- [Algolia를 사용한 검색 기능 구현하기](https://develogger.kro.kr/blog/LKHcoding/125)
