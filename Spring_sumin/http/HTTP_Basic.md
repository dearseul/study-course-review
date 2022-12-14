# HTTP 기본 (11~15)

## 모든 것이 HTTP
* HTTP 메시지에 모든 것을 전송
    - 서버 간에 데이터를 주고 받을 때 대부분 HTTP 사용
    - 거의 모든 형태의 데이터 전송 가능
    - JSON, XML 등
    
* 기반 프로토콜
    - TCP : HTTP/1.1, HTTP/2
    - UDP : HTTP/3
    - 현재 HTTP/1.1 주로 사용

* HTTP 특징
    - 클라이언트 서버 구조
    - 무상태 프로토콜(스테이스리스), 비연결성
    - HTTP 메시지
    - 단순함
    
## 클라이언트 서버 구조
* Request Response 구조
* 클라이언트는 서버에 요청을 보내고, 응답을 대기
* 서버가 요청에 대한 결과를 만들어서 응답

## 무상태 프로토콜 (스테이스리스)
* 서버가 클라이언트의 상태를 보존하지 않음
* 장점 : 서버 확장성 높음 (스케일 아웃)
* 단점 : 클라이언트가 추가 데이터 전송

- stateful, stateless 차이
    - 상태 유지 : 항상 같은 서버가 유지
    - 무상태 : 수평 확장에 유리함. 
        - 갑자기 고객이 증가해도 점원 대거 투입 가능
        - 갑자기 클라이언트의 요청이 확 증가해도 서버를 대거 투입할 수 있음
        - 무한한 서버 증설이 가능
    
- 무상태 한계
    - 상태 유지 (예. 로그인) 해야 하는 경우에는?
    - 로그인 한 사용자의 경우 로그인 했다는 상태를 서버에 유지해야 함
    - 일반적으로 브라우저 쿠키와 서버 세션 등을 사용해서 유지
    - 상태 유지는 최소한으로 사용
    
## 비연결성
* 특징
    - HTTP는 기본이 연결을 유지하지 않는 모델
    - 일반적으로 초 단위의 이하의 빠른 속도로 응답
    - 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
        - 예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지 않음
    - 서버 자원을 효율적으로 사용 가능    
    
- 한계와 극복
    - TCP/IP 연결을 새로 맺어야 함
    - 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 이미지 등 수많은 자원들이 다운로드
    - 지금은 HTTP 지속 연결로 문제 해결
    - HTTP/2, HTTP/3에서 더 많은 최적화
    
* 스테이스리스를 기억하자
    - 같은 시간에 맞추어 발생하는 대용량 트래픽
        - 예) 선착순 이벤트, 명절 ktx 예약 등
    
## HTTP 메시지
* HTTP 메서드
    - GET, POST, PUT, DELETE 
    - GET : 리소스 조회 / POST : 요청 내역 처리
    
