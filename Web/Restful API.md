# Restful API

> REST는 표현 상태 전송 을 나타냅니다. API(응용 프로그래밍 인터페이스)가 작동하는 방식을 설정하는 제약 조건 집합입니다. API가 RESTful이면 API가 REST 아키텍처를 준수한다는 의미입니다. 간단히 말해서 API에 관한 한 REST와 RESTful 사이에는 차이가 없습니다. REST는 제약 조건의 집합입니다. RESTful은 이러한 제약 조건을 준수하는 API를 나타냅니다. 웹 서비스, 응용 프로그램 및 소프트웨어에서 사용할 수 있습니다 .
> 

# REST(Representational State Transfer)란

## REST의 정의

- Representational State Transfer (대표적인 상태 전달)의 약자
- 월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
- REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일
- REST는 네트워크 상에서 Client 와 Server 사이의 통신 방식 중 하나

## 구체적인 개념

- HTTP URI (Uniform Resource Identifier)를 통해 자원 (Resource)를 명시하고, HTTP Method(Post, Get, Put, Delete) 를 통해 해당 자원에 대한 CRUD Operation 을 적용하는 것을 의미한다.
- 즉, `REST는 자원 기반의 구조`(ROA, Resource Oriented Architecture) 설계의 중심에 `Resource`가 있고, HTTP Method 를 통해 Resource 를 처리하도록 설계된 아키텍처를 의미한다
- 웹 사이트의 이미지, 텍스트 DB 내용 등의 모든 자원에 고유한 ID 인 `HTTP URI` 를 부여한다

---

## REST 장단점

### 장점

- 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화 해준다
- Hypermedia API 의 기본을 충실히 지키면서 범용성을 보장한다
- HTTP 프로토콜 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다

### 단점

- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URI 보다 Header 값이 어렵게 느껴짐
- 구형 브라우저가 아직 제데로 지원해주지 못하는 부분이 존재한다
    - PUT, DELETE 를 사용하지 못하는 점 (form 에 경우 <input type="hidden" name="_method" /> 로 줄 수 있다
    - pushState 를 지원하지 않는 점 ( history.pushState - 뒤로가기 )
- REST 방식에서 특정URL의 위치에서 뒤로가기를 실행할 때 해당URL이 아닌 다른URL로 이동해서 원하는 결과가 나오지 않을 수 있다.
    - **URI 를 통한 ServerSide Rendering 방식을 이용하게 된다면**
        - 메인 페이지 -> 보드 1 페이지 -> 보드 5 페이지 클릭 -> 뒤로가기 -> **보드 1 페이지**
    - **REST 방식을 이용하게 된다면**
        - 메인 페이지 -> 보드 1 페이지 -> 보드 5 페이지 클릭 -> 뒤로가기 -> **메인 페이지**

---

## REST 특징

- Server-Client(서버 클라이언트 구조)

- Stateless (무상태성)(cookie 를 이용해 session 을 서버에 저장했다면, rest 는 header 에 token 을 넣어 인증하고 세션을 저장하지 않는다)
    - 쿠키와 세션의 차이
        - 쿠키와 세션은 비슷한 역할을 하며, 동작 원리도 비슷하다. 그 이유는 세션도 결국 쿠키를 사용하기 때문이다.
        - 큰 차이점은 `사용자의 정보가 저장되는 위치`이다. 쿠키는 `서버의 자원을 전혀 사용하지 않으며`, 세션은 `서버의 자원을 사용한다.`
        - REST 유저의 정보가 세션에 저장되지 않기 때문에 보안적인 측면에서 이점을 지닌다.
- Cacheable(캐시 처리 가능)
- Layered System (계층화)
- Code On Demand (option)
- Uniform Interface (인터페이스 일관성)

<aside>
💡 기본적으로 GET Method 에만 캐시기능이 있습니다.

예전에 접속한 브라우저인 경우 서버에 해당 자원을 요청하는 것이 아닌 로컬 캐시에 저장된 곳에서 가져와 속도를 올리는데에 사용하게 됩니다.

대표적으로 `<img src=””>` `<script src=””>` `<link src=””>`가 될 수 있습니다.

POST Method 에서는 캐시기능을 지원하지는 않지만, 헤더에 `Expires`와 `Cache-Control header` 를 이용하여 caching을 구현하여 응답할 수 있습니다.

PUT, DELETE는 해당되지 않습니다.

</aside>

## REST 가 필요한 이유

- 애플리케이션 분리 및 통합 (MSA = Micro Soft Service Application)
- 다양한 클라이언트의 등장
- 즉, 최근의 서버 프로그램은 다양한 브라우저와 안드로이드폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다
- MSA (Micro Service Application) 분산 서비스와 관련되어있다 ( api call 을 통한 데이터 처리 )

## REST 구성 요소

### A. 자원 (Resource) URI

- 모든 자원에 고유한 id 가 존재하고, 이 자원은 Server 에 존재한다
- 자원을 구별하는 id 는 'localhost:8080/user/:userId' 와 같은 HTTP URI 이다
- Client 는 URI 를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server 에 요청한다

### B. 행위 (Verb) : Http Method

- HTTP 프로토콜의 Method 를 사용한다
- HTTP 프로토콜은 GET, POST, PUT, DELETE, HEAD 와 같은 메서드를 제공한다
    
    ### GET
    
    서버에게 Resource를 보내도록 요청하는 데 사용한다. (서버의 Resource를 읽음)
    
    ### HEAD
    
    GET과 동일하지만 **서버에서 Body를 Return하지 않음**
    
    - Resource를 받지 않고 오직 찾기만을 원할 때 사용
    - object가 존재할 경우 응답의 상태 코드 확인할 때
    - 서버의 응답 헤더를 봄으로써 Resource가 수정되었는 지 확인
    
    ### PUT
    
    서버에서 문서를 쓸 때 사용(GET과 반대)
    
    - PUT 메서드는 서버가 **클라이언트가 보낸 요청의 Body를 확인**한다.
    - 요청된 URL에 정의된 **새로운 Resource를 생성**하기 위함
    - 요청된 URL이 존재할 경우 대체
    
    ### POST
    
    **서버에 인풋 데이터를 보내기 위함** (HTML form에 많이 사용)
    
    ### PUT vs POST
    
    - PUT은 서버의 Resource에 데이터를 저장하기 위한 용도
    - POST는 서버에 데이터를 보내기 위한 용도
    
    ### TRACE
    
    클라이언트로부터 Request Packet이 방화벽, Proxy Server, Gateway 등을 packet의 변조가 일어날 수 있는데, 이때 **서버에 도달했을 때의 최종 Packet의 Request Packet을 볼 수 있다.**
    
    - 즉, 원본 데이터와 서버에 도달했을 때의 비교본 데이터를 서버의 응답 Body를 통해 확인할 수 있다.
    - 요청의 최종 수신자는 반드시 **송신자에게 200(OK) 응답의 내용(Body)으로 수신한 메세지를 반송**해야 한다.
    - 최초 클라이언트의 요청에는 Body가 포함될 수 없다.
    
    ### OPTION
    
    타겟 서버의 지원 가능한 메서드들을 알아보기 위함
    
    ### DELETE
    
    - Resource를 삭제하도록 요청
    - 그러나 HTTP 규격에는 클라이언트의 요청도 서버가 무효화시킬 수 있도록 정의되어 있음
    - DELETE 메서드는 항상 보장되지는 않는다.

### C. 표현 (Representation of Resource)

- Client 가 자원의 상태(정보)에 대한 조작을 요청하면 Server 는 이에 적절한 응답표현(Representation) 을 보낸다.
    - HTTP Status Code를 통한 응답표현이 일반적이다.
- REST 에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation 으로 나타내어 질 수 있다
- 옛날에는 XML 이였지만 현대에는 JSON 으로 표현하고 있다

<aside>
💡 **REST API (Representational State Transfer Application Programming Interface)**

</aside>

- API 는 해당 어플리케이션을 제어할 수 있게 해주는 중간 인터페이스(연결점입니다)
- 예를들어 키보드라는 인터페이스를 통해 하드웨어어 입력을 해주는 기능을 해주는 것과 같습니다
- 영화 조회 서비스 API 를 통해 특정 명령만 내리면 해당 어플리케이션이 그에 맞는 기능을 수행줍니다

## HTTP Status Code

### 1XX (정보 제공)

| 코드 | 메시지 | 설명 |
| --- | --- | --- |
| 1XX | Information(정보) | 정보 교환 |
| 100 | Continue | 클라이언트로부터 일부 요청을 받았으니 나머지 요청 정보를 계속 보내주길 바람. (HTTTP 1.1에서 처음 등장) |
| 101 | Switching Protocols | 서버는 클라이언트의 요청대로 Upgrade 헤더를 따라 다른 프로토콜로 바꿀 것임 (HTTP 1.1에서 처음 등장) |

### 2XX (성공)

| 코드 | 메시지 | 설명 |
| --- | --- | --- |
| 2XX | Success(성공) | 데이터 전송이 성공적으로 이루어졌거나, 이해되었거나, 수락되었음 |
| 200 | OK | 오류 없이 전송 성공 |
| 202 | Accepted | 서버가 클라이언트의 요청을 수락함 |
| 203 | Non-authorized Information | 서버가 클라이언트 요구 중 일부만 전송 |
| 204 | Non Content | 클라이언트의 요구를 처리했으나 전송할 데이터가 없음 |
| 205 | Reset Content | 새 문서 없음. 하지만 브라우저는 문서 창을 리셋해야 함(브라우저가 CGI 폼 필드를 전부 지우도록 할 때 사용 됨) (HTTP 1.1에서 처음 등장) |
| 206 | Partial Content | 클라이언트가 Range 헤더와 함께 요청의 일부분을 보냈고 서버는 이를 수행했음 (HTTP 1.1에서 처음 등장) |

### 3XX (리다이렉션)

| 코드 | 메시지 | 설명 |
| --- | --- | --- |
| 3XX | Redirection(방향 바꿈) | 자료의 위치가 바뀌었음 |
| 300 | Multiple Choices | 최근에 옮겨진 데이터를 요청 |
| 301 | Moved Permanently | 요구한 데이터를 변경된 URL에서 찾았음 |
| 302 | Moved Permanently | 요구한 데이터가 변경된 URL에 있었음을 명시. 301과 비슷하지만 새 URL은 임시 저장 장소로 해석됨 |
| 303 | See Other | 요구한 데이터를 변경하지 않았기 때문에 문제가 있음 |
| 304 | Not modified | 클라이언트의 캐시에 이 문서가 저장되었고 선택적인 요청에 의해 수행됨 (보통 지정된 날짜보다 더 나중의 문서만을 보여주도록 하는 If-Modified-Since 헤더의 경우) |
| 305 | Use Proxy | 요청된 문서는 Location 헤더에 나열된 프록시를 통해 추출되어야 함 (HTTP 1.1에서 처음 등장) |
| 307 | Temporary Redirect | 자료가 임시적으로 옮겨짐 |

### 4XX (클라이언트 요청 오류)

| 코드 | 메시지 | 설명 |
| --- | --- | --- |
| 4XX | Client Error(클라이언트 오류) | 클라이언트 측의 오류. 주소를 잘못 입력하였거나 요청이 잘못되었음 |
| 400 | Bad Requeset | 요청 실패. 문법 상 오류가 있어서 서버가 요청사항을 이해하지 못함 |
| 401.1 | Unauthorized | 권한 없음(접속 실패). 서버에 로그온 하려는 요청사항이 서버에 들어있는 권한과 비교했을 떄 맞지 않음 |
| 401.2 | Unauthorized | 권한 없음(서버 설정으로 인한 접속 실패). 서버에 로그온 하려는 요청사항이 서버에 들어있는 권한과 비교했을 때 맞지 않음 |
| 401.3 | Unauthorized | 권한 없음(자원에 대한 ACL에 기인한 권한 없음). 클라이언트가 특정 자료에 접근할 수 없음 |
| 401.4 | Unauthorized | 권한 없음(필터에 의한 권한 부여 실패). 서버에 접속하는 사용자들을 확인하기 위해 설치한 필터 프로그램이 있음 |
| 401.5 | Unauthorized | 권한 없음(ISA PI/CGI 어플리케이션에 의한 권한부여 실패). 이용하려는 서버의 주소에 ISA PI나 CGI 프로그램이 설치되어 있고, 권한을 부여할 수 없음 |
| 402 | Payment Required | 예약됨 |
| 403.1 | Forbidden | 금지(실행접근 금지). 실행시키지 못하도록 되어 있는 디렉토리 내의 실행 파일을 실행하려고 하였음 |
| 403.2 | Forbidden | 금지(읽기접근 금지)/ 접근한 데릭토리에 가용한 기본 페이지가 없음 |
| 403.4 | Forbidden | 금지(SSL 필요함). 접근하려는 페이지가 SSL로 보안유지 되고 있음 |
| 403.5 | Forbidden | 금지(SSL 128 필요함). 페이지가 128비트의 SSL로 보안유지 되고 있음 |
| 403.6 | Forbidden | 금지(IP 주소 거부됨). 사용자가 허용되지 않은 IP로부터 접근함 |
| 403.7 | Forbidden | 금지(클라이언트 확인 필요). 클라이언트가 자료에 접근할 수 있는지 확인 요함 |
| 403.8 | Forbidden | 금지(사이트 접근 거부됨). 서버가 요청사항을 수행하고 있지 않거나, 해당 사이트에 접근하는 것이 허락되지 않음 |
| 403.9 | Forbidden | 접근금지(연결된 사용자 수 과다). 서버가 BUSY 상태에 있어서 요청을 수행할 수 없음 |
| 403.10 | Forbidden | 접근금지(설정이 확실하지 않음) |
| 403.11 | Forbidden | 접근금지(패스워드 변경됨). 잘못된 암호를 입력했음 |
| 403.12 | Forbidden | 접근금지(Mapper 접근 금지됨). 클라이언트 인증용 맵이 해당 웹 사이트에 접근하는 것이 거부됨 |
| 404 | Not Found | 문서를 찾을 수 없음. 서버가 요청한 파일이나 스크립트를 찾지 못함 |
| 405 | Method not allowed | 메서드 허용 안 됨. 요청 내용에 명시된 메서드를 수행하기 위한 해당 자원의 이용이 허용되지 않음 |
| 406 | Not Acceptable | 받아들일 수 없음 |
| 407 | Proxy Authentication Required | 프록시 서버의 인증이 필요함 |
| 408 | Request timeout | 요청 시간이 지남 |
| 409 | Conflict | 요청을 처리하는 데 문제가 있음. 보통 PUT 요청과 관계가 있다. 보통 다른 버전의 파일을 업로드할 경우 발생함 (HTTP1.1에서 새로 등장) |
| 410 | Gone | 영구적으로 사용할 수 없음 |
| 411 | Length Required | 클라이언트가 헤더에 Content-Length를 포함하지 않으면 서버가 처리할 수 없음 (HTTP 1.1에서 새로 등장) |
| 412 | Precondition Failed | 선결조건 실패. 헤더의 하나 이상의 선결조건을 서버에서 충족시킬 수 없음 |
| 413 | Request-URI too long | 요청한 URI가 너무 김 |
| 414 | Unsupported media type | 요청이 알려지지 않은 형태임. (HTTP 1.1에서 새로 등장) |
| 415 | Unsupported media type | 요청이 알려지지 않은 형태임. (HTTP 1.1에서 새로 등장) |

### 5XX (서버 응답 오류)

| 코드 | 메시지 | 설명 |
| --- | --- | --- |
| 5XX | Server Error(서버 오류) | 서버 측의 오류로 올바른 요청을 처리할 수 없음 |
| 500 | Internal Server Error | 서버 내부 오류 |
| 501 | Not Implemented | 필요한 기능이 서버에 구현되지 않았음 |
| 502 | Bad gateway | 게이트웨이 상태 나쁨 |
| 503 | Service Unavailable | 외부 서비스가 죽었거나 현재 멈춘 상태 또는 이용할 수 없는 서비스 |
| 504 | Gateway timeout | 프록시나 게이트웨이 역할을 하는 서버에서 볼 수 있음. 초기 서버가 원격 서버로부터 응답을 받을 수 없음. (HTTP 1.1에서 새로 등장) |
| 505 | HTTP Version Not Supported | 해당 HTTP 버전을 지원하지 않음 |
---

### REST API 정의

- REST 를 기반으로 서비스 API 를 구현한 것
- 최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.

### REST API 특징

- REST 기반으로 시스템을 분산해 확장성과 재사용을 높여 유지보수 및 운용을 편리하게 할 수 있다
- REST 는 HTTP 표준을 기반으로 구현하므로, HTTP 를 지원하는 프로그래밍언어로 클라이언트, 서버를 구현할 수 있다

---

### 기본 설계 규칙

- A. URI는 자원(Resource) 를 표현해야 한다
    - resource 는 명사
    - 소문자 복수형
    - GET /members/1
- B. 자원에 대한 행위는 HTTP Method (GET, PUT, PATCH, DELETE, POST 등)으로 표현한다
    - 1. URI 에 HTTP Method 가 들어가면 안된다
        - GET /members/delete/1 -> DELETE /members/1
    - 2. 어떤 행위(Behavior)나 행동(Action) 에 관해서 동사 표현이 들어가면 안된다
        - GET /members/insert/2 -> POST /members/2
        - GET /members/show/1 -> GET /members/1
- **슬래시 구분자(/) 는 계층 관계를 나타내는데 사용된다**
- **URI 마지막 문자로 슬래시(/) 를 포함하지 않는다**
- **대소문자 구분으로서 kebab case 형식을 사용한다 (team-board)**
    - 먹는 케밥에 꼬챙이를 낀 모습이며, 모두 소문자로 표현하며, 단어와 단어 사이에는 하이픈(-)를 사용합니다.
    - 스프링의 yml 파일이나 url 주소에서 주로 사용합니다.
    
    원문 : USER LOGIN LOG
    
    케밥식: user-login-log
    
- **밑줄(_ )은 URI에 사용하지 않는다.**
    - 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
- **URI 경로에는 소문자가 적합하다.**
    - URI 경로에 대문자 사용은 피하도록 한다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
- **파일확장자는 URI에 포함하지 않는다.**
    - REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
    - Accept header를 사용한다.
    - Ex) [http://restapi.example.com/members/soccer/345/photo.jpg](http://restapi.example.com/members/soccer/345/photo.jpg)
     (X)
    - Ex) GET / members/soccer/345/photo HTTP/1.1 Host: [restapi.example.com](http://restapi.example.com/) Accept: image/jpg (O)
- **리소스 간에는 연관 관계가 있는 경우**
    - /리소스명/리소스 ID/관계가 있는 다른 리소스명
    - Ex) GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
- **:id는 하나의 특정 resource를 나타내는 고유값**
    - Ex) student를 생성하는 route: POST /students
    - Ex) id=12인 student를 삭제하는 route: DELETE /students/12

---

# 면접용 요약

# RESTful

## RESTful의 개념

- RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
    - • 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.

## RESTful의 목적

- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- RESTful API를 구현하는 근본적인 목적이 퍼포먼스 향상에 있는게 아니라, 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는게 주 동기이니, 퍼포먼스가 중요한 상황에서는 굳이 RESTful API를 구현하실 필요는 없습니다.
- RESTful 하지 못한 경우
    - Ex1) CRUD 기능을 모두 POST로만 처리하는 API
    - Ex2) route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)
