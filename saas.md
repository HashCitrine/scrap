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

## AWS Service
- Cloud9 : 클라우드 기반의 웹 브라우저 통합 개발 환경으로 코드 작성 및 디버깅을 지원합니다.
- CloudFormation : AWS 리소스를 코드로 정의하고 관리할 수 있는 인프라 자동화 도구입니다.
- ECR : Docker 이미지와 같은 컨테이너 이미지를 저장하고 관리하는 서비스입니다.
- EC2 : 가상 서버를 제공하여 사용자가 필요에 따라 컴퓨팅 용량을 조정할 수 있게 합니다.
- S3 : 객체 스토리지 서비스로, 대용량 데이터를 안전하게 저장하고 관리할 수 있습니다.
- VPC : 가상 사설 클라우드를 생성하여 AWS 리소스를 격리된 네트워크 환경에서 운영할 수 있게 합니다.
- CloudWatch : AWS 리소스와 애플리케이션의 모니터링 및 로그 관리를 위한 서비스입니다.

### 주요 특화 서비스
- **ECS** : 컨테이너화된 애플리케이션을 쉽게 배포하고 관리할 수 있는 서비스입니다. -> EC2와 같은 별도 서버가 아닌, 컨테이너 단위로 서비스 배포하여 이용 가능
- **App2Container** : .net, JAVA 어플리케이션에 한해서 컨테이너화 지원 도구(CLI) -> 기존 자바가 돌아가고 있는 서버 환경에 설치하여 컨테이너화 및 CI/CD 파이프라인으로서 이용할 수 있음 (CloudFormation 설정에 따라 ECR -> ECS 이용하여 자동 배포 진행)
- **Amanzon Q** : 코드 작업 지원 도구(아마 LLM 기반? Gemini CLI, Claude Code, Cursor 등과 같은 역할)



## ECS 관련 AWS 서비스 정리
### ECS cluster
- 각 노드 서버에 Agent를 두고 instance를 관리함
- ECS Task : ECS Cluster에서의 최소 실행 단위(K8S의 Pod와 같은 단위인 듯?) -> `Task Definition` 으로 배포 설정 진행
- 하나의 task 당 10개의 컨테이너까지 이용 가능
- 빈팩(`(bin packing problem`) 전략, 메모리 가용 영역에 따른 배포 등을 설정하여 `비용 최적화` auto scaling 가능 -> `ECS Task Rebalancing`
- Fargate : EC2와 달리 서버리스 서비스 -> 위 기반에서 ECS 이용 가능 (비용 절약)
#### 배포 과정
1. task definition 업데이트 (`.json`)
2. task definition 적용 : `aws ecs register-task-definition --cli-input-json file://${FILE_NAME}.json`
   - 적용 내용 조회 : `aws ecs describe-task-definition --task-definition ${DEFINITION_NAME}`
3. task definition 기반으로 배포 : `aws ecs create-service`
- (예시)
```
export UI_TARGET_GROUP_ARN=$(aws elbv2 describe-target-groups --names ui-application \
 --query 'TargetGroups[0].TargetGroupArn' --output text)

aws ecs create-service \
 --cluster retail-store-ecs-cluster \
 --service-name ui \
 --task-definition retail-store-ecs-ui \
 --desired-count 2 \
 --launch-type FARGATE \
 --load-balancers targetGroupArn=${UI_TARGET_GROUP_ARN},containerName=application,containerPort=8080 \
 --network-configuration "awsvpcConfiguration={subnets=[${PRIVATE_SUBNET1},${PRIVATE_SUBNET2}],securityGroups=[${UI_SG_ID}],assignPublicIp=DISABLED}" 
```

### Auto Scailing Policies
- Traget Tracking : cpu 사용률 등을 기반으로 auto Scailing
- Step Scaling : 자원 사용률 이용 위반(임계값) 비율에 따라 auto Scailing
- alb drain : 배포 과정 중 트레픽을 일정 시간 유지하도록 하는 옵션
- 가용성 <-> 배포 속도 (availability <-> speed) 사이에서 밸런스를 잡아야 함

### Cluster Scailing
- 컨테이너 단위가 아닌 cluster 단위로 스케일링 진행
- `CapacityProviderReservation` 을 추적하여 동작 -> 필요한 인스턴스와 현재 실행 중인 인스턴스를 계산하며 동작

### Cloud Watch 
- 서비스들의 log 관리 (`Prometheus` 등과 같은 역할)
- 각 서비스에서 `awslogs` 드라이버를 이용해 cloudwatch로 로그 전달 가능
- awsfirelens 드라이버 활용해 fluentD 등과 연계 가능
- 관리 시 Managed Grafana, Prometheus 등의 서비스와 함께 사용
- `container insights` : metrics 시각화 도구(자원 사용량 전반에 대한 기본 대시보드 제공)

### Observability
- 관측 능력
- log(타임스탬프 기록), metrics(시계열 수치), traces(전체 흐름의 분산 이벤트 기록 - 가시화)

### Service Discovery
- 추가적인 인프라 발생
- DNS 기반으로 기본적인 디스커버리만 제공 -> 메트릭 제공이 다소 협소해짐

### Service Connect
- 다양한 서비스들의 연계된 메트릭을 제공

## Build & Deploy 도구
- jenkins, spinnaker 등

## 배포 전략
- rolling : 점진적인 배포, 배포 과정 중 유지할 인스턴스 수 등에 대해 설정 필요
- blue & green : 새로운 버전의 배포가 완료되면, 구 버전의 인스턴스(컨테이너, task)로 트레픽만 전환(로드밸런서 활용)

## 보안 부분
- [공동 책임 모델](https://aws.amazon.com/ko/compliance/shared-responsibility-model/)
- task role, task execution role
- IAM(Identity and Access Management) 권한 관리

### 인프라 리소스 테스트 도구
1. [hey](https://github.com/rakyll/hey) : 트래픽 부하
2. [stress](https://github.com/resurrecting-open-source-projects/stress) : CPU, Memory, Disk 리소스 부하


## 배포 자동화(CI/CD)
- Task Definition 관리 방안 필요(매번 새롭게 적용해야 하므로, 별도로 파일을 관리하거나 CI/CD 파이프라인에 녹여서 관리하는 등의 방안 필요)
