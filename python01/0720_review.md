# PYTHON 02. Data Model & Statements

> Check Point✨
>
> ​	✔️ Data model & Type conversion
>
> ​	✔️ Compound Statements



## 1. Mutable & Immutable

- Mutable

```
Dictionary		List		Set
```

- Immutable

```
String		Tuple		Range
```



## 2. 홀수만 담기

```python
numbers = list(range(1,51))
print(numbers[::2])
```

```
[1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35, 37, 39, 41, 43, 45, 47, 49]
```



## 3. Dictionary 만들기

```python
class_info = {
    '강민구' : '92',
    '김상훈' : '95',
    '김선민' : '97',
    '김승규' : '94',
    '김은송' : '96',
    '연승은' : '95'
}
```



## 4. 반복문으로 네모 출력

두 개의 정수 n과 m이 주어졌을 때, 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 별(*) 문자를 이용하여 출력하시오. 단, 반복문을 사용하여 작성하시오.

```python
for i in range(m):
    for j in  range(n):
        print('*', end='')
    print()
```

```
*****
*****
*****
*****
*****
*****
*****
*****
*****
```



## 5. 조건 표현식

```python
temp = 36.5
if temp >= 37.5:
  print('입실 불가')
else:
  print('입실 가능')
```

```python
temp = 36.5
print('입실 불가') if temp >= 37.5 else print('입실 가능')
```

```
입실 가능
```



## 6. 평균 구하기

```python
score = [80, 90, 99, 83]

total = sum(score)
n = len(score)

avg = total/n
print(avg)
```

```
88.0
```

