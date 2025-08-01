# SaaS 교육
(2025.08.01 ~ 05) 메가존클라우드, AWS와 함께하는 SaaS Readiness Program 진행 내용 메모

## SaaS 전환의 필요성
### 개요
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
  - 미터링(요금 계산) 및 테넌트(세입자) 구분 중요 -> Tier 구분 (Basic/Pro/Premium 등과 같은 요금 정책 등)
- 트랜드 및 대외 인지도, 이미지 등이 중요
- 업데이트 및 장애 예방을 위해 Blue/Green 배포 방식을 적용
- [SLO, SLI](https://www.atlassian.com/ko/incident-management/kpis/sla-vs-slo-vs-sli) 영향 증가
- 서비스 및 인프라 자동화
- [Cognito](https://docs.aws.amazon.com/ko_kr/cognito/latest/developerguide/what-is-amazon-cognito.html)
- B2C

### SaaS Bussiness (원가 / 마케팅)
- 이탈률 공식(churn Rate), 순증가 고객 공식(Net New Customers), 전체 고객 수 변화 공식(이번달 말 고객수)
- Net New : 신규 고객

### SaaS 보안
- 테넌트(세입자) 격리
- 인증 및 권한

### Tenant Vs Tier
- 다른 테넌트로부터 데이터, 어플리케이션을 안전하게 분리 필요 -> 데이터 유출, 성능 저하 등의 문제 방지를 위함
- Tier 격리 : 테넌트의 요구사항에 따라 격리 수준 구분 (원하는 형태의 `공유`도 필요)



## 교육 자료 (Notion)
- 참조 : https://www.notion.so/23af7bc8c4d480d999acc4e6ad6a1091?v=23ef7bc8c4d480d78ca9000c1ee43dbe

### 기존 리눅스와 공유하는 컨테이너 컨셉 기능
◾ **cgroups (control groups)**: 프로세스 그룹에 대한 자원(CPU, 메모리, I/O 등) 할당 및 제한 기능

◾ **Namespaces** (네임스페이스): 프로세스, 네트워크, 마운트 지점 등 시스템 자원을 격리하는 기능

◾ **Bind Mount** (바인드 마운트): 특정 디렉토리를 파일 시스템의 다른 위치에 그대로 연결하는 기술

◾ **OverlayFS** (오버레이FS): 여러 개의 파일 시스템 레이어를 하나로 합쳐서 마치 하나의 파일 시스템처럼 보이게 하는 기술  


◾ **capability :** 'root' 사용자에게 부여된 강력한 권한들을 더 세분화하여 필요한 최소한의 권한만 컨테이너에 부여하게 (네트워크 인터페이스를 설정하는 권한은 주고, 시스템 파일에 접근하는 권한은 주지 않는 식)


◾ **seccomp (Secure Computing mode):** 컨테이너가 불필요하거나 잠재적으로 위험할 수 있는 시스템 콜을 사용하지 못하도록 막아 보안 취약점 공격의 가능성을 줄입니다.

◾ **LSM (Linux Security Module):** SELinux와 같은 강화된 접근 제어 정책을 구현하여 컨테이너에 대한 보안을 더욱 견고하게 만듭니다.

### 레이어 줄이기
- Dockerfile 구성 시 `RUN` 단위로 이미지 레이어를 구성하며, 이를 줄이기 위해 명령어를 한 줄로 구성하기도 함(`&&` 활용)
- (예시) [nginx Dockerfile](https://github.com/nginx/docker-nginx/blob/master/stable/debian/Dockerfile)


## docker compose 활용하여 scale out
```
docker compose up --scale flask_app=2
```
- `--scale` 옵션을 이용해서 compose 에 정의된 서비스(예시의 `flask_app`)를 scale out 할 수 있음
