# rockgame

혹시 가위바위보 알아요? 제가 요즘 푸욱~ 빠진 게임이에요!! 저 좀 알려주세요!!


Made by codeblue

```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

void initialize()
{
    setvbuf(stdin, NULL, _IONBF, 0);
    setvbuf(stdout, NULL, _IONBF, 0);
}

void get_flag()
{
    system("cat /home/rockgame/flag");
}

int main(int argc, char *argv[])
{


    initialize();

    int money = 1000;
    char * valTran[3] = {"가위", "바위", "보"}; 
    while (1) 
    {   
        int batMoney = 0, playerValue = 0, comValue = 0;
        printf("==========================\n");
        printf("소유 금액 : %d\n", money);
        printf("배팅할 금액을 입력해주세요 : "); 
        scanf("%d", &batMoney);
        if (batMoney > money | batMoney < 0) 
        {
            printf("적절하지 않은 금액입니다.\n");
            continue;
        }
        do {
            if (playerValue) printf("올바른 값이 아닙니다\n");
            printf("가위바위보 게임을 시작합니다.\n");
            printf("가위 바위 보 중에 하나를 선택해주세요.(정수)\n");
            printf("[가위 : 0], [바위 : 1], [보 : 2]\n");
            scanf("%d", &playerValue);
        } while (playerValue != 0 && playerValue != 1 && playerValue != 2); 
        comValue = batMoney % 3;
        if ((playerValue + 1) % 3 == comValue) 
        {
            // comWin
            printf("저는 %s를 냈어요. 제가 이겼네요!!\n\n", valTran[comValue]);
            money -= batMoney;
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
            money += batMoney;
            if (money >= 10000)
            {
                printf("스승님! 저를 제자로 받아주세요ㅠㅠ\n");
                get_flag();

            }
        }
        else
        {
            printf("무승부에요!!! 다시 해봐요!\n\n");
        }
    }
    return 0;
}
```
Wirteup
--
가위바위로 도박하는 게임.<br>
사실상 그냥 무작위로 해도 이길 수 있는 게임이다...<br>
정석으로 풀려면 코드보고 batMoney % 3에 대해 계산해서 풀어도 된다.<br>
