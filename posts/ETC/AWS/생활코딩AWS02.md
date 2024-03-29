---
created: 2020-07-08
modified: 2020-07-08
tags: [AWS]
title: 생활코딩AWS02
author: Yo0oN
categories: [ETC, AWS]
---

생활코딩과 함께하는 AWS 탐구생활 강의의 2일차 내용입니다.<br>
윈도우10에서 진행하였습니다.


## 1. EC2 인스턴스 생성해보기.

![01](https://user-images.githubusercontent.com/53729311/180649246-7e986cf2-620e-47bb-a178-d4aeceefc945.jpg)

시작하기 전 AWS 우측 상단에 지역을 선택하는 칸이 있다.<br>
각자의 지역에 맞는 AWS 서버를 선택하자.

여러 제품 중 EC2를 신청해보자.

![02](https://user-images.githubusercontent.com/53729311/180649247-1c95c0a2-ff4a-4f86-8f57-32668fa85a68.jpg)

EC2에서 '인스턴스'라고 적힌 부분은 컴퓨터 한대를 뜻한다.<br>
인스턴스 시작을 누르면 여러 운영체제가 설치된 컴퓨터들을 볼 수 있다.<br>
그 중 '프리티어 사용가능'은 프리티어를 이용해 일정 기간동안 무료로 사용 가능한 제품들이다.

![03](https://user-images.githubusercontent.com/53729311/180649248-a7583c01-2c9f-459d-b36d-553cda95350a.jpg)

다음으로 넘어가 인스턴스 유형을 선택하고(프리티어로 선택해야 무료)<br>
다음으로 넘어가야 하는데, 버튼이 두개있다.<br>
'검토 및 시작'을 누르면 마지막 단계인 7번 검토부분으로, '다음'버튼을 누르면 인스턴스에 대한 설정을 해줄 수 있다.

![04](https://user-images.githubusercontent.com/53729311/180649249-f62d9f94-7556-475c-a5fc-5c39bceb846e.jpg)

인스턴스에 대한 모든 설정을 해준 후, 7번까지 온다면 마지막으로 인스턴스에 대한 정보를 알려준다.<br>
시작하기를 누르면 키페어를 받는 단계가 있는데, 일단 '새 키페어 생성'으로 선택한 후, 이름을 정해주고, 키페어를 다운받자.

![05](https://user-images.githubusercontent.com/53729311/180649250-b744b763-ed83-4d27-a14c-846daccb43e2.jpg)

다운받은 키페어를 보면 암호화 되어있는 개인키를 볼 수 있다.

![06](https://user-images.githubusercontent.com/53729311/180649251-8e77d751-6fa4-428e-8fa4-41ca9fc389d2.jpg)

개인키도 받으면 인스턴스를 살펴보러 가자.<br>
인스턴스 상태가 pending중이면 아직 생성중이고, running 중이면 생성이 완료되어 작동중이라는 뜻이다.

<br>

## 2. EC2 인스턴스 접속해보기.

가상컴퓨터를 하나 만들었으니 실제로 작동을 시켜보자.

![07](https://user-images.githubusercontent.com/53729311/180649252-da19e309-a77e-4d52-b9bc-0539e48a467b.jpg)

인스턴스를 마우스 우클릭 하여 연결을 선택하면 인스턴스에 연결할 수 있도록 원격 데스크톱 파일을 받을 수 있다.<br>
파일을 받은 후, 암호 가져오기를 통해 암호를 알아내자.

![08](https://user-images.githubusercontent.com/53729311/180649253-1fd569be-61a2-477f-823a-216f0968e143.jpg)

인스턴스를 생성할 때 받은 .pem파일을 선택하면 암호 해독을 통하여 암호를 볼 수 있다.

![10](https://user-images.githubusercontent.com/53729311/180649256-33b7d7fa-135e-4355-96a6-3dd4f3161283.jpg)

위에서 받은 원격 데스크톱 파일을 실행시킨 후 암호 해독으로 얻은 암호로 접속을 해보자.

![11](https://user-images.githubusercontent.com/53729311/180649259-911ad5a7-75c2-46ba-9f04-6b8ca6986cdd.jpg)

이제 AWS를 이용해 만들어진 가상 컴퓨터로 접속을 하였고, 우측 상단에 보면 해당 컴퓨터에 대한 정보가 적혀있다.

<br>

## 3. 접속 종료하기.

인스턴스에서 우클릭 후 상태를 보면 중지와 종료가 있다.<br>
중지는 가상컴퓨터의 전원을 끄고, 종료는 컴퓨터 자체를 삭제한다.(중지해서 컴퓨터를 껐다고해서 결제가 안되는것은 아님.)

![12](https://user-images.githubusercontent.com/53729311/180649260-ffd17457-e217-452e-85a9-20240dfdb3b9.jpg)

참고로 중지를 통해 전원을 끄고, 다시 연결하면 IP도 변경되니 주의하자.

<br>

## 4. 요금 확인하기.

프리티어를 사용하면 일정 부분까지는 무료지만, 시간이 지나거나 무료 제공량을 초과하면 돈이 부과된다.

![13](https://user-images.githubusercontent.com/53729311/180649262-c5a73cdd-7c5f-4b5f-a898-8c76d5841ccb.jpg)
<cite>[생활코딩과  AWS 탐구생활](https://youtu.be/CuvZTFJyufI) 강의 중..</cite>


마이페이지쪽을 보면 청구요금을 볼 수 있다.<br>
회원가입시 등록했던 카드로 결제가 이루어지며, **Bugets** 칸에서는 예산을 미리 설정해 두어 예산초과될 경우 알림을 준다.
