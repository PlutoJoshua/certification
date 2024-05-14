
## 그룹함수 (GROUP)

1. 개요
> AGGREGATE FUNCTION
- GROUP AGGREGATE FUNCTION이라고도 부르며, GROUP FUNCTION의 한 부분으로 분류
- COUNT, SUM, AVG, MAX, MIN 외 각종 집계 함수 포함

> GROUP FUNCTION
- 그룹 함수로는 집계 함수를 제외하고 소그룹 간의 소계를 계산하는 ROLLUP 함수, GROUP BY 항목들 간 다차원적인 소계를 계산할 수 있는 CUBE 함수, 특정 항목에 대한 소계를 계산하는 GROUPING SETS 함수가 있다
- ROLLUP, CUBE, DROUPING SETS 결과에 대한 정렬이 필요한 경우는 ORDER BY 절에 정렬 칼럼을 명시해야 한다

> WINDOW FUNCTION
- 분석함수나 순위함수로도 알려져 있는 원도우 함수는 데이터웨어 하우스에서 발전한 기능

2. ROLLUP 함수
- GROUP BY의 확장된 형태로 사용하기가 쉬우며 병렬로 수행이 가능하기 때문에 매우 효과적일 뿐 아니라 시간 및 지역처럼 계층적 분류를 포함하고 있는 데이터의 집계에 적합하도록 되어 있다
- ROLLUP에 지정된 GROUPING COLUMNS의 list는 subtotal을 생성하기 위해 사용되어지며, Grouping Colmns의 수를 N이라고 했을 때 N+1 Level 의 Subtotal이 생성된다
- ROLLUP의 인수는 계층 구조이므로 인수 순서가 바뀌면 수행 결과도 바뀌게 되므로 인수의 순서에도 주의해야 한다

1) 일반적인 group by 절 사용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkzDtq%2FbtshE90uwWl%2FpNu1wN83nkT69ZVbNozzlk%2Fimg.png)

2) GROUP BY 절 + ORDER BY 절 사용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7uUGJ%2FbtshAvXLR1B%2F5PKel6h1n3ueFKsvPYfOj1%2Fimg.png)

2-1) ROLLUP 함수 사용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfSF9A%2FbtshAArw7fB%2FH2v0ZtSsNZm5RWTwv0Rrg0%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmYk2I%2FbtshBm0yHme%2FTcet9KIfKkreEqMPiNihB0%2Fimg.png)

실행 결과에서 2개의 GROUPING COLUMNS(DNAME, JOB)에 대하여 다음과 같은 추가
LEVEL의 집계가 생성된 것을 볼 수 있다.

- L1 - GROUP BY 수행시 생성되는 표준 집계 (9건)
- L2 - DNAME 별 모든 JOB의 SUBTOTAL (3건)
- L3 - GRAND TOTAL (마지막 행, 1건)

3) GROUPING 함수 사용
- ROLLUP이나 CUBE에 의한 소계가 계산된 결과에는 GROUPING(EXPR) = 1이 표시되고, 그 외의 결과에는 GROUPING(EXPR) = 0이 된다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcrVtbz%2Fbtshz0DLgzz%2F1Hr31OydSNWuK1d9aTgmz1%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9lMhH%2FbtshPpBA1C4%2FlPfzDhikVg5HX7KwIu1g2K%2Fimg.png)


4) GROUPING 함수 + CASE 사용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbh8uLC%2Fbtshz1o8nYG%2FoyjtnshKKYC6rpDIif1qyK%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbgpFjo%2FbtshAwbk49m%2FTrbEY7ZnQR23lDfS4Cf301%2Fimg.png)

3. CUBE 함수
- 결합 가능한 모든 값에 대하여 다차원적인 집계를 생성하게 되므로 ROLLUP에 비해 다양한 데이터를 얻는 장점이 있는 반면에, 시스템에 부하를 많이 주는 단점이 있다

1) CUBE 함수 이용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJNbz7%2FbtshFarzz7J%2FO6DK1hdOwtqllp9cu2aQDK%2Fimg.png)

- CUBE 함수를 사용해 ROLLUP함수의 결과에다 업무별 집계까지 추가해 출력할 수 있는데, ROLLUP함수에 비해 업무별 집계를 표시한 5건의 레코드가 추가가 됨

2) UNION ALL 사용
- UNION ALL은 Set Operation 내용으로, 여러 SQL 문장을 연결하는 역할을 할 수 있다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjOiW5%2FbtshAZK6ODY%2FCP1GpLrrmiZi2PdlKifmtk%2Fimg.png)

- CUBE 함수를 사용하면서 가장 크게 개선되는 부분은 CUBE 사용 전 SQL에서 EXP, DEPT 테이블을 네 번이나 반복 엑세스하는 부분을 CUBE 사용 SQL에서는 한번으로 줄일 수 있다는 점임

4. GROUPING SET 함수
- GROUPING SETS는 원하는 부분의 소계만 손쉽게 추출할 수 있는 장점이 있다
- ROLLUP에서는 단지 가능한 Subtotal만을 생성하였지만, CUBE는 결합 가능한 모든 값에 대하여 다차원 집계를 생성한다
- CUBE를 사용할 경우에는 내부적으로는 GROUPING COLUMNS의 순서를 바꾸어서 또 한번의 쿼리를 추가 수행해야 한다. 뿐만 아니라 Grand Total은 양쪽의 쿼리에서 모두 생성되므로 한 번의 쿼리에서는 제거되어야만 하므로 ROLLUP에 비해 시스템 연산 대상이 많다
- GROUPING SETS를 이용해 더욱 다양한 소계 집합을 만들 수 있는데, GROUP BE SQL 문장을 여러번 반복하지 않아도 원하는 결과를 쉽게 얻을 수 있게 되었다
- GROUPING SETS에 표시된 인수들에 대한 개별 집계를 구할 수 있으며, 이때 표시된 인수들 간에는 계층구조인 ROLLUP과는 달리 평등한 관계이므로 인수의 순서가 바뀌어도 결과는 같다

- 일반 그룹 함수를 이용한 SQL
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fs84tV%2FbtshAvQ7dUZ%2FjBDljJX1bDvJCIofWZchX0%2Fimg.png)

- GROUPING SETS 사용 SQL
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBbvAQ%2FbtshA4lxdJE%2FZCdZRT93dh6g40UaBQtSWK%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyvO0d%2FbtshA5kqX5O%2FmhxqqOQ1C1HlqKU575tDiK%2Fimg.png)

- GROUPING SETS SQL - 순서 변경
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FciJGvv%2FbtshWuvy49P%2FtpsmANXL8TFXfI37X2mu2K%2Fimg.png)

- 3개의 인수를 이용한 GROUPING SETS 이용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8greh%2FbtshHMxcQzT%2FXrLEPIePfgI1t7inNDzcPK%2Fimg.png)

