## 1. 기본 개념
정규표현식은 패턴을 정의하여 특정한 형식을 가진 문자열을 찾는 데 사용됨

## 2. re 모듈 사용 방법
### 2.1 주요 함수
- re.match(): 문자열의 시작 부분에서 패턴과 일치하는지 확인
- re.search(): 문자열 전체에서 패턴과 일치하는 부분을 찾음
- re.findall(): 문자열에서 패턴과 일치하는 모든 부분을 리스트로 반환
- re.sub(): 패턴과 일치하는 부분을 다른 문자열로 대체
- re.split(): 패턴에 맞춰 문자열을 분리
```
import re

text = "The quick brown fox jumps over the lazy dog."

# match: 문자열의 시작에서 패턴을 찾음
result = re.match(r"The", text)
print(result)  # <re.Match object; span=(0, 3), match='The'>

# search: 문자열 전체에서 패턴을 찾음
result = re.search(r"fox", text)
print(result)  # <re.Match object; span=(16, 19), match='fox'>

# findall: 일치하는 모든 부분을 리스트로 반환
result = re.findall(r"\b\w{3}\b", text)  # 세 글자 단어 찾기
print(result)  # ['The', 'fox', 'the', 'dog']

# sub: 일치하는 부분을 다른 문자열로 대체
result = re.sub(r"lazy", "active", text)
print(result)  # "The quick brown fox jumps over the active dog."

# split: 패턴에 맞춰 문자열을 분리
result = re.split(r"\s+", text)  # 공백을 기준으로 분리
print(result)  # ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog.']

```

## 3. 정규표현식 패턴의 기초
각 패턴은 특정 조건에 맞는 문자열을 찾는 데 사용됨

### 3.1 문자 클래스
- [abc]: a, b, c 중 하나와 일치
- [\^abc\]: a, b, c를 제외한 문자와 일치
- [a-z]: 소문자 알파벳 중 하나와 일치
- [0-9]: 숫자 중 하나와 일치

```
re.findall(r"[a-z]", "abc123ABC")  # ['a', 'b', 'c']
```

### 3.2 특수 문자
- .: 임의의 문자와 일치 (개행 문자는 제외)
- \d: 숫자와 일치 (0-9)
- \D: 숫자가 아닌 문자와 일치
- \w: 문자와 일치 (알파벳 + 숫자 + _)
- \W: 문자가 아닌 것과 일치
- \s: 공백 문자와 일치 (공백, 탭, 줄바꿈)
- \S: 공백이 아닌 문자와 일치

```
re.findall(r"\d", "Phone number: 123-456-7890")  # ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0']
```

### 3.3 앵커(Anchors)
- ^: 문자열의 시작에 위치하는 패턴과 일치
- $: 문자열의 끝에 위치하는 패턴과 일치
- \b: 단어의 경계를 나타냄 (단어의 시작 또는 끝)
- \B: 단어 경계가 아닌 부분과 일치

```
re.findall(r"^The", "The quick brown fox")  # ['The']
re.findall(r"dog.$", "The lazy dog.")       # ['dog.']
```

### 3.4 반복 패턴
- \*: 0번 이상 반복 (ex: a*는 a가 0번 이상 반복)
- +: 1번 이상 반복 (ex: a+는 a가 1번 이상 반복)
- ?: 0번 또는 1번 등장 (ex: a?는 a가 0번 또는 1번 등장)
- {n}: 정확히 n번 반복 (ex: a{3}은 aaa와 일치)
- {n,}: 최소 n번 이상 반복
- {n,m}: n번에서 m번 사이의 반복

```
re.findall(r"a{2,3}", "aaaaab")  # ['aaa', 'aa'] 2-3번 반복
```

### 3.5 그룹화
- (): 그룹을 만들며, 그룹으로 묶인 부분에 대해 매칭 결과를 얻을 수 있음

```
match = re.search(r"(abc)+", "abcabcabc")
print(match.group())  # abcabcabc
```
### 3.6 선택(OR)
- |: OR 연산자처럼 사용되어, 여러 패턴 중 하나와 일치

```
re.findall(r"dog|cat", "dog and cat are animals")  # ['dog', 'cat']
```

## 4. 고급 패턴과 기능
### 4.1 비탐욕적 탐색
기본적으로 정규표현식은 탐욕적(Greedy)으로 작동하지만, 비탐욕적(Non-greedy) 탐색을 사용하면 최소한으로 일치하게 할 수 있음

- *?: 0번 이상 비탐욕적 반복
- +?: 1번 이상 비탐욕적 반복
- ??: 0번 또는 1번 비탐욕적

```
re.search(r"<.*>", "<html><body></body></html>").group()  # Greedy: <html><body></body></html>
re.search(r"<.*?>", "<html><body></body></html>").group()  # Non-greedy: <html>
```

### 4.2 전방 탐색과 후방 탐색
**전방 탐색(Lookahead)**과 **후방 탐색(Lookbehind)**은 문자열에서 특정 조건에 일치하지만, 그 조건을 결과에 포함시키지 않는 매칭 방식

- (?=...): 전방 탐색 (앞에 특정 패턴이 있는지 확인)
- (?<=...): 후방 탐색 (뒤에 특정 패턴이 있는지 확인)
- (?!...): 부정 전방 탐색 (특정 패턴이 없는지 확인)
- (?<!...): 부정 후방 탐색 (특정 패턴이 뒤에 없는지 확인)

```
# 'fox' 뒤에 'jumps'가 있는 경우에만 매칭
re.search(r"fox(?= jumps)", "The quick brown fox jumps over the lazy dog").group()  # fox

# 'jumps' 앞에 'fox'가 있는 경우에만 매칭
re.search(r"(?<=fox )jumps", "The quick brown fox jumps over the lazy dog").group()  # jumps
```

## 5. 실전 예시
### 5.1 이메일 추출

```
text = "Contact me at email@example.com or at admin@domain.org"
emails = re.findall(r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b", text)
print(emails)  # ['email@example.com', 'admin@domain.org']
```


### 5.2 URL 추출

```
text = "Visit https://www.example.com or http://example.org for more info"
urls = re.findall(r"https?://[A-Za-z0-9./-]+", text)
print(urls)  # ['https://www.example.com', 'http://example.org']
```

### 5.3 전화번호 추출
```
text = "My phone numbers are 010-1234-5678 and 02-987
```


## 6. 정규 표현식에서 특정 개수를 지정하는 방법 : 주로 {} 기호를 사용하여 패턴이 반복되는 횟수 지정

### 6-1. {n}: 정확히 n회 반복
특정 문자 또는 패턴이 정확히 n회 반복되는 경우
예시: a{3}는 aaa와 일치합니다.

### 6-2. {n,}: n회 이상 반복
특정 문자 또는 패턴이 n회 이상 반복되는 경우
예시: a{2,}는 aa, aaa, aaaa 등과 일치합니다.

### 6-3. {n,m}: n회 이상 m회 이하 반복
특정 문자 또는 패턴이 n회 이상 m회 이하 반복되는 경우
예시: a{1,3}는 a, aa, aaa와 일치하지만 aaaa와는 일치하지 않음

### 6-4. 예제
```
import re

# 정확히 2회 반복
pattern_exactly_two = r"a{2}"
print(re.findall(pattern_exactly_two, "a aa aaa aaaa"))  # ['aa', 'aa']

# 1회 이상 반복
pattern_one_or_more = r"a{1,}"
print(re.findall(pattern_one_or_more, "a aa aaa aaaa"))  # ['a', 'aa', 'aaa', 'aaaa']

# 2회 이상 4회 이하 반복
pattern_between_two_and_four = r"a{2,4}"
print(re.findall(pattern_between_two_and_four, "a aa aaa aaaa"))  # ['aa', 'aaa', 'aaaa']
```

### 6-5. 다른 예시들
- \d{2}: 두 개의 숫자가 연속해서 나타나는 패턴 (예: 12, 45 등)
- [A-Za-z]{3,5}: 3에서 5자 사이의 알파벳 대소문자가 연속해서 나타나는 패턴 (예: abc, abcd, abcde 등)

### 6-6. 주의사항
중괄호 {} 사용 시, 반드시 숫자와 함께 사용해야 하며, 패턴이 아닌 문자와 함께 사용하면 에러 발생
예를 들어, a{3}는 aaa와 일치하지만, a{abc}와 같은 형식은 잘못된 형식

