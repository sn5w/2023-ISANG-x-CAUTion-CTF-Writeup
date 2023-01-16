# lucky number

What's today's lucky number?


Made by neko_hat

nc misc.isangxcaution.xyz 33001

```python2
#!/usr/bin/env python 2.7

import os
import sys, signal
def timeout(dummy1 , dummy2):  
    print "[!] Timeout!"                           
    exit(1)
 
signal.signal(signal.SIGALRM, timeout) 
signal.alarm(30)  
lucky_num = int(os.urandom(512).encode('hex'), 16)
print "Welcome And Happy New Year!!"
print "Select Your LUCKEY NUMBER!!: ",
select_number = input()

if(lucky_num == select_number):
    print "Congraturations!"
    os.system("cat /flag")
    
else:
    print "Hmm... Try again!!"
```

Wirteup
--

주석과 print 포맷을 살펴보면 해당 소스 코드가 python 2 버전임을 알 수 있다. <br>
python 2에서의 input() 함수는 취약점이 존재하는데, 이를 이용해 변수의 값을 대입하거나, 명령어를 실행시킬 수도 있다. <br>
나는 input의 값으로 "lucky_num"을 입력해서 조건문을 true로 만들어 flag을 얻었다.
