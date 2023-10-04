## 01. Jupyter Intro
- 단축키
    - ctrl + enter : 지금 셀 실행
    - shift + enter : 지금 셀 실행 & 아래로 이동
    - alt + enter : 지금 셀 실행 & 아래에 새로운 셀 추가

## 1.0 변수
변수 이름 = 값
- 변수 이름은 어떤이름이든 상관 없음
- 영어, 숫자, '_'를 이용하여 선언
- 키워드는 사용불가
    - False, True, None,...
```
a = 10
```
```
import keyword
keyword.kwlist
```

## 1.1 number
`type()`를 통해서 데이터 타입을 확인할 수 있다.
- 정수 int
- 실수 float
- 복소수 complex
```
a = 1000
type(a)

b = 1.1
type(b)

c = 1 - 4j
type(c)
```
- 복소수
복소수는 허수를 j로 표현한다.
`c.imag`는 허수 부분의 숫자 -4.0을 출력해준다.
`c.real`은 정수 부분의 숫자 1을 출력해준다.

## 1.2 boolean
True, False로 이루어진 데이터 타입
```
a = True
type(a)
```
`bool`이 출력되어 나온다.

## 1.3 None
데이터가 없음을 의미한다. 이는 0과는 다른 의미이다.
```
a = None
type(a)
```
`Nonetype`가 나온다.

## 1.4 String
- 문자열은 `'`,`"`을 사용해 표현
```
a = 'Hello'
type(a)
```
`str`이 출력되어 나온다. 
- 출력하고 싶은 문장에 `'`가 있는 경우
```
print("'강알리샤'입니다.")
```
```
print('\'강알리샤\'입니다.')
```
- 문장줄 바꾸기와 들여쓰기
```
a = ```
여기는 \n문자열입니다.
여러 \t줄을 작성할 수 있어요.
    ```
```
`\n`을 사용해 문장줄을 바꾸고, `\t`를 사용해 들여쓰기를 할 수 있다.

- 여러 개를 함께 입력하기
```
print('하나', '둘', '셋')
```
출력결과는 하나 둘 셋이 나온다.

- string interpolation
    - %-fomatting
    - str.format()
    - f-stirring
```
age = 10

print('%s살입니다.'% age)
print('{}살입니다.'.format(age))
print(f'{age}살입니다.')

```
위의 세 가지 출력결과는 전부 `10살입니다.`가 나온다. 하지만 가장 최근 형식은 마지막 줄 방식이다.

## 2.0 연산자
- 산술연산자
- 비교연산자
- 논리연산자
- 복합연산자
- 기타연산자

## 2.1 산술연산자
```
a = 2
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
```
```
print(a**b) #a의 b제곱
print(a // b) #나눈 몫
print(a % b) #나눈 나머지
print(divmod(a, b)) #몫과 나머지(0,2)
```

## 2.2 비교연산자
```
a = 5
b = 10

print(a > b) #False
print(a < b) #True
print(a >= b) #False
print(a <= b) #True

print(a == b) #False
print(a != b) #True

print('hi' == 'hi') #True
print('Hi' == 'hi') #False

```

## 2.3 논리연산자
- and : 양쪽 모두 True면, True
- or : 하나라도 True면, True
- not : 값을 반대로 전환

-  파이썬은 평가결과를 얻을 수 있는 충분할 정보를 얻는다면 아직 평가하지 않은 피연산자가 있어도 평가를 멈춘다. 
- 단축평가(and) 
```
print(3 and 5)
print(3 and 0)
print(0 and 5)
print(0 and 0)
```
출력값은 5 0 0 0으로 나온다.
- 단축평가(or)
```
print(3 or 5)
print(3 or 0)
print(0 or 5)
print(0 or 0)
```
출력값은 3 3 5 0으로 나온다.

## 2.4 복합연산자
하단의 식을 더 간단하게 나타낸 방식을 실무에서 더 많이 사용한다.
```
a = a + b
a = a - b
a = a * b
a = a / b
a = a // b
a = a % b
a = a ** b
```
```
a += b
a -= b
a *= b
a /= b
a //= b
a %= b
a **= b
```

## 2.5 기타연산자
- concatenation
```
a = [1, 2, 3]
b = [9, 8, 7]

a + b
```
`[1, 2, 3, 9, 8, 7]`

- containment
```
print('a' in 'apple')
print('z' in 'apple')
```
`True`와 `False`
```
print(1 in [1, 2, 3])
print(100 in [1, 2, 3])
```
`True`와 `False`
```
a = 123123
b = 123123
print(a is b)
```
True가 아닌 `False`가 나오는 이유, 미리 저장공간에 저장해놓고 불러오는데 이 공간 위치가 달라서 그렇다. 하지만 많이 쓰는 숫자의 경우는 같은 공간에서 이미 저장되어 있는 것을 불러와 `True`가 나온다.
```
a = 10
b = 10
print(a is b)
```
## 연산자 우선순위
0. ()을 통해 그룹
1. **
2. 산술연산자(*, /)
3. 산술연산자(+, -)
4. 비교연산자, is, in
5. not
6. and, or

```
print(-3 ** 4) #-81
print((-3) ** 4) #81
```
연산자 우선순위 때문에 결과값이 꼬이는 경우가 있다. 그런 경우 `()`를 넣어서 우선순위를 바로 잡아 주면 된다. 

## 3.0 형변환
- 암시적 형변환
- 명시적 형변환

## 3.1 암시적 형변환

```
a = True
b = False 
c = 1
print(a + c) #2
print(b + c) #1
```
```
int_num = 3
float_num = 3.3
complex_num = 3 + 3j
print(int_num + float_num) #6.3
print(int_num + complex_num) #6+3j
```

## 3.2 명시적 형변환
- 숫자를 문자로 바꾸고 싶은 경우, `str()`로 감싸면 된다.
```
a = 1
b = '번'
a + b #Error
print(str(a) + b) #1번
```
- 문자를 숫자로 바꾸고 싶은 경우, `int()`로 감싸면 된다.
```
a = '100'
print(type(int(a))) #int
```
- 문자를 실수로 바꾸고 싶은 경우, `float()`로 감싸면 된다.
```
a = '3.3'
type(int(a)) #float
```
```
a = 1
b = 0
c = 100
print(bool(a)) #True
print(bool(b)) #False
print(bool(c)) #True
```
```
print(bool('')) #False
print(bool('apple')) #True
print(bool([])) #False 
print(bool([1, 2, 3])) #True
```

## 4.0 시퀀스 자료형
시퀀스는 데이터의 순서대로 나열된 자료구조 (순서대로 나열되어 있다는 것은 정렬된 것과는 다르다.)

1. 리스트(list)
2. 튜플(tuple)
3. 레인지(range)
4. 문자열(string)

## 4.1 List(배열)
- 선언 : 변수이름 = [value1, value2, value3]
- 접근 : 변수이름(index)

## 4.2 Tuple
- 선언 : 변수이름 = (value1, value2, value3)
- 접근 : 변수이름(index)
- list와 유사하지만 수정불가능(immutable)하다.

## 4.3 range
- range(n) : 0부터 n-1까지 범위
- range(n, m) : n부터 n-1까지 범위
- range(n, m, s) : n부터 m-1까지 범위, +s만큼 증가하는 범위

## 4.4 string

## 4.5 시퀀스에서 사용가능한 연산/함수

- indexing
- slicing ???