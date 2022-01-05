# 按照给定的规则

依次将 0 转换为 1，预测游戏的赢家

> 原文:[https://www . geesforgeks . org/通过按给定规则逐个回合地转换 0 到 1 来预测游戏赢家/](https://www.geeksforgeeks.org/predict-the-winner-of-a-game-by-converting-0-to-1-turn-by-turn-following-the-given-rules/)

给定仅由 **0** 和 **1** 组成的二进制字符串**字符串**，其中 **0** 表示未占用的位置， **1** 表示占用的位置。两个玩家 **A** 和 **B** 必须按照给定的规则依次占据一个未被占据的位置(将 0 转换为 1):

1.  玩家只能占据未被占据的位置
2.  玩家每回合只能移动到相邻位置

如果一个玩家在回合中不能移动，他就输了。假设 **A** 先走一步，如果双方都玩得最好，预测游戏的赢家。

**示例:**

> **输入:**str = " 1000 "
> T3】输出: A
> **说明:** A 进行第一次移动并占据字符串第二个索引处的位置(基于 0 的索引)，那么无论 B 选择哪个位置，都将只剩下一个未被占据的位置，该位置将在下一回合被 A 占据，B 不能进一步移动，因此 A 获胜。
> 
> **输入:**str = " 1001 "
> T3】输出: B

**进场:**

1.  求初始未占据位置的两个最长子串的长度(即 **0s** 的子串)。
2.  如果最大子串的长度为**甚至**，那么 **B** 将是赢家，而不管第二大子串的长度如何。这是因为 A 将总是占据最大子串的中间槽，因此在这种情况下，它将具有与给定子串中的 **B** 相同数量的移动槽。 **A** 需要比 **B** 更多的吃角子老虎才能赢得比赛，而在这种情况下，两者的吃角子老虎数量相等，因此 **A** 会输。
3.  如果最大子串的长度为**奇数**，则可能有两种情况:
    *   如果第二大子串的长度小于最大子串中 **A** 的槽数(即 **(n/2) + 1** ，其中 **n** 是子串的大小)，那么 **A** 将是赢家，因为 **B** 将总是具有比 **A** 更少的槽数，而不管他的初始决定(在最大或第二大子串之间进行选择)。
    *   否则， **B** 将成为赢家，因为 **B** 可以选择第二大的子串进行初始移动，并且将比**a**有更多的空位可用于进一步移动
4.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <math.h>

using namespace std;

// Function to predict the winner
string predictWinner(string s)
{
    int n = s.length();
    int max1 = 0, max2 = 0;
    int curr = 0;

    // Loop through the string to find out
    // lengths of longest two substrings of 0s
    for (int i = 0; i < n; i++) {
        if (s[i] == '0') {
            curr++;
        }
        else {
            if (max1 <= curr) {
                max2 = max1;
                max1 = curr;
            }
            else if ((curr < max1)
                     && (curr > max2)) {
                max2 = curr;
            }

            curr = 0;
        }
    }
    if (curr > 0) {
        if (max1 <= curr) {
            max2 = max1;
            max1 = curr;
        }
        else if ((curr < max1)
                 && (curr > max2)) {
            max2 = curr;
        }
    }

    // If longest substring
    // of 0s is of even length
    // then B will always be the winner
    if (max1 % 2 == 0) {
        return "B";
    }

    // Slot for A's moves
    // will be half the total
    // number of slots plus
    // one in longest substring
    int left = ceil((float)max1 / 2);

    // If slots for A's moves
    // are more than slots in
    // second largest sunstring
    // then A will be the
    // winner else B will be winner
    if (left > max2) {
        return "A";
    }

    return "B";
}

// Driver Code
int main()
{
    string s = "1000";
    string ans = predictWinner(s);
    cout << ans;
    return 0;
}
```

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>

// Function to predict the winner
char predictWinner(char s[], int n)
{
    int max1 = 0, max2 = 0;
    int curr = 0;

    // Loop through the string to find out
    // lengths of longest two substrings of 0s
    for (int i = 0; i < n; i++) {
        if (s[i] == '0') {
            curr++;
        }
        else {
            if (max1 <= curr) {
                max2 = max1;
                max1 = curr;
            }
            else if ((curr < max1) && (curr > max2)) {
                max2 = curr;
            }

            curr = 0;
        }
    }
    if (curr > 0) {
        if (max1 <= curr) {
            max2 = max1;
            max1 = curr;
        }
        else if ((curr < max1) && (curr > max2)) {
            max2 = curr;
        }
    }

    // If longest substring
    // of 0s is of even length
    // then B will always be the winner
    if (max1 % 2 == 0) {
        return 'B';
    }

    // Slot for A's moves
    // will be half the total
    // number of slots plus
    // one in longest substring
    int left = ceil((float)max1 / 2);

    // If slots for A's moves
    // are more than slots in
    // second largest sunstring
    // then A will be the
    // winner else B will be winner
    if (left > max2) {
        return 'A';
    }

    return 'B';
}

// Driver Code
int main()
{
    char s[] = "1000";
    int n = 4;
    char ans = predictWinner(s, n);
    printf("%c", ans);
    return 0;
}

// This code is contributed by saxenaanjali239.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.Math;
import java.util.*;

public class GeeksForGeeks
{

    // Function to predict the winner
    public static String predictWinner(String s)
    {
        int n = s.length();
        int max1 = 0, max2 = 0;
        int curr = 0;

        // Loop through the string to find out
        // lengths of longest two substrings of 0s
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == '0') {
                curr++;
            }
            else {
                if (max1 <= curr) {
                    max2 = max1;
                    max1 = curr;
                }
                else if ((curr < max1) && (curr > max2)) {
                    max2 = curr;
                }

                curr = 0;
            }
        }
        if (curr > 0) {
            if (max1 <= curr) {
                max2 = max1;
                max1 = curr;
            }
            else if ((curr < max1) && (curr > max2)) {
                max2 = curr;
            }
        }

        // If longest substring
        // of 0s is of even length
        // then B will always be the winner
        if (max1 % 2 == 0) {
            return "B";
        }

        // Slot for A's moves
        // will be half the total
        // number of slots plus
        // one in longest substring
        int left = (int)Math.ceil((float)max1 / 2);

        // If slots for A's moves
        // are more than slots in
        // second largest sunstring
        // then A will be the
        // winner else B will be winner
        if (left > max2) {
            return "A";
        }

        return "B";
    }

    // Driver Code
    public static void main(String args[])
    {
        String s = "1000";
        String ans = predictWinner(s);
        System.out.println(ans);
    }
}

// This code is contributed by saxenaanjali239.
```

## 计算机编程语言

```
# Python program for the above approach
import math

def predictWinner(s, n):

    max1 = 0
    max2 = 0
    curr = 0
    i = 0

    # Loop through the string to find out
    # lengths of longest two substrings of 0s
    for i in range(n):
        if s[i] == '0':
            curr += 1
        else:
            if max1 <= curr:
                max2 = max1
                max1 = curr
            elif (curr < max1) and (curr > max2):
                max2 = curr

            curr = 0

    if curr > 0:
        if max1 <= curr:
            max2 = max1
            max1 = curr
        elif (curr < max1) and (curr > max2):
            max2 = curr

    # If longest substring
    # of 0s is of even length
    # then B will always be the winner
    if max1 % 2 == 0:
        return "B"

    # Slot for A's moves
    # will be half the total
    # number of slots plus
    # one in longest substring
    left = math.ceil(max1 / 2)

    # If slots for A's moves
    # are more than slots in
    # second largest sunstring
    # then A will be the
    # winner else B will be winner
    if left > max2:
        return "A"

    return "B"

# Driver program to test the above function
s = "1000"
n = len(s)
ans = predictWinner(s, n)
print(ans)

# This code is contributed by saxenaanjali239.
```

## C#

```
// C# program for the above approach
using System;

class GeeksForGeeks
{

    // Function to predict the winner
    static string predictWinner(string s)
    {
        int n = s.Length;
        int max1 = 0, max2 = 0;
        int curr = 0;

        // Loop through the string to find out
        // lengths of longest two substrings of 0s
        for (int i = 0; i < n; i++) {
            if (s[i] == '0') {
                curr++;
            }
            else {
                if (max1 <= curr) {
                    max2 = max1;
                    max1 = curr;
                }
                else if ((curr < max1) && (curr > max2)) {
                    max2 = curr;
                }

                curr = 0;
            }
        }
        if (curr > 0) {
            if (max1 <= curr) {
                max2 = max1;
                max1 = curr;
            }
            else if ((curr < max1) && (curr > max2)) {
                max2 = curr;
            }
        }

        // If longest substring
        // of 0s is of even length
        // then B will always be the winner
        if (max1 % 2 == 0) {
            return "B";
        }

        // Slot for A's moves
        // will be half the total
        // number of slots plus
        // one in longest substring
        int left = (int)Math.Ceiling((float)max1 / 2);

        // If slots for A's moves
        // are more than slots in
        // second largest sunstring
        // then A will be the
        // winner else B will be winner
        if (left > max2) {
            return "A";
        }

        return "B";
    }

    // Driver Code
    public static void Main()
    {
        string s = "1000";
        string ans = predictWinner(s);
        Console.Write(ans);
    }
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to predict the winner
function predictWinner(s)
{
    let n = s.length;
    let max1 = 0, max2 = 0;
    let curr = 0;

    // Loop through the string to find out
    // lengths of longest two substrings of 0s
    for (let i = 0; i < n; i++) {
        if (s[i] == '0') {
            curr++;
        }
        else {
            if (max1 <= curr) {
                max2 = max1;
                max1 = curr;
            }
            else if ((curr < max1) && (curr > max2)) {
                max2 = curr;
            }
                curr = 0;
        }
    }
    if (curr > 0) {
        if (max1 <= curr) {
            max2 = max1;
            max1 = curr;
        }
        else if ((curr < max1) && (curr > max2)) {
            max2 = curr;
        }
    }

    // If longest substring
    // of 0s is of even length
    // then B will always be the winner
    if (max1 % 2 == 0) {
        return "B";
    }

    // Slot for A's moves
    // will be half the total
    // number of slots plus
    // one in longest substring
    let left = Math.ceil(max1 / 2);

    // If slots for A's moves
    // are more than slots in
    // second largest sunstring
    // then A will be the
    // winner else B will be winner
    if (left > max2) {
        return "A";
    }

    return "B";
}

// Driver Code

let s = "1000";
let ans = predictWinner(s);
document.write(ans);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
A
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)