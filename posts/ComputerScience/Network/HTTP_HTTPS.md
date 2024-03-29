---
created: 2021-03-21
modified: 2021-03-21
tags: [Network]
title: HTTP
author: Yo0oN
categories: [Network]
---

## 1. HTTP

HTTP는 Hypertext Transfer Protocol로, 서로 다른 시스템 사이에서 데이터를 주고받을 때 사용하는 '규칙'이다.

> Protocol? 두 사람이 대화를 할 때는 말이 필요하고, 말은 여러 문법이 있다. 네트워크에서는 말을 '네트워크 아키텍쳐'라 하고, 문법은 '프로토콜'이라 한다.

보통 HTTP를 통해 전송하는 데이터는 HTML, 이미지, 파일 등등이 있다.

클라이언트가 무언가를 달라고 *요청*할 때는 Request, 서버가 무언가를 줌으로 *응답*하는 것을 Response라 한다.

### 1-1. HTTP의 구조

프로토콜을 이용하여 데이터를 주고받을 때는 전송할 데이터와  그 데이터에 헤더를 추가하여 캡슐화 한 뒤 만들어진 패킷을 사용하여 주고받는다.    
HTTP는 크게 *HTTP Header*와 *Entity Body*로 이루어져 있다.

#### HTTP Header

HTTP Header는 3부분으로 이루어져 있다.    
1. Request Line (응답할 때는 Response Line)
```
HTTP Method/Request target/HTTP version
```
Header가 시작되는 부분으로 위와 같은 형태로 담겨있다.    
HTTP Method의 경우 해당 요청이 어떤 요청인지 알려준다. (1-2에서 설명)    

2. Message Header
```
Accept: 요청이 받을 수 있는 응답 Response 타입(ex. */*)
Accept-Encoding: 요청이 받을 수 있는 응답 인코딩 (ex.gzip, deflate)
Connection: 요청이 끝난후 Connection의 상태(ex. keep-alive)
Content-Type: body 타입(ex. application/json)
Content-Length: body 길이(ex. 257)
Host: 요청이 전송되는 target의 host(ex. google.com)
User-Agent: HTTPie/0.9.3
...
```
Message Header는 웹브라우저의 종류나 버전, body의 길이 등이 Key:Value 형태로 적혀있다.    

3. Blank Line
이부분은 말 그대로 공백인 줄로, Header와 Body를 구분하는데 사용된다.    

#### Entity Body

몸통부분은 상황에 따라 비어있을 수도 있지만 응답으로 돌아올 때 데이터가 담겨서 돌아오거나, POST 메소드를 이용하여 요청 시 데이터를 담아서 요청한다.    


### 1-2. HTTP의 메소드들

HTTP의 메소드에는 GET, POST, OPTIONS, PUT, DELETE가 있다.

#### GET

GET은 데이터를 서버로부터 리소스(데이터)를 받아올 때 사용한다.    
GET의 특징은 만약 요청 시 파라미터를 함께 보내야 한다면 URI에 함께 보인다.    
예를들어 6월 25일의 날씨를 조회하고 싶다면 `http://weather.com/weather?date=210625` 처럼 파라미터를 URI에서 볼 수 있게 된다.    
파라미터가 URI에 바로 보이도록 되어있다는 것은 파라미터를 HTTP Header에 담아 보낸다는 것인데, 이럴경우 Header의 길이가 제한되어 있어 보낼 수 있는 파라미터의 길이도 제한된다는 뜻이다. 그리고, 보안적인 문제가 있을 수 있다. (물론 바디에 담는다고 무조건 안전한건 아니다.)    
정상적으로 응답이 될 경우 응답 코드는 200(OK)이다.

#### POST

POST는 서버에 새로운 리소스를 생성할 때 사용된다.    
GET과는 다르게 파라미터를 전송할 때 HTTP Body에 담아서 하게된다. Body에 담아서 하게되면 길이의 제한이 없기 때문에 Header에 담을 때 보다 더 많은 양의 파라미터를 전송할 수 있다는 장점이 있다.    
정상적으로 응답이 될 경우 응답 코드는 201(Created)이다.

#### PUT

PUT의 경우 서버에 있던 기존 리소스를 수정할 때 사용된다. 만약 리소스가 없다면 새로운 리소스를 만들기도 한다.    
정상적으로 응답이 될 경우 응답 코드는 200(OK) 또는 204(No Content)이다.

#### DELETE

DELETE는 서버의 리소스를 삭제할 때 사용된다.    
정상적으로 응답이 될 경우 응답 코드는 200(OK), 202(Accepted) 등..이다.

#### OPTIONS

OPTIONS는 요청 URI에서 사용 가능한 메서드를 받아오는데 사용할 수 있다.    
이때는 HTTP 헤더에 `Allow: 사용 가능한 메서드들..` 같은 형태로 응답을 받게 된다.
    
### 1-3. idempotent?

사전을 찾아보면 *idempotent*는 '멱동성'이라고 나온다.     
그리고 이 특징을 가진 메서드들은 여러 번 호출 가능한 메서드이고, 호출시마다 결과가 동일해야 한다는 특징이 있다.

HTTP 메소드에서는 GET, HEAD, OPTIONS 등이 idempotent하며, POST는 그렇지 않다.    
POST의 경우 요청을 하면 할 때마다 서버에 새로운 리소스를 만들기 때문에 idempotent가 아니다.    
하지만 GET, HEAD, OPTIONS는 서버의 리소스 상태를 변경하지 않으며 리소스를 조회하거나 메타데이터를 검색하기 때문에 idempotent가 맞다.    
그리고 PUT의 경우 리소스를 업데이트 하고, DELETE는 삭제에 사용되는데, 만약 처음 업데이트 또는 삭제 한다면 리소스가 변경되겠지만 계속 같은값으로 업데이트 또는 삭제하려고 하면 이미 변경되어 더이상 변경되지 않기 때문에 idempotent에 해당한다고 한다. (물론 DELETE도 특정 값이 아니라 '첫번째 리소스 삭제' 이런식으로 되어있다면 idempotent가 아니다.)

### 1-4. Caching

캐싱은 자주 요청-응답하는 데이터를 저장해두는 기능이다.    
만약 특정 리소스가 반복적으로 요청될 경우 이를 캐싱하여 다음에 같은 요청할 때 서버에서 리소스를 받아오는 것이 아니라 요청을 가로채 캐싱되어있는 리소스를 제공하게 해준다.    
이럴경우 클라이언트는 리소스를 빨리 얻게되기 때문에 응답 시간이 빨라진다는 장점이 있다. 하지만 리소스가 변경되었음에도 계속 같은 값을 내주게 될 수도 있다.    

여기서 캐싱하는 조건은 변하지 않는 리소스일 경우에만 캐싱하는 것이다.    
그래서 GET메소드를 사용하는 리소스는 캐싱이 가능하지만, PUT, DELETE 같이 리소스가 변할 수 있는 것들은 캐싱을 할 수 없다.    
POST의 경우 기본적으로는 캐싱이 불가능하지만 따로 조작을 하면 캐싱이 가능하게 할 수도 있다.

> 캐싱에도 여러 종류가 있는데 이는 나중에 캐싱 글을 따로 작성 예정입니다.

----

## 2. HTTPS

HTTPS는 HTTP의 단점을 보완한 것이다.    
HTTP와의 다른 특징은 아래와 같다.

1. SSL 인증서를 이용하여 데이터를 암호화
2. TLS 프로토콜을 통해 보안을 유지
3. SEO 검색엔진 최적화 기능
4. AMP 가속화된 모바일 페이지 - 컨텐츠를 모바일 환경에서 빠르게 로딩할 수 있도록 HTML의 불필요한 부분을 없애 빠르게 로딩한다.


<hr>

- 참고

[REST API Tutorial](https://restfulapi.net/)
