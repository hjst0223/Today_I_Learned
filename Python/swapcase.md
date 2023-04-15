# 🎨 대소문자 다루기
### swapcase() : 대문자->소문자, 소문자->대문자
```python
>>> 'viel Spaß!'.swapcase()
'VIEL sPASS!'
>>> 'HeLlo wORld!'.swapcase()
'hElLO WorLD!'
````

### capitalize() : 문자열의 맨 앞 문자만 대문자 변환
```python
>>> 'viel Spaß!'.capitalize()
'Viel spaß!'
>>> 'HeLlo WORld!'.capitalize()
'Hello world!'
```

### title() : 문자열 내 각 단어의 첫 문자만 대문자 변환
```python
>>> 'viel Spaß!'.title()
'Viel Spaß!'
>>> 'HeLlo wORld!'.title()
'Hello World!'
```

### casefold() : 소문자로 변환 + 유니코드가 아닌 문자열도 변환
```python
>>> 'viel Spaß!'.casefold()
'viel spass!'
>>> 'HeLlo wORld!'.casefold()
'hello world!'
```
