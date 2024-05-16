## 함수(FUNCTION)

1. 내장 함수(BUILT-IN FUNCTION)
- 벤더에서 제공하는 함수인 내장함수와 사용자가 정의할 수 있는 함수로 나눌 수 있음
- 내장 함수는 다시 함수의 입력 값이 단일행 값이 입력되는 단일행 함수(SINGLE-ROW-FUNCTION)와 여러 행의 값이 입력되는 다중행 함수(MULTI-ROW FUNCTION)로 나뉨

| 종류        | 내용                       | 예                                                                                                    |
| --------- | ------------------------ | ---------------------------------------------------------------------------------------------------- |
| 문자형<br>함수 | 문자를 입력하면 문자/ 숫자 값 반환     | LOWER, UPPER, SUBSTR/SUBSTRING, LENGTH/LEN, LTRIM, RTRIM, TRIM, ASCII                                |
| 숫자형<br>함수 | 숫자를 입력하면 숫자 값 반환         | ABS, MOD, ROUND, TRUNC, SIGN, CHR/CHAR, CEIL/CEILING, FLOOR, EXP, LOG, LN, POWER, SIN, COS, TAN      |
| 날짜형<br>함수 | DATE 값 연산                | SYSDATE/GETDATE, EXTRACT/DATEPART, TO_NUMBER(TO_CHAR(d,'YYYY' \| 'MM' \| 'DD'))/YEAR \| MONTH \| DAY |
| 변환형<br>함수 | 문자, 숫자, 날짜형 값 data 타입 변환 | TO_NUMBER, TO_CHAR, TO_DATE/CAST, CONVERT                                                            |
| NULL 관련   | NULL 처리 함수               | NVL/ISNULL, NULLIF, COALESCE                                                                         |

> 단일행 함수 특징
- SELECT, WHERE, ORDER BY 절에 사용 가능
- 각 행들에 대해 개별적으로 작용하여 데이터 값들을 조작하고 각 행에 대한 조작 결과를 리턴
- 여러 인자(Argumemt)를 입력해도 단 하나의 결과만 리턴
- 함수인 인자로 상수, 변수, 표현식 사용 가능. 하나의 인수를 가지는 경우도 있지만 여러 개의 인수를 가질 수도 있다
- 특별한 경우가 아니면 함수의 인자로 함수를 사용하는 함수의 중첩 가능

2. 문자형 함수
- 문자 데이터를 매개 변수로 받아들여서 문자나 숫자 값의 결과를 돌려주는 함수

| 문자형 함수           | 함수 설명                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------- |
| LOWER            | 소문자로 변환                                                                                                           |
| UPPER            | 대문자로 변환                                                                                                           |
| ASCII            | ASCII 코드 번호로 변환                                                                                                   |
| CHR/CHAR         | ASCII 코드를 문자, 숫자로 변환                                                                                              |
| CONCAT           | 문자열 1, 문자열 2 연결 // 합성연산자 ' \| \| '(Oracle)이나 '+'(SQL)와 동일                                                         |
| SUBSTR/SUBSTRING | m위치에서 n개의 문자 길이에 해당하는 문자 반환<br>n 생략: 마지막 문자까지                                                                     |
| LENGTH/LEN       | 문자열 개수 숫자값으로 반환                                                                                                   |
| LTRIM            | 첫 문자부터 확인해 지정 문자가 나타나면 해당 문자를 제거<br>(지정 문자가 생략되면 공백이 디폴트)<br>SQL에서는 지정문자 사용 불가 = 공백만 제거 가능                        |
| RTRIM            | 마지작 문자부터 확인해 지정 문자가 나타나는 동안 해당 문자 제거<br>(지정 문자가 생략되면 공백이 디폴트)<br>SQL에서는 지정문자 사용 불가 = 공백만 제거 가능                    |
| TRIM             | 문자열 머리말, 꼬리말, 또는 양쪽에 있는 지정 문자를 제거<br>(leading \| trailng \| both 생략되면 both가 디폴트)<br>SQL에서는 지정문자 사용 불가 = 공백만 제거 가능 |

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlW6mq%2Fbtshh7QgP8y%2FzqVHeR2wAbkIKCFkI0ZGEk%2Fimg.png)

3. 숫자형 함수
- 데이터를 입력받아 처리하고 숫자를 리턴하는 함수

| 숫자형 함수                              | 함수 설명                         |
| ----------------------------------- | ----------------------------- |
| ABS                                 | 숫자 절대값 반환                     |
| SIGN                                | 양수, 음수, 0 구별                  |
| MOD                                 | 숫자 1을 숫자2로 나누어 나머지 값을 리턴      |
| CEIL/CEILING                        | 숫자보다 크거나 같은 최소 정수 리턴          |
| FLOOR                               | 숫자보다 작거나 같은 최대 정수 리턴          |
| ROUND                               | 숫자를 소수점 m자리에서 반올림하여 리턴        |
| TRUNC                               | 숫자를 소수 m자리에서 잘라서 버림           |
| SIN, COS, TAN ,,,                   | 숫자의 삼각함수 값 리턴                 |
| EXP(), POWER(), SQRT(), LOG(), LN() | 숫자의 지수, 거듭제곱, 제곱근, 자연 로그 값 리턴 |
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbnXOf0%2Fbtshi6C1SCA%2FYiXmb9aRJl6vveFCChy0iK%2Fimg.png)

4. 날짜형 함수
- DATE 타입의 값을 연산하는 함수
- Oracle의 TO_NUMBER(TO_CHAR()) 함수의 경우 변환형 함수로 구분할 수도 있으나 SQL의 YEAR, MONTH, DAY 함수와 매핑하기 위해 여기서 설명

| 날짜형 함수              | 함수 설명                                                                                         |
| ------------------- | --------------------------------------------------------------------------------------------- |
| SYSDATE/GETDATE()   | 현재 날짜와 시각 출력                                                                                  |
| EXTRACT / DATEPART  | 날짜 데이터에서 년/월/일 데이터 출력(시간/분/초 가능)                                                              |
| TO_NUMBER(TOCHAR()) | 날짜 데이터에서 년/월/일 데이터 출력(시간/분/초 가능)<br>Oracle EXTRACT = SQL DEPART<br>TO_NUMBER 함수 제외시 문자형으로 출력됨 |
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKs9A3%2Fbtshj3sibOf%2F6aJdkEV2a0K27Q6UBH1Kf0%2Fimg.png)

5. 변환형 함수
- 특정 데이터 타입을 다양한 형식으로 출력하고 싶을 경우에 사용되는 함수

| 종류            | 설명                                 |
| ------------- | ---------------------------------- |
| 명시적 데이터 유형 변환 | 데이터 변환형 함수로 데이터 유형을 변환하도록 명시해주는 경우 |
| 암시적 데이터 유형 변환 | 데이터베이스가 자동으로 데이터 유형을 변환하여 계산하는 경우  |
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDCBfB%2FbtshjuRcqtx%2Ft5gFUupUjxZKqQGKZECHRk%2Fimg.png)

6. CASE 표현
- IF - THEN - ELSE 논리와 유사한 방식으로 표현식을 작성해서 SQL의 비교연산 기능을 보완

| CASE 표현                                                                                      | 함수 설명                                                                                                                   |
| -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| CASE<br>   SIMPLE_CASE_EXPRESSION 조건<br>   ELSE 표현절<br>END                                   | SIMPPLE_CASE_EXPRESSION 조건이 맞으면 조건 내의 THEN 절을 수행하고, 조건이 맞지 않으면 ELSE절 수행                                                 |
| CASE<br>                                   SEARCHED_CASE_EXPRESSION 조건<br>   ELSE 표현절<br>END | SEARCHED_CASE_EXPRESSION 조건이 맞으면 조건 내의 THEN절을 수행하고, 조건이 맞지 않으면 ELSE 절 수행                                                |
| DECODE(표현식, 기준값1, 값1)<br>-> 기준값2, 값2, ... , 디폴트값                                             | Oracle 에서만 사용되는 함수, 표현식의 값이 기준값 1이면 값 1 출력, 기준값 2면 값 2 출력. 그리고 기준값이 없으면 디폴트 값 출력. CASE표현의 SIMPLE_CASE_EXPRESSION 조건과 동일 |

7. NULL 관련 함수
가) NVL/ISNULL 함수

| 일반형 함수                               | 함수 설명                                                                                                   |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| NVL(표현식1, 표현식2) / ISNULL(표현식1, 표현식2) | 표현식 1의 결과값이 NULL이면 표현식 2의 값을 출력<br>단, 표현식 1과 표현식2의 결과 데이터 타입이 같아야 함<br>NULL 관련 가장 많이 사용되는 함수이므로 상당히 중요함 |
| NULLIF(표현식1, 표현식2)                   | 표현식 1과 표현식2와 같으면 NULL, 같지 않으면 표현식 1 리턴                                                                  |
| COALESCE(표현식1, 표현식2,...)             | 임의의 개수 표현식에서 NULL이 아닌 최초의 표현식을 나타냄. 모든 표현식이 NULL이라면 NULL을 리턴                                            |

나) NULL과 공집합
> 일반적인 NVL/ISNULL 사용
> 공집합의 NVL/ISNULL 사용
- SELECT 1 FROM DUAL WHERE 1=2; 와 같은 조건이 대표적인 공집합을 발생시키는 쿼리이며, 위와같이 조건에 맞는 데이터가 한 건도 없는 경우를 공집합이라고 하고, NULL 데이터와는 다르게 이해해야 함

다) NULLIF
- EXPR1 = EXPR2면 NULL을, 같지 않으면 EXPR1을 리턴. 특정 값을 NULL로 대채하는 경우 사용

```
NULLIF (EXPR1, EXPR2)
```

라) 기타 NULL 관련 함수(COALESCE)
- 인수의 슷자가 한정되어 있지 않으며, EXPR에서 NULL이 아닌 최초의 EXPR을 나타냄
- 모든 EXPR이 NULL이면 NULL을 리턴

## GROUP BY, HAVING 절

1. 집계함수(Aggregate Function)
 - 여러 행들의 그룹이 모여서 그룹당 단 하나의 결과를 돌려주는 함수
 - group by 절은 행들을 소그룹화 함
 - SELECT 절, HAVING절, ORDER BY 절에 사용할 수 있다
```
집계 함수명 ([DISTINCT | ALL] 칼럼이나 표현식)
- ALL : Default 옵션이므로 생략 가능
- DISTINCT : 같은 값을 하나의 데이터로 간주할 때 사용하는 옵션

```

- 집계 함수는 그룹에 대한 정보를 제공하므로 주로 숫자 유형에 사용되지만, MAX, MIN, COUNT 함수는 문자, 날짜 유형에도 적용이 가능한 함수다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFGmRR%2FbtshFajUAbZ%2FVN1mXB364Znv4W0AEUsNh0%2Fimg.png)

2. GROUP BY 절, HAVING 절
- SQL 문에서 FROM 절과 WHERE 절 뒤에 오며, 데이터들을 작은 그룹으로 분류하여 소그룹에 대한 항목별로 통계 정보를 얻을 때 추가로 사용됨
```
SELECT [DISTINCT] 칼럼명 [ALIAS명]
FROM 테이블명
[WHERE 조건식]
[GROUP BY 칼럼이나 표현식]
[HIVING 그룹조건식] ;
```

> GROUP BY 절과 HAVING 절의 특성
- GROUP BY 절을 통해 소그룹별 기준을 정한 후, SELECT 절에 집계 함수 사용한다
- 집계 함수의 통계 정보는 null 값을 가진 행을 제외하고 수행한다
- GROUP BY 절에서는 SELECT 절과는 달리 ALIAS 명을 사용할 수 없다
- 집계 함수는 WHERE 절에는 올 수 없다(집계 함수를 사용할 수 있는 GROUP BY 절보다 WHERE 절이 먼저 수행됨)
- WHERE 절은 전체 데이터를 GROUP으로 나누기 전에 행들을 미리 제거 시킴
- HAVING 절은 GROUP BY 절에 의한 소그룹별로 만들어진 집계 데이터 중, HAVING 절에서 제한 조건을 두어 조건을 만족하는 내용만 출력함
- HAVING 절은 일반적으로 GROUP BY 절 뒤에 위치한다

3. CASE 표현을 활용한 월별 데이터 집계
- 집계함수(CASE())~GROUP BY 기능은 모델링의 제 1정규화로 인해 반복되는 칼럼의 경우 구분 칼럼을 두고 여러 개의 레코드로 만들어진 집합을 정해진 칼럼 수만큼 확장해서 집계 보고서를 만드는 유용한 기법

4. 집계 함수와 NULL
- 리포트의 빈칸을 NULL이 아닌 ZERO로 표현하기 위해 NVL(Oracle)/ISNULL(SQL) 함수를 사용하는 경우가 많은데, 다중 행 함수를 사용하는 경우는 오히려 불필요한 부하가 발생하므로 굳이 NVL 함수를 다중 행 함수 안에 사용할 필요가 없다
- 리포트 출력 때 NULL이 아닌 0을 표시하기 싶은 경우에는 NVL(SUM(SAL), 0)이나, ISNULL(SUM(SAL), 0)처럼 전체 SUM의 결과가 NULL인 경우(대상 건수가 모두 NULL인 경우)에만 한 번 NVL/ISNULL 함수를 사용하면 된다
