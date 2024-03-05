# OOP
- Object-oriented programming(객체 지향 프로그래밍)
- 코드의 변경을 최소화하고 유지보수를 용이하게 하기 위해 고안된 개발 방법론
- 객체 : 실재하는 대상으로, 이를 표현하기 위한 속성과 기능을 가지고 있음
- Class : 객체를 구현하기 위한 설계도로서, 변수(속성)과 함수(기능)를 가지고 있음

## 4대 원칙
1. 추상화
- 객체의 어떤 성질, 공통성, 본질을 추출한 것
- 예시) 이동 수단으로서 자동차와 오토바이는  
  핸들(손잡이), 바퀴, 시트(안장) 등의 공통된 속성을  
  시동을 걸기, 앞으로 가기, 뒤로 가기, 멈추기 등의 공통된 기능을 가지고 있음
- abstract, interface 등을 통해 속성/기능 선언

2. 상속
- 같은 속성과 기능을 가진 객체들이, 해당 속성/기능을 반복적으로 선언하지 않고 재사용 가능하도록 함
- extends, implements(interface)

3. 다형성
- 어떤 객체의 속성/기능을 객체의 상황에 따라 다양하게 변경될 수 있음
- 상속한 부모의 함수(기능)의 수행 내용을 변경할 수 있음(override)
- 객체 특정 기능이 여러 상황(매개변수)에 따라 다른 역할을 수행할 수 있음(overload)

4. 캡슐화
- 객체의 고유한 속성/기능이 외부의 영향을 받아 변경되지 않도록 보호/은닉하는 것
- 접근제한자(public, protected, private)를 통해 구현

## 참고
- [객체 지향 프로그래밍의 4가지 특징ㅣ추상화, 상속, 다형성, 캡슐화](https://www.codestates.com/blog/content/%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%8A%B9%EC%A7%95)
- [자바스크립트 객체지향 프로그래밍](https://poiemaweb.com/js-object-oriented-programming)