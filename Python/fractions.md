# 🐑 fractions 모듈 사용하기
- 유리수 계산 시 사용하는 모듈
```python
>>> from fractions import Fraction
>>> a = Fraction(2, 3) # (분자, 분모)
```

## 기약분수
```python
>>> Fraction(16, -10)
Fraction(-8, 5)
```

## 문자열
```python
>>> a = Fraction('2/3')
Fraction(2, 3)
```

## 분자, 분모
```python
>>> a.numerator
2
>>> a.denominator
3
```

## 계산
```python
>>> result = Fraction(1, 5) + Fraction(2, 5)
>>> result
Fraction(3, 5)
```

## 실수로 변환
```python
>>> float(result)
0.6
```

## 십진수를 유리수로 변환
```python
>>> from decimal import Decimal
>>> Fraction(Decimal('1.1'))
Fraction(11, 10)
```

## Examples
```python
>>> Fraction('1.414213 \t\n')
Fraction(1414213, 1000000)
>>> Fraction('-.125')
Fraction(-1, 8)
>>> Fraction('7e-6')
Fraction(7, 1000000)
>>> Fraction(2.25)
Fraction(9, 4)
>>> Fraction(1.1)
Fraction(2476979795053773, 2251799813685248)
```
[참고](https://docs.python.org/ko/3/library/fractions.html)
