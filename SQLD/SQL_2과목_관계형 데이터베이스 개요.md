1. 데이터베이스

	가) 데이터베이스의 발전
	- 1960년대 : 플로우차트 중심의 개발방법을 사용, 파일 구조를 통해 데이터를 저장, 관리
	- 1970년대 : 데이터베이스 관리 기법 태동되던 시기. 계층형(Hierarchical) 데이터베이스, 망형(Network) 데이터 베이스 등 제품이 상용화됨
	- 1980년대 : 현재 대부분의 기업에서 사용되고 있는 관계형 데이터베이스가 상용화되었으며 Oracle, Sybase, DB2와 같은 제품이 사용됨
	- 1990년대 : Oracle, Sybase, DB2, Teradata, SQL Server 외 많은 제품들이 보다 향상된 기능으로 정보시스템의 확실한 핵심 솔루션으로 자리잡게 되었으며, 인터넷 환경의 급속한 발전과 객체지행 정보를 지원하기 위해 객체 관계형 데이터베이스로 발전하였다

	나) 관계형 데이터베이스(Relational Database)
	- 1970년 영국의 수학자였던 E.F Codd 박사의 논문에서 처음 관계형 DB가 소개된 이후, IBM의 SQL 개발 단계를 거쳐 Oravle을 선발로 여러 회사에서 상용화된 제품을 내놓았다. 이후 관계형 DB의 여러 장점이 알려지면서 기존의 파일시스템과 계층형, 망형 데이터베이스를 대부분 대체하면서 주력 데이터베이스가 되었다

2. SQL(Structured Query Language)
- 관계형 데이터베이스에서 데이터 정의, 데이터 조작, 데이터 제어를 하기 위해 사용하는 언어

| 명령어의 종류                                        | 명령어                               | 설명                                                                                                                |
| ---------------------------------------------- | --------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| 데이터 조작어<br>(DML: DATA Manipulation Language)   | SELECT                            | 데이터베이스에 들어 있는 데이터를 조회하거나 검색하기 위한 명령어를 말하는 것으로 RETRIEVE라고도 함                                                       |
|                                                | INSERT<br>UPDATE<br>DELETE        | 데이터베이스의 테이블에 들어 있는 데이터에 변형을 가하는 종류의 명령어. EX) 데이터를 테이블에 새로운 행을 집어넣거나, 원하지 않는 데이터를 삭제하거나 수정하는 것들의 명령어들을 DML이라고 부른다. |
| 데이터 정의어<br>(DDL: Data Definition Language)     | CREATE<br>ALTER<br>DROP<br>RENAME | 테이블과 같은 데이터 구조를 정의하는데 사용되는 명령어들로 그러한 구조를 생성, 변경, 삭제, 이름을 변경하는 데이터 구조와 관련된 명령어들을 DDL 이라고 부른다                       |
| 데이터 제어어<br>(DCL: Data Control Language)        | GRANT<br>REVOKE                   | 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어                                                                           |
| 트랜잭션 제어어<br>(TCL: Transation Control Language) | COMMIT<br>ROLLBACK                | 논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 작업단위(트랜잭션) 별로 제어하는 명령어                                                           |

3. TABLE
- 테이블은 데이터를 저장하는 객체(OBJECT)로서 관계형 데이터베이스의 기본단위
- 관계형 데이터베이스에서는 모든 데이터를 칼럼과 행의 2차원 구조로 나타낸다
- 세로 방향을 칼럼, 가로 방향을 행이라 하고, 칼럼과 행이 겹치는 하나의 공간을 필드라고 함
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTYfdd%2FbtsgJ0wd61d%2FresCbtxnGtHahHrsaH9bdk%2Fimg.png)

- 분할된 테이블은 그 칼럼의 값에 의해 연결됨. 이렇게 테이블을 분할하여 데이터의 불필요한 중복을 줄이는 것을 정규화(Nomalization) 이라고 한다. 데이터의 정합성 확보와 데이터 입력/수정/삭제 시 발생할 수 있는 이상현상(Anomaly)을 방지하기 위해 정규화는 관계형 데이터베이스 모델링에서 매우 중요한 프로세스이다.

| 용어  | 설명                                         |
| --- | ------------------------------------------ |
| 정규화 | 테이블을 분할해 데이터의 정합성을 확보하고, 불필요한 중복을 줄이는 프로세스 |
| 기본키 | 테이블에 존재하는 각 행을 한 가지 의미로 특정할 수있는 한 개 이상의 칼럼 |
| 외부키 | 다른 테이블의 기본키로 사용되고 있는 관계를 연결하는 칼럼           |
4. ERD(Entity Relationship Diagram)
- 데이터 정보 간에는 어떤 의미의 관계가 존재하며, 다른 테이블과도 어떤 의미의 연관성이나 관계를 가지고 있다
- ERD는 이와 같은 관계의 의미를 직관적으로 표현할 수 있는 좋은 수단임
- ![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRGKBO%2FbtsgEcRRPLa%2FdspccdmNFJwoMRt8jwKNp0%2Fimg.png)


## DDL(Data Definition Language)

1. 데이터 유형
- 데이터베이스의 테이블에 특정 자료를 입력할 때, 그 자료를 받아들일 공간을 자료의 유형별로 나누는 기준. 즉 특정 칼럼을 정의할 때 선언한 데이터 유형은 그 칼림이 받아들일 수 있는 자료의 유형을 규정

| 데이터 유형       | 설명                                                                                                                                                                                                           |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CHARACTER(s) | - 고정 길이 문자열 정보(Oracle, SQL Server 모두 CHAR로 표현)<br>- s는 기본 길이 1바이트, 최대 길이 Oracle 2,000바이트, SQL Server 8,000바이트<br>- s만큼 최대 길이를 갖고 고정 길이를 가지고 있으므로 할당된 변수 값의 길이가 s 보다 작을 경우 그 차이 길이만큼 공간으로 채워짐                 |
| VARCHAR(s)   | -CHARACTER VARYING의 약자로 가변 길이 문자열 정보(Oracle: VARCHAR2, SQL Server: VARCHAR)<br>- s는 최소 길이 1바이트, 최대 길이 Oracle 4,000바이트, SQL Server 8.000바이트<br>- s만큼의 최대 길이를 갖지만 가변 길이로 조정되기 때문에 할당된 변수값의 바이트만 적용됨 (Limit 개념) |
| NUMERIC      | - 정수, 실수 등 숫자 정보(Oracle: NUMBER, SQL: 10가지 이상의 숫자 타입)<br>- Oracle은 처음 전체 자리수를 지정하고 그 다음 소수 부분의 자리 수를 지정함<br>ex. 정수 부분 6자리, 소수점 부분 2자리 > 'NUMBER(8,2)'와 같이 된다.                                                |
| DATETIME     | - 날짜와 시각 정보(Oracle: DATE, SQL: DATETIME)<br>- Oracle: 1초 단위, SQL: 3.33ms 단위 관리                                                                                                                               |
2. CREATE TABLE
- 테이블은 일정한 형식에 의해서 생성된다. 테이블 생성을 위해서는 해당 테이블에 입력될 데이터를 정의하고, 정의한 데이터를 어떠한 데이터 유형으로 선언할 것인지를 결정해야 한다

	가) 테이블과 칼럼의 정의
	- 테이블에 존재하는 모든 데이터를 고유하게 식별할 수 있으면서 반드시 값이 존재하는 단일 칼럼이나 칼럼의 조합들(후보키)중에 하나를 선정하여 기본키 칼럼으로 지정함
	![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDFSOw%2Fbtsg0mT65DN%2Fnyt64oQscm8JAAxkmm86n1%2Fimg.png)

	나) CREATE TABLE
```
CREATE TABLE 테이블 이름 (
	칼럼명 1 DATATYPE [DEFAULT 형식],
	칼럼명 2 DATATYPE [DEFAULT 형식],
	칼럼명 3 DATATYPE [DEFAULT 형식]
);
```
- 테이블 명은 객체를 의미할 수 있는 적절한 이름을 사용. 가능한 단수형
- 테이블 명은 다른 테이블의 이름과 중복되지 않아야 함
- 한 테이블 내에서는 칼럼 명이 중복되게 지정될 수 없다
- 테이블 이름을 지정하고 각 칼럼들은 괄호로 묶어 지정함
- 각 칼럼들은 콤마 ','로 구문되고, 테이블 생성문의 끝은 세미콜론 ';' 으로 끝남
- 칼럼에 대해서는 다른 테이블까지 고려하여 데이터베이스 내에서는 일관성있게 사용하는 것이 좋다 (데이터 표준화 관점)
- 칼럼 뒤에 데이터 유형은 꼭 지정되어야 함
- 테이블명과 칼럼명은 반드시 문자로 시작해야 하고. 벤더 별로 길이에 대한 한계가 있다
- 벤더에서 사전에 정의한 예약어는 쓸 수 없다
- A-Z, a-z, 0-9,_, $, '#' 문자만 허용
- 테이블 생성 시 대/소문자 구분은 하지 않음. 기본적으로 테이블이나 칼럼 명은 대문자로 이루어짐
- DATETIME 데이터 유형에는 별도로 크기를 지정하지 않는다
- 문자 데이터 유형은 반드시 가질 수 있는 최대 길이를 표시해야 한다
- 칼럼과 칼럼의 구분은 콤마로 하되, 마지막 칼럼은 콤마를 찍지 않는다
- 칼럼에 대한 제약조건이 있으면 CONSTRAINT를 이용하여 추가할 수 있다

다) 제약조건
- 데이터의 무결성을 유지하기 위한 데이터베이스의 보편적인 방법으로 테이블의 특정 칼럼에 설정하는 제약

| 구분                   | 설명                                                                                                                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PRIMARY KEY<br>(기본키) | 테이블에 저장된 행 데이터를 고유하게 식별하기 위한 기본키를 정의함. 하나의 테이블에 하나의 기본키 제약만 정의할 수 있다 <br>기본키 제약을 정의하면 DBMS는 자동으로 UNIQUE 인덱스를 생성하며, 기본키를 구성하는 칼럼에는 NULL을 입력할 수 없다<br> 결국 '기본키 제약 = 고유키 제약 & NOT NULL제약' 이 된다 |
| UNIQUE KEY<br>(고유기)  | 테이블에 저장된 행 데이터를 고유하게 식별하기 위한 고유키를 정의한다. 단, NULL은 고유키 제약의 대상이 아니므로, NULL값을 가진 행이 여러 개가 있더라도 고유키 제약 위반이 되지 않는다                                                                                |
| NOT NULL             | NULL 값의 입력을 금지한다. 디폴트 상태에서는 모든 칼럼에서 NULL을 허가하고 있지만, 이 제약을 지정함으로써 해당 칼럼은 입력 필수가 된다. NOT NULL을 CHECK의 일부분으로 이해할 수도 있다                                                                         |
| CHECK                | 입력할 수 있는 값의 범위 등을 제한한다. CHECK제약으로는 TRUE or FALSE로 평가할 수 있는 논리식을 지정한다                                                                                                                        |
| FOREIGN KEY<br>(외래키) | 관계형 데이터베이스에서 테이블 간의 관계를 정의하기 위해 기본키를 다른 테이블의 외래키로 복사하는 경우 외래키가 생성된다<br>외래키로 지정 시 참조 무결성 제약 옵션을 선택할 수 있다                                                                                     |

라) 생성된 테이블 구조 확인
- 테이블을 생성한 후 테이블의 구조가 제대로 만들어졌는지 확인할 필요가 있다. Oracle의 경우 "DESCRIBE 테이블명;" 또는 간략히 "DESC 테이블명;"으로 해당 테이블에 대한 정보를 확인할 수 있다. SQL의 경우 "sp_help ‘dbo.테이블명"으로 해당 테이블에 대한 정보를 확인할 수 있다

마) SELECT 문장을 통힌 테이블 생성 사례
- CTAS: Create Table  ~ As Select ~
- 기존 테이블을 이용한 CTAS방법을 이용할 수 있다면 칼럼별로 데이터 유형을 다시 재정의하지 않아도 되는 장점이 있다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fby328S%2FbtsgL9VSNOs%2FD2tidVWtdGN4CRQPieMbwK%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbm2evD%2FbtsgUtTNbpm%2FpICLgFKNN7Ts7NGDGkFWk0%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbzy409%2FbtsgUr2MlQl%2F7Fb2CNx90GvOpT2BlnCl3K%2Fimg.png)

---

3. ALTER TABLE

	가) ADD COLUMN
	- 기존 테이블에 필요한 칼럼을 추가하는 명령
	- 주의할 것은 새롭게 추가된 칼럼은 테이블의 마지막 칼럼이 되며 칼럼위치 지정 불가
```
ALTER TABLE 테이블명

ADD 추가할 칼럼 명 데이터 유형;
```

나) DROP COLUMN
-테이블에서 필요없는 칼럼을 삭제할 수 있으며, 데이터가 있거나 없거나 모두 삭제 가능
한 번에 하나의 칼럼만 삭제 가능. 칼럼 삭제 후 최소 하나 이상 칼럼이 테이블에 존재해야 함
한번 삭제된 칼럼은 복구 불가
```
ALTER TABLE 테이블명

DROP COLUMN 삭제할 칼럼명;
```

다) MODIFY COLUMN
- 칼럼의 데이터 유형, 디폴트 값, NOT NULL 제약조건에 대한 변경을 포함할 수 있다

```
# Oracle
ALTER TABLE A
MODIFY (칼럼명 1 데이터 유형 [DEFAULT 식][NOT NULL],
		칼럼명2 데이터 유형 ...);

# SQL
ALTER TABLE A
ALTER (칼럼명 1 데이터 유형 [DEFAULT 식][NOT NULL],
		칼럼명2 데이터 유형 ...);
```

라) DROP CONSTRAINT
- 테이블 생성 시 부여했던 제약조건을 삭제하는 명령어
```
ALTER TABLE A DROP CONSTRAINT 제약조건명;
```

4. RENAME TABLE
- 명령어를 사용해 테이블 이름 변경
```
RENAME 변경전 테이블명 TO 변경후 테이블명;
```
- SQL에서는 sp_rename을 이용해 테이블 이름 변경
```
sp_rename 변경전 테이블명, 변경후 테이블명;
```


5. DROP TABLE
- DROP 명령어를 사용하면 테이블의 모든 데이터및 구조를 삭제한다. CASCADE CONSTRAINT 옵션은 해당 테이블과 관계가 있었던 참조되는 제약조건에 대해서도 삭제한다는 것을 의미
```
DROP TABLE 테이블면 [CASCADE CONSTRAINT];
```

5. TRUNCATE TABLE
- 테이블 자체가 삭제되는 것이 아닌 해당 테이블에 들어 있던 모든 행을 제거하고 저장 공간을 재사용가능하도록 해제함. 테이블 구조를 완전히 삭제하는 건 DROP TABLE!
```
TRUNCATE TABLE PLAYER;
```

## DML(Data Manipulation Language)
1. INSERT
- 테이블에 데이터를 입력하는 방법은 두 가지 유형이 있으며 한 번에 한 건만 입력된다
```
> INSERT INTO 테이블명 (COLUMN_LIST)
VALUES (COLUMN_LIST에 넣을 VALUE_LIST);

> INSERT INTO 테이블명
VALUES (전체 COLUMN에 넣을 VALUE_LIST);

```

2. UPDATE
- 다음에 수정되어야 할 칼럼이 존재하는 테이블명을 입력하고 SET 다음에 수정되어야 할 칼럼명과 해당 칼럼에 수정되는 값으로 수정이 이루어짐
```
UPDATE 테이블명
SET 수정되어야 할 칼럼명 = 수정되기를 원하는 새로운 값;
```

3. DELETE
- DELETE FROM 다음 삭제를 원하는 자료가 저장되어 있는 테이블명을 입력하고 실행. 이때 FROM 문구는 생략 가능한 키워드임. WHERE 절을 사용하지 않는다면 테이블 전체 테이터 삭제
```
DELETE [FROM] 삭제를 원하는 정보가 들어있는 테이블명;
```

- DDL(CREATE, ALTER, RENAME, DROP)명령어인 경우 직접 데이터베이스의 테이블에 영향을 미치때문에 DDL 명령어를 입력하는 순간 명령어에 해당하는 작업이 즉시완료(AUTO COMMIT)
- DML(INSERT, UPDATE, DELETE, SELECT)명령어인 경우 조작하려는 테이블을 메모리 버퍼에 올려놓고 작업하기 때문에 실시간으로 영향을 미치지 않음. 따라서 버퍼에 처리한 DML 명형어가 실제 테이블에 반영되기 위해서는 COMMIT 명령어를 입력해 TRANSACTION을 종료해야 함

4. SELECT
- 사용자가 입력한 데이터는 언제든 조회가 가능
```
SELECT [ALL/DISTINCT] 칼럼명, 칼럼명, ...
FROM 해당 칼럼들이 있는 테이블명;

- ALL : DEFAULT 옵션. 중복 데이터 모두 출력
- DISTINCT : 중복된 데이터는 `1건`으로 처리해서 출력
```

5. 산술연산자와 합성 연산자
	가) 산술연산자
	- NUMBER, DATE 자료형에 대해 적용되며 일반적으로 수학의 사칙연산과 동일. 우선순위를 위한 괄호적용 가능
```
SELECT PLAYER_NAME 이름, HEIGHT = WEIGHT "키-몸무게"
FROM PLAYER;
```
-
	나) 합성연산자 (CONCATENATION)
	- 문자와 문자를 연결하는 경우 2개의 수직바에 의해 이루어짐 (Oracle)
	- 문자와 문자를 연결하는 경우 + 표시에 의해 이루어짐 (SQL)
	- 두 벤더 모두 공통적으로 CONCAT(STR1, STR2) 함수 사용 가능
	- 칼럼과 문자 또는 다른 칼럼과 연결시킴
	- 문자 표현식의 결과에 의해 새로운 칼럼 생성
```
# Oracle
SELECT PLAYER_NAME || '선수,' || HEIGHT || 'cm,' || WEIGHT || 'kg' 체격정보

FROM PLAYER;
```

---

## TCL (Transaction Control Language)

1. 트랜잭션 개요
- 데이터베이스의 논리적 연산 단위
- 밀접히 관련되어 분리될 수 없는 한 개 이상의 데이터 베이스 조작
- 분할할 수 없는 최소단위. 그렇기 때문에 전부 적용하거나 전부 취소(ALL OR NOTHING)

| 특성                   | 내용                                                                         |
| -------------------- | -------------------------------------------------------------------------- |
| 원자성<br>(atomicity)   | 트랙잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않는 상태로 남아있어야 함 (all or nothing) |
| 일관성<br>(consistency) | 트랜잭션이 실행되기 전의 데이터베이스 내용이 잘못되어 있지 않다면 트랜잭션이 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 안됨 |
| 고립성<br>(isolation)   | 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안된다                           |
| 지속성<br>(durability)  | 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 데이터베이스의 내용은 영구적으로 저장된다                        |

2. COMMIT
- 입력한 자료나 수정한 자료, 삭제한 자료에 대해서 전혀 문제가 없다고 판단한 경우 COMMIT 명령어를 통해 트랜잭션을 완료할 수 있다
> COMMIT 이나 ROLLBACK 이전의 데이터 상태
- 단지 메모리 BUFFER에만 영향을 받았기 때문에 데이터의 변경 이전 상태로 복구 가능
- 현재 사용자는 SELECT 문장으로 결과 확인 가능
- 다른 사용자는 현재 사용자가 수행한 명령의 결과를 볼 수 없음
- 변경된 행은 잠금(LOCKING)이 설정되어 다른 사용자가 변경 불가
- 관련된 행에 대한 잠금(LOCKING)이 풀리고, 다른 사용자들이 행을 조작할 수 있게 됨

> COMMIT 이후의 데이터 상태
- 데이터에 대한 변경 사항이 데이터베이스에 반영됨
- 이전 데이터는 영원히 잃어버리게 됨
- 모든 사용자는 결과를 볼 수 있음

> SQL에서의 트랜잭션
- AUTO COMMIT : SQL의 기본 방식이며, DML, DDL을 수행할 때마다 DBMS가 트랜잭션을 컨트롤하는 방식
- 암시적 트랜잭션 : 트랜잭션의 시작은 DBMS가 처리하고 트랜잭션의 끝은 사용자가 명시적으로 COMMIT 또는 ROLLBACK 처리
- 명시적 트랜잭션 : 트랜잭션의 시작과 끝을 모두 사용자가 명시적으로 지정하는 방식

3. ROLLBACK
- 테이블 내 입력, 수정, 삭제한 데이터에 대해 COMMIT 이전에 변경 사항을 취소하기 위해 롤백ROLLBACK 기능 사용
- 데이터 변경 사항이 취소되어 데이터의 이전 상태로 복구되며, 관련된 행에 대한 잠금(LOCKING)이 풀리고 다른 사용자들이 데이터 변경을 할 수 있게 된다

> COMMIT과 ROLLBACK을 사용함으로써 얻는 효과
- 데이터 무결성 보장
- 영구적인 변경을 하기 전에 데이터의 변경 사항 확인 가능
- 논리적으로 연관된 작업을 그룹핑하여 처리 가능
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdaaNEa%2Fbtsg9C3rK0C%2FMtONlBvVAXKHEAKK489BsK%2Fimg.png)

4. SAVEPOINT
- SAVEPOINT를 정의하면 ROLLBACK할 때 트랜잭션에 포함된 전체 작업을 롤백하는 것이 아닌 현시점에서 SAVEPOINT까지 트랜잭션의 일부만 롤백할 수 있다
> SAVEPOINT SVPT1;
>  SAVETANSACTION SVTR1;
- SAVEPOINT 명을 부여하여 실행하면 저장점 설정 이후에 있었던 데이터 변경에 대해서만 원래 데이터 상태로 되돌아가게 됨
- SQL은 SQVE TRANSACTION을 사용하여 동일한 기능 수행

> ROLLBACK TRANSACTION SVTR1;
- 저장점가지 롤백할 때는 ROLLBACK 뒤에 저장점명을 지정함

---


## 윈도우 함수(WINDOW FUNCTION)

1. 개요
- 분석 함수나 순위 함수로도 알려져 있는 윈도우 함수는 데이터웨어하우스에서 발전한 기능

> WINDOW FUNCTION 종류

- 순위 관련 함수(RANK, DENSE_RANK, ROW_NUMBER)
- 집계 관련 함수(SUM, MAX, MIN, AVG, COUNT)
- 행 순서 관련 함수(FIRST_VALUE, LAST_VALUE, LAG, LEAD)
- 비율 관련 함수(CUME_DIST, PERCENT_RANK, NTILE, RATIO_TO_REPORT)
- 선형 분석을 포함한 통계 분석 관련 함수(CORR, COVAR_SAMP, STDDEV, STDDEV_POP 등)

> WINDOW FUNCTION SYNTAX

- WINDOW FUNCTION: 기존에 사용하던 함수도 있고, 새롭게 WINDOW 함수용으로 추가된 함수도 있다.
- ARGUMENTS(인수) : 함수에 따라 0 ~ N 개의 인수가 지정될 수 있다
- PARTITION BY 절 : 전체 집합을 기준에 의해 소그룹으로 나눌 수 있다
- ORDER BY 절 : 어떤 항목에 대해 순위를 지정할지 ORDER BY 절을 기술
- WINDOWING 절 : 함수의 대상이 되는 행 기준의 범위를 강력하게 지정

```
SELECT WINDOW_FUNCTION (ARGUMENTS) OVER
([PARTITION BY 칼럼] [ORDER BY  절] [WINDOWING 절])
FROM 테이블명;
```

2. 그룹 내 순위 함수

가) RANK 함수 : ORDER BY를 포함한 QUERY 문에서 특정 항목(칼럼)에 대한 순위를 구하는 함수
- 특정 범위(PARTITION) 내에서 순위를 구할 수도 있고 전체 데이터에 대한 순위를 구할 수도 있다
- 동일한 값에 대해서는 동일한 순위를 부여하게 된다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbOSh6%2FbtshWtyQHWG%2FmDXr1XxyqKPLdHN6YODWDK%2Fimg.png)

- 하나의 문장에 ORDER BY SAL DESC 조건과 PARTITION BY JOB 조건이 충돌 났기 때문에 HOB 별로는 정렬되지 않고 ORDER BY SAL DESC 조건으로 정렬 되었다

나) DENSE_RANK 함수
- RANK 함수와 흡사하나 동일한 순위를 하나의 건수로 취급한다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoQK5P%2FbtshWuYKJez%2FAmo64lkjeqwILY7nKkwWT1%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbsb1LE%2Fbtsh4lFFxtC%2FjOEev57exxkCqX8z0xHY30%2Fimg.png)

- FORD와 SCOTT, WARD와 MARTIN은 동일한 SALARY이므로 RANK와 DENSE_RANK칼럼에서 모두 같은 순위를 부여한다

다) row_number 함수
- RANK나 DESNE_RANK 함수가 동일한 값에 대해서는 동일한 순위흘 부여하는데 반해, 동일한 값이라도 고유한 순위를 부여한다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FS1jYf%2Fbtsh2FZdv6f%2FRv5kxMKfHLGd2HFFP6i4kk%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjewTP%2Fbtsh4PNjKEd%2F03iiQyfOgZ2ZfkZevYbcI0%2Fimg.png)

3. 일반 집계 함수

가) SUM 함수
- 파티션별 윈도우의 합 구하기
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FctusA8%2Fbtsh2mlkGgF%2FwSeLB79dRh02mD4aBZTMp1%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdf5six%2Fbtsh4m5FAmr%2FhLFnZZ3WrfsHOW1nzKgQn1%2Fimg.png)

나) MAX 함수
- 파티션별 윈도우의 최댓값
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBBlyJ%2Fbtsh2ndr8ZF%2FlKo8SQm1oU1CNY5wK1pjXk%2Fimg.png)

다) MIN 함수
- 윈도우의 최솟값
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLhRL0%2Fbtsh3lsrdlf%2FkE2rHXpnRb6zLHJGkcu680%2Fimg.png)


라) AVG 함수
- 원하는 조건에 맞는 데이터에 대한 통계값을 구할 수 있다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcp8XKk%2FbtshYcQ8HBU%2FJ7Kk3RaZaQDzZb5jJSgs41%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBZLYT%2FbtshWt6GYz3%2Fa05bWKcgKR54nqjISfh3S0%2Fimg.png)


마) COUNT 함수
- 원하는 조건에 맞는 데이터에 대한 통계값 구하기
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fs5T50%2Fbtsh2OVXyMQ%2FDy7wkhDV13X8YcXt4yVwz0%2Fimg.png)


4. 그룹 내 행 순서 함수
가) FIRST_VALUE 함수
- 파티션별 윈도우에서 가장 먼저 나온 값을 구한다
- SQL에서는 지원하지 않는 함수
- MIN 함수를 이용해 같은 결과를 얻을 수 있다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc5RWhf%2Fbtsh2QsJqEh%2FJk74YhhkCkV0pqJa18aYl0%2Fimg.png)


나) LAST_VALUE 함수
- 파티션별 윈도우에서 가장 나중에 나온 값을 구함
- SQL에서는 지원 안함
- MAX 함수를 활용해 같은 결과를 얻을 수 있다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxN2BM%2FbtshYcp3Zx0%2FfmCQqAuFsdB7HyNkncXoJ0%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbM7nv%2Fbtsh2txNK03%2Fmu0KxEDf7LTpQWB504duJK%2Fimg.png)

다) LAG 함수
- 윈도우에서 이전 몇 번째 행의 값을 가져올 수 있다
- SQL에서는 지원하지 않는 함수

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcq2vc1%2Fbtsh3mdQtXG%2FHSNkReyl5KubHNbj5BA8Dk%2Fimg.png)

라) LEAD 함수
- 파티션별 윈도우에서 이후 몇 번째 행의 값을 가져올 수 있다
- SQL 에서는 지원 안함

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxDk6T%2FbtshWuR1Tne%2FGQJdreNElpAssnCwEoJXLk%2Fimg.png)

6. 그룹 내 비율 함수

가) RATIO_TO_REPORT 함수
- 파티션 내 전체 SUM(칼럼) 값에 대한 행별 칼럼 값의 백분율을 소수점으로 구함
- 결과값은 <0 & <= 1의 범위를 가짐. 개별 RATIO의 합은 1
- SQL 지원 안함

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FumlZt%2Fbtsh3Dfyx6j%2FkESuKesntKFma1dXCEK951%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJwERk%2FbtshZviPR6Q%2FhUjb8I3HZaGMKwYNd4IQT0%2Fimg.png)


나) PERCENT_RANK 함수
- 파티션별 윈도우에서 제일 먼저 나오는 것을 0으로, 제일 늦게 나오는 것을 1로 하여 값이 아닌 행의 순서별 백분율을 구함
- 결과값은 >=0 & <= 1의 범위를 가짐. 
- SQL 지원 안함

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fzo9Lt%2Fbtsh2tYP48P%2FPwE2olRhMIIYUWKKxyHAU1%2Fimg.png)

다) CUME_DIST 함수
- 파티션별 윈도우의 전체 건수에서 현재 행보다 작거나 같은 건수에 대한 누적 백분율을 구함
- 결과값은 <0 & <= 1의 범위를 가짐.
- SQL 지원 안함

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcuV4g0%2Fbtsh2sljSWm%2FKcJAph5d7DiKfIHrYl13Ik%2Fimg.png)

라) NTILE 함수
- 파티션별 전체건수를 ARGUMENT 값으로 N 등분한 결과를 구할 수 있다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtwTnx%2Fbtsh33kONhl%2F7ZzLgoIQUvdNjFVlOAya7k%2Fimg.png)


## DCL (Data Control Language)

1. 개요
유저를 생성하고 권한을 제어할 수 있는 DCL 명령어가 있다

2. 유저와 권한
- 대부분의 데이터베이스는 데이터 보호와 보안을 위해서 유저와 권한을 관리하고 있다
- SQL 은 인스턴스에 접속학 위해 로그인을 생성하게 되며, 인스턴스 내에 존재하는 다수의 데이터베이스에 연결하여 작업하기 위해 유저를 생성한 후 로그인과 유저를 매핑해주어야 함
- Oracle은 유저를 통해 데이터베이스에 접속하는 형태. 즉, 아이디와 비밀번호 방식으로 인스턴스에 접속하고 그에 해당하는 스키마에 오브젝트 생성 등의 권한을 부여받게 된다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4IecN%2Fbtsh4ZoREGJ%2FNEyVaB0iEjZmkBayxS7270%2Fimg.png)

가) 유저 생성과 시스템 권한 분석
- 유저를 생성하고 데이터베이스에 접속한다
- 사용자가 실행하는 모든 DDL 문장은 그에 해당하는 적절한 권한이 있어야만 실행
- 새로운 유저를 생성하려 일단 유저 생성 권한(CREATE USER)이 있어야 한다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcyMzDF%2Fbtsh2O2JuWK%2Fdir1GLWHmN6IcFmwXqud4k%2Fimg.png)

나) Object에 대한 권한 부여
- 오브젝트 권한은 특정 오브젝트인 테이블, 뷰 등에 대한 SELECT, INSERT, DELETE, UPDATE 작업 명령어를 의미

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMtjy6%2FbtshWukbITW%2FUyTPCUr66n24NyAvVT1cc1%2Fimg.png)

3. Role 을 이용한 권한 부여
- 데이터베이스 관리자는 ROLE을 생성하고, ROLE에 각종 권한들을 부여한 후 ROLE이나 유저에게 부여할 수 있다
- ROLE에 포함되어 있는 권한이 필요한 유저에게 해당 ROLE만을 부여함으로써 빠르고 정확하게 필요한 권한을 부여할 수 있게 된다

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcl64MJ%2Fbtsh4leEdTK%2FeYKPzxl1saxeUZ4g2LI4v1%2Fimg.png)

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFBX3f%2Fbtsh1T4MbCF%2FqPaJWR8KkXqGOh9Ml5T3o1%2Fimg.png)

- Oracle Role
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmKiZa%2Fbtsh4lZ0s2Y%2FXZlouC0Gi808l2shnHL2Pk%2Fimg.png)

- SQL

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn4pGo%2Fbtsh2lGJE9v%2FHkFhv3K6yMvXcw3GGmPJdK%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbag0Fw%2Fbtsh6z4xbXG%2FQIFRgmQzXkXk2Sk0pO0Ri0%2Fimg.png)


## 절차형 SQL

1. 절차형 SQL 개요
- 일반적인 개발 언어처럼 SQL에도 절차 지향적인 프로그램이 가능하도록 DBMS 벤더 별로 PL(Procedural Language)/SQL(Oracle), SQL(DB2), T-SQL 등의 절차형 SQL을 제공하고 있다
- SQL문의 연속적인 실행이나 조건에 따른 분기처리를 이용하여 특정 기능을 수행하는 저장 모듈을 생성할 수 있다

2. PL/SQL 개요
- Oracle의 PL/SQL은 블록구조로 되어 있고 블록 내에는 DML 문장과 쿼리 문장, 그리고 절차형 언어(IF, LOOP) 등을 사용할 수 있으며 절차적 프로그래밍을 가능하게 하는 트랜잭션 언어

가) PL/SQL 특징
- 블록 구조로 되어 있어 각 기능별로 모듈화 가능
- 변수, 상수 등을 선언하여 SQL 문장 간 값을 교환
- IF, LOOP 등의 절차형 언어를 사용하여 절차적인 프로그램 가능
- DBMS 정의 에러나 사용자 정의 에러를 정의하여 사용할 수 있다
- Oracle에 내장되어 있으므로 지원하는 어떤 서버로도 프로그램을 옮길 수 있다
- 응용 프로그램의 성능을 향상시킨다
- 여러 SQL 문장을 Block으로 묶고 한 번에 Block 전부를 서버로 보내기 때문에 통신량을 줄일 수 있다
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4azdJ%2FbtsiaZpSo9l%2FM3zfcMAgDkeOoqrF1BwN10%2Fimg.png)

나) PL/SQL 구조
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXkPoN%2FbtsibflIdG5%2FfXt7wxeWg3xp3pDGf8wFWk%2Fimg.png)

- DECLARE : BEGIN ~ END 절에서 사용될 변수와 인수에 대한 정의 및 데이터 타입을 선언하는 선언부
- BEGIN ~ END : 개발자가 처리하고자 하는 SQL문과 여러 가지 비교문, 제어문을 이용하여 필요한 로직을 처리하는 실행부
- EXCEPTION : BEGIN ~ END 절에서 실행되는 SQL문이 실행될 때 에러가 발생하면 에러를 어떻게 처리할지 정의하는 예외 처리부

다) PL/SQL 기본 문법(Syntax)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdyglCK%2FbtsidXj5y2p%2FxRQiIqgHxOt61y2Sg9aVM0%2Fimg.png)

- CREATE TABLE 명령어로 테이블을 생성하듯 CREATE 명령어로 데이터베이스 내에 프로시저를 생성할 수 있다

3. T-SQL 개요
- T-SQL은 근본적으로 SQL 를 제어하기 위한 언어
- 변수 선언 기능 @@이라는 전역변수(시스템 함수)와 @이라는 지역변수가 있다
- 지역변수는 사용자가 자신의 연결 시간 동안만 사용하기 위해 만들어지는 변수. 전역변수는 이미 SQL 서버에 내장된 값
- 데이터 유형을 제공. 즉, INT, FLOAT, VARCHAR 등의 자료형 의미
- 연산자 산술 연산자와 비교연산자, 논리연산자 사용 가능
- 흐름 제어 기능 IF-ELSE와 WHILE, CASE-THEN 사용 가능
- 주석 기능
- 한 줄 주석 : --
- 범위 주석 /*내용*/, 여러 줄도 가능함

나) T-SQL 구조
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcqIPzK%2Fbtsibb4IwZB%2FBSp5wHFmCs7Whw15KPURp1%2Fimg.png)

- DECLARE : BEGIN ~ END 절에서 사용될 변수와 인수에 대한 정의 및 데이터 타입을 선언하는 선언부
- BEGIN ~ END : 개발자가 처리하고자 하는 SQL문과 여러 가지 비교문, 제어문을 이용하여 필요한 로직을 처리하는 실행부
- ERROR 처리 : BEGIN ~ END 절에서 실행되는 SQL문이 실행될 때 에러가 발생하면 에러를 어떻게 처리할지 정의하는 예외 처리부

다) T-SQL 기본 문법

![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdiR0Kp%2Fbtsib1Hwa3L%2FFY5GjX2eVHyKDyw7lWRzK1%2Fimg.png)
![-](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdjdzDm%2Fbtsic6VTo3i%2FhHJmMAGZkYbrN1OpGShAWK%2Fimg.png)

4. Trigger
- 특정 테이블에 INSERT, UPDATE, DELETE와 같은 DML 문이 수행되었을 때, 데이터베이스에서 자동으로 동작하도록 작성된 프로그램
- 사용자가 직접 호출하여 사용하는 것이 아니고 데이터베이스에서 자동적으로 수행하게 된다
- 테이블과 뷰, 데이터 베이스 작업을 대상으로 정의할 수 있으며, 전체 트랜잭션 작업에 대해 발생되는 Trigger와 각 행에 대해서 발생되는 Trigger가 있다

5. 프로시저와 트리거의 차이점
- 프로시저는 BEGIN ~ END 절 내에 COMMIT, ROLLBACK과 같은 트랜잭션 종료 명령어를 사용할 수 있지만, 데이터베이스 트리거는 BEGIN ~ END 절 내에서 사용할 수 없다

| 프로시저                   | 트리거                    |
| ---------------------- | ---------------------- |
| CREATE Procedure 문법 사용 | CREATE Trigger 문법 사용   |
| EXECUTE 명령어로 실행        | 생성 후 자동 실행             |
| COMMIT, ROLLBACK 실행 가능 | COMMIT, ROLLBACK 실행 안됨 |
