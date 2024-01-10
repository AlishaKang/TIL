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
