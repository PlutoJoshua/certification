
## 집합연산자(SET OPERATOR)
1. 집합 연산자
- 두 개 이상의 테이블에서 조인을 사용하지 않고 연관된 데이터를 조회하는 방법 중 다른 방법
- 집합 연산자를 사용하기 위해서는 다음 제약 조건을 만족해야 함
- SELECT 절의 칼럼 수 동일
- SELECT 절의 동일 위치에 존재하는 칼럼의 데이터 타입이 상호 호환 가능(반드시 동일한 데이터 타입일 필요는 없음)
- 만족하지 않으면 데이터베이스가 오류를 반환함
- 집합 연산자의 종류

| 집합 연산자    | 연산자의 의미                                                                                                                                                                         |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UNION     | 여러 개의 SQL문 결과에 대한 합집합으로 결과에서 모든 중복된 행은 하나의 행으로 만든다                                                                                                                              |
| UNION ALL | 여러 개의 SQL문의 결과에 대한 합집합으로 중복된 행도 그대로 결과로 표시됨. = 단순히 결과만 합쳐 놓은 것. 일반적으로 여러 질의 결과가 상호 배타적인(Exclusive) 일 때 많이 사용함/ 개별 SQL문의 결과가 서로 중복되지 않는 경우, UNION과 결과가 동일하다(정렬 순서에는 차이가 있을 수 있음) |
| INTERSECT | 여러 개의 SQL 문의 결과에 대한 교집합. 중복된 행은 하나의 행으로 만든다                                                                                                                                     |
| EXCEPT    | 앞의 SQL문의 결과에서 뒤의 SQ문의 결과에 대한 차집합. 중복된 행은 하나의 행으로 만든다. (일부 DB는 NINUS를 사용)                                                                                                        |
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdixblF%2FbtshTvIadHl%2FPFfXDcm2waj7M6HwEQ4lek%2Fimg.png)

- 집합 연산자 예제
```
SELECT 칼럼명1, 칼럼명2, ...
FROM 테이블명1
[WHERE 조건식]
[[GROUP BY 칼럼이나 표현식]
[HAVING 그룹 조건식]]
집합연산자
SELECT 칼럼명1, 칼럼명2, ...
FROM 테이블명2
[WHERE 조건식]
[[GROUP BY 칼럼이나 표현식]
[HAVING 그룹 조건식]]
[ORDER BY 1, 2 [ASC 또는 DESC]];

-------------------------------------

SELECT PLAYER_NAME 선수명, BACK_NO 백넘버
FROM PLAYER
WHERE TEAM_ID = 'K02'
UNION
SELECT PLAYER_NAME 선수명, BACK_NO 백넘버
FROM PLAYER
WHERE TEAM_ID = 'K07' ORDER BY 1;
```

## 계층형 질의와 셀프 조인

1. 계층형 질의
- 테이블에 계층형 데이터가 존재하는 경우 데이터를 조회하기 위해서 계층형 질의 (Hierarchical Query)를 사용한다
- 계층형 데이터란 동일 테이블에 계층적으로 상위와 하위 데이터가 포함된 데이터를 말함
- EX. 사원 테이블에서는 사원들 사이에 상위 사원(관리자)와 하위 사원 관계가 존재하고 조직 테이블에서는 조직들 사이에 상위 조직과 하위 조직 관계가 존재한다

가) Oracle 계층형 질의
```
SELECT ...
FROM 테이블
WHERE condition AND condition ...
START WITH condition
CONNECT BY [NOCYCLE] condition AND conditon ...
[ORDER SIBLINGS BU column, column, ...]
```

> START WITH 절
- 계층 구조 전개의 시작 위치를 지정하는 구문.즉 루트 데이터를 지정함(액세스) - CONNECT BY 절은 다음에 전개될 자식 데이터를 지정하는 구문이다. 자식 데이터는 CONNECT BY 절에 주어진 조건을 만족해야 한다

> PRIOR
- CONNECT BY 절에 사용되며, 현재 읽은 칼럼을 지정한다. PRIOR 자식 = 부모 형태를 사용하면 계층 구조에서 자식데이터에서 부모데이터(자식 -> 부모) 방향으로 전개하는 순방향 전개를 한다. 그리고 PRIOR 부모  = 자식 형태를 사용하면 반대로 부모 데이터에서 자식 데이터(부모-<자식) 방향으로 전개하는 역방향 전개를 한다

> NOCYCLE
- 데이터를 전개하면서 이미 나타났던 동일한 데이터가 전개 중에 다시 나타난다면 이것을 사이클이 형성되었다고 한다. 사이클이 발생한 데이터는 런타임 오류가 발생한다. 그렇지만 NOCYCLE를 추가하면 사이클이 발생한 이후의 데이터는 전개하지 않는다

> ORDER SIBLINGS BY
- 형제 노드(동일 LEVEL) 사이에서 정렬을 수행한다

>WHERE
- 모든 전개를 수행한 후에 지정된 조건을 만족하는 데이터만 추출한다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fxq3HR%2FbtshCc4d5AJ%2FefGzfH7wmLyDQvFgY8Rne0%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMAchb%2FbtshFaygksp%2F89pDX0xXX1zZVSDR0SQOO0%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAbExD%2FbtshBk9rqDj%2FUPRQx1832HMrNH4zJQ4f5k%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcB4yFs%2FbtshMVHhagW%2Flk0Uc4dbf8G9v6kiAuT0z1%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcTyVN2%2FbtshA4MuXAC%2FQ1m23FtRe5rnv4SBvKy3e0%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsntW2%2FbtshA5xQCk1%2F77xiCLOb6hhDJMOPajUhQ1%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrI35F%2FbtshAASt7N7%2FRkNyKj0styok4M2ZOGJeK1%2Fimg.png)

START WITH 를 통해 추출된 루트 데이터가 1건이기 때문에 루트사원은 모두 A이다. 경로는 루트로부터 현재 데이터까지의 경로를 표시한다

나) SQL 계층형 질의
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8pYno%2FbtshPp9kylJ%2FF4xujm6YPgdK0ZnmCGvkI1%2Fimg.png)

- WITH 절의 CTE 쿼리를 보면, UNION ALL 연산자로 쿼리 두 개를 결합했다. 둘중 위에 있는 쿼리를 '앵커 멤버(ANCHOR MEMBER)'라고 하고, 아래에 있는 쿼리를 '재귀 멤버(RECURSIVE MEMBER)'라고 한다. 아래는 재귀적 쿼리의 처리 과정이다
- 앵커 멤버가 시작점이자 OUTER 집합이 되어 INNER 집합인 재귀 멤버와 조인을 시작한다. 이어서 앞서 조인한 결과가 다시 OUTER 집합이 되어 재귀 멤버와 조인을 반복하다가 조인 결과가 비 있으면 즉, 더 조인할 수 없으면 지금까지 만들어진 결과 집합을 모두 합하여 리턴한다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdw11yP%2FbtshBm0uCU3%2FkSpcKMpM25CEX7Sweqym60%2Fimg.png)


2. 셀프 조인
- 동일 테이블사이의 조인을 말한다. 따라서 FROM 절에 동일 테이블이 두 번 이상 나타난다. 동일 테이블 사이의 조인을 수행하면 테이블과 칼럼 이름이 모두 동일하기 때문에 식별을 위해 반드시 ALIAS를 사용해야 한다
```
SELECT ALIAS명1.칼럼명, ALIAS명2.칼럼명, ...
FROM 테이블1 ALIAS명1, 테이블2 ALIAS명2
WHERE ALIAS명1.칼럼명2 = ALIAS명2.칼럼명1;
```

```
SELECT WORKER.ID 사원번호, WORKER.NAME 사원명, MANAGER.NAME 관리자명
FROM EMP WORKER, EMP MANAGER
WHERE WORKER.MGR = MANAGER.ID;
```

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FIhmYj%2FbtshMV8nHAl%2FPCgKDt7XhmuPzzEOcFquJ1%2Fimg.png)

- 셀프 조인은 동일한 테이블(사원)이지만 그림과 같이 개념적으로는 두 개의 서로 다른 테이블을 사용하는 것과 동일하다. 동일 테이블을 다른 테이블인 것처럼 처리하기 위해 테이블 별칭을 사용한다. 여기서는 E1, E2를 사용하였다. 차상위 관리자를 구하기 위해서 E1.관리자 = E2.사원 조인 조건을 사용한다

```
SELECT E1.사원, E1.관리자, E2관리자 차상위_관리자
FROM 사원 E1, 사원 E2
WHERE E1.관리자 = E2.사원
ORDER BY E1.사원
```

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbIcjpW%2FbtshTvIb26c%2F418KOMrKvwXMmEvYkkLtl0%2Fimg.png)

