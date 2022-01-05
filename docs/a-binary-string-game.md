# 二进制字符串游戏

> 原文:[https://www.geeksforgeeks.org/a-binary-string-game/](https://www.geeksforgeeks.org/a-binary-string-game/)

给定一个二进制字符串 **S** 。任务是当两个玩家按照给定的条件用绳子进行最佳游戏时，确定游戏的赢家:

*   玩家 1 总是第一个开始。
*   两个玩家轮流选择一整块连续相等的字符，并从给定的二进制字符串中删除它们 **S.**
*   玩家 1 只能选择奇数个连续相等的字符，玩家 2 只能选择偶数个连续相等的字符。玩家可以什么都不选，只有在什么都不选的情况下才算轮到自己。
*   移除所有角色后，得分最高的玩家赢得游戏，如果得分相等，则打印**-1”**

> **输入:** S = "1110011001010"
> **输出:**玩家 1
> **说明:**
> 所选角色将加粗，玩家 1 的分数为 Score_1，玩家 2 的分数为 Score_2 :
> 转 1:(玩家 1)**111**0011001010 "→“00110010”Score _ 1 “0000**1**010”→“0000010”Score _ 1 = 4
> 回合 4:(玩家 2)“0000010”
> 他不能做任何事情，因为只有一个‘1’存在，这是一个奇数。
> 同样，他不能选择‘0’，因为它们是奇数(5 和 1)，因此，Score_2 =2
> 回合 5:(玩家 1)“00000**1**0”→“000000”Score _ 1 = 5
> 回合 6:(玩家 2)”**0000000**→“Score _ 2 = 2(本回合未删除‘1 ’)
> 
> 最终得分:Score_1 = 5，Score_2 = 2
> 因此，玩家 1 获胜。
> 
> **输入:**S**=**“11111101”
> **输出:**选手 2
> **解说:**
> 转 1:(选手 1)“11111110**1**→“111110”评分 _1 = 3
> 转 2:(选手 2)**111111**0”→“0”****
> 
>  ****最终得分:Score_1 = 3，Score_2 = 6
> 因此，2 号选手获胜。****

******进场:******

1.  ****如果我们仔细观察这场比赛，我们就会明白只有连续的 **1s** 对这些球员的得分有贡献。****
2.  ****创建一个列表来存储字符串中连续 1 的长度。****
3.  ****[按降序排列](https://www.geeksforgeeks.org/sorting-algorithms/)列表。****
4.  ****现在遍历列表，如果列表元素是奇数，它将被添加到**玩家 1** 的分数中，如果是偶数，它将被添加到**玩家 2** 的分数中。****
5.  ****现在，如果玩家 1 的分数大于玩家 2 的分数，则打印**“玩家 1”**，如果玩家 2 的分数大于玩家 1 的分数，则打印**“玩家 2”**。****
6.  ****如果有平局，打印“-1”，即分数相同。****

****下面是上述方法的实现。****

## ****C++****

```
**// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the result of
// the game
string gameMax(string S)
{

    // length of the string
    int N = S.length();

    // List to maintain the lengths of
    // consecutive '1's in the string
    vector<int> list;

    // Variable that keeps a track of
    // the current length of the block
    // of consecutive '1's
    int one = 0;

    for(int i = 0; i < N; i++)
    {
        if (S[i] == '1')
        {
            one++;
        }
        else
        {

            // Adds non-zero lengths
            if (one != 0)
            {
                list.push_back(one);
            }
            one = 0;
        }
    }

    // This takes care of the case
    // when the last character is '1'
    if (one != 0)
    {
        list.push_back(one);
    }

    // Sorts the lengths in
    // descending order
    sort(list.begin(), list.end(),
         greater<int>());

    // Scores of the 2 players
    int score_1 = 0, score_2 = 0;

    for(int i = 0; i < list.size(); i++)
    {

        // For player 1
        if (list[i] % 2 == 1)
        {
            score_1 += list[i];
        }

        // For player 2
        else
        {
            score_2 += list[i];
        }
    }

    // In case of a tie
    if (score_1 == score_2)
        return "-1";

    // Print the result
    return (score_1 > score_2) ? "Player 1" :
                                 "Player 2";
}

// Driver Code
int main()
{

    // Given string S
    string S = "11111101";

    // Function call
    cout << gameMax(S);
}

// This code is contributed by rutvik_56**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to return the result of
    // the game
    public static String gameMax(String S)
    {
        // length of the string
        int N = S.length();

        // List to maintain the lengths of
        // consecutive '1's in the string
        List<Integer> list = new ArrayList<>();

        // Variable that keeps a track of
        // the current length of the block
        // of consecutive '1's
        int one = 0;

        for (int i = 0; i < N; i++) {

            if (S.charAt(i) == '1') {
                one++;
            }
            else {

                // Adds non-zero lengths
                if (one != 0) {
                    list.add(one);
                }
                one = 0;
            }
        }

        // This takes care of the case
        // when the last character is '1'
        if (one != 0) {
            list.add(one);
        }

        // Sorts the lengths in
        // descending order
        Collections.sort(list,
                         Collections.reverseOrder());

        // Scores of the 2 players
        int score_1 = 0, score_2 = 0;

        for (int i = 0; i < list.size(); i++) {

            // For player 1
            if (list.get(i) % 2 == 1) {
                score_1 += list.get(i);
            }

            // For player 2
            else {
                score_2 += list.get(i);
            }
        }

        // In case of a tie
        if (score_1 == score_2)
            return "-1";

        // Print the result
        return (score_1 > score_2) ? "Player 1"
                                   : "Player 2";
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string S
        String S = "11111101";

        // Function Call
        System.out.println(gameMax(S));
    }
}**
```

## ****蟒蛇 3****

```
**# Python3 program for
# the above approach

# Function to return the
# result of the game
def gameMax(S):

    # Length of the string
    N = len(S)

    # List to maintain the lengths of
    # consecutive '1's in the string
    list = []

    # Variable that keeps a track of
    # the current length of the block
    # of consecutive '1's
    one = 0

    for i in range(N):
        if(S[i] == '1'):
            one += 1
        else:

            # Adds non-zero lengths
            if(one != 0):
                list.append(one)
            one = 0

    # This takes care of the case
    # when the last character is '1'
    if(one != 0):
        list.append(one)

    # Sorts the lengths in
    # descending order
    list.sort(reverse = True)

    # Scores of the 2 players
    score_1 = 0
    score_2 = 0

    for i in range(len(list)):

        # For player 1
        if(list[i] % 2 == 1):
            score_1 += list[i]

        # For player 2
        else:
            score_2 += list[i]

    # In case of a tie
    if(score_1 == score_2):
        return '-1'

    # Print the result
    if(score_1 > score_2):
        return "Player 1"
    else:
        return "Player 2"

# Driver Code

# Given string S
S = "11111101"

# Function call
print(gameMax(S))

# This code is contributed by avanitrachhadiya2155**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the result of
// the game
public static String gameMax(String S)
{

    // length of the string
    int N = S.Length;

    // List to maintain the lengths of
    // consecutive '1's in the string
    List<int> list = new List<int>();

    // Variable that keeps a track of
    // the current length of the block
    // of consecutive '1's
    int one = 0;

    for(int i = 0; i < N; i++)
    {
        if (S[i] == '1')
        {
            one++;
        }
        else
        {

            // Adds non-zero lengths
            if (one != 0)
            {
                list.Add(one);
            }
            one = 0;
        }
    }

    // This takes care of the case
    // when the last character is '1'
    if (one != 0)
    {
        list.Add(one);
    }

    // Sorts the lengths in
    // descending order
    list.Sort();
    list.Reverse();

    // Scores of the 2 players
    int score_1 = 0, score_2 = 0;

    for(int i = 0; i < list.Count; i++)
    {

        // For player 1
        if (list[i] % 2 == 1)
        {
            score_1 += list[i];
        }

        // For player 2
        else
        {
            score_2 += list[i];
        }
    }

    // In case of a tie
    if (score_1 == score_2)
        return "-1";

    // Print the result
    return (score_1 > score_2) ?
         "Player 1" : "Player 2";
}

// Driver Code
public static void Main(String[] args)
{

    // Given string S
    String S = "11111101";

    // Function Call
    Console.WriteLine(gameMax(S));
}
}

// This code is contributed by Amit Katiyar**
```

## ****java 描述语言****

```
**<script>
// javascript program for the
// above approach

// Function to return the result of
// the game
function gameMax(S)
{

    // length of the string
    let N = S.length;

    // List to maintain the lengths of
    // consecutive '1's in the string
    let list = [];

    // Variable that keeps a track of
    // the current length of the block
    // of consecutive '1's
    let one = 0;

    for(let i = 0; i < N; i++)
    {
        if (S[i] == '1')
        {
            one++;
        }
        else
        {

            // Adds non-zero lengths
            if (one != 0)
            {
                list.push(one);
            }
            one = 0;
        }
    }

    // This takes care of the case
    // when the last character is '1'
    if (one != 0)
    {
        list.push(one);
    }

    // Sorts the lengths in
    // descending order
    list.sort();
    list.reverse();

    // Scores of the 2 players
    let score_1 = 0, score_2 = 0;

    for(let i = 0; i < list.length; i++)
    {

        // For player 1
        if (list[i] % 2 == 1)
        {
            score_1 += list[i];
        }

        // For player 2
        else
        {
            score_2 += list[i];
        }
    }

    // In case of a tie
    if (score_1 == score_2)
        return "-1";

    // Prlet the result
    return (score_1 > score_2) ?
         "Player 1" : "Player 2";
}

// Driver Code

    // Given string S
    let S = "11111101";

    // Function Call
    document.write(gameMax(S));

   // This code is contributed by target_2.
</script>**
```

******输出:******

```
**Player 2**
```

*******时间复杂度:**O(N)*
T5**辅助空间:** O(N)****