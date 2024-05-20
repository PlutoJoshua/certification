데이터 출처 : 데이터전문가포럼카페 
(https://cafe.naver.com/sqlpd?iframe_url=/MyCafeIntro.nhn%3Fclubid=21771779)

### 1. 엔터티는 주식별자 속성을 가지고 있어야 하나 예외적으로 주식별자 속성망을 가지고 있어도 엔터티로 인정이 되는 엔터티는?

**관계엔터티**

### 2. 데이터 품질을 위한 데이터 모델링 방법 (*논쟁이 있는 문제*)

> 데이터 모델링 방법

### 3. 개념 데이터 모델링에 대한 설명으로 적절하지 않은 것은?

추상화라 구체화하는게 적합하지 않다 
-> **개념 데이터 모델은 추상적이므로 그 모델은 상위의 문제에 대한 구조화를 쉽게 함**

### 4. 외부 스키마 특징

**뷰 단계 여러 개의 사용자 관점으로 구성. 개개 사용자 단계로서 개개 사용자가 보는 개인적 DB 스키마
DB의 개개 사용자나 응용 프로그래머가 접근하는 DB정의
-> 응용 프로그램 관점에서의 요구사항, 사용자 관점, DB 정의**
### 4. (1) 개념 스키마 특징

외부 스키마가 필요로 하는 데이터를 모두 모아놓은 것. 설계자 관점
DB에 저장되는 데이터와 사용자 관계  표현 -> 모든 사용자 관점 통합, 조직 전체 통합
### 4. (2) 내부 스키마 특징

데이터베이스가 물리적으로 저장된 형식, 개발자 관점
	-> 데이터 모델링은 통합 관점의 개념 스키마를 만들어가는 과정

### 5. 그 업무에 원래 존재하는 정보로서 다른 엔터티와 관계에 의해 생성되지 않고 독립적으로 생성이 가능하고 자신은 타 엔터티의 부모 역할을 하게 되는 엔터티?

**기본 엔터티**

### 6. 식별자와 비식별자의 관계

1. **식별자**(==실선==)
- 자식이 부모의 기본키를 상속받아 기본키로 사용하는 경우
- 강한 연결관계, 부모에 종속, NULL X, 1:1 or 1:N 관계
- 문제점 : 자식의 주식별자 속성이 지속적으로 증가할 수 있음 -> 복잡, 오류 가능성
2. **비식별자**(==점선==)
- 부모로부터 속성을 받아 일반 속성으로 사용하는 경우(약한 종속)
- 문제점 : 부모까지 조인, 불필요 현상 발생 -> SQL 구문이 길어져 성능 저하

### 7. 인스턴스, 엔터티, 속성, 속성값 다이어그램

**엔터티 --<- 인스턴스 ---<-속성 ----속성값**
![-](data:image/png;base64,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)

### 8. 9. 정규화
1. **제 1정규화**
- 테이블 컬럼이 원자성(한 속성이 하나의 값을 갖는 특성)을 갖도록 테이블을 분해하는 단계
- 쉽게 말해 하나의 행과 컬럼의 값이 반드시 한 값만 입력되도록 행을 분리하는 단계
2. **제 2정규화**
- 제 1정규화를 진행한 테이블에 대해 완전 함수 종속을 만들도록 테이블을 분해
- *완전함수 종속* : 기본키를 구성하는 모든 칼럼의 값이 다른 칼럼을 결정짓는 상태
- 기본키의 부분집합이 다른 칼럼과 1:1 대응 관계를 갖지 않는 상태를 의미
- 즉, PK가 2개 이상일 때 발생하며 PK의 일부와 종속되는 관계가 있다면 분리한다
3. **제 3정규화**
- 제 2정규화를 진행한 테이블에 대해 이행적 종속을 없애도록 테이블을 분리
- 이행적 종속성이란 A->B, B->C의 관계가 성립할 때, A->C가 성립되는 것을 의미함
- (A,B)와 (B,C)로 분리하는 것이 제 3정규화
- 3차 정규형은 1, 2차를 포함한다

### 10. 속성
< ERD >
PK : 사원번호
속성 : 주민등록번호, 부서번호(FK)
- 부서번호는 **외부식별자** 이다

**속성** : 대상들이 갖는 속성(하나의 특징으로 정의될 수 있는 것)
- **업무에서 필요로 하는 고유한 성질, 특징(관찰 대상) -> ==컬럼==으로 표현할 수 있는 단위
- 업무상 인스턴스로 관리하고자 하는 **더이상 분리되지 않는 최소의 데이터 단위**
- 반드시 해당 업무에서 필요하고 관리하고자 하는 정보여야 함
- **정해진 주식별자에 함수적 종속성을 가져야 한다**
- 하나의 속성은 한 개의 값만을 가짐(한 컬럼의 값은 각 인스턴스마다 하나씩만 저장)
- 하나의 속성에 여러 개의 값이 있는 다중값일 경우 별도의 엔터티를 이용하여 분리함
- 하나의 인스턴스는 속성마다 반드시 하나의 속성값을 가진다
	-> 각 속성이 하나의 값을 가지고 있음을 의미(속성의 **원자성**)

### **원자성** : 
데이터 모델에서 각 엔터티의 <u>인스턴스가 해당 속성에 대해 단일하고 명확한 값을 가지는 것</u>

### **함수적 종속성**
- 한 속성의 값이 다른 속성의 값에 종속적인 관계를 갖는 특징
- 즉, **어떤 속성 A의 값에 의해 다른 속성 B도 유일하게 결정된다면,** B는 A에 함수적으로 종속됐다하고, 이를 수식으로 나타내면 A->B 로 표현함


### 식별자 분류
1) 대표성 여부

| 주 식별자                                                                                                         | 보조 식별자                                                                                                             |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| - 유일성과 최소성을 만족하면서 <br>엔터티를 대표하는 식별자<br>- 엔터티 내에서 각 인스턴스를 유일하게 <br>구분할 수 있는 식별자<br>- 타 엔터티와 참조관계를 연결할 수 있는 식별자 | - 엔터티 내 각 인스턴스를 구분할 수 있는<br> 구분자지만, 대표성을 가지지 못해<br>참조 관계 연결을 할 수 없는 식별자<br>- 유일성과 최소성은 만족하지만 <br>대표성을 만족하지 못하는 식별자 |

2) 생성 여부

| 내부 식별자                               | 외부 식별자                           |
| ------------------------------------ | -------------------------------- |
| - 다른 엔터티 참조 없이 엔터티 내부에서 스스로 생성되는 식별자 | - 다른 엔터티와 관계로 인하여 만들어지는 식별자(외래키) |

3) 속성 수

| 단일 식별자        | 복합 식별자         |
| ------------- | -------------- |
| - 하나의 속성으로 구성 | 2개 이상의 속성으로 구성 |

4) 대체 여부

| 본질 식별자                  | 인조 식별자                                    |
| ----------------------- | ----------------------------------------- |
| - 비즈니스 프로세스에서 만들어지는 식별자 | - 인위적으로 만들어지는 식별자<br>- 자동 증가하는 일련번호 같은 형태 |

