## ORDER BY 절
1. ORDER BY 정렬
- SQL 문장으로 조회된 데이터들을 다양한 목적에 맞게 특정 칼럼을 기준으로 출력하는데 사용함
- 칼럼명 대신에 SELECT 절에서 사용한 ALIAS 명이나 칼럼 순서를 나타내는 정수도 사용 가능
- 별도로 정렬방식을 지정하지 않으면 기본적으로 오름차순이 적용되며, SQL 문장의 제일 마지막에 위치함
- ORDER BY 절에서 칼럼명, ALIAS 명, 칼럼 순서를 같이 혼용하는 것도 가능함
```
SELECT 칼럼명 [ALIAS 명]
FROM 테이블명
[WHERE 조건식]
[GROUP BY 칼럼이나 표현식]
[HAVING 그룹 조건식]
[ORDER BY 칼럼이나 표현식 [ASC 또는 DESC]];

ASC : 오름차순(기본값)
DESC : 내림차순
```

2. SELECT 문장 실행 순서
- GROUP BY 절과 ORDER BY 가 같이 사용될 때 SELECT 문장은 6개의 절로 구성되고, SELECT 문장의 수행 단계는 아래와 같다
```
5. SELECT 칼럼명 ALIAS 명
1. FROM 테이블명
2. WHERE 조건식
3. GROUP BY 칼럼이나 표현식
4. HAVING 그룹조건식
6. ORDER BY 칼럼이나 표현식;
```

1) 발췌 대상 테이블을 참조한다(FROM)
2) 발췌 대상 데이터가 아닌 것은 제거한다 (WHERE)
3) 행들을 소그룹화한다 (GROUP BY)
4) 그룹핑된 값의 조건에 맞는 것만을 출력한다 (HAVING)
5) 데이터 값을 출력/계산한다 (SELECT)
6) 데이터를 정렬한다 (ORDER BY)

3. TOP N 쿼리
> ROWNUM

- Oracle에서 순위가 높은 N개의 로우를 추출하기 위해 ORDER BY 절과 WHERE 절의 ROWNUM 조건을 같이 사용하는 경우가 있는데 이 두 조건으로 원하는 결과를 얻을 수 없다
- ROWNUM 조건을 ORDER BY 절보다 먼저 처리되는 WHERE 절에서 처리하므로, 정렬 후 원하는 데이터를 얻기 위해서는 인라인 뷰에서 먼저 데이터 정렬을 수행한 후 메인 쿼리에서 ROWNUM 조건을 사용해야 함

> TOP()

- SQL는 TOP 조건을 사용하게 되면 별도 처리 없이 관련 Orader By절의 데이터 정렬 후 원하는 일부 데이터만 쉽게 출력할 수 있다
- TOP절을 사용하여 결과 집합으로 반환되는 행 수를 제한할 수 있다. WITH TIES 옵션은 ORDER BY 절의 조건 기준으로 TOP N의 마지막 행으로 표시되는 추가 행의 데이터가 같을 경우 N+ 동일 순서 데이터를 추가 반환하도록 지정하는 옵션이다

## 조인(JOIN)
1. 개요
- 두 개 이상의 테이블들을 연결 또는 결합하여 데이터를 출력하는 것
- JOIN은 관계형 데이터베이스의 가장 큰 장점이면서 대표적인 핵심 기능
- 일반적인 경우 행들은 PRIMARY KEY(PK)나 FOREIGN(FK)값의 연관에 의해 JOIN이 성립된다. 하지만 어떤 경우에는 이러한 PK, FK 관계 없이 논리적인 값들의 연관만으로 JOIN이 성립 가능함

2. EQUI JOIN
- 두 개의 테이블 간에 칼럼 값들이 서로 정확하게 일치하는 경우에 사용하는 방법으로 대부분 PK <->FK 관계 기반
- 그러나 일반적으로 테이블 설계 시에 나타난 PK <-> FK의 관계를 이용하는 것이지 반드시 PK <-> FK의 관계로만 EQUI JOIN이 성립하는 것은 아니다

```
SELECT 테이블1.칼럼명, 테이블2.칼럼명, ...
FROM 테이블1, 테이블2
WHERE 테이블1.칼럼명1 = 테이블2.칼럼명2;
 -> WHERE 절에 JOIN 조건을 넣는다
```

- 같은 내용을 ANSI/ISO SQL 표준 방식으로 표현하면 아래와 같다

```
SELECT 테이블1.칼럼명, 테이블2.칼럼명, ...
FROM 테이블1 INNER JOIN 테이블2
ON 테이블1.칼럼명1 = 테이블2.칼럼명2;
 -> ON 절에 JOIN 조건을 넣는다
```

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkBxFX%2FbtshzCbyP9n%2FIjN3lvixZKeL5BAPrQDiK0%2Fimg.png)

3. Non EQUI JOIN
- 두 개의 테이블 간에 칼럼값들이 서로 정확하게 일치하지 않는 경우 사용됨
- "=" 연산자가 아닌 다른 연산자(BETWEEN, >, >=, <, <= 등) 연산자들을 사용해 JOIN 수행

```
SELECT 테이블1.칼럼명, 테이블2.칼럼명, ...
FROM 테이블1, 테이블2
WHERE 테이블1.칼럼명 BETWEEN 테이블2.칼럼명1 AND 테이블2.칼럼명2;
```

4. 3개 이상 TABLE JOIN
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbzpkLX%2FbtshBj9TXEB%2F2EQVQ1z5RBpiq0YTwyVAM1%2Fimg.png)

- JOIN이 필요한 기본적인 이유는 정규화에서 부터 출발함. 정규화란 불필요한 데이터의 정합성을 확보하고 이상현상 발생을 피하기 위해 테이블을 분할하여 생성하는 것
- 성능 측면에서도 간단한 데이터를 조회하는 경우에도 규모가 큰 테이블에서 필요한 데이터를 찾아야 하기 때문에 오히려 검색 속도가 떨어질 수도 있다
- 관계형 데이터베이스의 큰 장점이면서 SQL 튜닝의 중요 대상이 되는 JOIN을 잘못 기술하게 되면 시스템 자원 부족이나 과다한 응답시간 지연을 발생시키는 주요 원인이 되므로 JOIN 조건은 신중히 작성
## 표준 조인(STANDARD JOIN)
1. 개요
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUVS1r%2FbtshAwCgH5v%2FoKE3wWKM89GKy1rllHxreK%2Fimg.png)

가) 일반 집합 연산자
- UNION : 수학의 합집합 제공
- INTERSECTION : 수학의 교집합 제공 -> INTERSECT
- DIFFERENCE : 수학의 차집합 제공 -> EXCEPT(Oracle은 MINUS)
- PRODUCT : 수학의 곱집합 제공 -> CROSS JOIN 으로 구현됨
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fq0En1%2FbtshArnO9iW%2F2QS82HzSmzPDEJ77mXl5F0%2Fimg.png)

나) 순수관계 연산자
- 관계형 데이터베이스를 구현하기 위해 새롭게 만들어진 연산자
- SELECT 연산 : SQL 문장에서 WHERE 절의 조건절 기능으로 구현(SELECT 연산과 SELECT 절의 의미가 다름)
- PROJECT 연산 : WHERE 절의 INNER JOIN 조건과 함께 FROM 절의 NATURAL JOIN, INNER JOIN, OUTER JOIN, USING 조건절, ON 조건절 등으로 가장 다양하게 발전
- DIVIDE 연산은 나눗셈과 비슷한 개념으로 왼쪽 집합을 'XZ'로 나누었을 때, 즉 'XZ'를 모두 가지고 있는 'A'가 답이 되는 기능으로 현재 사용되지 않음

1. FROM 절 JOIN 형태
- INNER JOIN : WHERE 절에서부터 사용하던 JOIN의 DEFAULT 옵션으로 JOIN 조건에서 동일한 값이 있는 행만 반환함. DEFAULT 옵션으므로 생락 가능하지만, CROSS / OUTER JOIN과는 같이 사용할 수 없다
- NATURAL JOIN : INNER JOIN의 하위 개념으로 NATURAL JOIN은 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 EQUI JOIN을 수행한다. NATURAL INNER JOIN이라고도 표시할 수 있으며, 결과는 NATURAL JOIN과 같다
- USING 조건절
- ON 조건절 : NATURAL JOIN 처럼 JOIN 조건이 숨어 있지 않고, 명시적으로 JOIN 조건을 구분할 수 있고, NATURAL JOIN 이나 USING 조건절 처럼 칼럼명이 똑같아야 된다는 제약없이 칼럼명이 상호 다르더라도 JOIN조건으로 사용할 수 있으므로 앞으로 가장 많이 사용될 것으로 예상된다. 다만, FROM 절에 테이블이 많이 사용될 경우 다소 복잡하게 보여 가독성이 떨어지는 단점이 있다.

3. INNER JOIN
- OUTER JOIN과 대비하여 내부 JOIN이라고 하며 JOIN 조건에서 동일한 값이 있는 행만 반환함. INNER JOIN표시는 그동안 WHERE 절에서 사용하면 JOIN 조건을 FROM절에서 정의하겠다는 표시이므로 USING 조건절이나 ON 조건절을 필수적으로 사용해야 한다

```
WHERE 절 JOIN 조건

SELECT EMP.DEPTNO, EMPNO, ENAME, DNAME
FROM EMP, DEPT
WHERE EMP.DEPNO = DEPT.DEPTNO;
```

4. NATURAL JOIN
- 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 EQUI JOIN 수행
- NATURAL JOIN이 명시되면 추가로 USING 조건절, ON 조건절, WHERE 절에서 JOIN 조건을 정의할 수 없다. 그리고 SQL 에서는 지원하지 않는 기능임
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb62M1K%2FbtshRxTAvPA%2FS7UESoQ7ZDAYcQrRGXPkRk%2Fimg.png)

5. USING 조건절
- 모든 일치되는 칼럼들에 대해 JOIN이 이루어지지만 FROM 절의 USING 조건절을 이용하면 같은 이름을 가진 칼럼들 중에서 원하는 칼럼에 대해서만 선택적으로 EQUI JOIN을 할 수 있다. 다만 이 기능은 SQL에서 지원하지 않는다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb9uvkc%2FbtshCbxpxbG%2Ff1CLFxJBdfgxqLzOLQXrK0%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fle53z%2FbtshA3NyRDr%2Fd8AObvN8ljhrXEmwHyxZ1k%2Fimg.png)

6. ON 조건절
- JOIN 서술부(ON 조건절)와 비 JOIN(WHERE 조건절)를 분리하여 이해가 쉬우며, 칼럼명이 다르더라도 JOIN 조건을 사용할 수 있는 장점이 있다
- USING 조건절을 이용한 JOIN 에서는 JOIN 칼럼에 대해서 ALIAS나 테이블명과 같은 접두사를 사용하면 SYMTAX에러사 발생하지만, 반대로 ON 조건절을 사용한 JOIN의 경우에는 ALIAS나 테이블명과 같은 접두사를 사용하여 SELECT에 사용되는 칼럼을 논리적으로 명확하게 지정해주어야 한다.(DEPTNO -> E.DEPTNO)
- ON 조건절은 WHERE 절의 JOIN 조건과 같은 기능을 하면서도 명시적으로 JOIN의 조건을 구분할 수 있으므로 가장 많이 사용될 것으로 예상된다. 다만 FROM 절에 테이블이 많이 사용될 경우 다소 복잡하게 보여 가독성이 떨어지는 단점이 있다

가) WHERE절과의 혼용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcxDyLV%2FbtshCbqBJ55%2FO6mIXl3bflDYKtPksslKF0%2Fimg.png)

나) ON 조건절 + 데이터 검증 조건 추가
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbdwkpr%2FbtshBjbmEt3%2F3NxYEdmtRhZnuPK1ckeTY0%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPtzU3%2FbtshCeA0jSW%2Fvw85maeBbOoorCax71aEr1%2Fimg.png)

다) ON 조건절 예제
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5ynsv%2FbtshA5xNnT5%2F4hnS2dGiSVHof7tbsKOOX1%2Fimg.png)

라) 다중 테이블 JOIN
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEc0lx%2FbtshTvVFawn%2FqMUI4ZbKFD5rX7goQi4L41%2Fimg.png)

7. CROSS JOIN
- 일반 집합 연산자의 PRODUCT의 개념으로 테이블간 JOIN 조건이 없는 경우 생길 수 있는 모든 데이터의 조합
- 정상적인 데이터 모델이라면 CROSS PRODUCT가 필요한 경우는 많지 않지만, 간혹 튜닝이나 리포트를 작성하기 위해 고의적으로 사용하는 경우가 있을 수 있다. 그리고 웨어하우스의 개별 DIMENSION(차원)을 FACT(사실) 칼럼과 JOIN 하기 전에 모든 DIMENSION의 CROSS PRODUCT를 먼저 구할 때 유용하게 사용 가능

8. OUTER JOIN
- INNER JOIN과 대비하여 OUTER JOIN이라고 불리며, JOIN 조건에서 동일한 값이 없는 행도 반환할 때 사용

가) LEFT OUTER JOIN
- 조인 수행 시 먼저 표기된 좌측 테이블에 해당하는 데이터를 먼저 읽은 후, 나중 표기된 우측 테이블에서 JOIN 대상 데이터를 읽어온다. 즉, TABLE A와 B가 있을 때 (A 기준) A와 B를 비교해서 B의 JOIN 칼럼에서 같은 값이 있을 때 그 해당 데이터를 가져오고, B의 JOIN 칼럼에서 같은 값이 없는 경우에는 A 테이블에서 가져오는 칼럼들은 NULL 값으로 채운다

나) RIGHT JOIN
- 조인 수행 시 LEFT JOIN과 반대로 우측 테이블이 기준이 되어 결과를 생성한다. TABLE A와 B가 있을 때 (B 기준) A와 B를 비교해서 A의 JOIN 칼럼에서 같은 값이 있을 때 그 해당 데이터를 가져오고, A의 JOIN 칼럼에서 같은 값이 없는 경우에는 A 테이블에서 가져오는 칼럼들은 NULL 값으로 채운다. 그리고 RIGHT JOIN으로 OUTER 키워드를 생략해서 사용할 수 있다

다) FULL OUTER JOIN
- 조인 수행 시 좌측, 우측 테이블의 모든 데이터를 읽어 JOIN하여 결과를 생성한다. 즉, TABLE A와 B가 있을 때 (A, B 모두 기준이 됨) RIGHT OUTER JOIN과 LEFT OUTER JOIN의 결과를 합집합으로 처리한 결과와 동일하다. 단, UNION ALL이 아닌 UNION 기능과 같으므로 중복되는 데이터는 삭제한다. 그리고 FULL JOIN으로 OUTER 키워드를 생략해서 사용할 수 있다

9. INNER VS OUTER VS CROSS JOIN
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuSgty%2FbtshKRrtr1q%2FBKxa2E4TA952jRSVYlgGIK%2Fimg.png)

- 1) INNER JOIN의 결과
    양쪽 테이블에 모두 존재하는 키 값이 B-B, C-C 인 2건이 출력된다.  
    
- 2) LEFT OUTER JOIN의 결과
    TAB1을 기준으로 키 값 조합이 B-B, C-C, D-NULL, E-NULL 인 4건이 출력된다. 
    
- 3) RIGHT OUTER JOIN의 결과
	TAB2를 기준으로 키 값 조합이 NULL-A, B-B, C-C 인 3건이 출력된다.
	
-  4) FULL OUTER JOIN의 결과
    양쪽 테이블을 기준으로 키 값 조합이 NULL-A, B-B, C-C, D-NULL, E-NULL 인 5건이 출력된다.  
      
- 5) CROSS JOIN의 결과
    JOIN 가능한 모든 경우의 수를 표시하지만 OUTER JOIN은 제외
    양쪽 테이블 TAB1과 TAB2의 데이터를 곱한 개수인 4 * 3 = 12건이 추출됨. 키 값 조합이 B-A, B-B, B-C, C-A, C-B, C-C, D-A, D-B, D-C, E-A, E-B, E-C 인 12건이 출력
