# MYSQL 기초
• SQL(Structured Query Language)
관계형 데이터베이스 표준 언어로서 가장 많이 사용되는 데이터 언어


## SQL의 기능별 분류
- 데이터 정의어 (DDL)
- 데이터 조직어 (DML)
- 데이터 제어어 (DCL)

## SQL 사용 준비
MYSQL 버전과 시스템 날짜시간 정보 확인
```
select version();
select current_date(), current_time(), now();
```
현재 접속한 사용자 아이디 확인
```
select user();
```
데이터베이스 목록 확인
```
show DATABASE;
```

## 데이터 조작문
- SELECT문
-- SELECT 컬럼명 FROM 테이블명;
```
SELECT * FROM 학생;
```
```
SELECT 학번, 이름 FROM 학생;
```
- DISTINCT -- 중복행 제거 검색
```
SELECT DISTINCT 소속학과 FROM 학생;
```
- WHERE -- 조건식
```
SELECT 이름, 학년, 소속학과, 휴대폰번호 FROM 학생
WHERE 학년>=2 AND 소속학과='컴퓨터';
```
- ORDER BY -- 순서화 정렬
```
SELECT 이름, 학년, 소속학과 FROM 학생
WHERE 소속학과='컴퓨터' OR 소속학과='정보통신'
ORDER BY 학년 ASC; #ASC 오름차순, DESC 내림차순
```


- 집계함수
    - COUNT()
    - MAX()
    - MIN()
    - SUM()
    - AVG()

- GROUP BY -- 그룹화 검색
```
SELECT 성별, MAX(나이) AS '최고 나이' FROM 학생
GROUP BY 성별;
```
- HAVING -- 그룹 조건 검색
    - GROUP BY 통해서 생성된 그룹 중에서 특정 조건을 만족하는 그룹만으로 검색을 제한
    - WHERE절이 행에 대한 `검색_조건식`을 의미한다면, HAVING절은 `그룹 조건식`을 의미
```
SELECT 학년, COUNT(*) AS '학년별 학생수' FROM 학생;
GROUP BY 학년;
HAVING COUNT(*)>2;
```
- LIKE -- 문자 연산자 검색
    - '_' _겟수만큼 문자 겟수 의미
    ```
    SELECT 학번, 이름 FROM 학생
    WHERE 이름 LIKE '이__';    
    ```
    - '%' 0개 이상의 모든 문자 출력 허용
    ```
    SELECT 이름, 주소, 학년 FROM 학생
    WHERE 주소 LIKE '%서울%'
    ORDER BY 학년 DESC;
    ```

- 널 값 검색 IS NULL, IS NOT NULL 
```
SELECT 이름, 휴대폰번호 FROM 학생
WHERE 휴대폰번호 IS NULL;
```

- UNION -- 집합 연산자 검색
```
SELECT 학번 FROM 학생
WHERE 성별 = '여'
UNION
SELECT 학번 FROM 수강
WHERE 평가학점='A';
```

- Subquery 
    - 질의문 안에 중첩되어 포함된 또 다른 SELECT 검색문
    - 괄호 안의 가장 안쪽 부 질의문부터 수행
- IN
    - 나열된 값 중에서 하나라도 일치한다면 참(true)을 반환함
- NOT IN
    - 나열된 값들 중 어떤 값도 일치하지 않을 경우 참을 반환

```
SELECT 이름 FROM 학생
WHERE 학번 IN ('s001', 's003');
```

- 부 질의문
    - 내부질의(inner query)
    - 외부질의(outer query)

- EXISTS 연산자
    - 부 질의문의 실행 결과로 반환되는 행이 존재하는지 존재 유무를 확인하는 연산자
```
SELECT 이름 FROM 학생
WHERE EXISTS (
    SELECT * FROM 수강
    WHERE 수강.학번=학생.학번 AND 과목번호='c002'
)
```

- JOIN 
```
SELECT 열_리스트 FROM 조인테이블_리스트
WHERE <조인_조건식> AND <검색_조건식>
```
- 크로스 조인
- 동등 조인
```
SELECT * FROM 학생.수강
WHERE 학생.학번=수강.학번;
```

- 셀프 조인
- 외부 조인(OUTER JOIN)
```
SELECT 학생.학번, 이름, 평가학점 FROM 학생
LEFT OUTER JOIN 수강 ON 학생.학번=수강.학번
```

- INSERT -- 행 삽입
```
INSERT INTO 학생1
VALUES ('g001', '김연아2', '서울 서초', 4, 23, '여', '010-1111-2222', '컴퓨터');
```

- UPDATE -- 행 수정
```
UPDATE 학생1
SET 학년=3
WHERE 이름='이은진';
```

- DELETE -- 행 삭제
```
DELETE FROM 학생1
WHERE 이름='송윤아';
```
모든 행 삭제
```
DELETE FROM 학생1;
```


# MYSQL 활용
## 1. 데이터 정의문

- CREATE -- 테이블 생성
```
CREATE TABLE tbl_subject2 (
sub_no CHAR(4) NOT NULL PRIMARY KEY,
sub_name VARCHAR(20) NOT NULL,
sub_classroom CHAR(5) NOT NULL,
sub_dept VARCHAR(20) NOT NULL,
sub_time INT NOT NULL
) ;
```
- DESC -- describe 약자로 각 컬럼의 데이터 유형 등을 확인 가능하다.
```
DESC tbl_students2;
```

- ALTER -- 테이블 수정
```
ALTER TABLE 학생2
    ADD 등록날짜 DATETIME NOT NULL DEFAULT '2019-12-30';
```
```
ALTER TABLE 학생2
    DROP COLUMN 등록날짜;
```

- DROP -- 테이블 삭제
```
DROP TABLE 테이블명;
```

## 2. 데이터 제어문
- CREATE USER -- 사용자 계정 생성
```
CREATE USER 사용자_계정 IDENTIFIED BY '비밀번호';
```
생성된 사용자 계정 정보 확인
```
SELECT host, user FROM mysql.user;
```
- GRANT -- 권한 부여
```
GRANT 권한_내용 ON 권한대상 TO 사용자계정;
```
사용자 계정의 권한 확인
```
SHOW GRANTS FOR 'user1'@'127.1.1.1';
```
현재 접속 사용자의 권한 표시
```
SHOW GRANTS; 
```
- 권한 철회(REVOKE) 및 계정 삭제(DROP USER)
```
REVOKE 권한내용 ON 권한대상 FROM 사용자계정;
```
```
DROP USER 'user1'@'127.1.1.1';
```
- 사용자 계정 생성
    - 'manager' 관리자 계정 생성
```
CREATE USER 'manager'@'%' IDENTIFIED BY '1234';
```
- 'manager'계정에 권한 부여
```
GRANT ALL ON *.* TO 'manager'@'%' WITH GRANT OPTION;
```
- 현재 접속한 사용자 아이디를 확인
```
SELECT user(); 
```

## 3. 뷰
- 데이터베이스를 바라보는 창문(window)

### 3.1 뷰의 정의
- 실제 데이터를 저장하지 않는 가상 테이블(virtual table)
- 뷰에 대해 사용자가 질의를 요청할 때 비로소 DBMS는 뷰 정의를 참조하여 질의를 수행하고 그 결과를 사용자에게 반환
- 주로 기반 테이블로부터 정의되지만 또 다른 뷰를 기반으로도 정의될 수도 있음

### 3.2 뷰의 장점
- 편의성 : 복잡한 질의문 작성이 쉽고 간단해진다. 
- 보안성 : 데이터 보안 유지가 쉽다. 
- 재사용성 : 반복되는 질의문 작성에 효율적이다. 
- 독립성 : 스키마 변경에도 뷰 질의문은 변경할 필요가 없다

### 3.3 뷰 생성
```
CREATE VIEW 뷰이름(열 리스트)
AS SELECT 검색문
```
```
CREATE VIEW VI_고학년학생(학생이름, 나이, 성, 학년)
AS SELECT 이름, 나이, 성별, 학년 FROM 학생
WHERE 학년 >= 3 AND 학년 <= 4
```
뷰의 생성 확인
```
SELECT * FROM VI_고학년학생;
```
### 3.3 뷰를 이용한 검색
- 뷰를 통한 데이터 변경
    - 뷰 검색은 제한 없이 가능한 반면 뷰 변경은 특정한 경우로 한정
- 뷰 변경이 제한되는 이유
    - 뷰를 정의하는 ‘SELECT_검색문’의 조건이 다양하기 때문
    - 뷰가 참조하는 기반 테이블을 변경해야 하므로 내부 처리가 어려운 경우는 변경이 허용되지 않음

### 3.4 뷰 삭제
```
DROP VIEW 뷰이름;
```
```
DROP VIEW V1_고학년학생;

SHOW TABLES;
```

## 4. 인덱스

### 4.1 인덱스 개념
- 테이블 안의 데이터를 쉽고 빠르게 찾을 수 있도록 만든 데이터베이스 객체
- 책 페이지를 목차나 색인을 통해 쉽게 찾는 것과 같은 원리

### 4.2 인덱스의 필요성
- SQL을 실행할 때, 디스크 접근 횟수를 줄여 검색 속도를 높이기 위함
    - 대부분 DBMS는 B-트리(Balanced tree) 구조의 인덱스를 지원
    - 장점 : 루트 노드로부터 리프 노드까지의 탐색 길이가 같아서 모든 데이터에 대한 일정 수준의 검색 시간을 보장

### 4.3 인덱스의 생성
```
CREATE INDEX 인덱스이름 
ON 테이블명 (열 이름들)
```
생성된 인덱스 확인
```
SHOW INDEX FROM 테이블명;
```
인덱스 삭제
```
DROP INDEX 인덱스명 ON 테이블명;
```

### 4.4 인덱스 적용 고려사항
- 불필요한 인덱스는 오히려 성능을 떨어뜨리고 저장 공간만 낭비할 수 있음
- 인덱스는 꼭 필요한 만큼만 효과적으로 생성해야 함

【인덱스 생성이 필요한 경우】

 - 기본키와 외래키의 경우, 인덱스 생성이 바람직함. 대부분의 DBMS는 기본키에 대해서 자동으로 인덱스를 생성함
- WHERE 절 조건식에 자주 사용되는 테이블 열의 경우, 인덱스 생성이 바람직함
- 조인 조건식에 자주 사용되는 테이블 열도 인덱스 생성이 바람직함
- 하나의 테이블에 3~5개 정도의 인덱스가 효과적임
- 가변길이 문자형이나 실수형, 날짜형 열보다는 정수형, 고정길이 문자형 열에 인덱스를 생성하는 것이 바람직함
- ORDER BY절이나 GROUP BY절에 자주 사용되는 열의 경우, 인덱스 생성을 고려할 수 있음

【인덱스 생성이 불필요한 경우】

- 갱신이 빈번한 테이블 열의 경우, 인덱스가 바람직하지 않음
- 집계 함수, 내장 함수를 적용하여 열 값을 변형하는 경우, 인덱스가 효과적이지 않음
-  ‘성별’ 같은 열처럼 도메인이 작아서 열의 선택도(selectivity)가 높을 경우, 인덱스가 바람직하지 않음
- 범위 검색을 하는 경우, 인덱스가 바람직하지 않음
- 테이블의 행 개수가 별로 없는 경우, 인덱스가 바람직하지 않음

# SQL 응용
## 내장함수
### 1.1 내장함수의 개요
- 내장 함수
    - 내장 함수(built-in function)와 사용자 정의 함수(user-defined function) 구분
    - 열 이름이나 상수 값을 입력받아 값 하나를 결과로 반환
    -  기본 연산 함수와 시스템 정보 제공 함수, 데이터 가공 함수 등이 지원
    - SELECT절이나 WHERE절 뿐만 아니라 UPDATE SET절 등에서도 사용 가능
    - ABS(), CEIL(), FLOOR(), ROUND(), FORMAT() 등

### 1.2 내장함수의 적용
```
SELECT ABS(+17), CEIL(3.28), FLOOR(4.25);
```
```
SELECT LENGTH(소속학과), RIGHT(학번,2) FROM 학생;
```
```
SELECT 신청날짜, LAST_DAY(신청날짜) FROM 수강
WHERE YEAR(신청날짜) = '2019';
```

## 2. 저장 프로시저
### 2.1 저장 프로시저(store procedure)
- 미리 작성하여 데이터베이스 안에 저장한 SQL 문장들의 묶음
- 독립된 프로그램으로 데이터베이스 안에 하나의 객체로 저장
- 장점: 최적화된 SQL문을 미리 데이터베이스에 작성해둘 수 있고 복잡한 SQL문을 전달할 필요가 없어 네트워크 부하가 줄어들며 여러 응용 프로그램간의 공유가 가능함

- CREATE -- 저장 프로시저 생성
```
CREATE PROCEDURE 프로시저이름
BEGIN
    ...
    SQL 명령문;
    ...
END
```

### 2.2 삽입, 수정 저장 프로시저 생성
```

```