---
created: 2020-07-12
modified: 2020-07-12
tags: [AWS]
title: 생활코딩AWS05
author: Yo0oN
categories: [ETC, AWS]
---


생활코딩과 함께하는 AWS 탐구생활 강의의 6, 7일차 내용입니다.

## 1. Cloud Front

CloudFront는 기본적으로 Cache Server이고, CDN 기능을 제공해준다.<br>
해당 기능을 이용한다면, 이제 웹서버는 사용자와 바로 만나지 않는다.<br>
클라이언트는 CloudFront로 요청을 하면, CloudFront는 다시 웹서버에 요청을 한다.<br>
요청을 받은 웹서버는 CloudFront로 응답을 해주고, CloudFront는 응답 받은 정보를 가지고 있다가, 후에 클라이언트에게 요청이 오면 해당 정보를 응답해준다.<br>
이렇게 한다면 웹서버는 CloudFront가 정보를 가지고 있는 동안은 쉴 수 있고, CloudFront는 캐시서버가 된다.<br>

참고로 AWS에서는 웹서버를 Origin, CloudFront를 Distribution이라고도 부른다.

![01](https://user-images.githubusercontent.com/53729311/180649436-9b816e69-e04b-4e77-8f61-9953ca0e18c1.jpg)

서비스 중 Cloud Front를 들어가 Get Distribute -> Get Started를 누르면 Distribution을 생성할 수 있다.<br>
위의 사진 중 Origin Domain Name에 도메인을 적으면 되는데, 만약 AWS에서 웹서버로 사용중인 제품이 있다면 해당 제품을 적어도 된다.<br>
하지만 내가 따로 서버를 운영중이라면, 해당 서버의 도메인을 적으면 된다.<br>
(IP, http, 경로 외에 도메인만 적어야 하고, 아래쪽에 포트번호를 추가해주어야한다.)<br>

<br>

![02](https://user-images.githubusercontent.com/53729311/180649440-3d81898a-045c-4a6f-b035-4776c4286310.jpg)

Distribution Settings란에서는 CDN 사용에 관한 설정을 할 수 있다.<br>
<br>
필요한 설정을 모두 마치고 생성을 하자.<br>

![03](https://user-images.githubusercontent.com/53729311/180649441-8896642c-3ca3-4f3a-9f4f-de0a8dda12b8.jpg)

생성이 끝나고 해당 Distribution을 보면 Domain Name이라는 것이 있다.<br>
CloudFront의 주소이다. 해당 주소를 이용하여 CloudFront에 요청하면 이제 CloudFront는 웹서버에 다시 요청을 하고, 받은 응답을 클라이언트에게 응답해 줄 것이다.

![04](https://user-images.githubusercontent.com/53729311/180649442-bb0a6246-df66-45d0-b9e7-64ad897663f5.jpg)
<br>

### 1-1. 참고..Cache?

사용자는 웹브라우저를 이용하여 웹서버에 요청을 하고, 웹서버는 응답을 해준다.<br>
그런데 응답을 해주는 시간이 오래 걸리는 페이지라고 생각해보자.<br>
사용자는 이에 답답함을 느끼고, 좀 더 빠르게 사용하기를 원할것이다.<br>
이때 나온 기술이 Cache이다.<br>
사용자에게 한번 컨텐츠를 제공한적이 있다면, 해당 컨텐츠를 사용자의 컴퓨터에 저장하고, 이후 요청시에는 컴퓨터에 저장되어 있는 컨텐츠를 보이도록 해주는것이다.<br>
은닉하다, 숨기다 라는 뜻을 가진 이름처럼 사용자의 컴퓨터에 컨텐츠를 숨겨두고 빠르게 응답을 해주는 것이다.

<br>

## 2. 캐시서버의 문제..

캐시서버는 미리 저장되어 있는 컨텐츠를 제공해준다고 하였다.<br>
물론 빠르게 응답해준다는 장점이 있지만, 미리 저장된 컨텐츠를 제공하기 때문에 원본이 바뀌어도 바뀐것을 모르고 본인이 가진것만을 제공한다.<br>


![06](https://user-images.githubusercontent.com/53729311/180649445-bfbfd3b9-a077-42ce-8701-0b126c300cc1.jpg)

우리가 만든 CloudFront도 마찬가지다.<br>

![05](https://user-images.githubusercontent.com/53729311/180649443-19640bb0-d0bd-4749-9a4a-cbc834466d57.jpg)

위의 그림을 보면 Minimum TTL, Maximum TTL, Default TTL이 있다.<br>
순서대로 최소 캐시 유지시간, 최대 캐시 유지시간, 평균 캐시 유지시간이다.<br>
해당 기능을 이용하여 CloudFront가 캐시를 가지고 있더라도 중간중간 웹서버에 요청을 하여 바뀐 정보를 다시 받아올 수 있다.

-------

오늘 7일차 수업까지 모두 마쳤다.<br>
어떻게 사용하는지 간단하게만 알려주는 강의여서 자세한 기능까지는 알지 못하지만, 생각보다 다양한 기능이 있고, 이전에는 어렵게만 느껴졌던 기능들이 어렵지만은 않게 느껴졌다.<br>
다음에 AWS를 사용하게 된다면 그때 다양한 기능들을 더 찾아봐야겠다..
