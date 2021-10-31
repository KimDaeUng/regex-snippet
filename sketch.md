
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

## 연결어미별 절 분절
### Reference
- [<한국어 어미의 분류> 어말어미, 선어말어미, 연결어미, 종결어미, 전성어미](https://m.blog.naver.com/zzangdol57/30169103790)
- [정규표현식의 개념과 기초문법](https://soooprmx.com/%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EA%B8%B0%EC%B4%88-%EB%AC%B8%EB%B2%95/)

```python
import re
# 연결어미 정규표현식
p = re.compile(r'(.*?)+(((으){0,1}(며|나))|(고|아|어|지|면|지|게))+([^ㄱ-힇])(,){0,1}')

split_txt = []
for i in range(10):
    try:
        spt = p.search(error_text)[0]
        split_txt.append(spt)
        error_text = error_text[len(spt):]
    except:
        split_txt.append(error_text)
        break
```
```python
# 원문
'2020년 제21대 총선 때 속초시·고성군·양양군의 인구 하한선 미달로 앞선 상황이 되풀이되었고 자치구시군 분할을 금지한 선거법에 따라 속초시·철원군·화천군·양구군·인제군·고성군으로 선거구가 획정될 뻔했으나, 더불어민주당, 미래통합당, 민생당 등 3당 및 문희상 국회의장이 6개 시군을 관할하는 선거구가 문제가 있다는 공감대를 보이며 이 지역에 대해서만 적용되는 특례를 부칙으로 달아 춘천시 일부를 분할하여 선거구를 구성하기로 결정, 인제군만이 속초시·고성군·양양군으로 넘어가고 철원군, 화천군, 양구군은 분할된 춘천시 일부 지역과 함께 춘천시·철원군·화천군·양구군 을 선거구가 되었으며 이 과정에서 다른 지역과 분리된 홍천군은 홍천군·횡성군·영월군·평창군에 속하게 되면서 다시금 횡성군과 한 선거구로 묶이게 되었다.'
# 분절 결과
['2020년 제21대 총선 때 속초시·고성군·양양군의 인구 하한선 미달로 앞선 상황이 되풀이되었고 ',
 '자치구시군 분할을 금지한 선거법에 따라 속초시·철원군·화천군·양구군·인제군·고성군으로 선거구가 획정될 뻔했으나,',
 ' 더불어민주당, 미래통합당, 민생당 등 3당 및 문희상 국회의장이 6개 시군을 관할하는 선거구가 문제가 있다는 공감대를 보이며 ',
 '이 지역에 대해서만 적용되는 특례를 부칙으로 달아 ',
 '춘천시 일부를 분할하여 선거구를 구성하기로 결정, 인제군만이 속초시·고성군·양양군으로 넘어가고 ',
 '철원군, 화천군, 양구군은 분할된 춘천시 일부 지역과 함께 춘천시·철원군·화천군·양구군 을 선거구가 되었으며 ',
 '이 과정에서 다른 지역과 분리된 홍천군은 홍천군·횡성군·영월군·평창군에 속하게 ',
 '되면서 다시금 횡성군과 한 선거구로 묶이게 ',
 '되었다.']
 ```

