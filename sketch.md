
# 조건 탐색
## e.x.) "-","."," "외 다른 글자가 포함되어 있는 경우
```python
import re
pattern = re.compile(r'[^\-\.\s]+')
matched_chr = pattern.findall(user_input)
```
## 비밀번호 규칙
- 8자리 이상 30글자 미만
- 영어 대문자와 소문자 최소 1개씩 포함
- 하나 이상의 숫자 포함
- 하나 이상의 특수기호 (!@#$%^&*) 포함
```python
password_checker = re.compile("^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*])[A-Za-z\d!@#$%^&*]{8,30}$"  )
mat = re.search(password_checker, password)
bool(mat) # 만족 여부
```

# 제거 및 치환
## 양끝 공백 문자 제거
```python
import re
result = re.sub('^\s*|\s*$', '', result)
```

## 문장부호 `.,!?` 삭제
```python
user_input_ = re.sub(r'[.,!?]+', '', user_input)
```

---

## 자소 문자 제거
```python
import re
def remove_consonant_vowel(text):
    jaeum_list = ['ㄱ','ㄲ','ㄴ','ㄷ','ㄸ','ㄹ','ㅁ','ㅂ','ㅃ','ㅅ','ㅆ','ㅇ','ㅈ','ㅉ','ㅊ','ㅋ','ㅌ','ㅍ','ㅎ']
    moeum_list = ['ㅏ','ㅑ','ㅓ','ㅕ','ㅗ','ㅛ','ㅜ','ㅠ','ㅡ','ㅣ','ㅘ','ㅚ','ㅙ','ㅜ','ㅟ','ㅝ','ㅢ']
    jamo_checker = re.compile('['+''.join(jaeum_list)+''.join(moeum_list)+']+')
    new_text = re.sub(jamo_checker,'',text)

    return new_text
```

## 특정 문자(`@`)가 최대 2번 포함된 경우 제거
```python
def myFunction(text:List[str]): 
    for word in slang_list:
        if word in text:
            text = text.replace(word,'*'*len(word))
        for char_idx,char in enumerate(word):
            for special_token in ['@','@@']:
                special_word = word[:char_idx]+special_token+word[char_idx:]
                if special_word in text:
                    text = text.replace(special_word,'*'*len(special_word))
                    
    return text
```
