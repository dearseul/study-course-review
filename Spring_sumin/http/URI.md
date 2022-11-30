# URI와 웹 브라우저 요청 흐름 (09~10)

## URI
- URI(Resource Identifier) 안에 URL(Resource Locator)와 URN(Resource Name)이 있음.
### URI 뜻
- Uniform : 리소스 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것
- Identifier : 다른 항목과 구분하는데 필요한 정보
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음.
### URL 문법
- schem://host:port/path?query=~
- schem 
    - 주로 프로토콜 사용
    - 프로토콜이란 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
- host
    - 호스트명
    - 도메인 명 또는 IP 주소 직접 입력
- path
    - 리소스 경로, 계층적 구조
    
## 웹 브라우저 요청 흐름
### HTTP 메시지 전송
1. 웹 브라우저가 HTTP 메시지 생성
2. SOCKET 라이브러리를 통해 전달 (TCP/IP 연결 후 데이터 전달)
3. TCP/IP 패킷 생성, HTTP 메시지 포함
4. 서버는 TCP/IP 껍데기를 까서 메시지를 꺼내 처리