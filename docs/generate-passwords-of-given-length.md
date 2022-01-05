# 生成给定长度的密码

> 原文:[https://www . geesforgeks . org/generate-给定长度的密码/](https://www.geeksforgeeks.org/generate-passwords-of-given-length/)

给定一个整数 **N** ，任务是生成长度为 **N** 的易、中、强三级随机密码。

> **简易等级密码:**仅由数字或字母组成。
> **中级密码:**由字母和数字组成。
> **强级别密码**–由字母、数字和/或特殊字符组成。

**示例:**

> **输入:** N = 5
> **输出:**
> 易等级密码(仅限数字):98990
> 易密码(仅限字母):tpFEQ
> 中等级密码:b3bC8
> 强等级密码:7`74n
> 
> **输入:** N = 7
> **输出:**
> 易等级密码(仅限数字):7508730
> 易等级密码(仅限字母):mdzckjn
> 中等级密码:4Z05s66
> 强等级密码:2384Qu9

**方法:**
按照以下步骤解决问题:

*   对于每个密码级别，迭代给定的长度。
*   要生成每个密码，根据密码级别使用[随机数生成](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)随机分配字符和数字。

下面是上述方法的实现:

## C

```
// C program to generate
// password of given length
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Function to generate easy level
// password with numbers
void easylevelpassnumbers(int n)
{
    int i;

    // Random character generation
    // setting the seed as TIME
    srand(time(NULL));
    printf("Easy level password "
           "(only numbers): ");
    for (i = 0; i < n; i++) {

        // rand() to assign random
        // characters in the password
        printf("%d", rand() % 10);
    }
    printf("\n");
}

// Function to generate easy level
// password with letters
void easylevelpassletters(int n)
{
    int i, d;
    printf("Easy level password"
           " (only letters): ");
    for (i = 0; i < n; i) {
        d = rand() % 123;
        if ((d >= 65 && d <= 90)
            || d >= 97) {
            printf("%c", (char)d);
            i++;
        }
    }
    printf("\n");
}

// Function to generate random
// medium level password
void midlevelpass(int n)
{
    int i, d;
    printf("Medium level password: ");
    for (i = 0; i < n; i++) {
        d = rand() % 123;

        // Random alphabetic characters
        if ((d >= 65 && d <= 90)
            || d >= 97) {
            printf("%c", (char)d);
        }
        else {

            // Random digits
            printf("%d", d % 10);
        }
    }

    printf("\n");
}

// Function to generate strong
// level password
void stronglevelpass(int n)
{
    int i, d;
    printf("Strong level password: ");
    for (i = 0; i < n; i++) {
        d = rand() % 200;

        // Random special characters
        if (d >= 33 && d <= 123) {
            printf("%c", (char)d);
        }
        else {

            // Random digits
            printf("%d", d % 10);
        }
    }

    printf("\n");
}

// Driver Code
int main()
{
    int n = 5;

    easylevelpassnumbers(n);
    easylevelpassletters(n);
    midlevelpass(n);
    stronglevelpass(n);
}
```

**Output:**

```
Easy level password (only numbers): 36707
Easy level password (only letters): cQWxF
Medium level password: 56G4w
Strong level password: 83s20

```

***时间复杂度:** O(N)
**辅助空间:** O(N)*