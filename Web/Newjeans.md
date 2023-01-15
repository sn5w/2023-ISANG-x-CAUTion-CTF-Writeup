# Newjeans
web.isangxcaution.xyz:28282

Made by yenua
```python
from flask import Flask, request, render_template, make_response, Response

app = Flask(__name__)

try:
    FLAG = open('./flag.txt', 'r').read()
except:
    FLAG = 'IxC{*** REDUCTED ***}'

@app.route('/')
def index():
    resp = make_response(render_template('index.html', text="Can you get the correct answer?"))
    resp.set_cookie('answer', 'no')
    cookie = request.cookies.get('cookie', None)
    
    if cookie:
        if cookie == "Yammy":
            resp = make_response(render_template('index.html', text=f'Congratulations! flag is {FLAG}'))
            resp.set_cookie('answer', 'yes')
    return resp
    
app.run(host='0.0.0.0', port=8282)
```

Cookie name: cookie
Cookie value: Yammy
로 설정하면 FLAG를 return 해준다.

```html

<html lang="en">
<head>
<title>Newjeans</title>
</head>
<body>
<br>
<div style="text-align : center;">
	<h1>🎵NewJeans - Cookie🎵</h1>
	<br>
	<iframe width="640" height="360"  src="https://www.youtube.com/embed/VOmIplFAGeg" sandbox="allow-forms allow-scripts allow-same-origin"></iframe>
	<br>
	<br>
	Congratulations! flag is IxC{c00k13_15_d3l1c10u5!}
</div>
</body>
</html>
```
