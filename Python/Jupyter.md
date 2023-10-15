# 01. Jupyter Intro
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
- range(n, m) : n부터 m-1까지 범위
- range(n, m, s) : n부터 m-1까지 범위, +s만큼 증가하는 범위

## 4.4 string

## 4.5 시퀀스에서 사용가능한 연산/함수

- indexing
- slicing 
- not in
- concatenation
- *

## 5.0 시퀀스 데이터가 아닌 자료구조

- set
- dictionary


## 5.1 set
- 수학에서 사용하는 집합과 동일하게 처리(중복된 값이 없음)
- 선언 : 변수이름 = {value1, value2, value3}

## 5.3 dictionary
- 선언 : 변수이름 = {key1: value1, key2: value2, key3: value3}

## 데이터 타입
1. Number
2. Boolean
3. String

## 자료구조
- 시퀀스 자료향
    1. [List] : mutable
    2. (Tuple) : immutable
    3. range() : immutable
    4. 'String' : immutable

- 시퀀스가 아닌 자료형
    1. {Set} : mutable
    2. {Dict: ionary} : mutable

# 02 Control of flow
## 제어문
- 조건문(if문)
```
if <조건식>:
    조건식이 참인 경우 실행하는 코드
elif <조건식>:
    elif조건식이 참인 경우 실행하는 코드
else:
    거짓인 경우 실행하는 코드
```

- 조건표현식
```
ture_value if <조건식> else false_value
```

## 반복문
- while문
```
while <조건식>:
    실행할 코드
```
- for
```
for variable in sequence:
    실행할 코드
```
- dictionary 반복
1. for key in dict:
2. for key in dict.keys():
3. for value in dict.values():
4. for key, value in dict.items():

- break 반복문 종료
```
for i in range(100):
    print(i)
    if i > 10:
        print('10넘었어!!')
        break
```
- continue
    - continue 이후의 코드를 실행하지 않고 다음 반복을 실행
    ```
    for i in range(10):
    if i % 2:
        continue

    print(i)
    ```
- else 
    - 끝까지 반복이 진행이 된 경우, 실행. break를 만나지 않은 경우.
- pass
- match
```
match value:
    case 조건:
        실행할 코드
    case 조건:
        실행할 코드
    case __: #다운슬라이스 두 개
        실행할 코드
```

# 03 함수(Function)
## 함수의 선언과 호출
- 함수의 선언
```
def func_name(parameter1, parameter2):
    code1
    code2
    ...
    return value
```
- 함수의 호출(실행)
```
function_name(parameter1, parameter2)
```

## 함수의 return
- 함수가 return을 만나면 해당 값을 반환하고 함수를 종료
- 만약 return이 없다면 none을 자동으로 반환
- return은 오직 하나의 객체만 반환합니다.

## 함수의 인수
- 위치인수
    - 인수의 위치로 무슨 값을 대입하는 지 확인한다.
```
def cylinder(r, h):
    return 3.14 * r**2 * h
```
```
print(cylinder(10, 5))
print(cylinder(5, 10))
```
- 기본값 지정
```
def greeting(name='익명'): 
    return f'{name}님 안녕하세요!!'
```
- 키워드 인자
- 가변 인자 리스트
- 정의되지 않은 키워드 인지 처리하기
- dict를 인자로 넣기(unpacking)
- lambda 표현식
```
(lambda x, y: x + y)(1, 2) #3
```
- 타입힌트
    -  #타입힌트는 사람이 코드를 이해하기 위함, 변수 값 강제하는 성질 없음
```
def my_sum(a: int, b: int) -> int:
    return a + b
```
```
my_sum('1', 2) #Error
```
- 이름공간 scope
    - Local scope : 정의된 함수 내부
    - Enclosed scope : 상위 함수
    - Global scope : 함수 밖의 변수 혹은 import된 모듈
    - Built-in scope : python이 기본적으로 가지고 있는 함수 혹은 변수

- 재귀 recursive
    - 재귀 함수는 함수 내부에서 자기 자신을 호출하는 함수를 의미
```
# 팩토리얼(n! = 1 * 2 * 3 * ... * n)
def fact(n):
    result = 1

    while n > 1:
        result = result * n
        # result *= n

        n = n - 1
        # n -= 1

    return result    
```

- 피보나치 수열
    - F(0) = F(1) = 1
    - F(N) = F(N-1) + F(N-2)

# 04. Datastructure
## 문자열 메소드
```
a = 'hello my name is alisha'

a.capitalize() #첫 글자를 대문자로
a.title() #모든 단어의 시작글자를 대문자로
a.upper() #모두 대문자로
a.lower() #모두 소문자로

```
- `join()`는 징검다리처럼 연결해준다. #'hi??my??name'
```
my_list = ['hi', 'my', 'name']
'??'.join(my_list)
```

- `.strip([chars])`는 소괄호 안의 문자를 제거하고 출력해준다.
```
# .strip([chars])

my_string = '   hello\n   '
print(my_string) #공백 포함 출력
print(my_string.strip()) #공백 제거 출력

my_string2 = 'hihihellohihi'
print(my_string2.strip('hi'))
print(my_string2.lstrip('hi')) #왼쪽 문자 제거 출력
print(my_string2.rstrip('hi')) #오른쪽 문자 제거 출력
```

- `.replace(old, new, [count])`
```
a = 'wooooow'
a.replace('o', '!', 3) #'w!!!oow'
```

- `.find(x)`
```
a = 'apple'
print(a.find('p')) #1
print(a.find('z')) #없는 경우 -1출력
```

- `.index()`
```
a = 'apple'
print(a.index('a')) #a가 어느 자리에 있는지를 출력 #0
print(a.index('z')) #Error
```

- `.split()`
```
a = 'my_name_is'
a.split('_')
```

- `.count(x)`
```
'woooooooooooow'.count('w') #2
```

## 리스트 메소드
- `.append(x)`
```
numbers = [1, 5, 2, 6, 2, 1]
numbers.append(10)
print(numbers) #[1, 5, 2, 6, 2, 1, 10]
```

- `.extend(iterable)`
```
a = [99, 100]

numbers.extend(a)
print(numbers) #[1, 5, 2, 6, 2, 1, 10, 99, 100]
print(numbers + a) #[1, 5, 2, 6, 2, 1, 10, 99, 100, 99, 100]
```

- `.insert(idx, x)`
```
numbers.insert(3, 3.5)
print(numbers)
#[1, 5, 2, 3.5, 6, 2, 1, 10, 99, 100]
```

- `.remove(x)`
```
numbers.remove(3.5)
print(numbers)
```

- `.pop(x)`
```
numbers.pop() #제일 뒤 데이터 삭제
print(numbers)

numbers.pop(0) #0번자리 데이터 삭제
print(numbers)
```
```
num = numbers.pop()
print(num) #삭제될 마지막 문자 출력
```

- `.sort()`
```
numbers = [1, 6, 2, 1, 3, 2, 7, 10]
print(numbers)

print(numbers.sort()) #리스트 자체 변경 A -> A

print(numbers)
numbers.sort(reverse=True)
print(numbers)
```
- `sorted()`
```
numbers = [1, 6, 2, 1, 3, 2, 7, 10]
print(sorted(numbers)) #새로운 리스트 반환 A -> B
# [1, 1, 2, 2, 3, 6, 7, 10]
print(numbers)
# [1, 6, 2, 1, 3, 2, 7, 10]
```

- `.reverse()`
```
numbers = [1, 6, 2, 1, 3, 2, 7, 10]
numbers.reverse()
print(numbers) # 거꾸로 출력
numbers = numbers[  :  : -1 ] # 슬라이싱, 전부 거꾸로 출력 
print(numbers)

```

## list copy
- `.deepcopy()`
    - b = a[:]를 사용해서 lsit를 원소로 가진 list를 copy하면 copy인 b의 원소를 바꾸고 싶을 때 a도 바뀌는 문제가 생긴다. 이런 경우, `.deepcopy()`를 써서 해결 가능하다.
```
import copy
a = [1, 2, [99, 100]]
b = copy.deepcopy(a) #list안에 list있는 경우의 복제

b[2][1] = 1000

print(a) #[1, 2, [99, 100]]
print(b) #[1, 2, [99, 1000]]
```

## list comprehension
```
numbers = list(range(1, 11))
even_list2 = [ number for number in numbers if number % 2 == 0]
print(even_list2)
```

## 딕셔너리 메소드
- `.pop(key[, default]) `
```
info = {
    'name': 'Alisha',
    'location': 'Incheon',
}

print(info)
print(info.pop('location'))

print(info)
print(info.pop('location', None))
```

- `.update()`
```
info.update(name='park')
print(info)
```

- `.get(key[, default])`
```
print(info.get('name'))
print(info.get('phone'))
print(info.get('phone', '해당키가 없습니다.'))
```

## dict comprehension
- for
- comp

## 세트 메소드
- `.add(x)`
- `.update({set})`
- `.remove(x)`
- `.pop()`

## map, filter, zip
- map
```
a = '1 3 5 7 9'
# numbers = [1, 3, 5, 7, 9]
numbers = list(map(int, a.split()))
print(numbers)
```
- filter(function, iterable)
    - filter에 들어가는 function은 T/F 를 반환
```
def is_odd(x):
    return bool(x%2)
    
print(is_odd(5)) #True
print(is_odd(10)) #False

numbers = [1, 2, 3, 4, 5]
result2 = filter(is_odd, numbers)
print(list(result2))

```
- zip
```
a = [1, 2, 3, 4]
b = [100, 200, 300, 400, 500]

result = zip(a, b)
print(result)
print(list(result))
```