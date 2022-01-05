# 找到重新排列角色的玩家，先得到一个回文串

> 原文:[https://www . geeksforgeeks . org/find-the-player-who-重排-characters-get-a-回文-string-first/](https://www.geeksforgeeks.org/find-the-player-who-rearranges-the-characters-to-get-a-palindrome-string-first/)

给定一个只有小写英文字母组成的偶数长度的字符串 *S* ，我们有两个玩家在玩这个游戏。规则如下:

*   玩家赢得游戏，如果，在任何一步，玩家可以重新排列字符串的字符来获得回文字符串。
*   如果玩家不能赢得游戏，他必须**从字符串中移除任何字符**。

两个玩家都以最佳状态玩游戏，玩家 1 开始游戏。任务是打印游戏的获胜者。
**例:**

> **输入:**S = " abaaab "
> T3】输出:玩家-1
> 第一步玩家-1 安排人物获得“aabbaa”并赢得游戏。
> **输入:** S = "abca"
> **输出:**玩家-2
> 由于游戏正在进行优化，玩家-1 移除‘a’即可在第二次移动中获得玩家-2 无法重新排列的字符串“bca”，从而赢得游戏。
> Player-2 最佳移除‘b’，字符串现在为“ca”。
> 第三招，玩家-1 移除“a”由于无法重新排列字符，新串为“c”，下一招玩家-2 可以做回文。

**进场:**

*   计算 freq[]数组中每个字符的频率。
*   统计出现奇数次的字符。
*   如果计数为 *0* 或一个*奇数*，那么*玩家-1* 将始终赢得游戏，否则玩家-2 将获胜，因为玩家-2 将进行最后一步。

以下是上述方法的实现:

## C++

```
// C++ program to print the winner of the game
#include <bits/stdc++.h>
using namespace std;

// Function that returns the winner of the game
int returnWinner(string s, int l)
{
    // Initialize the freq array to 0
    int freq[26];
    memset(freq, 0, sizeof freq);

    // Iterate and count the frequencies
    // of each character in the string
    for (int i = 0; i < l; i++) {
        freq[s[i] - 'a']++;
    }

    int cnt = 0;

    // Count the odd occurring character
    for (int i = 0; i < 26; i++) {

        // If odd occurrence
        if (freq[i] & 1)
            cnt++;
    }

    // Check condition for Player-1 winning the game
    if (cnt == 0 || cnt & 1)
        return 1;
    else
        return 2;
}

// Driver code
int main()
{
    string s = "abaaab";
    int l = s.length();

    // Function call that returns the winner
    int winner = returnWinner(s, l);

    cout << "Player-" << winner;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the winner of the game
class GfG {
// Function that returns the winner of the game
static int returnWinner(String s, int l)
{
    // Initialize the freq array to 0
    int freq[]  =new int[26];

    // Iterate and count the frequencies
    // of each character in the string
    for (int i = 0; i < l; i++) {
        freq[s.charAt(i) - 'a']++;
    }

    int cnt = 0;

    // Count the odd occurring character
    for (int i = 0; i < 26; i++) {

        // If odd occurrence
        if (freq[i] % 2 != 0)
            cnt++;
    }

    // Check condition for Player-1 winning the game
    if ((cnt == 0)|| (cnt & 1) == 1)
        return 1;
    else
        return 2;
}

// Driver code
public static void main(String[] args)
{
    String s = "abaaab";
    int l = s.length();

    // Function call that returns the winner
    int winner = returnWinner(s, l);

    System.out.println("Player-" + winner);
}
}
```

## 蟒蛇 3

```
# Python 3 program to print the winner of the game

# Function that returns the winner of the game
def returnWinner(s, l):

    # Initialize the freq array to 0
    freq = [0 for i in range(26)]

    # Iterate and count the frequencies
    # of each character in the string
    for i in range(0, l, 1):
        freq[ord(s[i]) - ord('a')] += 1

    cnt = 0

    # Count the odd occurring character
    for i in range(26):

        # If odd occurrence
        if (freq[i] % 2 != 0):
            cnt += 1

    # Check condition for Player-1
    # winning the game
    if (cnt == 0 or cnt & 1 == 1):
        return 1
    else:
        return 2

# Driver code
if __name__ == '__main__':
    s = "abaaab"
    l = len(s)

    # Function call that returns the winner
    winner = returnWinner(s, l)

    print("Player-", winner)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to print the winner of the game
using System;

class GfG
{

// Function that returns the winner of the game
static int returnWinner(String s, int l)
{
    // Initialize the freq array to 0
    int []freq = new int[26];

    // Iterate and count the frequencies
    // of each character in the string
    for (int i = 0; i < l; i++)
    {
        freq[s[i] - 'a']++;
    }

    int cnt = 0;

    // Count the odd occurring character
    for (int i = 0; i < 26; i++)
    {

        // If odd occurrence
        if (freq[i] % 2 != 0)
            cnt++;
    }

    // Check condition for Player-1 winning the game
    if ((cnt == 0)|| (cnt & 1) == 1)
        return 1;
    else
        return 2;
}

// Driver code
public static void Main(String[] args)
{
    String s = "abaaab";
    int l = s.Length;

    // Function call that returns the winner
    int winner = returnWinner(s, l);

    Console.WriteLine("Player-" + winner);
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the winner
// of the game

// Function that returns the
// winner of the game
function returnWinner($s, $l)
{
    // Initialize the freq array to 0
    // int freq[26];
    // memset(freq, 0, sizeof freq);
    // $freg=array_fill()
    $freq = array_fill(0, 26, 0);

    // Iterate and count the frequencies
    // of each character in the string
    for ($i = 0; $i < $l; $i++)
    {
        $freq[$s[$i] - 'a']++;
    }

    $cnt = 0;

    // Count the odd occurring character
    for ($i = 0; $i < 26; $i++)
    {

        // If odd occurrence
        if ($freq[$i] & 1)
            $cnt++;
    }

    // Check condition for Player-1
    // winning the game
    if ($cnt == 0 || $cnt & 1)
        return 1;
    else
        return 2;
}

// Driver code
$s = "abaaab";
$l = strlen($s);

// Function call that returns
// the winner
$winner = returnWinner($s, $l);

echo "Player-" , $winner;

// This code is contributed
// by tushil
?>
```

## java 描述语言

```
<script>
    // Javascript program to print the winner of the game

    // Function that returns the winner of the game
    function returnWinner(s, l)
    {
        // Initialize the freq array to 0
        let freq = new Array(26);
        freq.fill(0);

        // Iterate and count the frequencies
        // of each character in the string
        for (let i = 0; i < l; i++)
        {
            freq[s[i].charCodeAt() - 'a'.charCodeAt()]++;
        }

        let cnt = 0;

        // Count the odd occurring character
        for (let i = 0; i < 26; i++)
        {

            // If odd occurrence
            if (freq[i] % 2 != 0)
                cnt++;
        }

        // Check condition for Player-1 winning the game
        if ((cnt == 0)|| (cnt & 1) == 1)
            return 1;
        else
            return 2;
    }

    let s = "abaaab";
    let l = s.length;

    // Function call that returns the winner
    let winner = returnWinner(s, l);

    document.write("Player-" + winner);

</script>
```

**Output:** 

```
Player-1
```