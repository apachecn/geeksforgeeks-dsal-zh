# C

中的随机密码生成器

> 原文:[https://www . geesforgeks . org/random-password-generator-in-c/](https://www.geeksforgeeks.org/random-password-generator-in-c/)

在本文中，我们将讨论如何生成由任意字符组成的给定长度的[随机](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)密码。

**进场:**

*   下面给出的程序涉及到[变量](https://www.geeksforgeeks.org/variables-in-c/)、[数据类型](https://www.geeksforgeeks.org/c-data-types/)、[数组](https://www.geeksforgeeks.org/array-data-structure/)、[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)等基本概念。
*   请按照以下步骤解决此问题:
    *   取密码的长度，并声明一个该长度的字符数组来存储该密码。
    *   声明字符数组的所有大写字母，小写字母，数字，特殊字符。
    *   现在根据下面的程序，执行各自的 [if-else](https://www.geeksforgeeks.org/decision-making-c-c-else-nested-else/) 并生成随机密码。

以下是上述方法的程序:

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Function to randomly generates password
// of length N
void randomPasswordGeneration(int N)
{
    // Initialize counter
    int i = 0;

    int randomizer = 0;

    // Seed the random-number generator
    // with current time so that the
    // numbers will be different every time
    srand((unsigned int)(time(NULL)));

    // Array of numbers
    char numbers[] = "0123456789";

    // Array of small alphabets
    char letter[] = "abcdefghijklmnoqprstuvwyzx";

    // Array of capital alphabets
    char LETTER[] = "ABCDEFGHIJKLMNOQPRSTUYWVZX";

    // Array of all the special symbols
    char symbols[] = "!@#$^&*?";

    // Stores the random password
    char password[N];

    // To select the randomizer
    // inside the loop
    randomizer = rand() % 4;

    // Iterate over the range [0, N]
    for (i = 0; i < N; i++) {

        if (randomizer == 1) {
            password[i] = numbers[rand() % 10];
            randomizer = rand() % 4;
            printf("%c", password[i]);
        }
        else if (randomizer == 2) {
            password[i] = symbols[rand() % 8];
            randomizer = rand() % 4;
            printf("%c", password[i]);
        }
        else if (randomizer == 3) {
            password[i] = LETTER[rand() % 26];
            randomizer = rand() % 4;
            printf("%c", password[i]);
        }
        else {
            password[i] = letter[rand() % 26];
            randomizer = rand() % 4;
            printf("%c", password[i]);
        }
    }
}

// Driver Code
int main()
{
    // Length of the password to
    // be generated
    int N = 10;

    // Function Call
    randomPasswordGeneration(N);

    return 0;
}
```

**Output:**

```
51WAZMT?Z$

```

 ***时间复杂度:**O(N)
T5】辅助空间: O(26)*