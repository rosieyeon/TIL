# Python 03. 함수

> Background
>
> ​	✔️ 함수
>
> ​	✔️ 매개변수와 인자



> Goal
>
> ​	✔️ 함수의 선언과 호출에 대한 이해
>
> ​	✔️ 함수의 반환에 대한 이해



## 1. List의 합 구하기

```python
def list_sum(nums_list):
    total = 0
    for nums in nums_list:
        total += nums
    return total
```

```python
>>> list_sum([1, 2, 3, 4, 5])
15
```



## 2. Dictionary로 이루어진 List의 합 구하기

```python
def dict_list_sum(list_info):
    total = 0
    for dic in list_info:
        total += dic['age']
    return total
```

```python
>>> dict_list_sum([{'name': 'kim', 'age': 12}, 
                   {'name': 'lee', 'age': 4}])
16
```



## 3. 2차원 List의 전체 합 구하기

```python
def all_list_sum(lists_in_list):
    total = 0
    for lists in lists_in_list:
        for nums in lists:
            total += nums
    return total
```

```python
>>> all_list_sum([[1], [2,3], [4,5,6], [7,8,9,10]])
55
```

