# 寻找以二进制字符串形式给出分数的游戏的赢家

> 原文:[https://www.geeksforgeeks.org/find-winner-game/](https://www.geeksforgeeks.org/find-winner-game/)

给定一个代表排球比赛分数的二进制字符串。任务是根据以下条件找到比赛的获胜者:

*   在排球比赛中，两队互相比赛，先得 15 分的队将获胜，除非两队都得到了 14 分。
*   如果两队都得到了 14 分，那么保持领先 2 分的队将是胜者。

在给定的二进制字符串中，0 表示 GEEK 的团队输一分，1 表示 GEEK 的团队赢一分。你必须找出 GEEK 的球队是赢了还是输了这场比赛。

 **例:**

```
Input : score[] = 01011111111110110101
Output : GEEK's won

Input : score[] = 010101010101010101010101010100
Output : GEEK's lost

```

**案例一:**当其中一队先得 15 分，第二队得分低于 15 分。然后遍历给定的二进制字符串并存储 0 和 1 的计数。在那之后，如果你数到一是 15，数到零小于 15，那么 GEEK 赢了，另一方面，如果你数到零是 15，数到一小于 15，那么 GEEK 输了。

**情况二:**当两个队都得了 14 分，然后将两个队的计数都重置为零，并且对于每个零或一，增加他们的计数，同时检查 abs(计数[0]–计数[1])是否等于 2，如果发生这种情况，则意味着任何一个队比其对手多得了两分，并且将是赢家。然后，您可以根据计数[0]和计数[1]的值找到获胜者。

下面是上述方法的实现:

## C++

```
// Cpp program for predicting winner
#include <bits/stdc++.h>
using namespace std;

// function for winner prediction
void predictWinner(string score, int n)
{

    int count[2] = { 0 }, i;
    for (i = 0; i < score.size(); i++) {

        // increase count
        count[score[i] - '0']++; 

        // check losing condition
        if (count[0] == n && count[1] < n - 1) {
            cout << "GEEKS lost";
            return;
        }

        // check winning condition
        if (count[1] == n && count[0] < n - 1) {
            cout << "GEEKS won";
            return;
        }

        // check tie on n-1 point
        if (count[0] == n - 1 && count[1] ==
                                   n - 1) {
            count[0] = 0;
            count[1] = 0;
            break;
        }
    }

    for (i++; i < score.size(); i++) {

        // increase count
        count[score[i] - '0']++; 

        // check for 2 point lead
        if (abs(count[0] - count[1]) == 2) {

            // condition of lost
            if (count[0] > count[1])
                cout << "GEEKS lost";

            // condition of win
            else
                cout << "GEEKS won";

            return;
        }
    }
}

// driver program
int main()
{
    string score = "1001010101111011101111";
    int n = 15;
    predictWinner(score, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for 
// predicting winner
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
// function for 
// winner prediction
static void predictWinner(String score, 
                          int n)
{

    int count[] = new int[2], i;
    for (i = 0;
         i < score.length(); i++) 
    {

        // increase count
        count[score.charAt(i) - '0']++; 

        // check losing
        // condition
        if (count[0] == n && 
            count[1] < n - 1) 
        {
            System.out.print("GEEKS lost");
            return;
        }

        // check winning condition
        if (count[1] == n && 
            count[0] < n - 1) 
        {
            System.out.print("GEEKS won");
            return;
        }

        // check tie on n-1 point
        if (count[0] == n - 1 && 
            count[1] == n - 1) 
        {
            count[0] = 0;
            count[1] = 0;
            break;
        }
    }

    for (i++; i < score.length(); i++) 
    {

        // increase count
        count[score.charAt(i) - '0']++; 

        // check for 2 point lead
        if (Math.abs(count[0] - 
                     count[1]) == 2) 
        {

            // condition of lost
            if (count[0] > count[1])
                System.out.print("GEEKS lost");

            // condition of win
            else
                System.out.print("GEEKS won");

            return;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String score = "1001010101111011101111";
    int n = 15;
    predictWinner(score, n);
}
}
```

## 蟒蛇 3

```
# Python 3 program for predicting winner

# function for winner prediction
def predictWinner(score, n):
    count = [0 for i in range(2)]

    for i in range(0, len(score), 1):

        # increase count
        index = ord(score[i]) - ord('0')
        count[index] += 1

        # check losing condition
        if (count[0] == n and count[1] < n - 1):
            print("GEEKS lost", end = " ")
            return

        # check winning condition
        if (count[1] == n and count[0] < n - 1):
            print("GEEKS won", end = " ")
            return

        # check tie on n-1 point
        if (count[0] == n - 1 and 
            count[1] == n - 1):
            count[0] = 0
            count[1] = 0
            break
    i += 1    

    for i in range(i, len(score), 1):

        # increase count
        index = ord(score[i]) - ord('0')
        count[index] += 1

        # check for 2 point lead
        if (abs(count[0] - count[1]) == 2):

            # condition of lost
            if (count[0] > count[1]):
                print("GEEKS lost", end = " ")

            # condition of win
            else:
                print("GEEKS won", end = " ");

            return

# Driver Code
if __name__ == '__main__':
    score = "1001010101111011101111"
    n = 15
    predictWinner(score, n)

# This code is contributed by 
# Surendra_Gangwar
```

## C#

```
// C# program for predicting winner 
using System;

class GFG
{
// function for winner prediction 
public static void predictWinner(string score, 
                                 int n)
{

    int[] count = new int[2]; int i;
    for (i = 0; i < score.Length; i++)
    {

        // increase count 
        count[score[i] - '0']++;

        // check losing 
        // condition 
        if (count[0] == n && count[1] < n - 1)
        {
            Console.Write("GEEKS lost");
            return;
        }

        // check winning condition 
        if (count[1] == n && count[0] < n - 1)
        {
            Console.Write("GEEKS won");
            return;
        }

        // check tie on n-1 point 
        if (count[0] == n - 1 && 
            count[1] == n - 1)
        {
            count[0] = 0;
            count[1] = 0;
            break;
        }
    }

    for (i++; i < score.Length; i++)
    {

        // increase count 
        count[score[i] - '0']++;

        // check for 2 point lead 
        if (Math.Abs(count[0] - count[1]) == 2)
        {

            // condition of lost 
            if (count[0] > count[1])
            {
                Console.Write("GEEKS lost");
            }

            // condition of win 
            else
            {
                Console.Write("GEEKS won");
            }

            return;
        }
    }
}

// Driver Code 
public static void Main(string[] args)
{
    string score = "1001010101111011101111";
    int n = 15;
    predictWinner(score, n);
}
}

// This code is contributed by Shrikant13
```

**Output:**

```
GEEKS won

```

本文由**[Shivam Pradhan(anuj _ charm)](http://www.facebook.com/ma5ter6it)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。