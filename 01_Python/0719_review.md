# PYTHON 01. Data Model & Statements

> CHECK POINT✨
>
> ​	✔️ Basic grammar
>
> ​	✔️ Variables and Data model



## 1. Python Identifiers

An identifier is a user-defined name to represent the basic building blocks of Python. It can be a **variable**, a **function**, a **class**, a **module**, or any other object.



### Naming Rules for Identifiers

- Identifiers are made with a combination of letters in lowercase **(a to z)** or uppercase **(A to Z)**, digits **(0 to 9)** or an underscore ` _ `.

- An identifier cannot start with a digit.

- Cannot use special symbols like (!, @, #, $, %, .) in identifiers.

- A keyword cannot be used as an identifier. In Python, keywords are the reserved names that are built-in in Python.

  ```
  False			await			else			import			pass
  None			break			except			in			raise
  True			class			finally			is			return
  and			continue			for			lambda			try
  as			def			from			nonlocal			while
  assert			del			global			not			with
  async			elif			if			or			yield
  ```

- The length of the identifiers can be as long as you want.

  

### Best Practices for Python Identifiers

Python gives you few more guidelines that are not compulsory but which makes everyone to understand things better.

> PEP8 →  https://www.python.org/dev/peps/pep-0008/
>
> Google Style Guide → https://google.github.io/styleguide/pyguide.html



## 2. Floating Point Arithmetic

Unfortunately, most decimal values do not have an exact representation. Actually we can enter only approximated values by the binary floating-point numbers which are stored in the machine. It will cause the erre likt this:

```python
>>> num1 = 0.1 * 3
>>> num2 = 0.3
>>> num1 - num2 == 0
>>> print(num1-num2)
```

```jupyter notebook
False
5.551115123125783e-17
```

We will go over several solutions to solve this problem.

1. Using any small number

```python
>>> abs(num1-num2) <= 1e-10
```

```
True
```

2. Machine epsilon in system

```python
>>> import sys
>>> print(abs(num1-num2)) <= sys.float_info.epsilon)
>>> print(sys.float_info.epsilon)
```

```
True
2.220446049250313e-16
```

3. Using math module

```python
>>> import math
>>> math.isclose(num1, num2)
```

```
True
```



## 3. Escape Sequence(1)

- Enter (New Line)  : \n

```python
>>> print('Everything I need is \non the ground')
```

```
Everything I need is 
on the ground
```

- Tab : \t

```python
>>> print('Rosé\tOn The Ground')
```

```
Rosé    On The Ground
```

- Back Slash : \\\

```python
>>> print('Her name is \'Rosé\' from BlackPink')
```

```
Her name is 'Rosé' from BlackPink
```



## 4. String Interpolation

- %-formatting

```python
>>> name = 'Rosé'
>>> print('Hello %s' %name)
```

```
Hello Rosé
```

- str.format()

```python
>>> name = 'Rosé'
>>> print('Hello {}'.format(name))
```

```
Hello Rosé
```

- f-strings

```python
>>> name = 'Rosé'
>>> print(f'Hello {name}')
```

```
Hello Rosé
```



## 5. Type Conversion & Type Casting

Python has two type of type conversion.

1. Implicit Type Conversion
2. Explicit Type Conversion

### Implicit Type Conversion

Python automatically converts one data to another data type. This doesn't need an user involvement.

### Explicit Type Conversion

We convert the data type of an object to required data type. This type of conversion is called type casting because we casts the type of the objects.

```python
>>> str(1)
>>> type(str(1)
```

```
str
```



```python
>>> int('30')
>>> type(int('30'))
```

```
int
```



```python
>>> int(5)
>>> type(int(5))
```

```
int
```



```python
>>> bool('50')
>>> type(bool('50'))
```

```
bool
```



Typecasting can be done by assigning the required data type function to the expression. The code below will make an error.

```python
>>> int('3.5')
```

```python
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
/var/folders/d3/r3hpdk4d5zn58pvyxndjnhjw0000gn/T/ipykernel_8011/509476775.py in <module>
----> 1 int('3.5')

ValueError: invalid literal for int() with base 10: '3.5'
```



## 6. Making Rectangle

```python
>>> n, m = 5, 9
>>> print(('*'*n +'\n') *m) 
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



## 7. Escape Sequence(2)

```python
print("""
\"파일은 c:\\Windows\\Users\\내문서\\Python에 저장이 되었습니다.\"
나는 생각했다. \'cd를 써서 git bash로 들어가 봐야지\'
""")
```

```
"파일은 c:\Windows\Users\내문서\Python에 저장이 되었습니다."
나는 생각했다. 'cd를 써서 git bash로 들어가 봐야지'
```



## 8. Quadratic Formula

```python
import cmath
a = float(input('a: '))
b = float(input('b: '))
c = float(input('c: '))

sol_1 = (-b-cmath.sqrt((b**2)-(4*a*c)))/(2*a)
sol_2 = (-b+cmath.sqrt((b**2)-(4*a*c)))/(2*a)

print(f'Solutions: {sol_1} and {sol_2}')
```

```
a: 2
b: 7
c: 6
Solutions: (-2+0j) and (-1.5+0j)
```

