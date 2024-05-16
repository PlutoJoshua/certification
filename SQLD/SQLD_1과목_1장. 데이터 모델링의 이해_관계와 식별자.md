
## 관계
1. 개념
	가) 관계의 정의 
	- 사전적 정의 : 상호 연관성이 있는 상태
	- 데이터 모델 정의 : 엔터티의 인스턴스 사이의 논리적인 연관성으로서 존재의 형태로서나 행위로써 서로 연관성이 부여된 상태

	나) 관계의 페어링
	- 관계는 엔터티 안 인스턴스가 개별적으로 관계를 가지는 것(페어링)이고, 집합 관계로 표현
	- 개별 인스턴스가 각각 다른 종류의 관계를 가지고 있다면 두 엔터티 사이에 두 개 이상의 관계가 형성될 수 있다
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsH0zu%2FbtseKfu1eaK%2FgylkkmOAEY2eFkmPEdeOF1%2Fimg.png)

2. 분류
- 관계를 연결함에 있어 어떤 목적으로 연결되었느냐에 따라 분류 됨
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoHDZJ%2FbtseCFPQpy2%2FFdiRZHbFR9MMHhWB19Odlk%2Fimg.png)
- UML(Umified Modeling Language)
1) 연관관계(Association) : 항상 이용하는 관계로 존재적 관계에 해당, 실선으로 표현
2) 의존관계(Dependency) : 상대방 클래스의 행위에 의해 관계가 형성될 때 구분, 점선으로 표현

3. 관계의 표기법
- 관계명(Membership) : 관계의 이름
- 관계차수(Cardinality) : 1:1, 1:M, M:N
- 관계선택사양(Optionality) : 필수관계, 선택관계

가) 관계명(Membership)
- 엔터티가 관계에 참여하는 형태를 지칭. 각각의 관계명에 의해 두 가지의 관점으로 표현
- 관계가 시작되는 편 : 관계 시작점, 받는 편 : 관계 끝점
- 참여자의 관점에 따라 관계 이름이 능동적이거나 수동적으로 명명됨
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ftkrb9%2FbtsfjJvOdSi%2FqnAnZQCnqWeU9HekZF9xl0%2Fimg.png)

나) 관계차수(Degree/Cardinality)
- 두 개의 엔터티가 관계에서 참여자의 수를 표현하는 것
- 일반적인 표현 방법 1:M, 1:1, M:N
	1) 1:1(ONE TO ONE) 표기 방법
	- 관계를 맺는 다른 엔터티의 엔터티에 대해 단지 하나의 관계만을 가지고 있다
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJoRTv%2FbtsfdX3ldld%2FwAwWPS9i4diB9KTkXdeV7K%2Fimg.png)

	2) 1:M(ONE TO MANY) 표기 방법
- 관계를 맺는 다른 엔터티의 엔터티에 대해 하나나 그 이사의 수와 관계를 가지고 있다. 그러나 반대 방향은 하나의 관계를 가진다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtHAMO%2Fbtsfe66wNFw%2F5vHWsxuFM6mfu6i9xWwwHK%2Fimg.png)

3) M:M(MANY TO MANY) 표기 방법
- 각각의 엔터티는 관ㄱㅖ를 맺는 다른 엔터티의 엔터티에 대해 하나나 그 이상의 수와 관계를 가지고 있다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRh9d0%2FbtsfeAz6heE%2FnfdK4QN10W3pCEuk9yXiLK%2Fimg.png)

다) 관계선택사양(Optionality)
- 참여하는 엔터티가 항상 참여하는지 아니면 참여할 수도 있는지를 나타내는 방법이 필수와 선택참여 이다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQP4qp%2FbtsfvnM2448%2Fkgex07ZB2KedWrJGaG674k%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcIrtXv%2Fbtsfdb8F2ee%2FZs3gWrCQur6iT0p4cHzGK1%2Fimg.png)


4. 관계의 정의 및 읽는 방법
- 기준(Source) 엔터티를 한 개(One) 또는 각(Each)으로 읽는다
- 대상(Target) 엔터티의 관계참여도 즉 개수(하나, 하나 이상)를 읽는다
- 관계선택사양과 관계명을 읽는다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fef17V5%2FbtsfCs8lhfP%2FRbNOhT6HIkjtnPQFuXmxD0%2Fimg.png)


## 식별자
1. 개념
- 하나의 엔터티에 구성되어 있는 여러 개의 속성 중에 엔터를 대표할 수 있는 속성.
- ==하나의 엔터티는 반드시 하나의 유일한 식별자가 존재해야 한다==
- 식별자는 엔터티내에서 인스턴스들을 구분할 수 있는 구분자이다.

2. **식별자의 특징**

| 특징      | 내용                                             | 비고                                    |
| ------- | ---------------------------------------------- | ------------------------------------- |
| **유일성** | 주식별자에 의해 엔터티내에 <br>모든 인스턴스들을 유일하게 구분함          | 사원번호는 모든 직원들에 대해<br>고유하게 부여           |
| **최소성** | 주식별자를 구성하는 속성의 수는 <br>유일성을 만족하는 최소의 수          | 사원분류코드 + 사원번호는<br>부적절한 구조             |
| **불변성** | 주식별자가 한 번 특정 엔터티에 지정되면 <br>그 식별자의 값은 변하지 않아야 함 | 사원번호의 값이 변함 -><br>이전 기록 말소, 새로운 기록 발생 |
| **존재성** | 주식별자가 지정되면 반드시 데이터 값 존재<br>(Null 안됨)           | 사원번호 없는 회사직원 없음                       |
- 외부식별자의 경우 주식별자 특징과 일치하지 않으며 참조무결성 제약조건(Referential Interity)에 따른 특징을 가지고 있다.

3. 식별자 분류 및 표기법
	가) 식별자 분류
	- 자신의 엔터티 내에서 대표성을 가지는가? 주식별자 / 보조식별자
	- 엔터티 내에서 스스로 생성되었나?  내부식별자 / 외부식별자
	- 단일 속성으로 식별이 되는가 ? 단일 식별자 / 복합식별자 
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbu4d8e%2FbtsfjI5dwNO%2FI3AlAbhCiodgnKpcZD12Ok%2Fimg.png)

| 분류        | 식별자                             | 설명                                                      |
| --------- | ------------------------------- | ------------------------------------------------------- |
| 대표성 여부    | 주식별자<br>(Primary Identifier)    | 엔터티 내에서 각 어커런스를 구분할 수 있는 구분자. 타 엔터티아 참조관계를 연결할 수 있는 식별자 |
|           | 보조식별자<br>(Alternate Identifier) | 엔터티 내에서 각 어커런스를 구분할 수 있는 구분자이나 대표성을 가지지 못해 참조관계 연결을 못함  |
| 스스로 생성 여부 | 내부식별자                           | 엔터티 내부에서 스스로 만들어지는 식별자                                  |
|           | 외부식별자<br>(Foreign Identifier)   | 타 엔터티와의 관계를 통해 타 엔터티로부터 받아오는 식별자                        |
| 속성의 수     | 단일식별자<br>(Single Identifier)    | 하나의 속성으로 구성된 식별자                                        |
|           | 복합식별자<br>(Composit Identifier)  | 둘 이상의 속성으로 구성된 석별자                                      |
| 대체여부      | 본질식별자                           | 없무에 의해 만들어지는 식별자                                        |
|           | 인조식별자                           | 업무적으로 만들어지지는 않지만 원조식별자가 복잡한 구성을 가지고 있기 때문에 인위적으로 만든 식별자 |

나) 식별자 표기법
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuG4N4%2Fbtsfg2CTo10%2FgivqDQkdKoU3tMon5rxoi0%2Fimg.png)


4. 주식별자 도출 기준
	가) ==해당 업무에서 자주 이용되는 속성을 주식별자로 지정하도록 함==
	- ex. 직원이라는 엔터티의 유일 식별 가능 속성은 주민번호와 사원번호가 존재할 수 있다
	- 사원번호가 회사에서 직원을 관리할 때 흔히 사용되므로 사원번호를 주식별자로 지정하고 주민등록번호는 보조식별자로 사용
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDZ4ZP%2FbtsfcMujiJq%2FxKWcPdpr23zVHtPzNaXh31%2Fimg.png)

	나) ==명칭, 내역 등과 같이 이름으로 기술되는 것을 피함==
	- 명칭, 내역 등과 같이 이름으로 기술되는 것들은 주식별자로 지정하지 않도록 한다
	- 한 회사에 부서이름이 100개가 있다고 할 때, 각각의 부서 이름은 유일하게 구별될 수 있다고 하여 부서이름을 주식별자로 지정하지 않도록 해야 한다
	- 부서명의 경우 부서코드를 부여하여 코드 엔터티에 등록한 후 부서코드로 주식별자를 지정하는 방법과 부서일련번호(부서번호)를 주식별자로 하고 부서명은 보조식별자로 활용하는 두 가지 방법이 있다
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbk0Rlt%2FbtsfeAz9Rzx%2F9MmfSfe8t7utWBnLY8YpPk%2Fimg.png)

	다) ==속성의 수가 많아지지 않도록 함==
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDo74W%2FbtsfdbOpmm8%2FiTh6SUEls9Xo0GCOCok8rK%2Fimg.png)
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd4CYOl%2FbtsfXehb1uJ%2FlzK7EuhmwxCVYGi1RSuyk0%2Fimg.png)복잡한 쿼리
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdprGVQ%2Fbtsfvn0Fscu%2FR7kmFfXQnmE412alKgmZQK%2Fimg.png) 단순화한 쿼리

5. 식별자 관계와 비식별자 관계에 따른 식별자
	가) 식별자 관계와 비식별자 관계의 결정
	- 엔터티에 주식별자가 지정되고 엔터티 간 관계를 연결하면 부모 쪽의 주식별자를 엔터티의 속성으로 내려보낸다
	- 이 때 자식엔터티에서 부모엔터티로부터 받은 외부식별자를 자식의 주식별자로 이용할 것인지 또는 부모와 연결이 되는 속성으로서만 이용할 것인지를 결정해야 함
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKs0Oj%2FbtsfehHnF7u%2FsmSzVDf44sfG9RrUkuyvoK%2Fimg.png)

나) 식별자 관계
- 부모로부터 받은 식별자를 자식엔터티의 주식별자로 이용하는 경우는 Null값이 오면 안되므로 반드시 부모엔터티가 생성되어야 자기 자신의 엔터티가 생성
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBkeyY%2FbtsfjKu9yTr%2FiTF08R6BzcOyuKMnSDewWk%2Fimg.png)

다) 비식별자 관계
- 부모엔터티로부터 속성을 받았지만 자식엔터티의 주식별자로 사용하지 않고 일반적인 속성으로 사용하는 경우
1) 자식엔터티에서 받는 속성이 반드시 필수가 아니어도 무방하기 때문에 부모 없는 자식이 생성될 수 있다
2) 엔터티별로 데이터의 생명주기를 다르게 관리할 경우
3) 여러 개의 엔터티가 하나의 엔터티로 통합되어 표현되었는데 각각의 엔터티가 별도의 관계를 가질 때
4) 자식엔터티에 주식별자로 사용하여도 되지만 자식엔터티에서 별도의 주식별자를 생성하는 것이 더 유리하다 판단될 때
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4miBH%2FbtsfdbnkEBa%2FuTipUSFsKkm1ZSLMJ8aerK%2Fimg.png)

라) 식별자와 비식별자관계 비교

| 항목         | 식별자관계                                                                         | 비식별자관계                                                                                                                 |
| ---------- | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 목적         | 강한 연결관계 표현                                                                    | 약한 연결관계 표현                                                                                                             |
| 자식 주식별자 영향 | 자식 주식별자의 구성에 포함                                                               | 자식 일반 속성에 포함                                                                                                           |
| 표기법        | 실선 표현                                                                         | 점선 표현                                                                                                                  |
| 연결 고려사항    | - 반드시 부모엔터티 종속<br>- 자식 주식별자 구성에 부모 주식별자 포함 필요<br>- 상속받은 주식별자 속성을 타 엔터티에 이전 필요 | - 약한 종속관계<br>- 자식 주식별자 구성을 독립적으로 구성<br>- 자식 주식별자 구성에 부모 주식별자 부분 필요<br>- 상속받은 주식별자속성을 타 엔터티에 차단 필요<br>- 부모쪽의 관계참여가 선택관계 |
