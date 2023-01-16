# rockgame3

큰 도움을 얻었어요. 이젠 절대로 저를 못 이길걸요?! 코드도 보여드릴게요. 이젠 완벽합니다.


Made by codeblue

nc misc.isangxcaution.xyz 33171

```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

int batMoney;
int money = 1000;

void initialize()
{
    setvbuf(stdin, NULL, _IONBF, 0);
    setvbuf(stdout, NULL, _IONBF, 0);
}

void get_flag()
{
    system("cat /home/rockgame3/flag");
}

int inputMoney(void) 
{
    printf("==========================\n");
    printf("소유 금액 : %d\n", money);
    printf("배팅할 금액을 입력해주세요 : "); 
    scanf("%d", &batMoney);
    if (batMoney > money) 
    {
        printf("가지고 있는 금액보다 큰 금액입니다.\n");
        return inputMoney();
    }
    else if(batMoney >= 99 == 0)
    {
        printf("100원 이상을 배팅해야합니다.\n");
        return inputMoney();
    }
    return batMoney;
    
    
}

int computerAI(int playerValue)
{
    switch (playerValue)
    {
    case 0:
        return 1;
        break;
    case 1:
        return 2;
        break;
    case 2:
        return 0;
        break;
    default:
        return 0;
        break;
    }
}

int main()
{

    initialize();
    char * valTran[3] = {"가위", "바위", "보"}; 
    while (1) 
    {   
        int playerValue = 0, comValue = 0;
		  if (money >= 1050)
		  {
		      printf("스승님! 저를 제자로 받아주세요ㅠㅠ\n");
				get_flag();
		  }
        money -= batMoney = inputMoney();
        abc:
		  
        printf("가위바위보 게임을 시작합니다.\n");
        printf("가위 바위 보 중에 하나를 선택해주세요.(정수)\n");
        printf("[가위 : 0], [바위 : 1], [보 : 2]\n");
        scanf("%d", &playerValue);
        if (playerValue < 0) 
        {
            printf("올바른 값이 아닙니다.");
            goto abc;
        }
        comValue = computerAI(playerValue);
        if ((playerValue + 1) % 3 == comValue) 
        {
            // comWin
            printf("저는 %s를 냈어요. 제가 이겼네요!!\n\n", valTran[comValue]);
            if (money <= 100)
            {
                printf("당신! 돈 100원도 없다면서요!?\n");
                printf("다시 연습해와요~~~~~\n");
                return 0;
            }
        }
        else if ((comValue + 1) % 3 == playerValue)
        {
            // playerWin
            printf("저는 %s를 냈어요. 제가 졌네요...!!\n\n", valTran[comValue]);
            goto ddd;
            money += 2 * batMoney;
        }
        else
        {
            printf("무승부에요!!! 기본 금액만 지급됩니다!\n");
            goto ddd;
        }
	

        while (NULL)
        {
            if (0)
            {
                ddd:
                money += 100;
            }
        }
    }

```

Writeup
--
정상적으로는 플레이어가 절대 이길 수 없는 사기 도박 게임.<br>
대신 무승부이면 100원을 돌려주는 점을 이용해서 풀 수 있다.<br>
컴퓨터는 최소 배팅 금액이 100원이라고 하지만 실제로 코드를 보면 99원이다.<br>
1050원만 벌면 되기 때문에 50번만 무승부하면 flag를 얻을 수 있다. <br>

```python
import socket

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_address = ('misc.isangxcaution.xyz', 33171)
sock.connect(server_address)

recvdata = sock.recv(4096)
print(recvdata.decode())

for i in range(52):
    sock.send(('99\n').encode('utf-8'))
    recvdata = sock.recv(4096)
    print(recvdata.decode())
    sock.send(('3\n').encode('utf-8'))
    recvdata = sock.recv(4096)
    print(recvdata.decode())

recvdata = sock.recv(4096)
print (recvdata.decode())
sock.close()
exit()
```
ex code.
