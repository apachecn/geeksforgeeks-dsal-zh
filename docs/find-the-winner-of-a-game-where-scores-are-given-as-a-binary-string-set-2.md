# 寻找以二进制字符串形式给出分数的游戏的赢家|第 2 集

> 原文:[https://www . geeksforgeeks . org/find-一场比赛的获胜者-分数以二进制字符串集-2 给出/](https://www.geeksforgeeks.org/find-the-winner-of-a-game-where-scores-are-given-as-a-binary-string-set-2/)

给定一个代表排球比赛比分的二进制字符串 **字符串**。任务是根据以下条件找到比赛的获胜者:

*   在排球比赛中，两队互相比赛，先得 15 分的队将获胜，除非两队都得到了 14 分。
*   如果两队都得到了 14 分，那么保持领先 2 分的队将是胜者。

在给定的二进制字符串中， **0** 表示**极客队输**一分， **1** 表示**极客队赢**一分。任务是找出 GEEK 的团队是赢了还是输了这场比赛。

**示例:**

> **输入:**str = " 01011111111111110110101 "
> T3】输出:GEEK s 赢了
> T6】说明: GEEK 以 15-5 的比分获胜
> 
> **输入:**str = " 01010101010101010101010101010100 "
> **输出:** GEEK 的输了
> **说明:**对手以 16-14 的比分获胜

**天真法:**天真法在本题 [**集-1**](https://www.geeksforgeeks.org/find-winner-game/) 中有提及。

**高效进场:**无论时间线是什么，最后得分的玩家都是赢家。原因如下:

> 游戏以某人赢得该盘并满足赢得游戏所需的条件而结束。
> 
> *   如果比赛结束时有人先得了 15 分，那么他将是最后一盘的赢家。
> *   如果在达到 15-14 的状态后，有人保持两分领先赢得了比赛，那么最后一盘保持两分领先的人也将是获胜者。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above appoach
#include <bits/stdc++.h>
using namespace std;

// Function to find the winner
// from given timeline
string findTheWinner(string str, int N)
{
    // If last point scored is 1 then
    // GEEK is winner
    if (str[N - 1] == '1') {
        return "GEEK's won";
    }

    // Else GEEK lost
    return "GEEK's lost";
}

// Driver Code
int main()
{
    // Input score timeline
    string str1 = "01011111111110110101";
    int N1 = str1.size();
    string str2 = "010101010101010101010101010100";
    int N2 = str2.size();

    // Print the winner
    cout << findTheWinner(str1, N1) << endl;
    cout << findTheWinner(str2, N2) << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the winner
# from given timeline
def findTheWinner(str, N):

    # If last point scored is 1 then
    # GEEK is winner
    if (str[N - 1] == '1'):
        return "GEEK's won"

    # Else GEEK lost
    return "GEEK's lost"

# Driver Code

# Input score timeline
str1 = "01011111111110110101"
N1 = len(str1)
str2 = "010101010101010101010101010100"
N2 = len(str2)

# Print the winner
print(findTheWinner(str1, N1))
print(findTheWinner(str2, N2))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# implementation of the above appoach
using System;

class GFG{

// Function to find the winner
// from given timeline
static string findTheWinner(string str, int N)
{

    // If last point scored is 1 then
    // GEEK is winner
    if (str[N - 1] == '1')
    {
        return "GEEK's won";
    }

    // Else GEEK lost
    return "GEEK's lost";
}

// Driver Code
public static void Main()
{

    // Input score timeline
    string str1 = "01011111111110110101";
    int N1 = str1.Length;
    string str2 = "010101010101010101010101010100";
    int N2 = str2.Length;

    // Print the winner
    Console.WriteLine(findTheWinner(str1, N1));
    Console.WriteLine(findTheWinner(str2, N2));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find the winner
      // from given timeline
      function findTheWinner(str, N)
      {

          // If last point scored is 1 then
          // GEEK is winner
          if (str[N - 1] == '1') {
              return "GEEK's won";
          }

          // Else GEEK lost
          return "GEEK's lost";
      }

      // Driver Code

      // Input score timeline
      let str1 = "01011111111110110101";
      let N1 = str1.length;
      let str2 = "010101010101010101010101010100";
      let N2 = str2.length;

      // Print the winner
      document.write(findTheWinner(str1, N1) + '<br>');
      document.write(findTheWinner(str2, N2) + '<br>');

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
GEEK's won
GEEK's lost
```

***时间复杂度:*** O(1)
***辅助空间:*** O(1)