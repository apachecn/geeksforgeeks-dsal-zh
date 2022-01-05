# C 中的随机数记忆游戏

> 原文:[https://www . geesforgeks . org/random-number-memory-game-in-c/](https://www.geeksforgeeks.org/random-number-memory-game-in-c/)

在本文中，将设计一个简单的数字记忆游戏在 [C 编程语言](https://www.geeksforgeeks.org/c/)中。这是一个简单的记忆数字游戏，其中一个随机数被显示，并在一段时间后被隐藏。任务是猜测显示的数字以继续游戏。

**如何玩这个游戏:**

*   **按键盘上的 1** 开始游戏。
*   控制台上会显示一个随机的正数，玩家必须记住。
*   几秒钟后，显示的数字将消失。
*   在控制台的下一行，玩家必须输入前面显示的数字。
*   如果输入的数字与前一个数字相同，则玩家的分数增加 1，游戏继续。
*   如果输入的数字不正确，游戏结束并显示玩家的分数。

下面是上述方法的实现:

## C

```
// C program to implements the above
// memory game
#include <conio.h>
#include <dos.h>
#include <stdio.h>
#include <stdlib.h>

// Function to generate the random
// number at each new level
int randomnum(long level)
{
    clrscr();
    printf("Level %ld \n", level);

    long num;
    num = (rand() % 100 * level)
          + 1 + level * 5.2f;

    printf("Number : %ld \n", num);
    delay(2000 - (10 * level));
    clrscr();

    // Return the number
    return num;
}

// Driver Code
void main()
{
    clrscr();
    long num;
    long guessnum;

    long level = 1;

    long inputnum;

    // Start the game
    printf("Press 1 to start Game! ");
    scanf("%ld", &inputnum);

    // Game Starts
    if (inputnum == 1) {

        // Iterate until game ends
        do {

            // Generate a random number
            num = randomnum(level);

            // Get the guessed number
            scanf("%ld", &guessnum);
            level++;

            // Condition for the Game
            // Over State
            if (guessnum != num) {
                printf("You Failed! ");
            }
        } while (num == guessnum);
    }

    getch();
}
```

**输出:**

<video class="wp-video-shortcode" id="video-593226-1" width="640" height="360" preload="metadata" controls=""><source type="video/mp4" src="https://media.geeksforgeeks.org/wp-content/uploads/20200910005553/c-programming-min-game.mp4?_=1">[https://media.geeksforgeeks.org/wp-content/uploads/20200910005553/c-programming-min-game.mp4](https://media.geeksforgeeks.org/wp-content/uploads/20200910005553/c-programming-min-game.mp4)</video>