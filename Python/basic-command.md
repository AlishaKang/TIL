## Python 규칙들
1. 대소문자를 구분한다.
2. git add. != git add .
3. message != massage 타이핑 오류 조심하기

## 변수, Variable
1. 숫자
dust = 10
2. 글자(string)
dust = '5'
3. 참/거짓(boolean)
dust = True # False

## 한 줄 전체 주석처리
`ctrl + /`

## list와 dict
- list
    - 0번부터 시작해서 출력값은 50이 나온다.
```
dust_list = [10, 20, 0 ,50, 100]
print(dust_[3])
```
- dict
    - dictionary의 줄임말이다. 출력값은 50.
```
dust_dict = {
    '서울': 100,
    '대전': 10,
    '부산': 50,
}
print(dust_dict['부산'])
```

## 조건문
```
age = 10

if age > 20:
    print('성인입니다.')
elif age > 8:
    print('청소년입니다.')
else: 
    print('어린이입니다.')
```
```
dust = 30

if dust >= 150:
    print('매우나쁨')
elif 80 <= dust < 150:
    print('좋음')
elif 30 <= dust < 80:
    print('보통')
else:
    print('좋음')
```

## 반복
```
menus = ['짬뽕', '곱창', '마라탕', '도넛']

n = 0
while n < 4:
    print(menus[n])
    n = n + 1
```
- for item in list
```
menus = ['짬뽕', '곱창', '마라탕', '도넛']
for menu in menus:
    print(menu)
```
- 두 예제 전부 모든 메뉴들을 출력해 보여준다.

## 리스트에서 최댓값 max()
```
numbers = [1, 2, 3, 4, 5]
max_num = max(numbers)
print(max_num)

```

## 무작위의 정수
```
import random
random_number = random.randint(1, 100)
print(random_number)
```
- key = value
- randint는 randomint의 줄임말
```
menus = ['김밥', '라면', '만두']
random_number = random.randint(0,2)
print(menus[random_number])
```
- 랜덤하게 한 메뉴를 출력해준다.
```
menus = ['김밥', '라면', '만두']
menu = random.choice(menus)
print(menu)
```

## 무작위의 정수 
- random.randint를 사용하면 중복된 숫자가 나올 수도 있지만 random.sample을 사용하면 비복원 숫자 즉, 중복없는 숫자 선택을 할 수 있다. 이를 통해서 로또 번호 추천기를 만들 수 있다.
```
numbers = range(1,46) #1이상 46미만
lucky_number = random.sample(numbers, 6)
print(lucky_number)
```
- 위의 예제 출력값을 오름차순 정렬을 하고 싶다면 `sorted()`를 사용해 마지막 줄을 `print(sorted(lucky_number))`로 바꿔주면 된다.

## 로또 날짜와 정보 가져오기

```
URL = 'https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=1086'

import requests

res = requests.get(URL)

#data = res.text #문자
data = res.json() #자료형

drwtNo1 = data['drwtNo1']
drwtNo2 = data['drwtNo2']
drwtNo3 = data['drwtNo3']
drwtNo4 = data['drwtNo4']
drwtNo5 = data['drwtNo5']
drwtNo6 = data['drwtNo6']

print(data['drwNoDate']) #로또 날짜

lotto_number = [drwtNo1, drwtNo2, drwtNo3, drwtNo4, drwtNo5, drwtNo6]
print(lotto_number)
```
- 내가 만들어낸 로또 추천 숫자와 교집합을 알고 싶은 경우
```
print(set(lucky_number) & set(lotto_number))
```
- 교집합이 없는 경우, set()을 출력한다.