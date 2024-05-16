

## 엔터티
1. 개념
- 사람, 장소, 물건, 사건, 개념 등의 명사에 해당
- 업무상 관리가 필요한 관심사
- 저장되기 위한 어떤 것(Thing)
- ==업무에 필요한 유용한 정보를 저장하고 관리하기 위한 집합적인 것==

2. 엔터티와 인스턴스에 대한 내용과 표기
- 대부분 사각형을 ㅗ표현됨. 다만 속성의 표현 방법이 조금씩 다름
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbalFhf%2FbtsedaCJdTT%2FEEJgtspvocS7y3DA8QkJPK%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfzFHz%2Fbtseo1Zkwv1%2FmsdruxFIKiiknmKGeAczRK%2Fimg.png)

3. 엔터티의 특징
	가) 업무에서 필요로 하는 정보
	- 반드시 시스템을 구축하고자 하는 업무에서 필요로 하고 관리하고자 하는 정보여야 함

	나) 식별이 가능해야 함
	- ==식별자(Unigue Identifier)에 의해 식별== 가능
	- 유일한 식별자는 그 엔터티의 인스턴스만의 고유한 이름

	다) 인스턴스의 집합
	- 영속적으로 존재하는 인스턴스의 집합이 되어야 함
	- 엔터티의 특징 중 '한 개'가 아닌 =='두 개' 이상이라는 집합 개념==이 매우 중요

	라) 업무 프로세스에 의해 이용
	![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbazeSR%2Fbtsep8EHbdW%2FhHy9b0CifdkRiYsd1bxE60%2Fimg.png)

	마) 속성을 포함
	- 엔터티에는 반드시 속성(Attributes)이 포함되어야 함
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb9ZaE8%2FbtselQEpIcM%2FU8pAd86GwtbthwPBiVKAdK%2Fimg.png)

	바) 관계의 존재
	- 엔터티는 다른 엔터티와 초소 한 개 이상의 관계가 존재해야 함
	- 단, 통계성 엔터티 도출, 코드성 엔터티 도출, 시스템 처리 시 내부 필요에 의한 엔터티 도출은 예외


4. 엔터티의 분류
	- 자신의 성격에 의해 실체 유형에 따라 구분하거나 업무를 구성하는 모습에 따라 구분이 되는 발생시점에 의해 분류될 수 있음

	가) **유무형에 따른 분류**
	1) ==유형엔터티==(Tangible Entity) : 물리적인 형태가 있고 안정적이며 지속적으로 활용되는 엔터티로 구분하기가 가장 용이 / 사원, 물품, 강사 등
	2) ==개념엔터티==(Conceptual Entity) : 물리적인 형태는 존재하지 않고 관리해야 할 개념적 정보로 구분 / 조직, 보험 상품 등
	3) ==사건 엔터티==(Event Entity) : 업무를 수행함에 따라 발생되는 엔터티 / 조직, 청구 미납 등

	나) 발생시점에 따른 분류
	1) ==기본/키 앤터티==(Fundamental Entity, Key Entity) : 원래 존재하는 정보로서 다른 엔터티와 관계에 의해 생성되지 않고, 독립적으로 생성이 가능하고 자신은 타 엔터티의 부모 역할을 함 / 사원, 부서, 고객, 상품, 자재 등
	2) ==중심엔터티==(Main Entity) : 기본 엔터티로부터 발생되고 그 업무에 있어서 중심적인 역할을 함 / 계약, 사고, 예금원장, 청구, 주문, 매출 등
	3) ==행위엔터티==(Active Entity) : 두 개 이상의 부모 엔터티로부터 발생되고 자주 내용이 바뀌거나 데이터량이 증가됨 / 주문목록, 사원변경이력 등
예시 ) ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdutEU%2Fbtses7RDZsg%2FKg7wkGLU9ZDeAEYsVx2XiK%2Fimg.png)


## 속성
1. 개념
- 사전적 의미 : 사물의 성질, 특징 또는 본질적인 성질
- 모델링 관점 : 업무에서 필요로 하는 인스턴스로 관리하고자 하는 의미상 더 이상 분리되지 않는 최소한의 데이터 단위
- 엔터티는 속성들에 의해 설명 된다
- **업무에서 필요로 함 / 의미상 더 분리되지 않음 / 엔터티를 설명하고 인스턴스의 구성요소가 됨**

2. 엔터티, 인스터스, 속성, 속성 값의 내용과 표기법
	가) 엔터티, 인스턴스, 속성, 속성 값의 관계
	- 한 개의 엔터티 > 두 개 이상의 인스턴스의 집합이어야 함
	- 한 개의 엔터티 > 두 개 이상의 속성을 가짐
	- 한 개의 속성 > 한 개의 속성 값을 가짐
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWbrQP%2FbtseAcFA2W5%2FuKGHuJEovx9MvaRlhMVpQk%2Fimg.png)

	나) 표기
	- 엔터티 내에 이름을 포함하여 표현
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb4iv8s%2FbtseyxjHRci%2F5xJXLP5ah4LpDzRbdJNhw1%2Fimg.png)

	다) 특징
	- 엔터티와 마찬가지로 반드시 해당 업무에서 필요해 관리하고자 하는 정보여야 함
	- 정규화 이론에 근간하여 정해진 주식별자에 함수적 종속성을 가져야 함
	- 하나의 속성에는 한 개의 값 많을 가짐. 하나의 속성에 여러 개의 값이 있는 다중 값일 경우 별도 엔터티로 분리

4. 속성의 분류
	가) 속성의 특성에 따른 분류
	1) ==기본 속성==
	- 업무로부터 추출한 모든 속성이 여기에 해당하며 엔터티에 가장 일반적이고 많은 속성을 차지
	2) ==설계 속성==
	- 업무상 필요한 데이터 이외에 데이터 모델링 규칙화를 위해 속성을 새로 만들거나 변형하여 정의하는 속성
	3) ==파생 속성==
	- 다른 속성에 영향을 받아 발생하는 속성. 계산된 값들이 해당됨
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbgQ72u%2FbtseH0ERxhw%2Fuk3Te4f10S7Md9v0didy6k%2Fimg.png)

	나) **엔터티 구성방식에 따른 분류**
	1) PK 속성 : 엔터티를 식별할 수 있는 속성
	2) FK 속성 : 다른 엔터티와의 관계에서 포함된 속성
	3) 일반 속성 : PK, FK에 포함되지 않은 속성
	![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEI1mV%2FbtseHmVK54V%2FnOXd7SGB4h1CG2stXkh1CK%2Fimg.png)

5. 도메인(domain)
- 속성이 가질 수 있는 범위
- 엔터티 내에서 속성에 대한 데이터 타입, 크기, 제약사항을 지정하는 것

6. 속성의 명명(Naming)
	1) 해당 업무에서 사용하는 이름을 부여
	2) 서술식 속성명은 사용 안함
	3) 약어 사용은 가급적 제한함
	4) 전체 데이터 모델에서 유일성 확보하는 것이 좋음
