# 🙄 변수의 정수 여부 확인하기
## is_integer()로 실수의 정수 여부 확인
```python
>>> (-2.0).is_integer()
True
>>> (3.2).is_integer()
False
```

## isinstance(object, classinfo)
```python
>>> x = 5
>>> isinstance(x, int)
True
>>> isinstance(x, float)
False
```
