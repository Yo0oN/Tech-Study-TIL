---
created: 2020-07-12
modified: 2020-07-12
tags: [AWS]
title: 생활코딩AWS04
author: Yo0oN
categories: [ETC, AWS]
---

생활코딩과 함께하는 AWS 탐구생활 강의의 4, 6일차 내용입니다.(5일차 생략)

## 1. S3의 요금

S3는 파일 업로드를 할 때, 또는 객체의 속성에서 요금제를 선택할 수 있다.<br>
객체별로 요금을 정산하는데, 자세한 계산법은 [AWS 요금계산기](https://calculator.aws) 참조하자.

<br>

![01](https://user-images.githubusercontent.com/53729311/180649403-e8b2f83c-4d21-4611-a5da-40ab4dd493b5.jpg)

<br>
<ol>
    <li>스탠다드
        <ul>
            자주 사용하는 데이터
        </ul>
    </li>
    <li>스탠다드 IA
        <ul>
            IA는 Infrequent Access, 자주 접근하지 않는이라는 뜻으로 저장만 해두고 자주 쓰지 않는 데이터에 사용한다.
        </ul>
    </li>
    <li>단일 영역 IA
        <ul>
            해당 항목은 가용영역 ≥ 1 이라 적혀있다.<br>
            다른 요금제는 내가 선택한 지역 뿐만 아니라 다른 지역에도 파일을 복사하여 백업을 해두지만,<br>
            단일영역 IA를 선택하면 최소 한군데에만 있어 후에 서버에 문제가 생기면 복원할 수 없을수도 있다.<br>
            그렇기 때문에 중요하지 않고, 삭제되어도 상관 없는 경우에만 사용한다.<br>
        </ul>
    </li>
    <li>Glacier
        <ul>Glacier는 빙하라는 뜻으로 그냥 저장만 해두고, 자주 사용하지 않는 데이터에 사용한다.<br>
            대신 파일에 접근하는데 시간이 오래걸린다.
        </ul>
    </li>
</ol>

<br>

## 2. S3의 다양한 기능들

![02](https://user-images.githubusercontent.com/53729311/180649405-4335f8b0-df87-425e-abb1-21afbcecb9d3.jpg)

AWS에는 여러 기능들이 있고, 폴더의 속성이나 [S3 설명서](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/what-is-s3.html) 부분에서 확인할 수 있다.


### 2-1. Web Server Hosting 기능

S3를 이용하여 웹사이트 호스팅을 할 수 있다.<br>

![03](https://user-images.githubusercontent.com/53729311/180649407-17374398-f290-417f-b9b2-a7b32ffa8e63.jpg)

버킷의 속성에 보면 정적 웹 사이트 호스팅 기능이 있고, 해당 기능을 사용하면 S3를 웹서버처럼 사용할 수 있다.<br>
(대신 버킷과 파일들은 외부에서 접속이 가능하도록 퍼블릭상태여야 한다.)

사진에서 보이는 엔드포인트가 웹사이트의 주소가 된다.<br>
해당 주소를 입력해보면 S3에 올린 사이트를 볼 수 있다.

![04](https://user-images.githubusercontent.com/53729311/180649408-8061c9e6-6817-4c2c-86f4-ca00302158eb.jpg)


### 2-2. Cloud Front 기능

Cloud Front 기능은 __CDN(Content Delievery Network) 과 같은 기능이다.

CDN은 전세계에 서버를 분산시켜 둔 후 외부에서 요청이 들어오면 요청에서 가장 가까운 장소에 있는 서버에서 미리 저장해 두었던 컨텐츠를 응답을 해준다.<br>
그래서 내가 지정한 서버의 위치보다 먼 곳에서 요청을 하더라도 빠르게 응답해준다.


### 2-3. 버전관리 기능

S3는 Git이나 SVN같은 버전관리 기능을 자체적으로 가지고 있다.
