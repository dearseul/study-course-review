## 스프링 DB 접근 기술
스프링 데이터 엑세스
- H2 데이터 베이스 설치
- 순수 Jdbc
- 스프링 JdbcTemplate
- JPA
- 스프링 데이터 JPA


H2 데이터베이스 설치
개발이나 테스트 용도로 가볍고 편리한 DB, 웹 화면 제공

- http://www.h2database.com
- 다운로드 및 설치
- h2 데이터베이스 버전은 스프링 부트 버전에 맞춘다. 
- 권한 주기: chmod 755 h2.sh (윈도우 사용자는 x) 
- 실행: ./h2.sh (윈도우 사용자는 h2.bat) 데이터베이스 파일 생성 방법
- jdbc:h2:~/test (최초 한번)\
- ~/test.mv.db 파일 생성 확인 
- 이후부터는 jdbc:h2:tcp://localhost/~/test 이렇게 접속