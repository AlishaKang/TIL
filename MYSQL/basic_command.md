# MYSQL 
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
