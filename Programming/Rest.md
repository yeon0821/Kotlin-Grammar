# Rest

------

- HTTP URI를 통해 자원을 명시하고, `HTTP Method (POST, GET, PUT, DELETE)`를 통해 해당 자원에 대한 `CRUD OPERATION`을 적용하는 것을 의미한다.
- 즉, REST는 자원 기반의 구조 (ROA: Resource Oriented Architecture) 설계의 중심에 Resoure가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.
- **웹의 모든 자원에 고유한 ID인 HTTP URI 를 부여한다.**

------

# 📖 REST의 구성

- 자원(Resource) - URL
- 행위(Verb) - Http Method
- 표현(Representations)

1. **자원 (Resource) URL**

- 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.

- 자원을 구별하는 ID는 `/orders/order_id/1` 와 같은 HTTP URI 이다.

  **2. 행위 (Verb) - Http Method**

- HTTP 프로토콜의 Method를 사용한다.

- HTTP 프로토콜은 `GET`, `POST`, `PUT`, `DELETE`와 같은 메서드를 제공한다.

  **3. 표현 (Representaion of Resource)**

- Client가 자원의 상태 (정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답 (Representation)을 보낸다

- REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타낼 수 있다.

- 현재는 JSON으로 주고 받는 것이 대부분이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f149600a-9f43-4dd0-bea6-2bd3667d712f/Untitled.png)

------

# 🔍**REST 특징**

**a. 클라이언트 / 서버 구조**

- 클라이언트는 유저와 관련된 처리를, 서버는 REST API를 제공함으로써 각각의 역활이 확실하게 구분되고 일괄적인 인터페이스로 분리되어 작동할 수 있게 한다
- REST Server: API를 제공하고 비지니스 로직 처리 및 저장을 책임진다.
- Client: 사용자 인증이나 context (세션, 로그인 정보) 등을 직접 관리하고 책임진다.
- 서로 간 의존성이 줄어든다.

**b. 무상태성 (Stateless)**

- REST는 HTTP의 특성을 이용하기 떄문에 무상태성을 갖는다.
- 즉 서버에서 어떤 작업을 하기 위해 상태정보를 기억할 필요가 없고 들어온 요청에 대해 처리만 해주면 되기 때문에 구현이 쉽고 단순해진다.

**c. 캐시 처리 가능 (Cacheable)**

- HTTP라는 기존 웹표준을 사용하는 REST의 특징 덕분에 기본 웹에서 사용하는 인프라를 그대로 사용 가능하다.
- 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
- 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상 시킬 수 있다.

**d. 자체 표현 구조 (Self - descriptiveness)**

- JSON을 이용한 메시지 포멧을 이용하여 직관적으로 이해할 수 있고 REST API 메시지만으로 그 요청이 어떤 행위를 하는지 알 수 있다.

**e. 계층화 (Layered System)**

- 클라이언트와 서버가 분리되어 있기 때문에 중간에 프록시 서버, 암호화 계층 등 중간매체를 사용할 수 있어 자유도가 높다

**f. 유니폼 인터페이스 (Uniform)**

- Uniform Interface는 Http 표준에만 따른다면 모든 플랫폼에서 사용이 가능하며, URI로 지정한 리소스에 대한 조작을 가능하게 하는 아키텍쳐 스타일을 말한다
- URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행
- 즉, 특정 언어나  기술에 종속되지 않는다.

------

# 😣 **REST의 단점들**

1. REST는 point-to-point 통신모델을 기본으로 한다. 따라서 서버와 클라이언트가 연결을 맺고 상호작용해야하는 어플리케이션의 개발에는 적당하지 않다.
2. REST는 URI, HTTP 이용한 아키텍처링 방법에 대한 내용만을 담고 있다. 보안과 통신규약 정책 같은 것은 전혀다루지 않는다. 따라서 개발자는 통신과 정책에 대한 설계와 구현을 도맡아서 진행해야 한다.
3. HTTP에 상당히 의존적이다. REST는 설계 원리이기 때문에 HTTP와는 상관없이 다른 프로토콜에서도 구현할 수 있기는 하지만 자연스러운 개발이 힘들다. 다만 REST를 사용하는 이유가 대부분의 서비스가 웹으로 통합되는 상황이기에 큰 단점이 아니게 되었다.
4. CRUD 4가지 메소드만 제공한다. 대부분의 일들을 처리할 수 있지만, 4가지 메소드 만으로 처리하기엔 모호한 표현이 있다.