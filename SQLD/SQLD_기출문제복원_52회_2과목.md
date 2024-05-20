데이터 출처 : 데이터전문가포럼카페 
(https://cafe.naver.com/sqlpd?iframe_url=/MyCafeIntro.nhn%3Fclubid=21771779)

### 11. SQL의 특징
1) 구조적
2) 집합적
3) 선언적
 -> SQL은 기본적으로 **구조적이고 집합적이고 선언적인 질의 언어**이다.

### 12. SQL의 분류

1) DDL(데이터 **정의**어) : CREATE, DROP, ALTER, RENAME
2) DML(데이터 **조작**어) : SELECT, INSERT, UPDATE, DELETE
3) DCL(데이터 **제어**어) : GRANT, REVOKE
4) TCL(데이터 **트랜잭션 제어**어) : COMMIT, ROLLBACK

### 13. SQL의 논리적인 순서
- FROM > WHERE > GROUP BY > HAVING >  SELECT > ORDER BY

### 14. NULLIF
- NULLIF('A','A') : NULL
- 표현식 1이 표현식 2와 같으면 NULL, 다르면 표현식 1 리턴

### 15. 트랜잭션의 특성(SQL문을 보고 어떤 특성에 위배되는지 판단)
1) **원자성** : 트랜잭션에 정의된 연산들 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아있어야 함
2) **일관성** : 트랜잭션 실행 전 데이터 베이스 내용이 잘못되어 있지 않다면 트랜잭션 실행 이후에도 데이터베이스 내용의 잘못이 있으면 안됨
3) **고립성** : 트랜잭션 실행 도중 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안됨
4) **지속성** : 트랜잭션이 성공적으로 수행되면 갱신한 데이터베이스 내용이 영구적으로 저장됨

### 16. NOT 연산자에 대한 결과
```
SELECT *
FROM SQLD_52_16
WHERE NOT (C1 <=2);
```

SQLD_52_16

| C1   | C2   |
| ---- | ---- |
| 1    | 10   |
| 2    | NULL |
| 3    | NULL |
| 4    | 20   |
| NULL | 30   |
 > 조건절에 NULL이 출력되는가? X / = 이 없어지는가? O
 > NULL은 제외하고 3, 4출력됨

### 17. NOT 연산자와 OR
```
SELECT *
FROM SQLD_52_26
WHERE NOT (C1 <=2 OR C2 IS NULL);
```

> 16번 + OR 조건절이 어떻게 변형되는가?
> WHERE C1 > 2 AND C2 IS NOT NULL 조건으로 나오는 결과

### 18. COALESCE

```
SELECT SUM(COALESCE[COL1, COL2, COL3])
FROM DATA ;
```
DATA

| COL1 | COL2 | COL3 |
| ---- | ---- | ---- |
| 1    | 2    | 3    |
| NULL | 2    | 3    |
| NULL | NULL | 3    |
> COALESCE : 첫 번째로 NULL이 아닌 값을 반환
> 각 행에서 NULL이 아닌 첫 번째 값 선택
> 1(첫 번째 행 > COL1) + 2(두 번째 행 > COL2) + 3(세 번째 행 > COL3) = 6

### 19. NULLIF(14번 참고)

### 20. PRIOR
- 계층형 쿼리에서 순방향/역방향을 지정하는 키워드

### 21. 빈칸 채우기 (테이블) 
<지문>
데이터는 관계형 데이터베이스의 기본 단위인 (     )형태로 저장된다. 모든 자료는 (     )에 등록되고, 우리는 (     )로부터 원하는 자료를 꺼내올 수 있다

### 22. JOIN

| 제품     |     | 생산제품     |     | 생산라인   |
| ------ | --- | -------- | --- | ------ |
| 제품코드   |     | 라인번호(FK) |     | 라인번호   |
| 제품명    | -<- | 제품코드(FK) | ->- | 최초가동일자 |
| 제품유형코드 |     |          |     |        |
| 단위     |     |          |     |        |
> 제품과 생산라인 엔터티를 JOIN 시 적절한 JOIN 조건이 없으므로 카티시안 곱이 발생한다

### 23. PRIOR의 위치
```
...
(     )MGRNO = (      )EMPNO
...
```

> PRIOR 자식 = 부모 형태를 사용하면 계층 구조에서 부모 데이터에서 자식 데이터 방향으로 전개하는 순방향 전개를 한다

**START WITH** : 계층 구조 전개의 시작 위치 지정, 결과에 포함
**CONNECT BY** : 다음에 전개될 자식 데이터 지정
**PRIOR** : CONNECT BY 절에 사용되며, 현재 읽은 칼럼을 지정, SELECT와 WHERE 절에도 사용 가능
		PRIOR 부모 = 자식 : 역방향
		PRIOR 자식 = 부모 : 순방향
**NOCYCLE** : 동일한 데이터가 전개되지 않음
**ORDER SIBLINGS BY** : 형제 노드간의 정렬 수행
WHERE : 모든 전개를 수행한 후에 지정된 조건을 모두 만족하는 데이터만 추출(필터링)

### 24. 계층형 질의(23번과 비슷)
- 너무 헷갈려서 GPT의 설명을 참고했다!
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    last_name VARCHAR2(50),
    manager_id NUMBER
);

INSERT INTO employees (employee_id, last_name, manager_id) VALUES (1, 'King', NULL);
INSERT INTO employees (employee_id, last_name, manager_id) VALUES (2, 'Kochhar', 1);
INSERT INTO employees (employee_id, last_name, manager_id) VALUES (3, 'De Haan', 1);
INSERT INTO employees (employee_id, last_name, manager_id) VALUES (4, 'Hunold', 3);
INSERT INTO employees (employee_id, last_name, manager_id) VALUES (5, 'Ernst', 3);

SELECT employee_id, last_name, manager_id
FROM employees
START WITH employee_id IN (4, 5)  -- 여러 직원으로 시작
CONNECT BY employee_id = PRIOR manager_id  -- 자식에서 부모로 연결
ORDER SIBLINGS BY last_name;

```

#### 쿼리 결과

| employee_id | last_name | manager_id |
| ----------- | --------- | ---------- |
| 4           | Hunold    | 3          |
| 5           | Ernst     | 3          |
| 3           | De Haan   | 1          |
| 1           | King      | NULL       |
1. **첫 번째 행**: employee_id가 4인 Hunold 직원으로 시작합니다.
2. **두 번째 행**: employee_id가 5인 Ernst 직원으로 시작합니다.
3. **세 번째 행**: Hunold와 Ernst의 manager_id는 둘 다 3이므로, employee_id가 3인 De Haan 직원을 찾습니다. -- 부모노드를 찾는 거임!
4. **네 번째 행**: De Haan의 manager_id는 1이므로, employee_id가 1인 King 직원을 찾습니다.
- 쿼리는 employee_id가 4와 5인 Hunold와 Ernst에서 시작하여 그들의 부모인 De Haan을 찾고, 다시 De Haan의 부모인 King을 찾는 과정입니다. Kochhar는 De Haan의 형제 노드이지만, 탐색 경로에 포함되지 않기 때문에 결과에 나타나지 않습니다.

### 25. DATE , BETWEEN
- GPT에게 문제를 복원해달라고 했다
```
CREATE TABLE orders (
    order_id NUMBER,
    order_date DATE
);

INSERT INTO orders (order_id, order_date) VALUES (1, TO_DATE('2024-04-09 23:59:59', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO orders (order_id, order_date) VALUES (2, TO_DATE('2024-04-10 00:00:00', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO orders (order_id, order_date) VALUES (3, TO_DATE('2024-04-10 23:59:59', 'YYYY-MM-DD HH24:MI:SS'));
INSERT INTO orders (order_id, order_date) VALUES (4, TO_DATE('2024-04-11 00:00:00', 'YYYY-MM-DD HH24:MI:SS'));

// 다음 SQL 쿼리를 실행했을 때의 결과로 알맞은 것은 무엇인가?
SELECT order_id, order_date
FROM orders
WHERE order_date BETWEEN TO_DATE('20240409', 'YYYYMMDD') AND TO_DATE('20240410', 'YYYYMMDD');
```

> WHERE 절의 BETWEEN 연산은 날짜 범위가 '2024-04-09 00:00:00'부터 '2024-04-10 23:59:59'까지의 데이터를 포함함

```
WHERE order_date BETWEEN TO_DATE('20240409', 'YYYYMMDD') AND TO_DATE('20240410', 'YYYYMMDD')
```

#### 쿼리 결과

| order_id | order_date          |
| -------- | ------------------- |
| 1        | 2024-04-09 23:59:59 |
| 2        | 2024-04-10 00:00:00 |
| 3        | 2024-04-10 23:59:59 |

### 26. HAVING
집계 결과(GROUP BY)에서 특정 조건을 부여할 수 있는 키워드

### 27. A와 B의 결과값이 다른 것?

```
1) SELECT COUNT(*) AS A / COUNT(NVL(COL1,0)) AS B

2) SELECT SUM(COL1) AS A / COUNT(NVL(COL1,0)) AS B

3) SELECT MAX(COL1) AS A / COUNT(NVL(COL1,0)) AS B

4) SELECT AVG(COL1) AS A / AVG(NVL(COL1,0) AS B
```
1) COUNT는 NULL도 포함해서 수를 세기 때문에 값이 동일
2) SUM, MAX는 0으로 치환하든 안하든 값은 동일(0을 더하나 0이 많아져서 최댓값을 구하나)
3) AVG는 NULL 값을 어떻게 처리하느냐에 따라 모수가 변하기 때문에 영향을 받음 => 정답

### 28. 조인 후 NVL 결과를 체크하는 문제
```
SELECT ..
FROM ..
WHERE A.N1 = B.N1
AND NVL(A.C1,-1) = NVL(B.C1,-1)
AND NVL(A.C2,-1) = NVL(B.C2,-1)
AND NVL(A.C3,-1) = NVL(B.C3,-1)
```
> NVL은 NULL일 경우 뒤의 값을 출력함

### 29. EXISTS, NOT EXISTS, <>
```
// 주문이 있는 고객 정보 찾기
SELECT * 
FROM Customers C 
WHERE EXISTS ( SELECT 1 
				FROM Orders O 
				WHERE O.CustomerID = C.CustomerID );

// 주문이 없는 고객 정보 찾기
SELECT * 
FROM Customers C 
WHERE NOT EXISTS ( SELECT 1 
				FROM Orders O 
				WHERE O.CustomerID = C.CustomerID );

// 주문 중 'Shipped' 상태가 아닌 주문이 있는 고객의 정보
SELECT * 
FROM Customers C 
WHERE EXISTS ( SELECT 1 
				FROM Orders O 
				WHERE O.CustomerID = C.CustomerID
				 AND O.Status <> 'Shipped' );
```

> EXISTS, NOT EXISTS는 서브쿼리에서 반환되는 데이터의 존재 여부에 따라 참/거짓을 판별, EXISTS에서 <> 조건은 서브쿼리의 결과와 비교할 값을 가지고 있어 조건에 따라 다른 결과 출력

```
CREATE TABLE SQLD_52_29_A (
    C1 NUMBER,
    C2 NUMBER
);

CREATE TABLE SQLD_52_29_B (
    C1 NUMBER,
    C2 NUMBER
);

INSERT INTO SQLD_52_29_A VALUES (1, 100);
INSERT INTO SQLD_52_29_A VALUES (2, 200);
INSERT INTO SQLD_52_29_A VALUES (3, 300);
INSERT INTO SQLD_52_29_A VALUES (4, 400);
INSERT INTO SQLD_52_29_A VALUES (NULL, 500);

INSERT INTO SQLD_52_29_B VALUES (1, 100);
INSERT INTO SQLD_52_29_B VALUES (3, 300);
INSERT INTO SQLD_52_29_B VALUES (NULL, 500);

//EXISTS
SELECT *
FROM SQLD_52_29_A A
WHERE EXISTS (
    SELECT 1
    FROM SQLD_52_29_B B
    WHERE A.C1 <> B.C1
);
--- 결과 ---
C1      C2
------- -------
2       200
4       400
NULL    500

//NOT EXISTS
SELECT * 
FROM SQLD_52_29_A A 
WHERE NOT EXISTS ( 
	SELECT 1 
	FROM SQLD_52_29_B B 
	WHERE A.C1 = B.C1 
);
--- 결과 ---
C1      C2
------- -------
2       200
4       400
```
> NULL 연산을 조심하자....

### 30. SQL의 DML 결과 문제

### 31.  서브쿼리(스칼라 서브쿼리 제외)
- 1:M일 때 메인 쿼리 레벨로 결과가 나옴
- 서브쿼리 테이블의 컬럼을 메인에서 사용할 수 있다
- SELECT, FROM, WHERE, GROUP BY, ORDER BY 모두에 올 수 있다
> 모두 애매함....

### 32. ORDER BY
ORDER BY는 기본이 **오름차순**

### 33. SQL 문 결과 맞추기

### 34. SQL 집합 연산자
- UNION : **합집합**(중복행 1개 처리)
- UNION ALL : **합집합**(중복 행도 표시)
- INTERSECT : **교집합**(INTERSECTION)
- EXCEPT, MINUS : **차집합**
- CROSS JOIN : **곱집합**(PRODUCT)

### 35. **CUBE**

**ROLLUP** : Subtotal을 생성하기 위해 사용, Grouping Columns의 수를 N이라 할 때 N+1 Level의 Subtotal이 생성됨. 인수 순서에 주의
**GROUPING** : Subtotal의 total을 생성
**CUBE** : 결합 가능한 모든 값에 대해 다차원 집계를 생성, ROLLUP에 비해 시스템 부하 심함
**GROUPING SETS** : 인수들에 대한 개별 집계를 구할 수 있다. 다양한 소계 집합 생성 가능, 순서 바뀌어도 상관 없음

| ROLLUP(A, B)                                                         | CUBE(A, B)                                                                                   | GROUPING SET(A, B)                    |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------- |
| GROUP BY A, B<BR>UNION ALL<BR>GROUP BY A<BR>UNION ALL<BR>모든 집합 그룹 결과 | GROUP BY A, B<br>UNION ALL<br>GROUP BY A<br>UNION ALL<br>GROUP BY B<br>UNION ALL<br>모든 집합 결과 | GROUP BY A<br>UNION ALL<br>GROUP BY B |
> ROLLUP이나 CUBE에 의한 소계가 계산된 결과에는 GROUPING(표현식)=1, 긔 외의 결과는 GROUPING(표현식) = 0 이 표시됨

### 36. ROLLUP
ROLLUP (A, B) 와 ROLLUP ((A, B))
```
* GROUP BY ROLLUP(A) : 전체 합계, 칼럼 A소계 
* GROUP BY ROLLUP(A,B) : 전체 합계, 칼럼 A소계, 칼럼 (A,B) 조합 소계 
* GROUP BY ROLLUP(A,B,C) : 전체 합계, 칼럼 A소계, 칼럼 (A,B)조합 소계, (A,B,C)조합 소계 
* GROUP BY ROLLUP(A,(B,C)) : 전체 합계, 칼럼 A소계, 칼럼 (A,(B,C)) 조합 소계 
* GROUP BY A, ROLLUP(B) : A그룹별 집계, A그룹 내부에서 B칼럼별 집계
```

### 37. SQL 문 결과 맞추기

### 38. 
```
SELECT COL1 
FORM ...
GROUP BY COL1 
HAVING COUNT(*) >= 3
```
> GROUP BY 결과 3 보다 크거나 같은 값 찾기

### 39. WINDOW FUNCTION
- 행과 행간의 관계를 정의하거나 행과 행간을 비교, 연산하는 함수 / OVER 필수
- ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
- > 현재 행을 기준으로 파티션 내에서 앞의 1건, 현재 행, 뒤의 1건을 범위로 지정
> 이건 도저히 이해가 안간다 ㅜ

### 40. RANK 함수
RANK : 특정 항목에 대한 순위를 구하는 함수. 동일한 값에 대해서는 동일한 순위 부여(1, 2, 2, 4)
DENSE_RANK : 동일한 순위를 하나의 등수로 간주(1, 2, 2, 3)
ROW_NUMBER : 동일한 값이라도 고유한 순위 부여 (1, 2, 3, 4)

### 41. CTAS 제약 조건
- **PRIMARY KEY** : 기본키 정의 (복사되지 않는다) > CTAS 기법 사용 시 주의할 점은 기존 테이블의 제약조건 중에 NOT NULL 제약만 새로 생성되는 테이블에 적용되고, 기본키/외래키/고유키/CHECK 등의 다른 제약조건은 없어진다는 점이다
- **UNIQUE KEY** : 고유키 정의
- **NOT NULL** : NULL값 입력 금지
- **CHECK** : 입력 값 범위 제한 / NULL 무시
- **FOREIGN KEY** : 외래키 정의

### 42. TIMESTAMP (+1 과 +0.9999)
1. **+1 (하루 추가)**: TIMESTAMP의 경우, +1은 24시간을 더하는 것과 같습니다. 즉, 현재 날짜와 시간에 24시간을 추가하여 다음 날로 넘어가는 것을 의미합니다. 예를 들어, 2024.03.11 00:00:00 에서 +1을 하면 2024.03.12 00:00:00 가 됩니다.
    
2. **0.9999 (하루 미만 추가)**: 0.9999는 하루를 24시간으로 나눈 값입니다. TIMESTAMP에서는 이를 사용하여 하루 미만을 추가할 수 있습니다. 예를 들어, 2024.03.11 00:00:00 에서 0.9999를 더하면 **2024.03.11 23:59:59.976** 이 됩니다.

### 43. **NATURAL JOIN**
- 두 테이블간 동일한 이름을 갖는 모든 칼럼에 대해 EQUI JOIN 수행
- USING, ON 조건절을 사용할 수 없음(WHERE에서 JOIN 정의 불가)
- SELECT EMP.DEPT처럼 OWNER 명 사용 불가(ALIAS 값은 접두사 안됨!)
- JOIN에 사용된 컬럼은 같은 데이터 타입이어야 함

### 44. JOIN
```
CREATE TABLE T1 (NO NUMBER, COLA VARCHAR2(10));

INSERT INTO T1 VALUES(1, 'AAA');

CREATE TABLE T2 (NO NUMBER, COLB VARCHAR2(10));

INSERT INTO T2 VALUES(1, 'BBB');
INSERT INTO T2 VALUES(3, 'CCC');

COMMIT;

SELECT A.NO, A.COLA, B.COLB
FROM T1 A, T2 B
WHERE B.NO = A.NO;
```
INNER JOIN / JOIN USING / NATURAL JOIN 모두 결과값이 1건이 나오지만
CROSS JOIN은 2건이 나옴

### 45. MERGE 구문
```
MERGE
INTO T1 A
USING T2 B
ON (B.EMPNO = A.EMPNO)
WHEN MATCHED THEN
	UPDATE SET A.SAL = B.SAL - 500 -- 매치되면 UPDATE !
	WHERE A.JOB = 'CLERK'
	DELETE
WHEN NOT MATCHED THEN
	INSERT (A.EMPNO, A.ENAME, A.JOB) -- 매치 안되면 INSERT !
	VALUES (A.EMPNO, A.ENAME, A.JOB)
	WHERE B.JOB = 'CLERK'
```

### 46. ROLE
- ROLE은 명령어가 아니다 !
- 명령어가 아닌 권한의 집합체를 의미. 즉 SELECT, DELETE, UPDATE와 같은 PRIVILEGE(권한)임
- GRANT, REVOKE로 ROLE을 부여하거나 회수 할 수 있다 >> ROLE도 권한처럼 부여 및 회수 가능

### 47. CASCADE
- DEPARTMENT 테이블과 EMPLOYEE 테이블에 대해 DEPARTMENT 의 ID 가 지워질 때 EMPLOYEE 의 ID 도 지워지도록 하는 제약조건 >> EMPLOYEE 테이블에 ON DELETE CASCADE 를 구현

### 48. LIKE
- 정확하게 일치하지 않아도 되는 패턴 조건 전달 시 사용
- %(자리수 제한 없는 모든), \_(하나 당 한 자리수, 모든 값을 표현)와 함께 사용
```
ENAME LIKE 'S%'    > 이름이 S로 시작하는
ENAME LIKE '%S%'   > 이름에 S를 포함하는
ENAME LIKE '%S'    > 이름이 S로 끝이나는
ENAME LIKE '_S%'   > 이름의 두 번째 글자가 S //'%S%'와 다름 주의
ENAME LIKE '__S__' > 이름의 가운데 글자가 S이며 길이가 5글자인
```

### 49. 제약조건
- 기본키는 한개이다(한개 이상일 수 없음!!)
### 50. DISTINCT
- 행의 중복을 제거하는 키워드