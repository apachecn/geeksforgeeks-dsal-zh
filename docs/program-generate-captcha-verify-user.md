# 生成验证码并验证用户的程序

> 原文:[https://www . geesforgeks . org/program-generate-captcha-verify-user/](https://www.geeksforgeeks.org/program-generate-captcha-verify-user/)

一个[验证码](https://en.wikipedia.org/wiki/CAPTCHA)(完全自动化的公共图灵测试，区分计算机和人类)是一个测试，以确定用户是否是人类。
因此，任务是每次生成唯一的验证码，并通过要求用户输入与自动生成的验证码相同的验证码，并用生成的验证码检查用户输入，来判断用户是否是人。
示例:

```
CAPTCHA: x9Pm72se
Input: x9Pm62es
Output: CAPTCHA Not Matched

CAPTCHA: cF3yl9T4
Input: cF3yl9T4
Output: CAPTCHA Matched
```

生成验证码的字符集存储在字符数组 chrs[]中，该数组包含(a-z，A-Z，0-9)，因此 chrs[]的大小为 62。
为了每次生成唯一的验证码，使用 rand()函数(rand()%62)生成随机数，该函数生成 0 到 61 之间的随机数，并将生成的随机数作为字符数组 chrs[]的索引，从而生成验证码[]的新字符，并且该循环运行 n 次(验证码的长度)以生成给定长度的验证码。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to automatically generate CAPTCHA and
// verify user
#include<bits/stdc++.h>
using namespace std;

// Returns true if given two strings are same
bool checkCaptcha(string &captcha, string &user_captcha)
{
    return captcha.compare(user_captcha) == 0;
}

// Generates a CAPTCHA of given length
string generateCaptcha(int n)
{
    time_t t;
    srand((unsigned)time(&t));

    // Characters to be included
    char *chrs = "abcdefghijklmnopqrstuvwxyzABCDEFGHI"
                  "JKLMNOPQRSTUVWXYZ0123456789";

    // Generate n characters from above set and
    // add these characters to captcha.
    string captcha = "";
    while (n--)
        captcha.push_back(chrs[rand()%62]);

    return captcha;
}

// Driver code
int main()
{
    // Generate a random CAPTCHA
    string captcha = generateCaptcha(9);
    cout << captcha;

    // Ask user to enter a CAPTCHA
    string usr_captcha;
    cout << "\nEnter above CAPTCHA: ";
    cin >> usr_captcha;

    // Notify user about matching status
    if (checkCaptcha(captcha, usr_captcha))
        printf("\nCAPTCHA Matched");
    else
        printf("\nCAPTCHA Not Matched");

    return 0;
}
```

## 蟒蛇 3

```
# Python program to automatically generate CAPTCHA and
# verify user
import random

# Returns true if given two strings are same
def checkCaptcha(captcha, user_captcha):
    if captcha == user_captcha:
        return True
    return False

# Generates a CAPTCHA of given length
def generateCaptcha(n):

    # Characters to be included
    chrs = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

    # Generate n characters from above set and
    # add these characters to captcha.
    captcha = ""
    while (n):
        captcha += chrs[random.randint(1, 1000) % 62]
        n -= 1
    return captcha

# Driver code

# Generate a random CAPTCHA
captcha = generateCaptcha(9)
print(captcha)

# Ask user to enter a CAPTCHA
print("Enter above CAPTCHA:")
usr_captcha = input()

# Notify user about matching status
if (checkCaptcha(captcha, usr_captcha)):
    print("CAPTCHA Matched")
else:
    print("CAPTCHA Not Matched")

# This code is contributed by shubhamsingh10
```

输出:

```
CAPTCHA: cF3yl9T4
Enter CAPTCHA: cF3yl9T4
CAPTCHA Matched
```

本文由**希曼舒·古普塔(巴格里)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。