# https
- HyperText Transfer Protocol over Secure Socket Layer
- HTTP의 보안이 강화된 버전(Secure Socket Layer가 추가된 버전)
- HTTP의 기본 포트는 80, HTTPS는 443

## 적용 및 이용
- 인증서 발급 및 적용 전
1. SSL 인증서 신청 : 사이트 정보 + 사이트 공개키를 인증기관에 전달
2. SSL 인증서 생성 : 전달받은 정보를 인증기관 개인키를 이용해 암호화하여 인증서 생성
3. SSL 인증서 발급 : 사이트에 인증서 저장(예: Nginx에 SSL 인증서 등록)  
   (신뢰된 인증기관의 공개키는 브라우저에 저장되어 있는 상태)

- 인증서 발급 및 적용 후
4. 사이트 최초 접근 : 이용자(Client)가 사이트 최초 접속 요청 시(Handshake) 사이트로부터 SSL 인증서를 전달 받음
5. 사이트 정보 / 사이트 공개키 복호화 : 신뢰된 인증기관의 경우, SSL 인증서를 브라우저에 인증기관 공개키가 있으므로, 이를 이용하여 사이트 정보 + 사이트 공개키 획득  
   (신뢰된 인증기관의 인증서가 아닌 경우 브라우저에서 경고 문구 등이 표시될 수 있음)
6. 대칭키 암호화 : 앞으로 사이트와의 통신에 이용할 대칭키를 사이트 공개키를 이용해 암호화
7. 대칭키 전달 : 사이트로 암호화된 대칭키 전달
8. 대칭키 복호화 : 사이트 개인키를 이용해 대칭키 획득
9. 암호화 통신 : 대칭키를 이용해 사이트와 이용자간의 암호화된 통신 진행

## 참조
- [HTTPS 란 무엇입니까?](https://www.ssl.com/ko/%EC%9E%90%EC%A3%BC-%EB%AC%BB%EB%8A%94-%EC%A7%88%EB%AC%B8/https-%EB%9E%80/)
- [SSL 통신과정 한 눈에 보기!](https://blog.naver.com/ssl_study/30151160122)
- [[Network/네트워크] HTTP & HTTPS - 정의, 특징, 흐름](https://velog.io/@yanghl98/Network%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-HTTP-HTTPS)
- [Advantages to Using TLS 1.3: FASTER, More Efficient, More Secure](https://embeddedcomputing.com/technology/security/advantages-to-using-tls-1-3-faster-more-efficient-more-secure)
- [Why Is TLS 1.3 Better And Safer Than TLS 1.2?](https://www.appviewx.com/blogs/why-is-tls-1-3-better-and-safer-than-tls-1-2/)