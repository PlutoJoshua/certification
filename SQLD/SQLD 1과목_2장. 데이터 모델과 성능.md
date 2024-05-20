## 성능 데이터 모델링의 개요

1. 성능데이터 모델링의 정의
- 데이터 베이스 성능향상을 목적으로 설계단계의 데이터 모델링 때부터 성능과 관련된 사항이 데이터 모델링에 반영될 수 있도록 하는 것
- 성능데이터 모델링은 정규화를 통해서도 수행할 수 있고 인덱스의 특징을 고려해서 칼럼의 순서도 변형할 수 있다. 또한 대량의 데이터 특성에 따라 비록 정규화된 모델이라도 테이블을 수직 또는 수평분할하여 적용하는 방법도 있고 논리적인 테이블을 물리적인 테이블로 전환할 때 데이터 처리의 성격에 따라 변환하는 방법도 성능 데이터 모델링의 범주에 포함될 수 있다

2. 성능 데이터 모델링 수행 시점
- 성능 향상을 위한 비용은 프로젝트 수행 중에 있어서 사전에 할수록 비용이 들지 않는다. 특히 분석/설계 단계에서 데이터 모델에 성능을 고려한 데이터 모델링을 수행할 경우 성능제하여 따른 재업무 비용을 최소화할 수 있는 기회를 가지게 된다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fz1Ctz%2Fbtsf6EtjARP%2FL2Tv57hzv95K3BgB86bwc1%2Fimg.png)

3. ==성능 데이터 모델링 고려사항==

- 데이터 모델링을 할 때 정규화를 정확하게 수행한다
- 데이터베이스 용량 산정을 수행한다
- 데이터베이스에 발생되는 트랜잭션의 유형을 파악한다
- 용량과 트랜잭션의 유형에 따라 반정규화를 수행한다
- 이렉모델의 조정, PK/FK 조정, 슈퍼타입/서브차입 조정 등을 수행한다
- 성능 관점에서 데이터 모델을 검증한다

---

## 정규화와 성능

1. 정규화를 통한 성능 향상 전략
- 데이터모델링을 하면서 정규화를 하는 것은 기본적으로 데이터에 대한 중복성을 제거해 주고 데이터가 관심사별로 처리되는 경우가 많기 때문에 성능이 향상되는 특징을 가진다
- 일반적으로 정규화가 잘 되어 있으면 입력/수정/삭제의 성능이 향상되고 반정규화를 많이 하면 조회의 성능이 향상된다고 인식될 수 있으나 데이터 모델링을 할 때 반정규화만이 조화 성능을 향상한다는 고정관념은 탈피되어야 한다
-  정규화로 성능이 저하되기 보다 정규화를 해야만 성능이 향상되는 경우가 많이 나타나기 때문

2. 반정규화된 테이블의 성능저하 사례 1
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FolFSD%2FbtsgbIKLJWY%2FiaT02is42XVIAgQ1pmMdLK%2Fimg.png)

- 왼쪽 그림은 2차 정규화가 안된 반정규화 테이블, 오른쪽 그림은 부분키 종속을 정규화하여 2차 정규화된 테이블의 모습
- 2차 정규화가 안된 테이블은 직급명과 함께 반정규화된 관서번호, 관서명을 조회하면 하나의 테이블에서 데이터가 조화되고, 2차 정규화된 테이블은 관서번호, 관서명이 관서 테이블에만 존재하기 때문에 두 개의 테이블을 조인하여 처리해야 한다.

3. 반정규화된 테이블의 성능저하 사례 2 : 두 개의 엔터티가 통합되어 반정규화된 경우
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcAsDOF%2Fbtsf6DJIzJ2%2F0dmKmj3NCNaCzKWQGn5vr1%2Fimg.png)

- 매각일자가 결정자가 되고 매각 시간과 매각 장소가 의존자가 되는 함수적 종속관계가 형성되는 관계. 매각 일자는 5천 건이 있고 일자별 매각 물건은 100만건이 있는 것으로 가정
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtGyD2%2Fbtsgcsgm8my%2FkBmJ3WYSMviAeLGO8qwAp1%2Fimg.png)

- 대량의 데이터에서 조인 조건이 되는 대상을 찾기 위해 인라인뷰를 사용하기 때문에 성능이 저하됨. 이를 정규화하려면 복합식별자 중에서 일반속성이 주식별자 속성 중 일부에만 종속관계를 가지고 있으므로 2차 정규화의 대상이 된다.

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdnrcX0%2Fbtsf5ewDZ2o%2Fswh1pmxNJ1KvcWUKdLbw41%2Fimg.png)

- 정규화를 적용했기 때문에 매각일자를 PK로 사용하는 매각일자별 매각내역과도 관계가 연결된다. 따라서 업무 흐름에 따른 정확한 데이터 모델링 표기도 가능해지고, 드라이빙된 테이블이 5천 건의 매각기일 테이블이 되므로 성능도 향상된다.
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlyWEY%2FbtsgcqJvyTW%2FZUwOgU1ElGYf5Nqv4eKlK1%2Fimg.png)

- 매각 기일 테이블이 정규화되면서 드라이빙이 되는 대상 테이블의 데이터가 5천 건으로 줄어 조회 처리가 빨라짐

4. 반정규화된 테이블의 성능저하 사례 3 : 동일한 속성 형식을 두 개 이상의 속성으로 나열하여 반정규화한 경우
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvYh5m%2Fbtsf5e4sbXb%2F7Di7mmnUntIKEGiwzmx2UK%2Fimg.png)

- 한 테이블에 인덱스가 많아지면 조회 성능은 향상되지만 데이터 입력/수정/삭제 성능은 저하된다. 그래서 일반업무처리(온라인성 업무)에서는 인덱스 수를 가급적 7-8개가 넘지 않도록 하는 것이 좋다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrF5WB%2FbtsgaMTRnFN%2FSUGJ0Pe9VsSoGpgz6q56F1%2Fimg.png)

- 각 유형별로 모두 인덱스가 걸려 있어야 인덱스에 의해 데이터를 찾을 수 있다. 이런 모델은 정규화를 적용해야 한다.
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMX6iq%2FbtsgbJiCbdm%2FgpstBhG7BoAcsf97v8S7ok%2Fimg.png)

- 중복 속성에 대한 분리가 1차 정규화의 정의임을 고려하면 모델 테이블은 1차 정규화의 대상이 된다. 로우단위의 대상도 1차 정규화의 대상이 되지만 칼럼 단위로 중복이 되는 경우도 1차 정규화의 대상이 된다.
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd2Wxas%2FbtsgbLncP6w%2FZuNnGRajEbIZm4vtBnv7i0%2Fimg.png)

- 위 SQL 구문은 유형코드 + 기능분류코드 + 모델 코드에 인덱스가 걸려 있으므로 인덱스를 통해 데이터를 조회함으로써 성능이 향상된다

6. 함수적 종속성(Functional Dependency)에 근거한 정규화 수행 필요
- 함수의 종속성은 데이터들이 어떤 기준값에 의해 종속되는 현상을 지칭하는 것
- 이 때 기준값을 결정자(Determinant)라 하고 종속되는 값을 종속자(Dependent)라고 한다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOUV4W%2Fbtsf5fCkm82%2FEtaZprz5SWGFR9iZKbTR81%2Fimg.png)

- 함수의 종속성은 데이터가 가지고 있는 근본적인 속성으로 인식되고 있다.==정규화의 궁극적인 목적은 반복적인 데이터를 분리하고 각 데이터가 종속된 테이블에 적절하게(프로세스에 의해 데이터의 정합성이 지켜질 수 있어야 함) 배치되도록 하는 것==이므로 이 함수의 종속성을 이용하여 정규화 작업이나 각 오브젝트에 속성을 배치하는 작업에 이용되는 것

---

## 반정규화와 성능

1. 반정규화를 통한 성능향상 전략
	가) 정의
	- 정규화된 엔터티, 속성, 관계에 대해 시스템의 성능향상과 개발과 운영의 단순화를 위해 중복, 통합, 분리 등을 수행하는 데이터 모델링 기법
	- 데이터 무결성이 깨질 수 있는 위험을 무릅쓰고 데이터를 중복하여 반정규화를 적용하는 이유 : 데이터를 조회할 때 디스크 I/O 량이 많아 성능이 저하되거나 경로가 너무 멀어 조인으로 인한 성능 저하가 예상되거나 컬럼을 계산하여 읽을 때 성능이 저하될 것이 예상되는 경우 반정규화 수행
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdcLvQE%2FbtsgndvMaH9%2F6C9WM2RQSf9ZuEyP7pJoM1%2Fimg.png)

	나) 반정규화의 적용방법

| 1. 반정규화 대상조사                                                   | 2. 다른 방법 유도 검토                                         | 3. 반정규화 적용                             |
| -------------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------- |
| - 범위처리 빈도수 조사<br>- 대량 범위 처리 조사<br>- 통계성 프로세스 조사<br>- 테이블 조인 개수 | - 뷰(VIEW) 테이블<br>- 클러스터링 적용<br>- 인덱스의 조정<br>- 응용어플리케이션 | - 테이블 반정규화<br>- 속성의 반정규화<br>- 관계의 반정규화 |
*반정규화의 대상 조사*
- 자주 사용되는 테이블에 접근(Access)하는 프로세스의 수가 많고 항상 일정한 범위만을 조회하는 경우
- 대량의 데이터가 있고 대량의 데이터 범위를 자주 처리하는 경우 처리범위를 일정하게 줄이지 않으면 성능을 보장할 수 없는 경우
- 통계성 프로세스에 의해 통계정보를 필요로 할 때 별도의 통계테이블(반정규화 테이블) 생성
- 테이블에 지나치게 많은 조인이 걸려 데이터를 조회하는 작업이 기술적으로 어려울 경우

*반정규화 대상에 대해 다른 방법으로 처리할 수 있는지 검토*
- 많은 조인이 걸려 데이터 조회 작업이 기술적으로 어려울 경우 뷰를 사용해 해결할 수도 있음
- 대량의 데이터 처리나 부분처리에 의해 성능이 저하되는 경우에 클러스터링을 적용하거나 인덱스를 조정함으로써 성능을 향상할 수 있다. 클러스터링 적용 방법은 대량의 데이터를 특정 클러스터링 팩트에 의해 저장방식을 다르게 하는 방법임
- 대량의 데이터는 Primary Key의 성격에 따라 부분적인 테이블로 분리할 수 있다. 즉 파티셔닝(Partitioning) 기법이 적용되어 성능저하를 방지할 수 있다
- 응용 어플리케이션에서 로직을 구사하는 방법을 변경함으로써 성능을 향상시킬 수 있다

*반정규화 적용*
- 반정규화를 하는 대상으로는 테이블, 속성, 관계에 대해 적용할 수 있으며 꼭 테이블과 속성, 관계에 대해 중복으로 가져가는 방법만이 아니고 테이블, 속성, 관계를 추가 / 분할 / 제거 가능

2. 반정규화 기법
	가) **테이블의 반정규화
	

| 기법<br>분류 | 기법             | 내용                                                                                     |
| -------- | -------------- | -------------------------------------------------------------------------------------- |
| 테이블 병합   | 1:1 관계 테이블 병합  | 1:1관계를 통합하여 성능 향상                                                                      |
|          | 1:M 관계 테이블 병합  | 1:M 관계를 통합하여 성능 향상                                                                     |
|          | 슈퍼/서브 타입 테이블병합 | 슈퍼/서브 관계를 통합하여 성능 향상                                                                   |
| 테이블 분할   | 수직분할           | 칼럼단위의 테이블을 디스크 I/O를 분산처리 하기 위해 테이블을 1:1로 분리하여 성능향상(트랜잭션의 처리되는 유형 파악 선행)                |
|          | 수평분할           | 로우 단위로 집중 발생되는 트랜잭션을 분석하여 I/O및 데이터 접근의 효율성을 높여 성능을 향상하기 위해 로우단위로 테이블을 쪼갬 (관계가 없음)      |
| 테이블 추가   | 중복 테이블 추가      | 다른 업무이거나 서버가 다른 경우 동일한 테이블 구조를 중복하여 원격 조인을 제거해 성능 향상                                   |
|          | 통계 테이블 추가      | SUM, AVG등을 미리 수행하여 계산해 둠으로써 조회 시 성능 향상                                                 |
|          | 이력 테이블 추가      | 이력 테이블 중에서 마스터 테이블에 존재하는 레코드를 중복하여 이력 테이블에 존재하는 방법은 반정규화의 유형                           |
|          | 부분 테이블 추가      | 하나의 테이블의 전체 칼럼 중 자주 이용하는 집중화된 칼럼들이 있을 때 디스크 I/O를 줄이기 위해 해당 칼럼들을 모아놓은 별도의 반정규화된 테이블을 생성 |

나) **칼럼 반정규화**

| 반정규화 기법             | 내용                                                                                                                                                                       |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 중복칼럼 추가             | 조인에 의해 처리할 때 성능저하를 예방하기 위해 즉, 조인을 감소시키기 위해 중복된 칼럼을 위치시킴                                                                                                                  |
| 파생칼럼 추가             | 트랜잭션이 처리되는 시점에 계산에 의해 발생되는 성능저하를 예방하기 위해 미리 값을 계산하여 칼럼에 보관함 = Derived Column                                                                                             |
| 이력 테이블 칼럼 추가        | 대량의 이력데이터를 처리할 때 불특정 날 조회나 최근 값을 조회할 때 나타날 수 있는 성능저하를 예방하기 위해 이력 테이블에 기능성 칼럼(최근값 여부, 시작과 종료일자 등)을 추가                                                                     |
| PK에 의한 칼럼 추가        | 복합의미를 갖는 PK를 단일 속성으로 구성하였을 경우 발생. 단을 PK안에서 특정 값을 별도로 조회하는 경우 성능저하가 발생될 수 있음. 이 때 이미 PK안에 데이터가 존재하지만 성능향상을 위해 일반 속성으로 포함하는 반정규화 방법                                        |
| 응용시스템 오작동을 위한 칼럼 추가 | 업무적으로는 의미가 없지만 사용자가 데이터 처리를 하다가 잘못 처리하여 원해 값으로 복구하기를 원하는 경우 이전 데이터를 임시적으로 중복 보관하는 기법. 칼럼으로 이것을 보관하는 방법은 오작동 처리를 위한 임시적인 기법이지만 이것을 이력데이터 모델로 풀어내면 정상적인 데이터 모델의 기법이 될 수 있음 |

다) **관계 반정규화** 

| 반정규화 기법 | 내용                                                                         |
| ------- | -------------------------------------------------------------------------- |
| 중복관계 추가 | 데이터를 처리하기 위한 여러 경로를 거쳐 조인이 가능하지만 이 때 발생할 수 있는 성능저하를 예방하기 위해 추가적인 관계를 맺는 방법 |

3. 정규화가 잘 정의된 데이터 모델에서 성능이 저하될 수 있는 경우 1
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNpGiD%2FbtsgkIw5cCf%2FGGbxUSsvkCvkGQ1OSqA5WK%2Fimg.png)

- 공급자와 전화번호, 메일주소, 위치는 1:M관계이므로 한 명의 공급자당 여러개의 전화번호, 메일주소. 위치가 존재함 -> 따라서 가장 최근에 변경된 값을 가져오기 위해서는 조금 복잡한 조인이 발생될 수밖에 없다
```
SELECT A.공급자명, B.전화번호, C.메일주소, D.위치 
	FROM 공급자 A,
	(SELECT X.공급자번호, X.전화번호 
    	FROM 전화번호 X,
			(SELECT 공급자번호, MAX(순번) 순번 
            	FROM 전화번호
                WHERE 공급자번호 BETWEEN '1001' AND '1005'
				GROUP BY 공급자번호) Y 
         WHERE X.공급자번호 = Y.공급자번호
		   AND X.순번 = Y.순번) B,
           (SELECT X.공급자번호, X.메일주소
			FROM 메일주소 X,
				(SELECT 공급자번호, MAX(순번)
				 FROM 메일주소
				 WHERE 공급자번호 BETWEEN 
                 GROUP BY 공급자번호) Y
			WHERE X.공급자번호 = Y.공급자번호 
              AND X.순번 = Y.순번) C,
			(SELECT X.공급자번호, X.위치 
             FROM 위치 X,
				(SELECT 공급자번호, MAX(순번) 
                 FROM 위치
				 WHERE 공급자번호 BETWEEN '1001' AND '1005'
				 GROUP BY 공급자번호) Y 
             WHERE X.공급자번호 = Y.공급자번호
			   AND X.순번 = Y.순번) D 
             WHERE A.공급자번호 = B.공급자번호 
               AND A.공급자번호 = C.공급자번호 
               AND A.공급자번호 = D.공급자번호
               BETWEEN '1001' AND '1005'
               AND A.공급자번호 BETWEEN '1001' AND '1005'

출처: [https://sancheck-developer.tistory.com/62](https://sancheck-developer.tistory.com/62) [개발하는 엉배:티스토리]
```
- 정규화된 모델이 적절하게 반정규화되지 않으면 복잡한 SQL문이 나오게 됨

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcnTPoZ%2FbtsgnYrCBSx%2FQBnFcRkI7SoZBPsOvtKkRk%2Fimg.png)

```
SELECT 공급자명, 전화번호, 메일주소, 위치
	FROM 공급자
WHERE 공급자번호 BETWEEN '1001' AND '1005'
```
- 위에서의 복잡한 SQL문장이 반정규화를 적용해 다음과 같이 간단하게 작성 되어 가독성이 높아지고 성능도 향상되었다.

4. 정규화가 잘 정의된 데이터 모델에서 성능이 저하된 경우 2
- 업무 영역이 커지고 다른 업무, 인터페이스가 많아짐에 따라 데이터베이스 서버가 여러대인 경우
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9HZL0%2FbtsgiDiMXfG%2F0wtUi3E7v5dDu1jJz2m1E0%2Fimg.png)

- 서버 A에 부서와 접수 테이블이 있고 서버 B에 연계라는 테이블이 있는데 서버 B에서 데이터를 조회할 때 빈번하게 조회되는 부서번호가 서버 A에 존재하기 때문에 연계, 접수, 부서 테이블이 모두 조인이 걸리게 된다. 게다가 분산데이터베이스 환경이기 때문에 다른 서버 간에 조인이 걸리게 되어 성능이 저하된다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCVaQc%2Fbtsgk0RMj7a%2FwMUVawbf4ISFXjCPzjo2YK%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmeIpr%2FbtsglyHtHpy%2FzmYKnIFxC7a4cGfqkiI7JK%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fl3hNW%2Fbtsgkjj3DzK%2FtbXPXiLCvyCejfsbTNcb91%2Fimg.png)

- 위의 분산 환경에 따른 데이터 모델을 다음과 같이 서버 A에 있는 부서테이블의 부서명을 서버 B의 연계테이블에 부서명으로 속성 반정규화를 함으로써 조회 성능을 향상시킴

---

## 대량 데이터에 따른 성능

1. 대량 데이터 발생에 따른 테이블 분할 개요
- 대량의 데이터가 하나의 테이블에 집약되어 있고 하나의 하드웨어 공간에 저장되어 잇으면 성능저하를 피하기 힘듦
- 하나의 테이블에 대량의 데이터가 존재하는 경우 인덱스의 Tree 구조가 너무 커져 효율성이 떨어져 데이터를 처리(입력, 수정, 삭제, 조회)할 때 디스크 I/O를 많이 유발하게 됨
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcWbMOJ%2FbtsgujJ1Sbf%2Fi2nT5oIfRzw4Bo9uB1zDcK%2Fimg.png)

- 칼럼이 많아지게 되면 물리적인 디스크 여러 블록에 데이터가 저장되게 된다. 따라서 데이터를 처리할 때 여러 블록에서 데이터를 I/O해야 하는, 즉 SQL 문장 성능이 저하되는 특징을 가지게 됨

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdXYZ2Y%2FbtsgwMEwrB8%2FHAMpt0vJRa3faQiZLhrfE0%2Fimg.png)

- 로우 체이닝 현상(Row Chaining) = 로우 길이가 너무 길어서 데이터 블록 하나에 데이터가 모두 저장되지 않고 두 개 이상의 블록에 걸쳐 하나의 로우가 저장되어 있는 형태

2. 한 테이블에 많은 수의 칼럼을 가지고 있는 경우
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FootRD%2FbtsgqAMO8xR%2FmFiK4PrkkcNV5NKksBBCl1%2Fimg.png)

- 칼럼의 앞쪽에 위피한 발행기관 명, 수량, 중간에 위치한 공고일, 발행일에 대한 정보를 가져오려면 물리적으로 칼럼의 값이 블록에 넓게 산재되어 있어 디스크 I/O가 많이 일어나게 된다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcs76FA%2FbtsgtCQRBfH%2F8bqkeF2X3fkbkI4szeJ0hk%2Fimg.png)

- 많은 칼럼을 가지고 있는 테이블에 대해서는 트랜잭션이 발생될 때 어떤 칼럼에 대해 집중적으로 발생하는 지 분석하여 테이블을 쪼개주면 디스크 I/O가 감소해 성능이 개선됨
- 많은 수의 칼럼을 가지는 데이터 모델 형식도 실전 프로젝트에서 흔히 나타나는 현상임. 트랜잭션을 분석하여 적절하게 1:1 관계로 분리함으로써 성능 향상이 가능하도록 해야 함

3. 대량 데이터 저장 및 처리로 인한 성능이 저하되는 경우
- 테이블에 많은 양의 데이터가 예상될 경우 파티셔닝을 적용하거나 PK에 의해 테이블을 분할하는 방법을 적용할 수 있다
- 오라클의 경우 크게 LIST PARTITION, RANGE PARTITION, HASH PARTITIOM, COMPOSITE PARTITION(특정값 지정, 범위, 해쉬적용, 범위와 해쉬 복합) 등이 가능함

가) RANGE PARTIOTION 적용
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdcGIB7%2Fbtsgv9NoDKJ%2Fvb1FC3TlCLTtzDJlWRHZLK%2Fimg.png)

- DBMS 내부적으로 SQL WHERE 절에 비교된 요금일자에 의해 각 파티션에 있는 정보를 찾아가므로 평균 1,000만 건의 데이터가 있는 곳을 찾아도 되어 성능이 개선됨
- RANGE PARTITION은 데이터 보관주기에 따라 테이블에 데이터를 쉽게 지우는 것이 가능하므로 (파티션 테이블을 DROP하면 되므로)데이터 보관주기에 따른 테이블 관리가 용이함

나) **LIST PARTITION 적용**
- 지점, 사업소, 사업장, 핵심적인 코드값 등으로 PK가 구성되어 있고 대량의 데이터가 있는 테이블이라면 값 각각에 의해 파티셔닝 되는 LIST PARTITION을 적용할 수 있다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAI2Aq%2Fbtsgujca0Ok%2FL5rklR46zOrvARBqKIvsYK%2Fimg.png)

- LIST PARTITION은 대용량 데이터를 특정값에 따라 분리 저장할 수는 있으나 RANGE PARTITION과 같이 데이터 보관주기에 따라 쉽게 삭제하는 기능은 제공될 수 없다

다) **HASH PARTITION**
- 지정된 HASH 조건에 따라 해쉬 알고리즘이 적용되어 테이블이 분리되며 설계자는 테이블에 데이터가 정확하게 어떻게 들어갔는지 알 수 없다. 역시 성능향상을 위해 사용하며 데이터 보관주기에 따라 쉽게 삭제하는 기능은 제공될 수 업다

4. 테이블에 대한 수평/수직 분할의 절차
1) 데이터 모델링 완성
2) 데이터베이스 용량 산정
3) 대량 데이터가 처리되는 테이블에 대해 트랜잭션 처리 패턴 분석
4) 칼럼 단위로 집중화된 처리 발생 여부, 로우 단위로 집중화된 처리 여부를 분석해 집중화된 단위테이블 분리 검토

---

## 데이터 베이스 구조와 성능

1. 슈퍼 / 서브 타입 모델의 성능 고려
	가) 슈퍼 / 서브 타입 데이터 모델 개요
	- Extended ER 모델이라고 부르는 슈퍼/서브 타입 데이터 모델은 최근에 데이터 모델링을 할 때 자주 쓰이는 모델링 방법이다
	- 공통의 부분을 슈퍼 타입으로 모델링하고 공통으로부터 상속 받아 다른 엔터티와 차이가 있는 속성에 대해서는 별도의 서브 엔터티로 구분하여 업무의 모습을 정확하게 표현하면서 물리적인 데이터 모델로 변환 할 때 선택의 폭을 넓힐 수 있는 장점이 있다

	나) 데이터 모델의 변환
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fetq4Ng%2FbtsgE6Ki5Yy%2FkxQwI2tqeJKtqDlEtbD48K%2Fimg.png)

- 슈퍼 / 서브 타입에 대한 변환을 잘못하면 성능이 저하되는 이유는 트랜잭션 특성을 고려하지 않고 테이블이 설계되었기 때문임
	1) 트랜잭션은 항상 일괄로 처리하는 데 테이블은 개별로 유지되어 Union 연산에 의해 성능이 저하될 수 있다
	2) 트랜잭션은 항상 서브타입 개별로 처리하는 데 테이블은 하나로 통합되어 있어 불필요하게 많은 양의 데이터가 집약되어 있어 성능이 저하될 수 있다
	3) 트랜잭션은 항상 슈퍼 + 서브 타입을 공통으로 처리하는 데 개별로 유지되어 있거나 하나의 테이블로 집약되어 있어 성능이 저하되는 경우
 - 해당 테이블에 발생되는 성능이 중요한 트랜잭션이 빈번하게 처리되는 기준에 따라 테이블을 설계해야 이러한 성능저하 현상을 예방할 수 있음을 기억해야 함
 ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxIy72%2FbtsgDh7bYQ2%2FD45mPUkZp63mwQwhUkbhtK%2Fimg.png)

다) 슈퍼 / 서브 타입 데이터 모델의 변환 기술
1) 개별로 발생되는 트랜잭션에 대해서는 개별 테이블로 구성
	- 업무적으로 발생되는 트랜잭션이 수퍼타입과 서브타입 각각에 대해 발생하는 것
	- 슈퍼타입과 서브타입 각각에 대해 독립적으로 트랜잭션이 발생이 되면 수퍼타입에도 꼭 필요한 속성만을 가지게 하고 서브타입에도 꼭 필요한 속성 및 자신이 타입에 맞는 데이터만 가지게 하기 위해서 모두 분리하여 1:1 관계를 갖도록 한다
2) 슈퍼 + 서브타입에 대해 발생되는 트랜잭션에 대해서는 슈퍼타입 + 서브타입 테이블로 구성
	- 슈퍼타입과 서브타입을 묶어 트랜잯ㄴ이 발생하는 업무 특징을 가지고 있을 때 다음 데이터 모델과 같이 ㅠ퍼타입 + 각 서브타입을 하나로 묶어 별도의 테이블로 구성하는 것이 효율적이다
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclUWsr%2FbtsgE6XT9w5%2FZl7FfdBKnZszQZPTMZkOQk%2Fimg.png)
3) 전체를 하나로 묶어 트랜잭션이 발생할 때는 하나의 테이블로 구성
	- 슈퍼타입과 서브타입의 테이블들을 하나로 묶었을 때 각각의 속성별로 제약사항(NULL/NOT NULL, 기본값, 체크값)을 정확하게 지정하지 못할지라도 대용량이고 성능향상이 필요하다면 하나의 테이블로 묶어서 만들어준다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FctAwsB%2FbtsgDgNZcAh%2Fqm87RkWT7XVvKKmpYaSJd1%2Fimg.png)


2. 인덱스 특성을 고려한 PK/FK 데이터베이스 성능 향상
	가) PK/FK 칼럼 순서와 성능 개요
	- 데이터를 조회할 때 가장 효과적으로 처리될 수 있도록 접근 경로를 제공하는 오브젝트가 인덱스. 일반적으로 데이터베이스 테이블에서는 균형잡힌 드리구조의 B * Tree 구조를 많이 사용함
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblrGYw%2FbtsgC2Pt37C%2Ffg5EBLlHUZANs1xmE5il60%2Fimg.png)
	- 물리적인 데이터 모델링 단계에서는 스스로 생성된 PK 순서 이외에 다른 엔터티로부터 상속받아 발생되는 PK 순서까지 항상 주의하여 표시하도록 해야 한다

	나) PK 칼럼의 순서를 조정하지 않으면 성능이 저하되는 이유
	![0](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnGKtv%2FbtsgEfujFgS%2FOwh8zKnSxCl18kQwbRyL7K%2Fimg.png)
	
	- 테이블에서 데이터 모델의 PK 순서에 따라 DDL이 그래도 생성이 되고 테이블의 데이터가 주문번호가 가장 먼저 정렬되고 그에 따라 주문일자가 정렬이 되고 마지막으로 주문목록코드가 정렬이 됨
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDGSbt%2FbtsgEg0ZyJh%2FiiJRjA2O3KNqvP9U91ONDk%2Fimg.png)
	- 인덱스의 정렬된 첫 번째 칼럼에 비교가 되었기 때문에 순차적으로 데이터를 찾아가게 된다. 맨 앞에 있는 칼럼이 제외된 상태에서 데이터를 조회할 경우 데이터를 비교하는 범위가 매우 넓어지게 되어 성능 저하를 유발하게 된다
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsSSw8%2FbtsgEgmpQk4%2FXVJxl0wFUpKOBM5VViAT21%2Fimg.png)
	- 주문번호에 대한 비교값이 들어오지 않으므로 인해 인덱스 전체를 읽어야만 원하는 데이터를 찾을 수 있게 된다. 이러한 이유로 인덱스를 읽고 테이블 블록에서 읽어 처리하는 데 I/O가 많이 발생하게 되므로 옵티마이저는 차라리 테이블에 가서 전체를 읽는 방식으로 처리함
	- PK 순서를 인덱스 특징에 맞게 고려하지 않고 바로 그대로 생성하게 되면, 테이블에 접근하는 트랜잭션의 특징에 효율적이지 않은 인덱스가 생성되어 있으므로 인덱스의 범위를 넓게 이용하거나 Full Scan을 유발하게 되어 성능이 저하된다
	다) PK 순서를 잘못 지정하여 성능이 저하된 경우(간단한 오류) 
	![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBB3zk%2FbtsgEDIrwmU%2FaCMa4PCJe6zbetUqzYrkZ1%2Fimg.png)
	- 입스마스터I01 인덱스가 수험번호 + 년도 + 학기 중 수험번호에 대한 값이 WHERE절에 들어오지 않으므로 FULL TABLE SCAN이 발생, 200만건의 데이터를 모두 읽게 되어 성능 저하
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcf7AUL%2FbtsgCGGcuQ3%2FOR8KJrShfe9kw2TGCBiutk%2Fimg.png)
	- PK 순서를 변경함으로써 인덱스를 이용 가능하도록 할 수 있다. 즉, 생성된 인덱스가 정상적으로 이용이 되어 평균 2만 건의 데이터를 처리함으로써 성능이 개선된 모습
	라) PK 순서를 잘못 지정하여 성능이 저하된 경우 (복잡한 오류)
	- 출급기 실적의 PK는 거래일자 + 사무소코드 + 출급기 번호 + 명세표 번호로 되어 있는 데 대부분은 SQL 문장에서는 조회를 할 때 사무소 코드가 '='로 들어오고 거래일자에 대해서는 'BETWEEN' 조회를 하고 있다
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FHLFEF%2FbtsgL81Ci4h%2Fo57kVKLTnsz6eSiAcWND41%2Fimg.png)
	- 실행계획을 분석해보면 인덱스가 정상적으로 이용되었기 때문에 sql 문장은 튜닝이 잘된 것으로 착가할 수 있지만 문제는 인덱스를 이용할 때 얼마나 효율적으로 이용하는지 검증이 필요하다
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbnGUKS%2FbtsgJ0W4a1Q%2FkylKHYFXcfkpDuC54rMqh1%2Fimg.png)
	- 거래일자 + 시무소코드로 구성된 그림을 보면 BETWEEN 비교를 한 거래일자 '20040701'이 인덱스의 앞에 위치하기 때문에 범위가 넓어졌고 사무소코드 + 거래일자로 구성된 인덱스의 경우 '='비교를 한 사무소코드 '000368'이 인덱스 앞에 위치하여 범위가 좁아졌다. 그러므로 이 경우 인덱스 순서를 고려하여 데아ㅣ터 모델의 PK 순서를 거래일자 + 사무소코드+출급기 번호+ 명세표번호에서 사무소코드 + 거래일자 + 출급기번호+ 명세표 번호로 수정하여 성능을 개선


3. 물리적인 테이블에 FK 제약이 걸려있지 않을 경우 인덱스 미생성으로 성능 저하
- 물리적인 테이블에 FK를 사용하지 않아도 데이터 모델관계에 의해 상속받은 FK 속성들은 SQL WHERE 절에서 조인으로 이용되는 경우가 많이 있으므로 FK 인덱스를 생성해야 성능이 좋은 경우가 빈번함
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqMUYb%2FbtsgC3ubNpT%2FZUaB38KoID2y6UV5OroY70%2Fimg.png)

- 수강신청 테이블에 있는 학사기준번호가 SQL WHERE 절에 비교자로 들어오지는 않았지만 수강신청 테이블에서 상속받은 학사기준 번호에 대해 인덱스를 생성하지 않으므로 인해 학사기준과 수강신청 테이블이 조인되면서 500만건의 수강신청 테이블이 FULL TABLE SCAN이 발생되어 성능이 저하됨

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdkEPCA%2FbtsgEbSIY3M%2Fd0uNQkWCadgyGJqJ55Hsqk%2Fimg.png)

- 물리적으로 학사기준과 수강신청이 연결되어 있지 않다고 하더라도 학사기준으로부터 상속받은 FK에 대해 FK 인덱스를 생성함으로써 SQL 문장이 조인이 발생할 때 성능 저하 예방

## 분산 데이터베이스와 성능

1. 분산 데이터베이스의 개요
- 여러 곳으로 분산되어 있는 데이터베이스를 하나의 가상 시스템으로 사용할 수 있도록 한 DB
- 논리적으로 동일한 시스템에 속하지만, 컴퓨터 네트워크를 통해 물리적으로 분산되어 있는 데이터들의 모임
- 데이터베이스를 연결하는 빠른 네트워크 환경을 이용하여 데이터베이스를 여러 지역 여러 노드로 위치시켜 사용성/성능 등을 극대화 시킨 데이터베이스

2. 분산 데이터베이스의 투명성(Transparency)
- 6가지 투명성을 만족해야 함
1) 분할 투명성(단편화) : 하나의 논리적 Relation이 여러 단편으로 분할되어 각 단편의 사본이 여러 site에 저장
2) 위치 투명성 : 사용하려는 데이터 저장 장소 명시 불필요. 위치정보가 System Catalog에 유지되어야 함
3) 지역사상 투명성 : 지역 DBMS와 물리적 DB사이의 Mapping 보장. 각 지역 시스템 이름과 무관한 이름 사용 가능
4) 중복 투명성 : db 객체가 여러 site에 중복되어 있는지 알 필요가 없는 성질
5) 장애 투명성 : 구성요소(DBMS, Computer)의 장애에 무관한 Transaction의 원자성 유지
6) 병행 투명성 : 다수 Transaction 동시 수행 시 결과의 일관성 유지, Time Stamp, 분산 2단계 Locking을 이용 구현

3. 분산 데이터베이스의 장단점

| 장점                                                                                                                                           | 단점                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| - 지역 자치성, 점증적 시스템 용량 확장<br>- 신뢰성과 가용성<br>- 효용성과 융통성<br>- 빠른 응답 속도와 통신비용 절감<br>- 데이터의 가용성과 신뢰성 증가<br>- 시스템 규모의 적절한 조절<br>- 각 지역 사용자의 요구 수용 증대 | - 소프트웨어 개발 비용<br>- 오류의 잠재성 증대<br>- 처리 비용의 증대<br>- 설계, 관리의 복잡성과 비용<br>- 불규칙한 응답 속도<br>- 통제의 어려움<br>- 데이터 무결성에 대한 위협 |

4. 분산 데이터베이스의 활용 방향성
- 업무적인 기능이 다양해지고 데이터의 양이 기하급수적으로 증가하는 최근 데이터베이스 환경에서 적용하는 고급화된 기술
- 업무적인 특징에 따라 분산 데이터베이스를 활용하는 기술이 필요함
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUeQjH%2FbtsgG5j3qz9%2FRPKyu7XlY9BLzPi8Kn5yS1%2Fimg.png)

5. 데이터베이스 분산구성의 가치
- 거리 또는 다른 서버에 접속하여 처리함으로 인해 발생되는 네트워크 부하 및 트랜잭션 집중에 따른 성능 저하 -> 분산 데이터 베이스 환겸을 구축함으로써 빠른 성능 제공이 가능해짐
- 
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb14E5W%2FbtsgCCXV5XQ%2Fp8S0SIZI4E00lOKshLiDQ1%2Fimg.png)

6. 분산 데이터베이스의 적용 기법
	가) 테이블 위치 분산
	- 테이블의 구조는 변하지 않음. 테이블이 다른 데이터베이스에 중복 생성되지 않음 -> 다만 설계된 테이블의 위치를 각각 다르게 위치시키는 것
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7wojV%2FbtsgG6i7tUv%2F7ZFrZ7H2uVus0Z7FkusK01%2Fimg.png)
	- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdNtKny%2FbtsgMbRK8se%2FQa2EbZiPoOTVrfJKtAQSHk%2Fimg.png)

	나) 테이블 분할 분산 (Fragmentation)
	- 단순히 위치만 다른 곳에 두는 것이 아니라 각각의 테이블을 쪼개어 분산하는 방법
	- 테이블을 나누는 기준
	1) 수평 분할(Horizontal Fragmentation) : 테이블의 로우 단위로 분리
	- 지사(Node)에 따라 테이블을 특정 칼럼의 값을 기준으로 로우로 분리함(칼럼은 분리x). 모든 데이터가 각 지사별로 분리되어 있는 형태를 가지고 있다
	2) 수직 분할(Vertical Fragmentation) : 테이블의 칼럼 단위로 분할
	- 지사에 따라 테이블을 칼럼을 기준으로 칼럼으로 분히함(로우 단위 분리x). 모든 데이터가 각 지사별로 분리되어 있는 형태. 칼럼을 기준으로 분할하였기 때문에 각각의 테이블에는 동일한 Primary Key 구조와 값을 가지고 있어야 함

	다) 테이블 복제 분산 (Replication)
	- 동일한 테이블을 다른 지역이나 서버에서 동시에 생성하여 관리하는 유형
	1) 부분 복제 (segment Replication)
	- 통합된 테이블을 한 군데(본사)에 가지고 있으면서 각 지사별로는 지사에 해당된 로우를 가지고 있는 형태
	- 각 지사에서 데이터 처리가 용이할 뿐만 아니라 전체 데이터에 대한 통합처리도 본사에 있는 통합 테이블을 이용하게 되므로 여러 테이블에 조인이 발생하지 않는 빠른 작업 수행이 가능해짐
	2) 광역 복제(Brocast Replication)
	- 통합된 테이블을 한 군데에 가지고 있으면서 각 지사에도 본사와 동일한 데이터를 모두 가지고 있는 형태
	- 모든 지사에 있는 데이터량과 본사에 있는 데이터량이 다 동일하다. 본사와 지사 모두 동일한 정보를 가지고 있으므로 본사나 지사나 데이터처리에 특별한 제약을 받지는 않는다

	라) 테이블 요약 분산 (Summarization)
	- 지역 간에 또는 서버 간에 데이터가 비슷하지만 서로 다른 유형으로 존재하는 경우
	1) 분석 요약 (Rollup Replication)
	- 각 지사별로 존재하는 요약정보를 본사에 통합하여 다시 전체에 대해서 요약정보를 산출하는 분산방법
	2) 통합 요약 (Consolidation Replication)
	- 지사별로 존재하는 다른 내용의 정보를 본사에 통합하여 다시 전체에 대해서 요약정보를 산출하는 분산방법

7. 분산 데이터베이스를 적용하여 성능이 향상된 사례
- 프로젝트를 수행할 때 단순한 분산 환경의 원리를 이해하지 않고 데이터베이스를 설계하여 성능이 저하되는 경우가 빈번함. 특히 복제 분산의 원리를 간단하게 응용하면 많은 없무적인 특성이 있는 곳에서 그 성능을 향상시켜 설계할 수 있다
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQwSLc%2FbtsgCCcIcKk%2FWVzRUs73rYJbS2N9aXgEyk%2Fimg.png)
- 성능이 중요한 사이트에 적용해야 함
- 공통코드, 기준정보, 마스터 데이터 등에 대해 분산환경을 구성하면 성능이 좋아짐
- 실시간 동기화가 요구되지 않을 때 좋음. 거의 실시간의 업무적인 특징을 가지고 있을 때도 분산 환경을 구성할 수 있다.
- 특히 서버에 부하가 집중될 때 부라를 분산할 때도 좋음
- 백업 사이트를 구성할 때 간단하게 분산기능을 적용하여 구성할 수 있다