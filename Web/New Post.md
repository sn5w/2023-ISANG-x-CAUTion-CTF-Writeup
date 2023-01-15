# New Post 
web.isangxcaution.xyz:20476

Made by 1unaram

```python
from flask import Flask, request

FLAG = 'IxC{???}'

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def index():

    if request.method == 'GET':
        return 'Hello IxC participant!'

    return f'Flag is {FLAG}'


if __name__ == '__main__':
    app.run(host="0.0.0.0", port=5000)
```

POST로 HTTP REQUEST를 보내면 FLAG가 RESPONSE로 온다.

```sh
❯ curl -X POST web.isangxcaution.xyz:20476
Flag is IxC{post_does_not_mean_writing}%
```
