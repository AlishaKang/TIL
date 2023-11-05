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
- indexing과 slicing을 할 수 있습니다.
- slicing은 [**시작(포함)**: **끝(포함)**] 규칙에 유의합니다. 둘 다 포함 합니다.
```
# df.loc[행인덱스, 열인덱스]
df.loc[5, 'class']
```
```
df.loc[2:5, ['age', 'fare', 'who']]
```
```
df.loc[2:5, 'class':'deck'].head()
```
```
df.loc[:6, 'class':'deck']
```

### loc - 조건필터
- boolean index를 만들어 조건에 맞는 데이터만 추출해 낼 수 있습니다.
```
condition = df['who'] == 'man'
condition
```
조건에 맞는 데이터만 추출하기 위한 두 가지 방법
```
df[condition].head()
```
```
df.loc[condition].head()
```
`loc`를 사용하는 방법이 문제가 덜 생긴다.

### loc - 다중조건
- 다중 조건은 먼저 condition을 정의하고 &와 |연산자로 복합 조건을 생성합니다.
```
# 조건1 정의
condition1 = (df['fare'] > 30)

# 조건2 정의
condition2 = (df['who'] == 'woman')
```
```
df.loc[condition1 & condition2]
```
```
df.loc[condition1 | condition2]
```

## iloc
- `loc`와 유사하지만, index만 허용합니다.
- loc와 마찬가지고, indexing / slicing 모두 가능합니다.
```
df.iloc[1, 3] #df.iloc[행인덱스, 열인덱스]
```
```
df.iloc[[0, 3, 4], [0, 1, 5, 6]]
```
loc에서는 slicing을 할 때 앞 뒤 둘 다 포함하지만 iloc에서는 기존의 규칙을 따른다.
```
df.iloc[:3, :5]
```

## at
- 하나의 인덱스만 가져옵니다. `loc`보다 속도가 빠르다는 장점은 있지만, 실질적인 효용성은 떨어집니다. 그냥 `loc`를 사용해도 똑같은 결과를 얻을 수 있습니다.
```
%timeit df.loc[0, 'fare']
```
```
%timeit df.at[0, 'fare']
```

## iat
- 하나의 인덱스만 가져옵니다. 속도가 빠르다는 장점은 있지만, 1개의 데이터만 조회 가능합니다. `iloc`로 대체 사용가능합니다.
```
%timeit df.iloc[0, 5]
```
```
%timeit df.iat[0, 5]
```

## where
- [도큐먼트](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.where.html)

`DataFrame.where(cond, other=nan, inplace=False, axis=None, level=None, errors='raise', try_cast=False)`

Pandas의 `where`는 Numpy의 `where`와 동작이 다릅니다.

- cond: True/False로 판단될 수 있는 식
- other: condition을 만족하지 못하는 요소에 할당 할 값
```
df['fare'].where(df['fare'] < 20, 0).tail(10)
```
이렇게 하면 fare행만 fare가 20 미만인 것들의 값과 아닌 행들은 0으로 바뀌어 나온다.
전체 DataFrame에 적용 시 다음과 같이 조건이 해당하는 값 외에는 모두 NaN로 채워지게 된다.
```
df.where(df['fare'] < 10)
```

## isin()
- 특정 값의 포함 여부는 isin 함수를 통해 비교가 가능합니다. (파이썬의 in 키워드는 사용 불가 합니다.) True와 False를 통해서 결과를 알려준다.
```
sample = pd.DataFrame({'name': ['kim', 'lee', 'park', 'choi'], 
                        'age': [24, 27, 34, 19]
                      })
sample
```
```
sample['name'].isin(['kim', 'lee'])
```
```
sample.isin(['kim', 'lee'])
```
```
condition = sample['name'].isin(['kim', 'lee'])
sample.loc[condition]
```

# 04 모듈 import
## describe() - 요약통계
전반적인 주요 통계를 확인할 수 있습니다.

기본 값으로 **수치형(Numerical) 컬럼**에 대한 통계표를 보여줍니다.
- **count**: 데이터 개수
- **mean**: 평균
- **std**: 표준편차
- **min**: 최솟값
- **max**: 최대값
```
df.describe()
```
**문자열 컬럼에 대한 통계표**도 확인할 수 있습니다.

- **count**: 데이터 개수
- **unique**: 고유 데이터의 값 개수
- **top**: 가장 많이 출현한 데이터 개수
- **freq**: 가장 많이 출현한 데이터의 빈도수
```
df.describe(include='object')
```

## count() - 개수
```
df.count()
```
```
df['age'].count()
```

## mean() - 평균
```
df.mean(numeric_only=True)
```
```
df['age'].mean()
```
```
condition = (df['adult_male'] == True)
df.loc[condition, 'age'].mean()
```

## `skipna=True` 옵션
기술 통계 함수에서는 `skipna=True`가 **기본으로 설정** 되어 있습니다.

만약, `skipna=False`로 설정하게 된다면, **NaN 값이 있는 column은 NaN 값으로 출력** 됩니다.
```
df.mean(skipna=False, numeric_only=True)
```
```
df.mean(skipna=True, numeric_only=True)
```

## median() - 중앙값
데이터의 중앙 값을 출력 합니다. 데이터를 **오름차순 정렬하여 중앙에 위치한 값**입니다.

이상치(outlier)가 존재하는 경우, `mean()`보다 `median()`을 대표값으로 더 **선호**합니다.
```
pd.Series([4, 5, 1, 2, 3]).median() #3.0
```
**짝수**개의 데이터가 있는 경우에는 **가운데 2개 중앙 데이터의 평균 값을 출력** 합니다.
```
pd.Series([1, 2, 3, 4, 5, 6]).median()
```
나이의 평균(mean)과 중앙값(median)은 약간의 **차이가 있음**을 확인할 수 있습니다.
```
print(f"나이 평균: {df['age'].mean():.5f}\n나이 중앙값: {df['age'].median()}\n차이: {df['age'].mean() - df['age'].median():.5f}")
```

## sum() - 합계
데이터의 **합계**입니다. 문자열 column은 모든 데이터가 붙어서 출력될 수 있습니다.
```
df.sum(numeric_only=True)
```
```
df['fare'].sum()
```

## cumsum() - 누적합, cumprod() - 누적곱
```
df['age'].cumsum()
```
```
df['age'].cumprod()
```

## var() - 분산, std() - 표준편차
```
df['fare'].var()
```
표준편차 = 분산의 제곱근 
```
np.sqrt(df['fare'].var()) 
```
```
df['fare'].std()
```

## min() - 최소값, max() - 최대값
```
df['age'].min()
```
```
df['age'].max()
```

## aff() - aggregation: 통합 통계 적용 (복수의 통계 함수 적용)
```
df['age'].agg(['min', 'max', 'count', 'mean'])
```

## quantile() - 분위
**Quantile이란 주어진 데이터를 동등한 크기로 분할하는 지점**을 말합니다

10%의 경우 0.1을, 80%의 경우 0.8을 대입하여 값을 구합니다.
```
df['age'].quantile(0.8) #상위20퍼
```

## unique() - 고유값, nunique() - 고유값 개수
```
df['who'].unique()
```
```
df['who'].nunique()
```

## mode() - 최빈값
```
df['who'].mode()
```

## corr() - 상관관계
`corr()`로 컬럼(column)별 **상관관계**를 확인할 수 있습니다.

- **-1~1 사이의 범위**를 가집니다.
- **-1에 가까울 수록 반비례** 관계, **1에 가까울수록 정비례** 관계를 의미합니다.
```
df.corr(numeric_only=True)
```
특정 컬럼에 대한 상관관계를 확인할 수 있습니다.
```
df.corr(numeric_only=True)['survived']
```

# 05 복제 - 결측치
## copy()
DataFrame을 **복제**합니다. 복제한 DataFrame을 수정해도 **원본에는 영향을 미치지 않습니다.**
```
df_copy = df.copy()
```

## 결측치
결측치는 **비어있는 데이터**를 의미합니다.

결측치에 대한 처리는 매우 중요합니다. 

결측치에 대한 처리를 해주려면 **다음의 내용**을 반드시 알아야 합니다.

1. 결측 데이터 확인
2. 결측치가 **아닌** 데이터 확인
3. 결측 데이터 **채우기**
4. 결측 데이터 **제거하기**

## 결측치의 확인 - isnull(), isnan()
```
df.isnull().sum()
```
```
df.isna().sum()
```
DataFrame 전제 결측 데이터의 갯수를 합산하기 위해서는 sum()을 두번 사용하면 된다.
```
df.isna().sum().sum()
```

## 결측치가 아닌 데이터 확인 - notnull()
```
df.notnull().sum()
```

## 결측 데이터 필터링
`isnull()` 함수가 결측 데이터를 찾는 **boolean index** 입니다.

즉, `loc`에 적용하여 조건 필터링을 걸 수 있습니다.
```
df.loc[df['age'].isnull()]
```

## 결측치 채우기 - fillna()
`fillna()`를 활용하면 결측치에 대하여 **일괄적으로 값을 채울 수** 있습니다.
```
df['age'].fillna(700).tail()
```
카테고리형 데이터를 채울려고 할 때, 이미 카테고리에 추가되어 있는 데이터는 바로 추가할 수 있다.
```
df1['deck'].fillna('A')
```
하지만 카테고리 안에 없는 새로운 카테고리로 채우고자 하는 경우, `add_categories`를 사용한 후 채워야 한다.
```
df1['deck'].cat.add_categories('No Data').fillna('No Data')
```
**최빈값(mode)**으로 채울 때에는 반드시 **0번째 index 지정**하여 값을 추출한 후 채워야 합니다.
```
df1['deck'].fillna(df1['deck'].mode()[0]).tail()
```

## NaN 값이 있는 데이터 제거하기 - dropna()
`dropna()`로 **1개 라도 NaN 값이 있는 행**은 제거할 수 있습니다. (`how='any'`)
```
df1.dropna()
```
기본 옵션 값은 `how=any`로 설정되어 있으며, 다음과 같이 변경할 수 있습니다.

- **any**: 1개 라도 NaN값이 존재시 drop
- **all**: 모두 NaN값이 존재시 drop
```
df1.dropna(how='all')
```

# 06 전처리 추가, 삭제, 데이터 변환
## 새로운 컬럼 추가
```
df1['VIP'] = True
```

## 삭제
### 행(row) 삭제
행 삭제시 **index를 지정하여 삭제**합니다.
```
df.drop(1)
```
```
df1.drop(np.arange(10))
```
```
df1.drop([1, 3, 5, 7, 9])
```

### 열(column) 삭제
열 삭제시 **반드시 `axis=1` 옵션을 지정**해야 합니다. 
```
df1.drop('class', axis=1).head()
```
```
df1.drop(['who', 'deck', 'alive'], axis=1)
```
삭제된 내용을 바로 적용하려면 `inplace=True`를 지정합니다.
```
df1.drop(['who', 'deck', 'alive'], axis=1, inplace=True)
```

## 컬럼간 연산
**컬럼(column) 과 컬럼 사이의 연산을 매우 쉽게 적용**할 수 있습니다.
```
df1['family'] = df1['sibsp'] + df1['parch']
```
**문자열의 합 (이어붙히기)도 가능**합니다.
```
df1['gender'] = df1['who'] + '-' + df1['sex']
```
**round(숫자, 소수 몇 째자리)**
```
df1['round'] = round(df1['fare'] / df1['age'], 2)
```
연산시 1개의 컬럼이라도 **NaN 값을 포함하고 있다면 결과는 NaN** 이 됩니다.
```
df1.loc[df1['age'].isnull(), 'deck':].head()
```

## 타입변환 astype()
```
df1['pclass'].astype('int32').head()
```
`category`로 변경시에는 Categories가 같이 출력 됩니다.
```
df1['who'].astype('category').head()
```
타입을 `category`로 변환했다면 **.cat**으로 접근하여 category 타입이 제공하는 **attribute를 사용**할 수 있습니다.
```
df1['who'].cat.codes
```

## 카테고리 이름 변경
```
df1['who'] = df1['who'].cat.rename_categories([f'Group({g})' for g in df1['who'].cat.categories])
df1['who'].value_counts()
```

## datetime - 날짜, 시간
### date_range

주요 옵션 값
- **start**: 시작 날짜
- **end**: 끝 날짜
- **periods**: 생성할 데이터 개수
- **freq**: 주기

```
dates = pd.date_range('20210101', periods=df.shape[0], freq='15H')
<!-- dates.shape #shape는 행과 열 정보 보여줌 -->
df1['date'] = dates #새로운컬럼 date생성 후 date를 대입
df1.head()
```
### datetime 타입

`datetime` 타입에서는 **dt** 접근자로 다음과 같은 날짜 속성에 쉽게 접근할 수 있습니다.

Pandas의 **dt (datetime) 날짜 관련 변수**는 다음과 같습니다.
[도큐먼트](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DatetimeIndex.year.html)
- pandas.Series.dt.year: 연도
- pandas.Series.dt.month: 월
- pandas.Series.dt.day: 일
- pandas.Series.dt.hour: 시
- pandas.Series.dt.minute: 분
- pandas.Series.dt.second: 초
- pandas.Series.dt.microsecond: micro 초
- pandas.Series.dt.nanosecond: nano 초
- pandas.Series.dt.week: 주
- pandas.Series.dt.weekofyear: 연중 몇 째주
- pandas.Series.dt.dayofweek: 요일
- pandas.Series.dt.weekday: 요일 (dayofweek과 동일)
- pandas.Series.dt.dayofyear: 연중 몇 번째 날
- pandas.Series.dt.quarter: 분기
```
df1['date'].dt.year.head()
```

**dayofweek**는 숫자로 요일이 표기 됩니다.
- 월요일: 0, 일요일: 6

```
df1['date'].dt.dayofweek.head(10)
```

### to_datetime()
**`pd.to_datetime()`**: datetime type으로 변환합니다.
```
pd.to_datetime(df2['대여일자'])
```
컬럼에 적용하려면 재대입해야 함, 그후 `.dt`접근자를 활용해 datetime 속성에 접근할 수 있습니다.
```
df2['대여일자'] = pd.to_datetime(df2['대여일자'])
df2['대여일자'].dt.day
```

## pd.to_numeric() - 수치형 변환

object나 numerical type이 아닌 컬럼을 **수치형(numerical) 컬럼으로 변환**할 때 사용합니다.