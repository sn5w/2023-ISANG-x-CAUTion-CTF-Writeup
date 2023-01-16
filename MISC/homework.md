# homework

my homework is solve math 50 problems in 30s.... plz help me!


Made by neko_hat

nc misc.isangxcaution.xyz 33002

```python
import random
import os
import sys, signal

def timeout(dummy1 , dummy2):
    print ("[!] Timeout!")
    exit(1)

signal.signal(signal.SIGALRM, timeout)
signal.alarm(30)
operator = "+-*/%^&|"

def calculation():
    a = random.randint(1, 999)
    b = random.randint(1, 999)
    res = 0
    op = random.choice(operator)
    if(op == '+'):
        print(f'{a} + {b} = ', end=' ')
        res  = a + b
    elif(op == '-'):
        if(a > b):
            print(f'{a} - {b} = ', end='')        
            res = a - b
        else:
            print(f'{b} - {a} = ', end='')   
            res = b - a
    elif(op == '*'):
        print(f'{a} * {b} = ', end='')   
        res =  a * b 
    elif(op == '/'):
        print(f'{a} / {b} = ', end='') 
        res = a // b
    elif(op == '%'):
        print(f'{a} % {b} = ', end='')
        res = a % b
    elif(op == '^'):
        print(f'{a} ^ {b} = ', end='') 
        res = a ^ b
    elif(op == '|'):
        print(f'{a} | {b} = ', end='')
        res = a | b 
    elif(op == '&'):
        print(f'{a} & {b} = ', end='')
        res = a & b
    return res

def main():
    cnt = 0
    for i in range(50):
        res = calculation()
        inp = int(input())
        if(res != inp):
            print("Nope!")
            exit(0)
        cnt+=1

    if(cnt == 50):
        print("Congraturations!")
        os.system("cat /flag")
        

if __name__ == '__main__':
    main()

```

Writeup
--
socket과 eval을 이용해 단순히 보내주는 계산식의 답을 구하여 50번 보내주면 flag를 return 해준다.
해당 소스는 다음에 업로드 예정
