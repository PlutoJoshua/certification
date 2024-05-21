### 1. 트랜잭션
- 데이터베이스의 논리적인 연산단위
- 트랜잭션에는 하나 이상의 SQL 문장이 포함된다
- 트랜잭션은 밀접히 관련되어 분리될 수 없는 한 개 이상의 DB조작을 가리킴
- 분할할 수 없는 최소 단위, 전부 적용하거나 전부 취소해야 함
- 하나의 트랜잭션에서 처리되는 데이터는 다른 트랜잭션에서 변경할 수 없음
> 트랜잭션의 특성
> 1) 원자성
> - 트랜잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않는 상태로 남아 있어야 함
> 2) 일관성
> - 트랜잭션이 실행되기 전의 데이터베이스 내용이 잘못 되어 있지 않다면 트랜잭션이 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 안됨
> 3) 고립성
> - 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어선 안됨
> 4) 지속성
> - 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 DB의 내용은 영구적으로 저장

### 2. ROWS / RANGE
> - `ROWS`는 현재 행까지의 물리적 행을 포함하여 계산
>- `RANGE`는 현재 행의 값까지의 논리적 범위를 포함해 계산, 동일한 값을 가지는 행 함께 고려
- ROWS

|V1|N1|CumulativeSum|
|---|---|---|
|1|10|10|
|2|20|30|
|2|30|60|
|3|40|100|
- RANGE

|V1|N1|CumulativeSum|
|---|---|---|
|1|10|10|
|2|20|60|
|2|30|60|
|3|40|100|

### 13. ORDER BY와 NULL
- 오라클에서는 NULL을 가장 큰 값으로,
- SQL에서는 NULL을 가장 작은 값으로 간주

### 14. 권한 부여
```
T1, T2 
Conn User1 
Create table user1.T1 
Conn User2              --USER2가 USER1의 테이블에 접근
select * from user1.T1 ​
```

-> GRANT SELECT ON user1.T1 to user2 ; -- 접근 권한 부여하기

### 15. NTILE
- 비율함수
1) RATIO_TO_REPORT : 전체 SUM(칼럼)값에 대한 행별 칼럼 값의 백분율을 소수점 반환
2) PERCENT_RANK : 제일 먼저 나오는 것 0, 제일 늦게 나오는 것 1, 행의 순서별 백분율
3) CUME_DIST : 전체 건수에서 현재 행보다 작거나 같은 건수에 대한 누적 백분율
4) NTILE : 전체 건수를 ARGUMENT 값으로 N 등분한 결과
	-> NTILE(3), 총 8개면 3, 3, 2로 구현

### 16. CUBE 결과값
```
SELECT A.설비ID, B.에너지코드, SUM(B.사용량), AS 사용량 합계
FROM 설비 A 
INNER JOIN 에너지 사용량 B
ON (A.설비ID = B.설비ID)
GROUP BY CUBE (A.설비ID, B.에너지코드)
ORDER BY A.설비ID, B.에너지코드;
```
-> CUBE 절에 나열된 모든 조합 ((설비ID), (에너지코드), (설비ID, 에너지코드), ())에 대해 SUB TOTAL

GROUP BY CUBE ((A.설비ID), (B.에너지코드), (A.설비ID, B.에너지코드)) -> 엄청 길게 나온다. 모든 수
GROUP BY GROUPING SETS ((A.설비ID), (A.설비ID, B.에너지코드)) -> 설비id 전체 가 안나옴
 = GROUP BY GROUPING SETS ((A.설비ID), (B.에너지코드), (A.설비ID, B.에너지코드)) 

### 17. NULL 연산
- NULL의 연산은 항상 NULL
- NULLIF는 0으로 나누어 에러가 생기는 문제를 방지하기 위해 많이 사용됨
- NULLIF(A, B) : A와 B가 같으면 NULL, 다르면 A를 출력함
### 18. 집계함수에 대한 NULL 연산
- 데이터 테이블

|A|B|C|D|
|---|---|---|---|
|10|NULL|NULL|20|
|NULL|10|20|NULL|
|30|NULL|10|NULL|
|4|6|10|10|
```
SELECT SUM(A + B + C + D)
```
각 행의 `A + B + C + D` 결과:

|A|B|C|D|A + B + C + D|
|---|---|---|---|---|
|10|NULL|NULL|20|NULL|
|NULL|10|20|NULL|NULL|
|30|NULL|10|NULL|NULL|
|4|6|10|10|30|
```
SELECT SUM(A) + SUM(B) + SUM(C) + SUM(D)
```
각 열의 `SUM` 결과:

- `SUM(A)`: 10 + 30 + 4 = 44
- `SUM(B)`: 10 + 6 = 16
- `SUM(C)`: 20 + 10 + 10 = 40
- `SUM(D)`: 20 + 10 = 30

결과:

| sum_a | sum_b | sum_c | sum_d | total_sum |
| ----- | ----- | ----- | ----- | --------- |
| 44    | 16    | 40    | 30    | 130       |

### 19. GROUP BY와 집계 함수
```
SELECT NVL(MAX(COL1), 'X')
FROM TAB1
WHERE COL2 > 9 -- `COL2 > 9`를 만족하는 데이터가 없음 >  쿼리의 결과 집합은 비어 있음
GROUP BY COL1; -- GROUP BY 절의 기준 컬럼이 있으므로, 데이터가 없는 경우에도 GROUP BY에 
					의해 하나의 결과 행이 생성 하지만 `COL1` 값이 없기 때문에 그룹화된 
					결과 없음 > 결과 집합은 비어 있음
```

- MAX 함수
	- 그룹화된 결과 집합에서 가장 큰 값 반환
	- 그룹화된 결과가 없다면 NULL 반환
-  NVL 함수
	- 첫 번재 변수가 NULL인 경우 두 번째 변수 반환
	- `NVL(MAX(COL1), 'X')`는 `MAX(COL1)`이 NULL인 경우 'X'를 반환 

```
SELECT NVL(MAX(COL1), 'X')
FROM TAB1
WHERE COL2 > 9
GROUP BY COL1; -- 결과는 'X'
```


### 20. ALTER TABLE문으로 데이터 타입 변경
1) `VARCHAR2` 타입에서 `NUMBER` 타입으로 변경
- 직접적으로 허용되지 않음(숫자데이터를 문자로 바꿀 수 없기 때문에)
- 반대도 마찬가지!

2) `DATE` 타입에서 `TIMESTAMP` 타입 변경
- 허용됨

### 21.  NOT EXISTS
### 테이블 데이터

#### 테이블 T1

|COL1|
|---|
|10|
|20|

#### 테이블 T2

|COL1|
|---|
|10|
|NULL|

```
SELECT COUNT(*)
FROM T1 
WHERE NOT EXISTS (SELECT 'X' FROM T2 WHERE T1.COL1 = T2.COL1);
```

### 22. NULL, 0 나누기
```
<SQL> SELECT 10 / NULL , 10 / 0 

FROM .... --> NULL, ERROR
```

### 23. SQL 결과 문제

### 24. SQL 결과 문제
### 데이터

#### 테이블 T1

|C1|
|---|
|1|
|2|
|3|

#### 테이블 T2

|C1|
|---|
|1|
|2|
|4|

#### 테이블 T3

|C1|
|---|
|1|
|2|
|3|
```
SELECT SUM(C.C1)
FROM T1 A
LEFT OUTER JOIN T2 B 
ON A.C1 =B.C1 
RIGHT OUTER JOIN T3 C 
ON B.C1 = C.C1 
WHERE 1=1;
```

--> 6

### 25. SUBSTR, ROUND
```
SUBSTR(string_expression, start_position, length)
```
- `string_expression`: 추출하고자 하는 문자열
- `start_position`: 추출을 시작할 문자열 내 위치. 첫 번째 문자의 위치는 1부터 시작
- `length` (옵션): 추출할 문자열의 길이. 지정하지 않으면 시작 위치부터 문자열의 끝까지 추출
- `NULL` 값에 대해 `SUBSTR` 함수를 사용하면 결과는 `NULL`

-  ROUND(값, 소수점자리)
### 26. INSERT FIRST
- `INSERT FIRST` 문:  각 조건에 대해 한 번만 검사를 수행하며, 첫 번째로 조건을 만족하는 경우에만 데이터를 삽입
- `INSERT ALL`문 : 한 번에 여러 개의 테이블에 INSERT를 할 수 있는 문법 조건 만족하는 모든 테이블에 INSERT
#### TAB1

|COL1|
|---|
|1|
|2|
|4|
```
INSERT FIRST
  WHEN COL1 >= 2 THEN INTO T1 VALUES(COL1)
  WHEN COL1 >= 4 THEN INTO T2 VALUES(COL1)
  ELSE INTO T3 VALUES(COL1)
SELECT * FROM TAB1;
```
### 쿼리 분석

1. **COL1 = 1**
    
    - 첫 번째 조건: `COL1 >= 2` (조건 불충족)
    - 두 번째 조건: `COL1 >= 4` (조건 불충족)
    - ELSE: `T3` 테이블에 삽입
    - **결과**: `T3`에 1 삽입
2. **COL1 = 2**
    
    - 첫 번째 조건: `COL1 >= 2` (조건 충족)
    - `T1` 테이블에 삽입
    - 두 번째 조건 및 ELSE: 검사되지 않음
    - **결과**: `T1`에 2 삽입
3. **COL1 = 4**
    
    - 첫 번째 조건: `COL1 >= 2` (조건 충족)
    - `T1` 테이블에 삽입
    - 두 번째 조건 및 ELSE: 검사되지 않음
    - **결과**: `T1`에 4 삽입

### 결과

각 조건을 분석한 결과:

- `T1`에 삽입된 행: 2, 4
- `T2`에 삽입된 행: 0
- `T3`에 삽입된 행: 1
```
SELECT COUNT(*) AS T1_count FROM T1;  -- 결과: 2
SELECT COUNT(*) AS T2_count FROM T2;  -- 결과: 0
SELECT COUNT(*) AS T3_count FROM T3;  -- 결과: 1
```

### 27. OR
TEAM은 A또는 B 이다 --> WHERE(TEAM_CODE =A OR TEAM_CODE = B)

### 28. ROWS / RANGE / PRECEDING
```
현재 행에서부터 이전 행까지의 누적합을 구하는 SQL
rows unbounded preceding
---
range unbounded preceding -- 이전 값 고려
rows between unbounded preceding and 1 preceding -- 전 행까지
range between unbounded preceding and 1 preceding -- 전 행까지
```


### 29. RANK, DENSE_RANK, ROW_NUMBER
- RANK : 중복 허용 X
- DENSE_RANK : 중복 허용 등수
- ROW_NUMBER : 단순 순위 매김

### 30. SQL 결과 문제

### 31. IDENTITY, CHECK
```
CREATE TABLE T1 (
    main INT IDENTITY(1,1), -- 자동으로 1부터 시작혀 1씩 증가
    mainvalue INT CHECK (mainvalue >= 3) -- 삽입되는 값은 3 이상
);

INSERT INTO T1 (mainvalue) VALUES (1), (2), (3);

---
INSERT INTO T1 (mainvalue) VALUES (1); -- 실패 (CHECK 제약 조건 위반)
INSERT INTO T1 (mainvalue) VALUES (2); -- 실패 (CHECK 제약 조건 위반)
INSERT INTO T1 (mainvalue) VALUES (3); -- 성공 (CHECK 제약 조건 충족)
---
```

### 32. WHERE IN, OR
```
SELECT * FROM ...
WHERE (COL1, COL2) IN ( ('A', 1000 ) , ('B', 2000) )

동일 결과 출력
---
SELECT * FROM ...
WHERE (COL1 = 'A' AND COL2 = 1000)
   OR (COL1 = 'B' AND COL2 = 2000)
```

### 33. VIEW
- 저장공간을 가지지는 않지만 테이블처럼 조회 및 수정할 수 있는 객체
- 종류
	- 단순뷰 : 하나의 테이블 조회 뷰
	- 복합뷰 : 둘 이상의 테이블 조인 뷰
- 특징
	- 기본 테이블로부터 유도된 테이블이기에 기본 테이블과 같은 형태의 구조를 가지고 있으며, 조작도 기본 테이블과 거의 같음
	- 뷰는 가상의 테이블이기에 물리적으로 구현되어 있지 않으며 저장 공간을 차지하지 않음
	- 데이터를 안전하게 보호 가능
	- 이미 정의되어 있는 뷰는 다른 뷰의 정의에 기초가 될 수 있음
	- 기본 테이블이 삭제되면 그 테이블을 참조하여 만든 뷰 역시 삭제됨
- 장점
	- 논리적 독립성 제공
	- 데이터 접근을 제어함으로써 보안 유지
	- 사용자의 데이터 관리 단순화
	- 데이터의 다양한 지원 가능
- 단점
	- 뷰의 정의 변경 불가
	- 삽입, 삭제, 갱신 연산에 제한
	- 인덱스 구성 불가

### 34. SAVEPOINT, ROLLBACK
```
<SQL>

INSERT INTO ... VALUES (1);
INSERT INTO ... VALUES (1);
INSERT INTO ... VALUES (3);
SAVEPOINT P1 ;
INSERT INTO ... VALUES (4);
ROLLBACK P1 ;
SELECT * FROM .... 
```

-> 1,2,3

### 하이리커 쿼리
 
 데이터
#### TAB1

| COL1 | COL2 | COL3 |
| ---- | ---- | ---- |
| A    | NULL | 1    |
| B    | A    | 2    |
| C    | A    | 3    |
| D    | B    | 4    |
```
SELECT COUNT(*)
FROM TAB1
WHERE COL3 <> 2 -- PRIOR절이 수행되고 난 다음 처리함
START WITH COL3 = 4
CONNECT BY COL1 = PRIOR COL2;
```
### 최종 결과

|COL1|COL2|COL3|
|---|---|---|
|A|NULL|1|
|D|B|4|

### 36. 매출 1,2위 구하기(ROWNUM)
```
SELECT ROWNUM RN, .... 
FROM ( SELECT ... FROM ... ORDER BY .. DESC )
WHERE ROWNUM <= 2 ;
```

### 37. IN 연산자의 중복값 처리
### 데이터

#### TAB

|COL1|
|---|
|100|
|200|
|300|
```
SELECT * FROM TAB 
WHERE COL1 IN (100, 200, 100);-- 각각의 값에 대해 딱 한 번만 일치하는 행 반환
```
 -> 2

### 38. NULL의 정렬
- (Oracle) `NULLS FIRST`와 `NULLS LAST`를 지원하여 `NULL` 값을 원하는 방식으로 정렬할 수 있음
- ORDER BY ... NVL(.. 0) 
- ORDER BY NULL FIRST ..

### 39. OUTER JOIN
### 주어진 데이터

#### 데이터

|A.COL1|B.COL1|
|---|---|
|1|10|
|2|100|
|3|220|
```
SELECT ...
FROM A
LEFT OUTER JOIN B ON (A.COL1 = B.COL1 AND B.COL1 > 200)
WHERE ...
```
### 예시 결과

#### 데이터

|A.COL1|B.COL1|
|---|---|
|1|NULL|
|2|NULL|
|3|220|
### 40. NOT EXISTS / NOT IN / OUTER JOIN 
1) NOT EXISTS
2) NOT IN 
3) OUTER JOIN 
-> 모두 같은 결과 !!
```
-- NOT EXISTS 사용
SELECT *
FROM table1 t1
WHERE NOT EXISTS (
    SELECT 1
    FROM table2 t2
    WHERE t1.col1 = t2.col1
);

-- NOT IN 사용
SELECT *
FROM table1
WHERE col1 NOT IN (
    SELECT col1
    FROM table2
);

-- OUTER JOIN 사용
SELECT t1.*
FROM table1 t1
LEFT JOIN table2 t2 ON t1.col1 = t2.col1
WHERE t2.col1 IS NULL;
```

### 41. SYSDATE
```
SELECT SYSDATE FROM DUAL; -- 현재 날짜와 시간 가져오기(2023-05-10 가정)

SELECT SYSDATE, TO_DATE('2023', 'YYYY') FROM DUAL; --현재 날짜, 2023-01-01
```

- `SYSDATE` 함수는 현재 시스템 날짜와 시간을 반환합니다.
- `TO_DATE('2023', 'YYYY')`는 문자열 '2023'을 날짜 형식으로 변환합니다. `'YYYY'` 형식은 연도를 나타내며, `TO_DATE` 함수는 날짜로 변환합니다.

|SYSDATE|TO_DATE('2023', 'YYYY')|
|---|---|
|2023-05-10 00:00:00|2023-01-01 00:00:00|

### 42. ROWS / RANGE
- rows는 현재 **행**을 기준으로 셈
- ranges는 현재 **값**을 기준으로 셈

* 참고 

| **구분**              | **설명**    |
| ------------------- | --------- |
| ROWS                | 물리적인 행 단위 |
| RANGE               | 논리적인 행 집합 |
| CURRENT ROW         | 현재 행      |
| UNBOUNDED PRECEDING | 첫번째 행     |
| UNBOUNDED FOLLOWING | 마지막 행     |
| [위치] PRECEDING      | [위치] 이전 행 |
| [위치] FOLLOWING      | [위치] 다음 행 |

### 43. SQL 결과 문제


### 44. 이스케이프 문자
### 데이터

|COL1|COL2|COL3|
|---|---|---|
|..|AB_C|..|
|..|DFG||
|..|A_BD|..|
```
SELECT *
FROM your_table
WHERE COL2 LIKE '%@_%' ESCAPE '@';
```

### 45. 제약 조건
- 데이터의 무결성을 위해 각 컬럼에 생성하는 데이터의 제약 장치
- 테이블 생성 시 정의 가능, 컬럼 추가 시 정의 가능, 이미 생성된 컬럼에 제약조건만 추가 가능
- PRIMARY KEY
	- 유일한 식별자(각 행을 구별할 수있는 식별자 기능)
	- 중복허용 X, NULL 허용 X  -- UNIQUE + NOT NULL
	- 특정 컬럼에 PRIMARY KEY 생성하면 NOT NULL 속성 자동 부여
	- CTAS로 테이블 복사 시 복사 X
	- 하나의 테이블에 여러 기본키 생성 불가
	- 하나의 기본키를 여러 컬럼을 결합해 생성 가능
	- primary key 생성 시 자동으로 UNIQUE INDEX 생성
- UNIQUE
	- 중복 허용 안함
	- **NULL 허용(여러개 가능)**
	- 자동으로 UNIQUE INDEX 생성
- NOT NULL
	- 다른 제약조건과 다르게 컬럼의 특징을 나타냄 => CTAS 로 복제시 따라감
	- 컬럼 생성 시 NOT NULL을 선언하지 않으면NULLABLE 컬럼으로 생성됨
	- 이미 만들어진 컬럼에 NOT NULL 선언 시 제약조건 생성이 아닌 컬럼 수정으로 해결
```
ALTER TABLE A ADD NOT NULL (COL2);
ALTER TABLE A MODIFY COL2 NOT NULL; -- 컬럼 수정으로 NOT NULL 처리
```
- FOREIGN KEY
	- 참조 테이블의 참조 컬럼에 있는 데이터를 확인하면서 본 테이블 데이터를 관리할 목적으로 생성
	- 반드시 참조(부모)테이블의 참조 컬럼이 사전에 PK 혹은 UNIQUE KEY를 가져야 함
	- FOREIGN KEY 옵션(생성 시 정의, 변경 불가 -> 재생성) 
	1. ON DELETE CASCADE : 부모 데이터 삭제 시 자식 데이터 함께 삭제
	2. ON DELETE SET NULL : 부모 데이터 삭제 시 자식 데이터의 참조값은 NULL 로 수정
- CHECK
	- 직접적으로 데이터의 값 제한(양수, (1,2,3,4)중 하나)

### 46. SQL 결과 문제

### 47, 48 복원 안됨

### 49. DCL
- 데이터베이스 접근권한, OBJECT 접근 권한을 부여하는 언어 명령어 '종류'

### 50. FLOOR
```
SELECT FLOOR(10.4), FLOOR(-2.4) FROM DUAL;
```

- FLOOR 함수 : 주어진 숫자보다 작거나 같은 가장 큰 정수를 반환하는 함수
- 10.4보다 작거나 같은 가장 큰 정수 : 10
- -2.4보다 작거나 같은 가장 큰 정수 : -3