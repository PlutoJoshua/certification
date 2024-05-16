

1. WHERE 조건절 개요
- 자료를 검색할 때 SELECT 절과 FROM절만을 사용하여 기본적인 SQL 문장을 구성한다면, 테이블에 있는 모든 자료들이 결과로 출력되어 실제로 원하는 자료를 확인하기 어려울 수 있다. 사용자들은 자신이 원하는 자료만을 검색하기 위해서 SQL문장에 WHERE절을 이용해 자료를 제한함
```
SELECT [ALL/DISTINCT] 칼럼명 [ALIAS명]

FROM 테이블명

WHERE 조건식;
```

>WHERE절 조건식
- 칼럼명(보통 조건식 좌측에 위치) 
- 비교연산자
- 문자, 숫자, 표현식(보통 조건식 우측에 위치)
- 비교 칼럼명 (JOIN 사용시)

2. 연산자의 종류
> WHERE 절에 사용되는 연산자 종류
- 비교 연산자(부정 비교 연산자 포함)
- SQL 연산자(부정 SQL 연산자 포함)
- 논리 연산자

| 구분            | 연산자                 | 의미                                               |
| ------------- | ------------------- | ------------------------------------------------ |
| 비교연산자         | =                   |                                                  |
|               | >                   |                                                  |
|               | >=                  |                                                  |
|               | <                   |                                                  |
|               | <=                  |                                                  |
| SQL 연산자       | BETWEEN a AND b     | a와 b값 사이에 있는 값(a, b 포함)                          |
|               | IN (list)           | 리스트 값 중 어느 하나라도 일치                               |
|               | LIKE ('비교문자열')      | 바교 문자열과 형태 일치 (%, _ 사용)                          |
|               | IS NULL             | NULL 값인 경우                                       |
| 논리 연산자        | AND                 | 앞에 있는 조건과 뒤에 있는 조건이 참(TRUE)이면 결과도 참 = 앞뒤조건 동시 만족 |
|               | OR                  | 앞 조건 참이거나 뒤 조건 참이면 결과도 참 = 앞뒤 조건 중 하나만 참이면 됨     |
|               | NOT                 | 뒤에 오는 조건에 반대되는 결과를 되돌려 줌                         |
| 부정 비교<br>연산자  | !=                  | 같지 않음                                            |
|               | ^=                  | 같지 않음                                            |
|               | <>                  | 같지 않음(ISO 표준, 모든 운영체제에서 사용 가능)                   |
|               | NOT 칼럼명 =           | ~와 같지 않다                                         |
|               | NOT 칼럼명 >           | ~보다 크지 않다                                        |
| 부정 SQL<br>연산자 | NOT BETWEEN a AND b | a와 b의 값 사이에 있지 않다(a, b 값 포함 안함)                  |
|               | NOT IN (list)       | list 값과 일치하지 않음                                  |
|               | IS NOT NULL         | NULL값을 갖지 않음                                     |

> 연산자의 우선순위
- 괄호로 묶은 연산이 제일 먼저 연산처리됨
- 연산자들 중에는 부정연산자(NOT)가 먼저 처리됨
- 비교 연산자(=,>,>=,<,<=), SQL 비교연산자(BETWEEN, IN, LIKE, IS NULL)가 먼저 처리됨
- 논리 연산자 중에서는 AND, OR의 순으로 처리됨

3. 비교 연산자
- 문자 유형 비교 방법

| 구분                          | 비교 방법                                                                                                                                           |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 비교 연산자의 양쪽이 모두 CHAR 유형인 경우  | - 길이가 서로 다른 CHAR형 타입이면 작은 쪽에 SPACE를 추가하여 길이를 같게 한 후에 비교<br>- 서로 다른 문자가 나올때까지 비교<br>- 달라진 첫 번째 문자의 값에 따라 크기 결정<br>- BLACNK의 수만 다르다면 서로 같은 값으로 결정 |
| 비교 연산자의 한 쪽이 VARCHAR 유형인 경우 | - 서로 다른 문자가 나올때까지 비교<br>- 길이가 다르다면 짧은 것이 끝날 때까지만 비교한 후에 길이가 긴 것이 크다고 판단<br>- 길이가 같고 다른 것이 없다면 같다고 판단<br>- VARCHAR는 NOT NULL까지 길이를 말함            |
| 상수값과 비교할 경우                 | - 상수 쪽을 변수 타입과 동일하게 바꾸고 비교<br>- 변수 쪽이 CHAR 유형이면 위의 CHAR 유형의 경우 적용<br>- 변수 쪽이 VARCHAR 유형이면 위의 VRCHAR 경우 적용                                       |

4. SQL 연산자
- SQL 문장에서 사용하도록 기본적으로 예약되어 있는 연산자로서 모든 데이터 타입에 대해서 연산이 가능한 4가지 종류가 있음
> LIKE 연산자에서의 와일드카트(Wildcard)
- 한 개 혹은 0개 이상의 문자를 대신해서 사용하기 위한 특수문자
- "%" : 0개 이상의 어떤문자
- "_ _" : 1개인 단일문자 

```
SELECT PLAYER_NAME 선수이름, POSITION 포지션, BACK_NO 백넘버, HEIGHT 키

FROM PLAYER

WHERE PLAYER_NAME LIKE '장%';
```

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwnxIP%2Fbtsg7GS76vl%2FAp1bn5WVpkye7kxGmoMyW0%2Fimg.png)

> IS NULL 연산자 : NULL(ASCII 00)
- NULL 값과의 수치 연산은 NULL 값을 리턴
- NULL 값과의 비교 연산은 거짓(FALSE)을 리턴
- 어떤 값과도 비교할 수 없으며 특정 값보다 크다, 적다고 표현할 수 없다

5. 논리 연산자
- 비교 연산자나 SQL 비교 연산자들로 이루어진 여러 개의 조건들을 논리적으로 연결시키기 위해서 사용되는 연산자

6. 부정 연산자
- 비교 연산자, SQL 비교 연산자에 대한 부정 표현

7. ROWNUM, TOP 사용
>  ROWNUM : 테이블이나 집합에서 원하는 만큼의 행만 가져오고 싶을 때 WHERE 절에서 행의 개수를 제한하는 목적으로 사용
```
# 한 건의 행만 가져오고 싶을 때
> SELECT PLAYER_NAME FROM PLAYER WHERE ROWNUM = 1;
> SELECT PLAYER_NAME FROM PLAYER WHERE ROWNUM <= 1;
> SELECT PLAYER)NAME FROM PLAYER WHERE ROWNUM < 2;

# 두 건 이상의 N 행을 가져오고 싶을 때
> SELECT PLAYER_NAME FROM PLAYER WHERE ROWNUM <= N;
> SELECT PLAYER_NAME FROM PLAYER WHERE ROWNUM <= N+1; < 행의 한계 지정 가능

# 테이블 내의 고유한 키나 인덱스 값을 만들 수 있다
> UPDATE MY_TABLE SET COLUMN1 = ROWNUM;
```

> TOP 절
- SQL 는 TOP 절을 사용하여 결과 집합으로 출력되는 행의 수를 제한
- Expression : 반환할 행의 수를 지정하는 숫자
- PERCENT : 쿼리 결과 집합에서 처음 Expression%의 행만 반환됨을 나타냄
- WITH TIES : ORDER BY 절이 지정된 경우에만 사용할 수 있으며, TOP N(PERCENT)의 마지막 행과 같은 값이 있는 경우 추가 행이 출력되도록 지정할 수 있다

```
TOP (Expression) [PERCENT] [WITH TIES]

# 두 건 이상의 N행을 가져오고 싶을 때
> SELECT TOP(N) PLAYER_NAME FROM PLAYER; < 출력되는 행의 개수 지정 가능  
```

---
