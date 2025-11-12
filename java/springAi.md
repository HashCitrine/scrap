# Spring AI
![spring-ai](https://images.ctfassets.net/mnrwi97vnhts/4mda205vy509Dx3vGkMwFr/af520e66dc79fb80cd1bc129a11d6d23/spring-ai-integration-diagram-3.svg)  
Spring 기반 프로젝트에서 AI 서비스와 통합하기 위한 여러 방안을 제공하는 프로젝트(패키지)

## 주요 제공 기능
- AI 모델 지원  
  : Open AI와 같은 외부 서비스를 이용하거나 Ollama 등을 이용해 직접 설치한 모델을 이용하는 등 다양한 AI 모델 연계 방안을 제공(채팅, 임베딩, 이미지, 오디오 등등)
- 다양한 유형의 데이터 입력 지원(`Prompt`)  
  : 텍스트, 이미지, 음성, 영상 등의 데이터를 입력 방안 제공
- 결과 출력 구조체(POJO) 지원(`StructuredOutputConverter`)  
  : 모델 결과를 출력할 때 POJO로 매핑
- 다양한 벡터 데이터 베이스 지원

## 개인적인 생각
- 기존 국내 개발자들의 기본적인 백엔드 개발 스택이 Java, Spring 에 머물러 있음  
  → 기존 개발자들이 AI 생태계로 진입하여 AI Engineer로 거듭나는데 좋은 발판이자 도구가 될 수 있을 것
- 그러나 모델 개발 및 데이터 분석 시에 Python 기반으로 구성된 시스템을 이용하여 진행해오고 있는 상황에서, Java 기술 스택을 채택하는 경우가 있을지 의문
  - 시스템 성능상 이점을 원한다면 Go, Rust 등의 대안이 더 효과적일 수 있음(Spring AI와 같은 방안이 제공되고 있는지는 확인 필요)
  - 어지간한 성능적 효율이 필요한 상황이 아니라면, AI 업종에서는 Python 기반으로 시스템을 통합하는 것이 유지보수 측면에서 나을 수 있음
  - User Client와 연계하여 이용하는 상황에서도 Javascript(React 기반) 쪽이 우세한 상황
  - Spring AI를 어떤 상황에서 채택하는 것이 유리할지 고민이 필요할 것 같음  
    (직접 모델을 다루지는 않지만, 기존에 Java 인력으로만 구성된 조직에서 AI 활용 서비스를 개발하고자 하는 경우 등...) 

## 참고
- [spring-ai reference](https://docs.spring.io/spring-ai/reference/api/index.html)
