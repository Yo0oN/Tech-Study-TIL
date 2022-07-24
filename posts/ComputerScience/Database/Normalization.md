# 정규화?

 ` 데이터를 효율적으로 관리하기 위해 데이터를 분해하는 과정.`

만약 데이터를 분해하지 않는다면 여러 단점이 있다.<br>
예를들어 테이블 A, B, C에 똑같이 들어있는 데이터가 있다. 데이터의 수정하려면 해당 데이터가 있는 모든 테이블들을 수정해야하고, 사람이 개발하는 이상 실수를 해서 테이블 한두개쯤은 빼먹게될 수도 있다.<br>
이럴경우 일부만 수정되어 정확한 값을 보장받을 수 없다.<br>
이 외에도 삽입할 때 의도와 다른 값들이 삽입되는 삽입이상, 삭제 시 다른 값들도 연쇄적으로 삭제되는 삭제이상 등이 있다.

정규화에는 총 6가지 과정  있는데, 아래의 데이터를 차례로 수정하며 공부해보자.

![image](https://user-images.githubusercontent.com/53729311/112869810-87d36780-90f8-11eb-9fd4-abc77df200eb.png)


<br>

## 1. 제 1 정규형

*Atomic. 도메인 원자값 - 하나의 속성이 복수개의 값을 가지고 있을 때 하나의 속성이 단일 값을 가지도록 설계해야 한다.*<br>
> 도메인? 하나의 컬럼이 가진 범위. 예를들어 전화번호 컬럼은 전화번호만 가지고 있어야 하고, 다른 값을 가지고 있으면 안된다. 이런 범위를 *도메인*이라 한다.<br>
도메인이 원자값이라는 것은 하나의 컬럼에 들어가는 값이 그 범위에 속하면서도, 더이상 쪼갤 수 없는 단위가 되어야 한다는 뜻이다.

그런데 원자값으로 쪼개다 보면 이름이나, 생년월일 같은 것들은 쪼개다보면 성과 이름, 년, 월, 일로 더 쪼갤 수 있다.<br>
그래서 원자값이라는 뜻이 애매하기 때문에 실제로 설계할 때는 원자값보다는 행과 열이 만나는 부분에는 하나의 값만 들어가고, 하나의 컬럼에는 중복값이 없도록 설계한다고 한다.

![image](https://user-images.githubusercontent.com/53729311/112869810-87d36780-90f8-11eb-9fd4-abc77df200eb.png)

위의 그림에서는 두개 이상의 과목을 듣는 학생이 있다. 과목 컬럼의 두개 이상의 값들이 들어간 곳이 있으니 이를 쪼개주자.

![image](https://user-images.githubusercontent.com/53729311/112870400-21027e00-90f9-11eb-8fe8-f1baa2d1e56d.png)



제 1 정규화에 따라 나뉜 모습이다. 왼쪽 테이블에는 학생에 대한 정보를, 오른쪽 테이블에는 해당 학생이 들은 과목을 넣었다.<br>
오른쪽 테이블은 학번을 이용하여 어떤 학생이 수강한 수업인지 알 수 있게 정리되었다. 하지만, 학번만으로는 수강한 과목을 모두 구분할 수 없기 때문에 학년도 함께 넣어주어 확실하게 구분할 수 있도록 하였다.
(혹시라도 재수강하게 된다면 이후에 같은 내용이 또 들어갈테니 수강했을 때의 학년 컬럼을 추가로 넣어주었다.)

제 1 정규화를 통해 오른쪽 테이블은 학번과 학년으로 행을 구분시키고 양쪽 테이블 모두 한 칸에 하나의 값만 들어가도록 해주었다.


## 2. 제 2 정규형

*키가 아닌 모든 속성들은 모두 기본키에 종속되어야 한다.*

위에서 두개의 테이블로 분리해주었는데, 오른쪽의 수강 과목 테이블을 보면 학번과 학년을 기준으로 어떤 수업을 들었는지 알 수 있다.<br>
여기서 학번이 기본키, 과목과 성적은 학번에 종속되어 있는 값들이다. 그 외에 교수, 책과 같은 데이터들은 학생별로 변하는 데이터가 아니고, 학번에 종속되지는 않는다.

그러면 다시 학번이라는 키에 종속되는 값과 아닌 값들을 분리해보자.

![image](https://user-images.githubusercontent.com/53729311/112869062-b43ab400-90f7-11eb-8912-3ab0cea90085.png)

이제 테이블을 두개로 나눠서 수강한과목 테이블의 값들은 학번에, 과목 테이블의 값들은 과목에 종속되도록 해서 제 2 정규화를 해주었다.

> 위에서 종속되어 있다라는 말이 어려울 수 있는데 종속되어 있는 것들은 해당 키로 찾을 수 있다고 생각하면 어떤 값들을 말하는건지 이해하기 쉽다.


## 3. 제 3 정규형

*이행적 함수 종속 제거*

제 3 정규화를 쉽게 말하면 기본키가 아닌 다른 후보키에 의존하지 않아야 한다는 뜻이다.

![image](https://user-images.githubusercontent.com/53729311/113036256-039fe380-91cf-11eb-9c79-6e3151cb49d3.png)

첫번째 테이블인 학생 정보가 담긴 테이블을 확인해보면 모든 컬럼들은 학번에 종속되어 있다. 하지만, 그 외에도 내부에서 서로 종속된 것이 있는데, 바로 대학과 전공이다.<br>
대학은 학번이라는 기본키에 종속되어 있기도 하지만, 대학은 전공에도 종속되어 있다. (전공을 보면 대학이 나오니까!)
										
![image](https://user-images.githubusercontent.com/53729311/113036973-dacc1e00-91cf-11eb-84ab-ca0e807128b8.png)

그러니 기본키가 아닌 다른 후보키에 의존하지 않도록 전공과 대학을 다른 테이블로분리하고, 학생 테이블에는 전공만 남겨서 제 3 정규화를 해주었다.

> 추가적으로 학생 테이블에서는 다른 테이블의 전공이라는 기본 키를 가져와 사용하고 있다. 이것을 외래키 Foreigner Key라고 부른다.


## 4. BCNF (Boyce-Codd Normal Form) = 3.5 정규형 = 강한 3정규형

*결정자이면서 후보키가 아닌 것을 제거 -> 후보키가 아닌 것들은 결정자가 될 수 없다.*

복합키로 구성될 때 일어난다.<br>
후보키 A, B가 있을 때, 후보키가 아닌 C를 A와 B를 이용하여 찾을 수있다. 하지만 그 반대인 C로는 A와 B를 찾을 수 없다.<br>
만약 그렇게된다면 C가 기본키가 되야할것이다.

그래서 BCNF는 후보키가 아닌 일반속성을 이용하여 다른 키들을 찾을 수 없어야 한다.

![image](https://user-images.githubusercontent.com/53729311/113190801-b9366980-9297-11eb-9aed-14c498da9878.png)

위의 그림에서 제약조건이 하나 있는데, 각 교수는 한 과목만 강의할 수 있고, 각 과목은 여러 교수들에 의해 강의될 수 있다는 것이다.<br>
학번으로는 과목명이나 교수를 특정지을 수 없다.(100, 200번은 수업을 여러개 듣기 때문에 하나의 과목을 특정지을 수 없다.)<br>
그리고 과목으로는 교수를 특정지을 수 없다.(하나의 과목을 여러 교수가 강의하고 있기 때문이다.)<br>
마지막으로 교수로는 학번을 정할 수 없고, 과목만 정할 수 있다.

위의 그림에서는 중복된 값들이 계속 나오기 때문에 하나의 기본키를 정할 수 없어서 복합키를 이용하여 다른 값들을 구해야 한다.<br>
학번과 과목명을 이용하여 교수를 구하는 것이 가능한데, 문제는 반대도 가능하다. 교수는 하나의 수업만 강의하기 때문에 후보키가 아닌 교수로 과목명을 알 수 있게 되고, 이럴경우 BCNF에 위배된다.

그러면 위의 테이블을 둘로 분리해주자.
							
![image](https://user-images.githubusercontent.com/53729311/113192178-6c539280-9299-11eb-88a7-ce1606eb763d.png)

분리해주면 이런 그림이 나온다.<br>
실제로 이런 경우는 자주 나오지 않고, 보통은 3 정규화까지 하고나면 BCNF는 할일이 없다고 한다..

> BCNF 참고 : [정보처리 실기_데이터베이스06강_정규화 by eduon](https://youtu.be/RXQ1kZ_JHqg?t=2451)


## 제 4 정규형

*릴레이션 R에서 다치종속 A ->> B가 성립하는 경우 다치종속의 제거*

A를 선택했는데 그에 따른 B가 여러개 나올 경우를 말한다. 만약 여러개가 나오는 것이 한 컬럼만 있으면 괜찮지만, 그것이 두개 이상일 경우 테이블을 분리해 주어야 한다.

![image](https://user-images.githubusercontent.com/53729311/113318443-70d88380-934b-11eb-9e16-8987f8a1d14f.png)

위의 테이블의 경우 과목을 이용하여 교재와 교수를 구할 수 있다. 하지만 DB를 선택했을 때 나오는 교재와 교수는 각각 여러개가 나오고, 이럴 경우 테이블을 두개로 분리해야 한다.
						
![image](https://user-images.githubusercontent.com/53729311/113318760-c01eb400-934b-11eb-9708-dca361789723.png)

분리하면 위와 같은 그림이 나온다.


## 제 5 정규형

*조인종속성 이용 - 후보키가 없는 테이블을 분리하고 다시 합쳤을 때 무손실분해원칙에 따라야 한다.*


테이블을 여러개로 분리했을 때 하나로 다시 합치게(Join) 된다면 무손실분해원칙에 의해 데이터 손실 없이 원래의 데이터가 그대로 나와야 한다.<br>
그리고 이런 조인 종속이 후보키를 통해서만 성립된다면 5정규형에 속하게 된다.<br>
이런 문제는 후보키가 없는 테이블을 분리하였을 때 일어난다.

![image](https://user-images.githubusercontent.com/53729311/113320581-9bc3d700-934d-11eb-8c17-4d6fe2e752b9.png)

테이블을 만들어보자면 위의 상황처럼 된다.<br>
첫번째 줄의 테이블을 두개의 테이블을 만들었는데 두개를 PK를 이용하여 합치는 4번째 행이 새로 생겨버렸다. 이럴 경우 3개로 분리해보자.
									
![image](https://user-images.githubusercontent.com/53729311/113321076-315f6680-934e-11eb-833c-84bbb9573b1c.png)

3개로 분리하면 이런 상황이 된다.

-------
참고 : [정보처리 실기_데이터베이스06강_정규화 by eduon](https://youtu.be/RXQ1kZ_JHqg)