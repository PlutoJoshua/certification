
## 서브쿼리

1. 서브쿼리(SubQuery)
- 하나의 SQL문 안엔 포함되어 있는 또 다른 SQL문
- 서브 쿼리는 메인 쿼리의 칼럼을 모두 사용할 수 있지만 메인 쿼리는 서브 쿼리의 칼럼을 사용할 수 없다
- 서브쿼리를 사용할 때 주의점
- 서브쿼리를 괄호로 감사서 사용한다
- 서브쿼리는 단일행 또는 복수 행 비교 연산자와 함께 사용 가능하다. 단일행 비교 연산자는 서브 쿼리의 결과가 반드시 1건 이하이어야 하고 복수행 비교 연산자는 서브쿼리의 결과 건수와 상관 없다
- 서브 쿼리에서는 ORDER BY를 사용하지 못한다.  ORDER BY 절은 SELECT 절에서 오직 한 개만 올 수 있기 때문에 ORDER BY 절은 메인 쿼리의 마지막 문장에 위치해야 한다

```
서브 쿼리가 SQL문에서 사용 가능한 곳
- SELECT 절
- FROM 절
- WHERE 절
- HAVING 절
- ORDER BY 절
- INSERT 문의 VALUES절
- UPDATE 문의 SET 절
```

- 동작하는 방식에 따른 서브 쿼리 분류

| 서브쿼리 종류                    | 설명                                                                                            |
| -------------------------- | --------------------------------------------------------------------------------------------- |
| UN-CORRELATED<BR>(비연관)서브쿼리 | 서브 쿼리가 메인 쿼리 칼럼을 가지고 있지 않는 형태의 서브쿼리. 메인쿼리에 값(서브쿼리가 실행된 결과)을 제공하기 위한 목적으로 주로 사용                |
| CORRELATED(연관)서브쿼리         | 서브쿼리가 메인쿼리 칼럼을 가지고 있는 형태의 서ㅂ,쿼리. 일반적으로 메인 쿼리가 먼저 수행되어 읽혀진 데이터를 서브쿼리에서 조건이 맞는지 확인하고자 할 때 주로 사용 |
- 반환되는 데이터의 형태에 따른 서브쿼리 분류

| 서브쿼리 종류                       | 설명                                                                                                         |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------- |
| SINGLE ROW 서브쿼리(단일행 서브쿼리)     | 서브 쿼리의실행 결과가 항상 1건 이하인 서브쿼리. 단일 행 서브쿼리는 단일행 비교 연산자와 함께 사용된다. 단일행 비교 연산자에는 (=, <, <=, >, >=, <>)이 있다        |
| MULTI ROW 서브쿼리(다중행 서브쿼리)      | 서브쿼리의 실행 결과가 여러 건인 서브쿼리를 의미. 다중 행 서브쿼리는 다중행 비교연산자와 함께 사용된다. 다중행 비교 연산자에는 (IN ,ALL, ANY, SOME, EXISTS) 가 있다 |
| MULTI COLUMN 서브쿼리(다중 칼럼 서브쿼리) | 서브쿼리의 실행 결과로 여러 칼럼을 반환한다. 메인 쿼리의 조건절에 여러 칼럼을 동시에 비교할 수 있다. 서브 쿼리와 메인 쿼리에서 비교하고자 하는 칼럼 개수와 컬럼의 위치가 동일해야 한다  |

2. 단일행 서브 쿼리
- 서브 쿼리가 단일행 비교연산자와 함께 사용할 때는 서브쿼리의 결과 건수가 반드시 1건 이하여야 한다
- 만약 서브쿼리의 결과 건수가 2건 이상을 반환하면 SQL문은 실행시간(RUNTIME)오류 발생
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFTP3o%2Fbtshz1o4b7Y%2FbK2KUP4fXq09sqa7NbI8N0%2Fimg.png)
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbA5WAe%2FbtshBiXUz5v%2F78vLIRH8HaKgWvIgAB18T1%2Fimg.png)
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbmg8qf%2FbtshE1nXdcF%2FYNKRP1KARoS3oWH4ZDoaB1%2Fimg.png)
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoQv30%2FbtshRxe3km2%2Fhkx6dLaIkaRBPV3uH3iNHK%2Fimg.png)

3. 다중행 서브 쿼리
- 서브 쿼리의 결과가 2건 이상 반환될 수 있다면 반드시 다중행 비교연산자와 함께 사용

| 다중행 연산자          | 설명                                                                                                                                              |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| IN (서브쿼리)        | 서브쿼리의 결과에 존재하는 임의의 값과 동일한 조건을 의미 (Multiple OR 조건)                                                                                               |
| 비교연산자 ALL (서브쿼리) | 서브쿼리의 결과에 존재하는 모든 값을 만족하는 조건을 의미. 비교 연산자로 ">"를 사용했다면 메인 쿼리는 서브쿼리의 모든 결과 값을 만족해야 하므로, 서브쿼리 결과의 최대값보다 큰 모든 건이 조건을 만족한다                            |
| 비교연산자 ANY (서브쿼리) | 서브쿼리의 결과에 존재하는 어느 하나의 값이라도 만족하는 조건. 비교 연산자로 ">"를 사용했다면 메인 쿼리는 서브 쿼리의 값들 중 어떤 값이라도 만족하면 되므로, 서브 쿼리의 결과의 최소값보다 큰 모든 건이 조건을 만족한다. (SOME은 ANY와 동일함) |
| EXSISTS (서브쿼리)   | 서브쿼리의 결과를 만족하는 값이 존재하는지 여부를 확인하는 조건을 의미. 조건을 만족하는 건이 여러 건이더라도 1건만 찾으면 더이상 검색하지 않음                                                               |

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclUK4B%2FbtshHNCNUpX%2FRpx7K35a8gr4OL7nzTJoT1%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJw626%2FbtshBknTPEk%2FRRF6HUQY2kkYOJYQxKdiU0%2Fimg.png)


4. 다중 칼럼 서브 쿼리
 - 서브쿼리의 결과로 여러 개의 칼럼이 반환되어 메인 쿼리의 조건과 동시에 비교되는 것
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc1Ul3n%2FbtshCcpBKCU%2FMADEMTDA55f1rOcjqkEX6K%2Fimg.png)

5. 연관 서브 쿼리
- 서브쿼리 내에 메인 쿼리 칼럼이 사용된 서브쿼리
-![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FckYim8%2FbtshCeVoEgS%2FqmBUucpqaAKzZEhiftar41%2Fimg.png)
평균 키보다 선수의 키가 크거나 같으면 조건이 맞지 않기 때문에 해당 데이터는 출력되지 않는데. 이와 같은 작업을 메인 쿼리에 존재하는 모든 행에 대해서 반복 수행한다

- EXISTS 서브쿼리는 항상 연관 서브쿼리로 사용된다. 또한 EXISTS 서브쿼리의 특징은 아무리 조건을 만족하는 건이 여러건이더라도 조건을 만족하는 1건만 찾으면 추가적인 검색을 진행하지 않는다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdicsFz%2FbtshMVm0nV1%2F2A1IbbkptJFbl4J40eFdL0%2Fimg.png)


6. 그 밖의 위치에서 사용하는 서브쿼리
가) SELECT  절에 서브쿼리 사용하기
- 스칼라 서브쿼리는 한행, 한 칼럼만을 반환하는 서브쿼리를 말한다. 스칼라 서브쿼리는 칼럼을 쓸 수 있는 대부분의 곳에서 사용할 수 있다
- 스칼라 서브쿼리 또한 단일 행 서브쿼리이기 때문에 결과가 2건 이상 반환되면 SQL문은 오류를 반환한다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvQi6M%2Fbtshz1o4yQE%2FZoL5WQ9Ew5oQIOD96jc2K0%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGerq8%2FbtshG8NR6fY%2FxsdWWWHHuKIPVVIdpKFKl0%2Fimg.png)


나) FROM 절에서 서브쿼리 사용하기
- FROM 절에서 사용되는 서브쿼리를 인라인 뷰(Inline View)라고 한다
- 서브쿼리의 결과가 마치 실행 시에 동적으로 생성된 테이블인 것처럼 사용할 수 있다
- 인라인 뷰는 SQL문이 실행될 때만 임시적으로 생성되는 동적인 뷰이기 때문에 데이터베이스에 해당 정보가 저장되지 않는다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdCDCTj%2FbtshCglofv5%2F1SokOtA79R87vINb39K4vK%2Fimg.png)

다) HAVING 절
- HAVING 절은 그룹함수와 함께 사용될 때 그룹핑된 결과에 대해 부가적인 조건을 주기 위해서 사용함
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F02dJc%2FbtshG8mP3JY%2F4NCKixo369yht6Exwz5nw1%2Fimg.png)


라) UPDATE문의 SET 절
- 현재 TEAM 테이블에는 STADIUM_NAME 칼럼이 없다. TEAM 테이블에 STADIUM_NAME을 추가했다고 가정하다. TEAM 테이블에 추가된 STADIUM_NAME의 값을 STADIUM 테이블을 이용하혀 변경하고자 할 때 다음과 같이 SQL문을 작성할 수 있다
- 서브쿼리의 결과가 NULL을 반환할 경우 해당 칼럼의 결과가 NULL이 될 수 있기 때문에 주의
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3WsOE%2FbtshE1VNuZP%2FYkzk52hxVZiLKRkLvEc9k1%2Fimg.png)

마) INSERT문의 VALUES 절
- PLAYER 테이블에 '홍길동' 선수를 삽입하고자 한다. 이때 PLAYER_ID 값을 현재 사용중인 PLAYER_ID에 1을 더한 값으로 넣고자 한다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fu5WTb%2FbtshG8AoRzp%2Fk1CMeTNvexCJRSAe20c3T1%2Fimg.png)


7. 뷰(View)
- 테이블은 실제로 데이터를 가지고 있는 반면, 뷰는 실제 데이터를 가지고 있지 않다. 뷰는 단지 뷰 정의(VIEW DEFINITION)만을 가지고 있다. 질의에서 뷰가 사용되면 뷰 정의를 참조해서 DBMS 내부적으로 질의를 재작성하여 질의를 수행한다
- 뷰 사용의 장점

| 장점  | 설명                                                                                   |
| --- | ------------------------------------------------------------------------------------ |
| 독립성 | 테이블 구조가 변경되어도 뷰를 사용하는 응용 프로그램은 변경하지 않아도 됨                                            |
| 편리성 | 복잡한 질의를 뷰로 생성함으로써 관련 질의르 단순하게 작성 가능. <br>또한 해당 형태의 SQL문을 자주 사용할 때 뷰를 이용하면 편리하게 사용 가능 |
| 보안성 | 직원의 급여정보와 같이 숨기고 싶은 정보가 존재한다면 뷰를 생성할 때 <BR>해당 칼럼을 빼고 생성함으로써 사용자에게 정보를 감출 수 있다        |

- 뷰는 DREATE VIEW문을 통해서 생성
```
DREATE VIEW V_PLAYER_TEAM
AS SELECT P.PLAYER_NAME, P.POSITION, P.BACK_NO, P.TEAM.ID, T.TEAM_NAME
	FROM PLAYER P, TEAM T
	WHERE P.TEAM_ID = T.TEAM_ID;
```

- 뷰 제거(DROP)
```
DROP VIEW V_PLAYER_TEAM;
DROP VIEW V_PLAYER_TEAM_FILTER;
```

