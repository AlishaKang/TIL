# 01 Pandas
- 어떤 언어로도 사용할 수 있는 가장 **강력하고 유연한 오픈 소스 데이터 분석 / 조직 도구**

## Series : Pandas의 1차원 배열
- 데이터를 담는 **차원 배열 구조**를 가집니다.
- **인덱스(index)를 사용 가능**합니다.
- **데이터 타입**을 가집니다. (dtype)

dtype을 지정한 경우
```
arr = np.arange(100, 105)
s = pd.Series(arr, dtype='int32')
```
list로 생성한 경우
```
s = pd.Series(['부장', '차장', '대리', '사원', '인턴'])
s
```
다양한 타입의 데이터가 섞인 경우, `object`타입으로 생성된다.
```
s = pd.Series([91, 2.5, '스포츠', 4, 5.16])
s
```
index붙이기
```
s = pd.Series(['부장', '차장', '대리', '사원', '인턴'])
s.index
s[0]
```
출력값은 '부장'이 나오게 된다. RangeIndex는 start=0 ~ stop=5 까지의 범위를 가져 음수 색인이 불가능하다. ex) s[-1] #Error

`RangeIndex`의 사용자 정의 `index`지정
```
s = pd.Series(['마케팅', '경영', '개발', '기획', '인사'], index=['a', 'b', 'c', 'd', 'e'])
s
```
위의 경우, 인덱스를 배열로 넣어서 음수 색인이 가능해진다. ex) s[-1] #인사
index를 붙이는 또다른 방법
```
s = pd.Series(['마케팅', '경영', '개발', '기획', '인사'])
s.index = list('abcde')
```
```
s.values #numpy array형식으로 value 가져옴
s.ndim #Series는 1차원 자료구조, 1 출력
s.shape #데이터의 모양, Series에서 데이터의 갯수 표시 (5, )
```
## NaN (Not a Number)
- 비어있는 결측치 데이터를 의미, 대입할 때는 np.nam으로 입력
```
s = pd.Series(['선화', '강호', np.nan, '소정', '우영'])
s
```
## Fancy indexing
```
s = pd.Series(['손흥민', '김연아', '박세리', '박찬호', '김연경'], index=['a', 'b', 'c', 'd', 'e'])
s[['a','c']]
```
## Boolean indexing
```
s[[True, True, False, False, True]] #True만 출력
```

## 결측값 찾는 함수 isnull(), isna()
```
s.isnull()
```
## 결측값이 아닌 것을 찾는 함수 notnull(), notna()
```
s.notnull()
```

## slicing
- 숫자형 index로 접근할 때는 뒷 index가 포함되지 않습니다. 새롭게 지정한 인덱스는 시작 index와 끝 index **모두 포함**합니다.
```
s[1:3] #1과 2출력
```
```
s['b':'c'] #b와 c출력
```

## DataFrame
`pd.DataFrame`

- 2차원 데이터 구조 (Excel 데이터 시트를 생각하시면 됩니다)
- 행(row), 열(column)으로 구성되어 있습니다.
- 각 열(column)은 각각의 데이터 타입 (dtype)을 가집니다.
```
pd.DataFrame([[1, 2, 3], 
              [4, 5, 6], 
              [7, 8, 9]], columns=['가', '나', '다'])
```
dict를 통한 생성 가능
```
data = {
    'name': ['Kim', 'Lee', 'Park'], 
    'age': [24, 27, 34], 
    'children': [2, 1, 3]
}
pd.DataFrame(data)
```
## T를 통해 DataFrame을 전치 가능
```
df.T #가로세로축 전환
```
## index붙이기
```
df.index = list('abc')
df
```

## 컬럼명 변경
```
df.rename(columns={'name': '이름'})
```
```
df.rename({'name': '이름'}, axis=1)
df = df.rename({'a': 'z'}, axis=0)
df
```
```
df.rename(columns={'name': '이름'}, inplace=True)
df
```

# 02 파일입출력
- Excel 데이터를 바로 읽어들일 수 있으며, `sheet_name`을 지정하면 해당 sheet를 가져옵니다.

[참고] `pd.read_excel()`로 엑셀 데이터 로드시 에러 발생한다면 `engine='openpyxl'`을 추가
```
excel = pd.read_excel('data/seoul_transportation.xlsx', sheet_name='철도', engine='openpyxl')
```
모든 시트를 가져오고 싶은 경우, `sheet_name`을 None으로 지정
```
excel = pd.read_excel('data/seoul_transportation.xlsx', sheet_name=None, engine='openpyxl')
excel
```
`keys()`로 **시트명을 조회**할 수 있습니다.
```
excel.keys() #dict_keys(['철도', '버스'])
```

## Excel로 저장하기
DataFrame을 Excel로 저장할 수 있으며, Excel로 저장시 **파일명**을 지정합니다.

- `index=False` 옵션은 가급적 꼭 지정하는 옵션입니다. 지정을 안하면 **index가 별도의 컬럼으로 저장**되게 됩니다.
- `sheet_name`을 지정하여, 저장할 시트의 이름을 변경할 수 있습니다.
```
excel.to_excel('sample1.xlsx', index=False, sheet_name='샘플')
```
- 여러 개의 시트에 저장하는 경우 `ExcelWriter`사용
```
writer = pd.ExcelWriter('sample2.xlsx')
excel.to_excel(writer, index=False, sheet_name='샘플1')
excel.to_excel(writer, index=False, sheet_name='샘플2')
excel.to_excel(writer, index=False, sheet_name='샘플3')
writer.close()
```

## CSV (Comma Separated Values)
- 한 줄이 한 개의 행에 해당하며, 열 사이에는 **쉼표(,)를 넣어 구분**합니다.
- Excel보다는 훨씬 가볍고 **차지하는 용량이 적기 때문에 대부분의 파일데이터는 csv 형태**로 제공됩니다.
```
df = pd.read_csv('data/seoul_population.csv')
```
파일이 큰 경우, `chunksize`를 통해서 끊어 불러오기 가능
```
df = pd.read_csv('data/seoul_population.csv', chunksize=10)
df
```
```
for d in df:
    display(d) #10개씩 출력
```
- CSV 저장하기 `pd.to_csv()`
```
df = pd.read_csv('data/seoul_population.csv')
df.to_csv('sample.csv', index=False)
```
- excel파일을 CSV로 저장하기
```
excel = pd.read_excel('data/seoul_transportation.xlsx', sheet_name='버스', engine='openpyxl')
excel.to_csv('data/sample3.csv', index=False)
```

# 03 조회
```
df.head() #위에서부터 5행 출력
df.tail() #밑에서부터 5행출력
```
## info()
- 컬럼별 정보(information)를 보여줍니다.
- 데이터의 갯수, 그리고 데이터 타입(dtype)을 확인할 때 사용합니다. 데이터 타입 중에서 object는 문자열, category는 문자열이면서 '남/여'처럼 카테고리화 할 수 있는 컬럼을 의미.
```
df.info()
```

## describe()
- 각 컬럼에 대한 요약 통계 제공
- 수치형 컬럼 (numerical column)의 통계를 기본으로 보여 줍니다.
```
df.describe()
```
categorical column (문자열 컬럼)에 적용하려는 경우, `include='object`적용하기
```
df.describe(include='object')
```

## value_counts
column안 데이터 분포를 확인
```
df['who'].value_counts() #man, woman, child의 이름과 수량이 나옴
```

## 속성: Attributes

속성 값은 **함수형으로 조회하지 않습니다.**

자주 활용하는 DataFrame은 **속성 값**들은 다음과 같습니다.

- df.ndim #2
- df.shape #(891, 15) #(행,열의 수)
- df.index #기본설정인 RangeIndex출력
- df.columns #열의 이름들 출력
- df.values #모든 값을 **numpy array 형식으로 출력**
- df.T #전치

## 타입 변환 (astype)
```
df['pclass'].astype('int32').head()
```
```
df['pclass'].astype('float32').head()
```
```
df['pclass'].astype('str').head()
```
`category`로 변경시에는 Categories가 같이 출력 됩니다.
```
df['pclass'].astype('category').head()
```
## 정렬 (sort)
### sort_index: index 정렬

- index 기준으로 정렬합니다. (기본 오름차순이 적용되어 있습니다.)
- 내림차순 정렬을 적용하려면, `ascending=False`를 옵션 값으로 설정합니다.
```
df.sort_index(ascending=False).head(5)
```

### sort_values: 값에 대한 정렬

- 값을 기준으로 행을 정렬합니다.
- by에 기준이 되는 행을 설정합니다.
- by에 2개 이상의 컬럼을 지정하여 정렬할 수 있습니다.
- 오름차순/내림차순을 컬럼 별로 지정할 수 있습니다.
```
df.sort_values(by='age').head()
```
```
df.sort_values(by='age', ascending=False).head() #내림차순
```
**문자열 컬럼도 오름차순/내림차순 정렬 가능**, 알파벳 순서 정렬
```
df.sort_values(by='class', ascending=False).head()
```
2개 이상의 컬럼을 기준으로 값을 정렬하는 경우
```
df.sort_values(by=['fare', 'age']).head()
```
```
df.sort_values(by=['fare', 'age'], ascending=[False, True]).head()
```

## Indexing, Slicing, 조건 필터링