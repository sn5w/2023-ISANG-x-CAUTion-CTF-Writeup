# Gotcha!

web.isangxcaution.xyz:20118


Made by 1unaram, smart_kang


단순히 계산식을 넘겨주고 2초안에 답하면 되는 문제,

```python
import requests
from bs4 import BeautifulSoup
# from os import system

s = requests.Session()
url = "http://web.isangxcaution.xyz:20118/"

page = s.get(url + 'index.php')
soup = BeautifulSoup(page.text, "html.parser")
eq = soup.find('p').getText()
ans = eval(eq[0:-4])
print(eq)
print(ans)

_data = {
    "uvalue": ans
}

# cmd = f'curl -d "uvalue={ans}" -X POST {url}result.php'
# system(cmd)
response = s.post(url + 'result.php', data=_data)
response2 = s.get(url + 'index.php')
# print(response2.text)
print(response.text)
```
다음과 같이 ex code를 작성해서 풀었다.
