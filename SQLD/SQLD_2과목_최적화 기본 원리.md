
1. 옵티마이저와 실행계획
- Optimizer : 사용자가 질의한 SQL문에 대해 최적의 실행 방법을 결정하는 역할 수행
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcHEWe9%2FbtsivQZsg4f%2Fn7LkFoKpnqizV2nSeQFAFK%2Fimg.png)

가) 규칙 기반 옵티마이저
- 규칙 기반 옵티마이저가 실행계획을 생성할 때 참조하는 정보에는 SQL문을 실행하기 위해서 이용 가능한 인덱스 유무와 (유일, 비유일, 단일, 복합 인덱스) 종류, SQL 문에서 사용하는 연산자의 종류, SQL문에서 참조하는 객체(힙 테이블, 클러스터 테이블 등)의 종류 등이 있다

| 순위  | 엑세스 기법                                                    | 규칙                                            |
| --- | --------------------------------------------------------- | --------------------------------------------- |
| 1   | Single row by rowid                                       | ROWID를 통해서 테이블에서 하나의 행을 액세스 하는 방식             |
| 2   | Single row by cluster join                                |                                               |
| 3   | Single row by hash cluster key with unique or primary key |                                               |
| 4   | Single row by unique or primary key                       | 유일 인덱스를 통해 하나의 행을 엑세스하는 방식                    |
| 5   | cluster join                                              |                                               |
| 6   | Hash cluster key                                          |                                               |
| 7   | Indexed cluster key                                       |                                               |
| 8   | Composite index                                           | 복합 인덱스에 동등 조건으로 검색하는 경우                       |
| 9   | Single column index                                       | 단일 칼럼 인덱스에 = 조건으로 검색하는 경우                     |
| 10  | Bounded range search on indexed columns                   | 인덱스가 생성되어 있는 칼럼에 양쪽 범위를 한정하는 형태를 검색하는 방식      |
| 11  | UnBounded range search on indexed columns                 | 인덱스가 생성되어 있는 칼럼에 한쪽 범위만 한정하는 형태로 검색 방식        |
| 12  | Sort marge join                                           |                                               |
| 13  | MAX or Min of indexed column                              |                                               |
| 14  | ORDER by on indexed column                                |                                               |
| 15  | Full table scan                                           | 전체 테이블을 액세스하면서 조건절에 주어진 조건을 만족하는 행만을 결과로 추출한다 |

나) 내용기반 옵티마이저
- 비용 기반 옵티마이저: SQL문을 처리하는데 필요한 비용이 가장 적은 실행계획을 선택하는 방식
- 비용: SQL문을 처리하기 위해 예상되는 소요시간 또는 자원 사용량
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUTc2d%2Fbtsiwjm0BD9%2Fc99B2e7wn18jsp6PttX7T1%2Fimg.png)

- 대안 계획 생성기 : 동일한 결과를 생성하는 다양한 대안 계획을 생성하는 모듈
- 비용 예측기 : 대안 계획 생성기에 의해서 생성된 대안 계획의 비용을 예측하는 모듈

2. 실행 계획
- 실행계획 : SQL에서 요구한 사항을 처리하기 위한 절차와 방법
- 실행계획 구성 요소 : 조인 순서 , 조인 기법, 액세스 기법, 최적화 정보, 연산 등이 있다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnecUS%2FbtsitAp6VYk%2FFPAiBYkfhC8U3c24Ir5Quk%2Fimg.png)

- 조인 기법 : 두 개의 테이블을 조인할 때 사용할 수 있는 방법. NL JOIN, HASH JOIN, Sort Merge JOIN 등
- 액세스 기법 : 하나의 테이블을 액세스 할 때 사용할 수 있는 방법. 테이블을 액세스하는 인덱스 스캔과 테이블 전체를 모두 읽으면서 조건을 만족하는 행을 찾는 전체 테이블 스캔 등이 있다
- 최적화 정보 : 옵티마이저가 실행계획의 각 단계마다 예상되는 비용 사항을 표시한 것
- 연산 : 여러가지 조작을 통해서 원하는 결과를 얻어내는 일련의 작업. 연산에는 조인기법, 액세스 기법, 필터, 정렬, 집계, 뷰 등 다양한 종류가 존재함

3. SQL 처리 흐름도
- SQL의 내부적인 처리 절차를 시각적으로 표현한 도표. 실행 계획을 시각화 한 것
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKFbty%2FbtsiuJfwrPm%2FKnfdRO9BTfs7q6lkOtZzn1%2Fimg.png)


## 최적화 기본 원리(인덱스 기본)

1. 인덱스 특징과 종류
- 원하는 데이터를 쉽게 찾을 수 있도록 돕는 책의 찾아보기와 유사한 개념
- 테이블을 기반으로 선택적으로 생성할 수 있는 구조
- 인덱스의 기본적인 목적 : 검색 성능 최적화
- INSERT, UPDATE, DELETE 같은 DML 작업은 테이블과 인덱스를 함께 변경해야 하기 때문에 오히려 느려질 수 있다는 단점이 존재

가) 트리 기반 인덱스
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdaHnI8%2FbtsiBJyVaJM%2FiuMxENOafk92nCOjWccts0%2Fimg.png)

- Root Block : 브랜치 블록 중에서 가장 상위에 있는 블록
- Branch Block : 분기를 목적으로 하는 블록
- Leaf Block : 트리의 가장 아래 단계에 존재
- Oracle에서 트리 기반 인덱스에는 B-트리 인덱스 외에도 비트맵 인덱스, 리버스 키 인덱스, 함수 기반 인덱스 등이 존재함

나) SQL 클러스터형 인덱스
- SQL 인덱스 종류는 저장 구조에 따라 클러스터형 인덱스와 비클러스텋ㅇ 인덱스로 나뉜다
- 클러스터형 인덱스 특징
- 인덱스의 리프 페이지가 곧 데이터 페이지. 따라서 테이블 탐색에 필요한 레코드 식별자가 리프 페이지에 없다
- 리프체이지의 모든 로우(=데이터)는 인덱스 키 칼럼 순으로 물리적 정렬되어 저장된다
- EmployeeID 기반 클러스터형 인덱스 생성
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdq5PyL%2FbtsizcnRfFT%2FZYzVtPCkurSQEuvPZo7KdK%2Fimg.png)
- 리프 블록에 인덱스 키 칼럼 외에도 테이블의 나머지 칼럼이 모두 함께 있다

2. 전체 테이블 스캔과 인덱스 스캔

가) 전체 테이블 스캔
- 테이블에 존재하는 모든 데이터를 읽어가면서 조건에 맞으면 결과로써 추출하고 조건에 맞지 않으면 버리는 방식으로 검색
- 검색 조건에 맞는 데이터를 찾기 위해서 테이블의 고수위 마크(HMM, High Water Mark) 아래의 모든 블록을 읽는다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLe5Z2%2Fbtsiu0IeppI%2FkZa3Fgz7Y2vpbwwtBeYHcK%2Fimg.png)

- 이와 같이 전체 테이블 스캔 방식은 테이블에 존재하는 모든 블록의 데이터를 읽는다. 그러나 이것은 결과를 찾기 위해 꼭 필요해서 모든 블록을 읽는 것 > 이렇게 읽은 블록들은 재사용성 떨어짐 > 전체 테이블 스캔 방식으로 읽은 블록들은 메모리에서 곧 제거될 수 있도록 관리됨

> 옵티마이저가 연산으로서 전체 테이블 스캔 방식을 선택하는 이유
1) SQL 문에 조건이 존재하지 않는 경우 (모든 데이터가 답이 됨)
2) SQL문의 주어진 조건에 사용 가능한 인덱스가 존재하지 않는 경우
3) 옵티마이저의 취사 선택(조건을 만족하는 데이터가 많은 경우)
4) 병렬처리 방식으로 처리하는 경우 또는 전체 테이블 스캔 발식의 힌트를 사용한 경우

나) 인덱스 스캔
- 인덱스를 구성하는 칼럼의 값을 기반으로 데이터를 추출하는 액세스 기법
- 검색을 위해 인덱스의 리프 블록을 읽으면 인덱스 구성 칼럼의 값과 테이블의 레코드 식별자를 알 수 있다
- 인덱스 유일 스캔 : 유일 인덱스를 사용하여 단 하나의 데이터를 추출하는 방식. 유일 인덱스 구성 칼럼에 대해 모두 '=' 값이 주어진 경우에만 가능한 인덱스 스캔 방식
- 인덱스 범위 스캔 : 인덱스를 이용하여 한 건 이상의 데이터를 추출하는 방식 
-  인덱스 역순 범위 스캔 : 인덱스의 리프 블록의 양방향 링크를 이용하여 내림차순으로 데이터를 읽는 방식
- 이 방식을 이용하여 최대값을 쉽게 찾을 수 있다. 이또한 인덱스 범위 스캔의 일종
- 이외에도 인덱스 전체 스캔, 인덱스 고속 전체 스캔, 인덱스 스킵 스캔 등이 존재
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHcLSX%2FbtsiBL4A7gU%2FfkB46GX62TW1Qk3jc1mXO0%2Fimg.png)

다) 전체 테이블 스캔 VS 인덱스 스캔 방식
> 데이터를 액세스 하는 방법
1. 인덱스 스캔 방식 : 인덱스를 경유해서 읽음
2. 전체 테이블 스캔 방식 : 테이블의 전체 데이터를 모두 읽으면서 데이터를 추출함

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdhjH38%2FbtsisPVyDa6%2FvqGNwkJ5MOrU7xNb19kb5k%2Fimg.png)

## SQL 최적화 기본 원리(조인 수행 원리)

1. 조인 수행 원리
- 조인 : 두 개 이상의 테이블을 하나의 집합으로 만드는 연산. SQL문에서 FROM 절에 두 개 이상의 테이블이 나열될 경우 조인이 수행됨
- 조인 기법은 두 개의 테이블을 조인할 때 사용할 수 있는 방법. 여기서는 조인 기법 중에서 자주 사용되는 NL JOIN, HASH JOIN, Sort Merge Join 등이 있다

2. NL JOIN
- 프로그래밍에서 사용하는 중첩된 반복문과 유사한 방식으로 조인을 수행
```
FOR 선행 테이블 읽음 -> 외부 테이블
	FOR 후행 테이블 읽음 -> 내부 테이블
		(선행 테이블과 후행 테이블 조인)
```

> NL JOIN의 작업 방법
1) 선행 테이블에서 주어진 조건을 만족하는 행을 찾음
2) 선행 테이블의 조인 키 값을 가지고 후행 테이블에서 조인 수행
3) 선행 테이블의 조건을 만족하는 모든 행에 대해 1번 작업 반복 수행

- NL JOIN 기법은 조인이 성공하면 바로 조인 결과를 사용자에게 보여줄 수 있다. 그래서 결과를 가능한 한 빨리 화면에 보여줘야 하는 온라인 프로그램에 적당한 조인 기법이다.

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc3bkWc%2FbtsiuBvaB0Q%2FxA4rk00JuABzpcOsVEgpS1%2Fimg.png)

3. Sort Merge Join
- 조인 칼럼을 기준으로 데이터를 정렬하여 조인을 수행한다
- 주로 스캔 방식으로 데이터를 읽는다
- 랜덤 액세스로 NL JOIM에서 부담이 되던 넓은 범위의 데이터를 처리할 때 이용되던 조인 기법이다
- 정렬할 데이터가 많아 메모리에서 모든 정렬 작업을 수행하기 어려운 경우에는 임시 영역을 사용해 성능이 떨어질 수 있다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbowomi%2FbtsitSEffJA%2Ft5HoMOCJUB80TTyOUBZKc0%2Fimg.png)

- Sort Merge Join의 동작
1) 선행 테이블에서 주어진 조건을 만족하는 행을 찾음
2) 선행 테이블의 조인 키를 기준으로 정렬 작업 수행
3)  1~2) 작업을 선행 테이블의 조건을 만족하는 모든 행에 대해 반복 수행
4) 후행 테이블에서 주어진 조건을 만족하는 행을 찾음
5) 후행 테이블의 조인 키를 기준으로 정렬 작업을 수행
6)  4~5) 작업을 후행 테이블의 조건을 만족하는 모든 행에 대해 반복 수행
7) 정렬된 결과를 이용하여 조인을 수행하며 조인에 성공하면 추출 버퍼에 놓음

- Sort Merge Join은 조인 칼럼의 인덱스를 사용하지 않기에 조인 칼럼의 인덱스가 존재하지 않을 경우에도 사용할 수 있는 조인 기법

3. Hash Join
- 해슁 기법을 이용하여 조인 수행
- 조인을 수행할 테이블의 조인 칼럼을 기준으로 해쉬 함수를 수행하여 서로 동일한 해쉬 값을 갖는 것들 사이에서 실제 값이 같은지를 비교하면서 조인을 수행
- Hash Join은 NL Join의 랜덤 액세스 문제점과 Sort Merge Join의 문제점인 정렬 작업의 부담을 해결하기 위한 대안으로 등장하였다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcEecEj%2FbtsitUvjP61%2FnWmvCuImRmbEfrvSgXDXq0%2Fimg.png)

- Hash Join의 동작
1) 선행 테이블에서 주어진 조건을 만족하는 행을 찾음
2) 선행 테이블의 조인 키를 기준으로 해쉬 함수를 적용하여 해쉬 테이블을 생성
		-> 조인 칼럼과 SELECT 절에서 필요로 하는 칼럼도 함께 저장됨
3) 1~2) 작업을 선행 테이블의 조건을 만족하는 모든 행에 대해 반복 수행
4) 후행 테이블에서 주어진 조건을 만족하는 행을 찾음
5) 후행 테이블의 조인 키를 기준으로 해쉬 함수를 적용해 해당 버킷을 찾음
		-> 조인 키를 이용해서 실제 조인될 데이터를 찾음
6) 조인에 성공하면 추출 버퍼에 넣음
7) 4~6) 작업을 후행 테이블의 조건을 만족하는 모든 행에 대해서 반복 수행

- Hash Join은 조인 칼럼의 인덱스를 사용하지 않기 때문에 조인 칼럼의 인덱스가 존재하지 않을 경우에도 사용할 수 있는 조인 기법
- Hash Join에서는 선행 테이블을 이용하여 먼저 해쉬 테이블을 생성한다고 해서 선행 테이블을 Build Input이라고도 하며, 후행 테이블은 만들어진 해쉬 테이블에 대해 해쉬값의 존재 여부를 검사한다고 해서 Prove Input이라고도 한다