# 📐 숫자 판별 - isdigit(), isnumeric(), isdecimal() 
- isdecimal( ) ⊆ isdigit( ) ⊆ isnumeric( )
## isdigit() : '-'. '.' 포함 실수/음수 판별 불가
```python
>>> 'abc'.isdigit()
False
>>> 'abc123'.isdigit()
False
>>> '123'.isdigit()
True
>>> '-123'.isdigit()
False
>>> '1.23'.isdigit()
False
>>> '3²'.isdigit()
True
>>> '⅔'.isdigit()
False
>>> '0123'.isdigit()
True
```

## isnumeric() : '-'. '.' 포함 실수/음수 판별 불가, 분수 판별 가능
```python
>>> 'abc'.isnumeric()
False
>>> 'abc123'.isnumeric()
False
>>> '123'.isnumeric()
True
>>> '-123'.isnumeric()
False
>>> '1.23'.isnumeric()
False
>>> '3²'.isnumeric()
True
>>> '⅔'.isnumeric()
True
>>> '0123'.isnumeric()
True
```

## isdecimal() : int 타입으로 변환 가능할 경우 True
```python
>>> 'abc'.isdecimal()
False
>>> 'abc123'.isdecimal()
False
>>> '123'.isdecimal()
True
>>> '-123'.isdecimal()
False
>>> '1.23'.isdecimal()
False
>>> '3²'.isdecimal()
False
>>> '⅔'.isdecimal()
False
>>> '0123'.isdecimal()
True
```

# 📘 알파벳 판별
## isalpha()
```python
>>> 'abc'.isalpha()
True
>>> 'abc123'.isalpha()
False
>>> '123'.isalpha()
False
>>> '12 3'.isalpha()
False
```

# 📚 숫자 + 알파벳 판별
## isalnum() : 문자열이 숫자나 알파벳으로만 구성되어있으면 True, 공백이 있으면 False
```python
>>> 'abc'.isalnum()
True
>>> 'abc123'.isalnum()
True
>>> '123'.isalnum()
True
>>> 'a bc'.isalnum()
False
>>> '-123'.isalnum()
False
```
