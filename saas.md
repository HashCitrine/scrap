# SaaS 교육
(2025.08.01 ~ 05) 메가존클라우드, AWS와 함께하는 SaaS Readiness Program 진행 내용 메모


## SaaS 전환의 필요성
- Software as a Service
- 서비스형 소프트웨어
- 주로 구독형 서비스
- 기기에 설치하지 않고 온라인으로 엑세스(웹 기반)
- 소프트웨어 라이센스

- IaaS : Infrastructure as a Service
- PaaS : Platform as a Service

- 기존 서비스에 대한 `Plugin` 형태로 제공되기도 함(ex: vscode 기반으로 동작하는 cursor 등)
- 전통 소프트웨어 대비 (일회성 수익, 인력 중심 확장, 낮은 영업이익률 <-> 반본 구독 수익, 기술 중심 확장, 높은 영업이익률)

### 특징(장단점)
- 인터넷 기반 : 접근 및 이탈 용이
- Metric 확보 중요 : Promethous, [Push Gateway](https://github.com/prometheus/pushgateway)
  - 미터링(요금 계산) 및 테넌트(서비스 이용 주체) 구분 중요 -> Tier 구분 (Basic/Pro/Premium 등과 같은 요금 정책 등)
- 트랜드 및 대외 인지도, 이미지 등이 중요
- 업데이트 및 장애 예방을 위해 Blue/Green 배포 방식을 적용
- [SLO, SLI](https://www.atlassian.com/ko/incident-management/kpis/sla-vs-slo-vs-sli) 영향 증가
- 서비스 및 인프라 자동화
- [Cognito](https://docs.aws.amazon.com/ko_kr/cognito/latest/developerguide/what-is-amazon-cognito.html)
- B2C


