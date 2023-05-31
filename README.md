# 2주차 주간보고서

### Rest API이란?

정보들이 주고 받아지는데 있어 개발자들 사이에 널리 쓰이는 일종의 형식(약속)이다. REST라는 형식을 사용하는 API라고 생각하면 된다. RESTful하게 만든 API는 협업을 할 때 동료 개발자가 요청을 보내는 주소만으로도 대략 무슨 요청인지 파악 가능하기 때문에 특별한 이유가 없다면 지키는 것이 좋다.

- REST의 구성요소
    1. 자원(URI)
    server에 존재하는 자원을 구별하는 ID가 URI이고, client는 URI를 이용해서 요청을 server에 보낸다.
    2. 행위(Method)
    HTTP 프로토콜 Method를 사용해서 CRUD를 표현한다.
    
        ```
        Create - 데이터 생성(POST)
        Read - 데이터 조회(GET)
        Update - 데이터 갱신(PUT-전체 갱신, PATCH-일부 갱신)
        Delete - 데이터 삭제(DELETE)
        
        ```
    3. 표현(Representation of Resource)
    client와 server가 데이터를 주고받는 형태로 보통 JSON, XML 포맷을 사용한다.  
- 설계 규칙
    1. URI는 명사를 사용하고, 대문자보단 소문자를 사용한다.
    2. '/'로 계층 관계를 표현한다.
    3. 언더바(\_)대신 하이픈(\-)을 사용한다.
    4. 파일 확장자는 URI에 포함하지 않는다.
    
    ```
    <https://velog.io/kikingki/img.png> (X)
    <https://velog.io/kikingki/img> (O)
    ```
    
    5. 행위를 포함하지 않는다.
    
    ```
    <https://velog.io/kikingki/create-post> (X)
    <https://velog.io/kikingki/post> (O)
    ```
    
    ---

    ### HTTP 통신 과정
    
    ![ref.https://www.cloudflare.com/ko-kr/learning/ssl/what-is-ssl/](https://www.cloudflare.com/img/learning/security/glossary/what-is-ssl/http-vs-https.svg)
    
    ref.[SSL이란 무엇입니까?](https://www.cloudflare.com/ko-kr/learning/ssl/what-is-ssl/)
    
    HTTP는 암호화되지 않고, HTTPS는 HTTP에 SSL 인증서가 추가되어 암호화된 통신이 가능하다.
    
    --- 
    ### www.naver.com을 주소창에 치면 어떻게 될까요?
    
    > 
    > 
    > 
    > *대기열, 캐싱, DNS, 라우팅, ARP, 초기연결을 거쳐 컨텐츠를 다운받게 되고 이 후 브라우저렌더링 과정을 거쳐 네이버라는 화면이 나타나게 됩니다.  또한 이러한 과정이 캡슐화, 비캡슐화 과정을 거쳐서 이뤄지게 됩니다.*
    > 
    
- 캐싱
    - 파일 복사본을 캐시 또는 임시 저장 위치에 저장하여 빠르게 액세스할 수 있도록 하는 프로세스입니다.
    - 데이터를 접근하는 시간이 오래 걸리거나 값을 다시 계산하는 시간을 절약하고 싶을 때 사용합니다.
    - 브라우저 캐시와 공유 프록시 캐시가 있습니다.
    - 컴퓨터 메모리의 캐시를 확인한 후 캐시미스가 일어나면 DNS 서버로 요청을 전달합니다.
- DNS(Domain Name System)
    - 사람이 잘 외우지 못하는 IP 주소를 대신해 Domain Name을 매핑해주는 서버입니다.
    - DNS 조회는 www.naver.com에 DNS 쿼리가 오면 [Root DNS]→ [.com DNS] → [.naver DNS] → [.www DNS] 과정을 거쳐 완벽한 주소를 찾아 IP 주소를 매핑합니다.
- 라우팅
    - IP 주소를 찾아가는 과정으로 라우팅 테이블, 서브 네트워크 등을 홉바이홉 통신으로 IP 주소를 찾습니다.
    - 라우팅 테이블은 게이트웨이와 모든 목적지에 대해 해당 목적지에 도달하기 위해 거쳐야하는 다음 라우터의 정보를 담고 있습니다.
    - 게이트웨이는 서로 다른 통신망, 프로토콜을 사용하는 네트워크 간의 통신을 가능하게 하는 관문 역할을 합니다.
- ARP(Address Resolution Protocol)
    - 찾아낸 IP(논리 주소)를 바탕으로 APR를 통해 MAC 주소(물리적인 주소)를 찾습니다.
    - ‘ARP Request 브로드캐스트’를 보내면 해당하는 IP 주소를 갖고 있는 장치가 ‘ARP reply 유니캐스트’로 MAC 주소를 응답해줍니다.
    - 역변환은 RARP(Reverse Address Resolution Protocol)
- 초기 연결
    - TCP는 3 Way-Handshake으로 연결을 설정하고, 4 Way-Handshake으로 연결을 종료합니다.
    - 신뢰성있는 데이터 전송이 필요할 때 TCP가 사용됩니다. 간단한 데이터나 동영상 데이터같은 경우엔 빠른 속도를 제공하는 비연결형 프로토콜 UDP를 사용합니다.
- 콘텐츠 다운로드
    - 브라우저는 서버로부터의 응답을 수신합니다.
- 캡슐화와 비캡슐화
    - 각 계층별로 헤더 혹은 트레일러를 삽입하는 캡슐화 과정을 거쳐 전달되고, 캡슐화된 데이터의 계층별 헤더를 제거하는 비캡슐화 과정을 거칩니다.
    </br>
#### Reference
[www.naver.com을 주소창에 치면 어떻게 될까요?](https://blog.naver.com/jhc9639/222700552159)

### API 가이드 문서 작성
 - 목적: 솔루션 확산 
 - 수신자:클라이언트 개발팀
 - 내용: 운영중인 sw의 활용도 제공 API 문서 작성
    - 접속자 수 API
    - 로그인 요청 수 API
    - 게시글 작성 수 API