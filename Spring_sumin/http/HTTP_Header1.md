# HTTP 헤더1 - 일반 헤더 (27~34)

## HTTP 헤더 개요
* 용도
    - HTTP 전송에 필요한 모든 부가정보
    - 표준 헤더가 매우 많고 필요시 임의 헤더 추가 가능
* HTTP BODY
    - 메시지 본문을 통해 표현 데이터 전달
    - 메시지 본문을 페이로드라고도 함
    - 표현은 요청이나 응답에 전달할 실제 데이타
    - 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
        - 데이터 유형, 길이 등
    
## 표현
- Content-Type
  - 표현 데이터의 형식 설명
- Content-Encoding
  - 표현 데이터 인코딩
  - 표현 데이터를 압축하기 위해 사용.
  - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
  - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
  - 예) gzip, identity
- Content-Language
  - 표현 언어의 자연 언어
- Content-Length
  - 표현 데이터의 길이. 바이트 단위
  
## 콘텐츠 협상
- 클라이언트가 선호하는 표현 요청
  - Accept : 클라이언트가 선호하는 미디어 타입 전달
  - Accept-Charset : 클라이언트가 선호하는 문자 인코딩
  - Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
  - Accept-Language : 클라이언트가 선호하는 자연 언어
- 협상 헤더는 요청시에만 사용  

### 협상과 우선순위1
- Quality Values(q) 값 사용
- 0~1 사이. 클수록 높은 순위. 생략시 1
- ex) Accept-Language:ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7

### 협상과 우선순위2
- 구체적인 것이 우선함
- Accept: text/*, text/plain, text/plain;format=flowed, */*
  - text/plain;format=flowed
  - text/plain
  - text/*
  - */*
  
### 협상과 우선순위3
- 구체적인 것을 기준으로 미디어 타입을 맞춤

## 전송 방식
- 단순 전송 : 데이터의 길이를 정확히 알 때 사용
- 압축 전송 : Content-Type을 추가로 넣어줌
- 분할 전송 : Transfer-Encoding:chunked을 추가로 넣어줌. Content-Length를 넣으면 안 됨.
- 범위 전송 : Content-Range를 추가로 넣어줌

## 일반 정보
- Form: 유저 에이전트의 이메일 정보
- Referer : 이전 웹 페이지 주소
  - 현재 요청된 페이지의 이전 웹 페이지 주소
  - Referer를 사용하여 유입 경로 분석 가능
- User-Agent
  - 클라이언트의 애플리케이션 정보 (웹 브라우저 정보 등)
  - 통계 정보
  - 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- Server
  - 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
  - 응답에서 사용
- Date
  - 메시지가 발생한 날짜와 시간
  - 응답에서 사용
  
## 특별한 정보
- Host
  - 요청한 호스트 정보 (도메인)
  - 요청에서 사용, 필수값.
  - 하나의 서버가 여러 도메인을 처리해야 할 때.
  - 하나의 IP 주소에 여러 도메인이 적용되어 있을 때
- Location
  - 페이지 리다이렉션
  - 웹 브라우저는 3xx 응답의 결과에 Lcoation 헤더가 있으면, Location 위치로 자동 이동
  - 201 (Created) : Location 값은 요청에 의해 생성된 리소스 URI
  - 3xx (Redirection) : Location 값은 요청을 자동으로 리디렉션 하기 위한 대상 리소스를 가리킴.
- Allow
  - 허용 가능한 HTTP 메서드
  - 405 (Method Not Allowed)에서 응답을 포함해야 함
  - Allow : GET, POST, PUT
- Retry-After
  - 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
  - 503 (Service-Unavailable) : 서비스가 언제까지 불능인지 알려줄 수 있음
  
## 인증
- Authorization : 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate
  - 리소스 접근시 필요한 인증 방법 정의
  - 401 Unauthorized 응답과 함께 사용

## 쿠키
- Set-Cookie : 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

### Stateless
- HTTP는 무상태 프로토콜임
- 클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어짐
- 클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못함
- 클라이언트와 서버는 서로 상태를 유지하지 않음.

### 쿠키
- 사용처
  - 사용자 로그인 세션 관리
  - 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
  - 네트워크 트래픽 추가 유발
  - 최소한의 정보만 사용 (세션 id, 인증 토큰)
  - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고
- 주의
  - 보안에 민감한 데이터는 저장하면 안 됨 (주민번호 등)
  
### 쿠키 - 생명 주기
- Set-Cookie : expires=~
  - 만료되면 쿠키 삭제
- Set-Cookie : max-age=~
  - 0이나 음수를 지정하면 쿠키 삭제
- 세션 쿠키 : 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지

### 쿠키 - 도메인
- 명시 : 명시한 문서 기준 도메인 + 서브 도메인 포함
  - domain = example.org를 지정해서 쿠키 생성하면, example.org는 물론이고 dev.example.org도 쿠키 접급
- 생략 : 현재 문서 기준 도메인만 적용
  - example.org에서 쿠키를 생성하고 domain 지정을 생략하면, example.org에서만 쿠키 접근, dev.example.org는 미접근
  
### 쿠키 - 경로
- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 path=/루트로 지정
- ex) path=/home

### 쿠키 - 보안
- Secure : https인 경우에만 전송
- HttpOnly : XSS 공격 방지. 자바스크립트에서 접근 불가. HTTP 전송에만 사용
- SameSite : 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송
