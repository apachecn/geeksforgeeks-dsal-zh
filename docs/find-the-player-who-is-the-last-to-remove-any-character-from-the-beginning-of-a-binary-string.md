# 找出最后一个从二进制字符串开头删除任何字符的玩家

> 原文:[https://www . geeksforgeeks . org/find-最后一个从二进制字符串开头删除任何字符的玩家/](https://www.geeksforgeeks.org/find-the-player-who-is-the-last-to-remove-any-character-from-the-beginning-of-a-binary-string/)

给定一个由[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是当两个玩家按照以下规则进行最佳游戏时，找到游戏的赢家:

*   **玩家 1** 开始游戏。
*   在每一回合中，玩家必须选择一个非空字符串，并从该字符串的开头移除正数量的字符。
*   **玩家 1** 只能选择以字符‘0’开头的字符串，而**玩家 2** 只能选择以字符‘1’开头的字符串。
*   不能移动的玩家输掉游戏。

**示例:**

> **输入:**arr[]= {“010”、“101”}
> **输出:**玩家 2
> **解释:**
> 玩家 1 的第一步= {0，101}
> 玩家 2 的第一步= {0，1}
> 玩家 1 的第二步= {1}
> 玩家 2 的第二步= {}
> 玩家 1 没有剩余移动。
> 因此玩家 2 获胜。
> 
> **输入:**arr[]= {“010”、“001”}
> **输出:**玩家 1

**方法:**想法是比较如果两个玩家都以最佳状态玩游戏，每个玩家可以移动的总次数。请遵循以下步骤:

1.  如果同一字符在任何字符串中连续出现，那么只需用该字符的一次出现来替换它们，因为最好删除开头出现的所有字符。
2.  现在，如果字符串有一个与其最后一个元素相同的开始元素，那么即使没有这个字符串，游戏的场景也保持不变，因为如果一个玩家在这个字符串上移动，另一个玩家通过从同一个字符串中移除字符来进行下一个移动，导致第一个玩家的位置完全相同。
3.  如果一个字符串的开始元素不同于它的最后一个元素，它需要玩家多走一步。
4.  所以，只要数一数每个玩家必须额外移动的次数。
5.  没有多余招式的玩家将输掉比赛。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the player who
// loses the game
void findPlayer(string str[], int n)
{

    // Moves for the first player
    int move_first = 0;

    // Moves for the second player
    int move_sec = 0;

    // Iterate over array of strings
    for (int i = 0; i < n; i++) {

        // Check if the first and last
        // character are the same
        if (str[i][0]
            == str[i][str[i].length() - 1]) {

            // Check if string start and
            // end with character '0'
            if (str[i][0] == 48)
                move_first++;
            else
                move_sec++;
        }
    }

    // If first player have less moves
    if (move_first <= move_sec) {
        cout << "Player 2 wins";
    }
    else {
        cout << "Player 1 wins";
    }
}

// Driver Code
int main()
{
    // Given array of strings
    string str[] = { "010", "101" };

    int N = sizeof(str)
            / sizeof(str[0]);

    // Function Call
    findPlayer(str, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find the player who
// loses the game
static void findPlayer(String str[],
                       int n)
{
  // Moves for the
  // first player
  int move_first = 0;

  // Moves for the
  // second player
  int move_sec = 0;

  // Iterate over array
  // of Strings
  for (int i = 0; i < n - 1; i++)
  {
    // Check if the first and last
    // character are the same
    if (str[i].charAt(0) ==
        str[i].charAt(str[i].length() - 1))
    {
      // Check if String start and
      // end with character '0'
      if (str[i].charAt(0) == 48)
        move_first++;
      else
        move_sec++;
    }
  }

  // If first player have less moves
  if (move_first <= move_sec)
  {
    System.out.print("Player 2 wins");
  }
  else
  {
    System.out.print("Player 1 wins");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array of Strings
  String str[] = {"010", "101"};

  int N = str[0].length();

  // Function Call
  findPlayer(str, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the player who
# loses the game
def findPlayer(str, n):

    # Moves for the first player
    move_first = 0

    # Moves for the second player
    move_sec = 0

    # Iterate over array of strings
    for i in range(n):

        # Check if the first and last
        # character are the same
        if (str[i][0] ==
            str[i][len(str[i]) - 1]):

            # Check if string start and
            # end with character '0'
            if (str[i][0] == 48):
                move_first += 1
            else:
                move_sec += 1

    # If first player have less moves
    if (move_first <= move_sec):
        print("Player 2 wins")
    else:
        print("Player 1 wins")

# Driver Code

# Given array of strings
str = [ "010", "101" ]

N = len(str)

# Function call
findPlayer(str, N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function to find the player who
// loses the game
static void findPlayer(string[] str, int n)
{

    // Moves for the first player
    int move_first = 0;

    // Moves for the second player
    int move_sec = 0;

    // Iterate over array of strings
    for(int i = 0; i < n; i++)
    {

        // Check if the first and last
        // character are the same
        if (str[i][0] ==
            str[i][str[i].Length - 1])
        {

            // Check if string start and
            // end with character '0'
            if ((str[i][0]) == 48)
                move_first++;
            else
                move_sec++;
        }
    }

    // If first player have less moves
    if (move_first <= move_sec)
    {
        Console.Write("Player 2 wins");
    }
    else
    {
        Console.Write("Player 1 wins");
    }
}

// Driver Code
public static void Main ()
{

    // Given array of strings
    string[] str = { "010", "101" };

    int N = str.Length;

    // Function call
    findPlayer(str, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to find the player who
// loses the game
function findPlayer(str, n)
{
  // Moves for the
  // first player
  let move_first = 0;

  // Moves for the
  // second player
  let move_sec = 0;

  // Iterate over array
  // of Strings
  for (let i = 0; i < n - 1; i++)
  {
    // Check if the first and last
    // character are the same
    if (str[i][0] ==
        str[i][str[i].length - 1])
    {
      // Check if String start and
      // end with character '0'
      if (str[i][0]== 48)
        move_first++;
      else
        move_sec++;
    }
  }

  // If first player have less moves
  if (move_first <= move_sec)
  {
    document.write("Player 2 wins");
  }
  else
  {
    document.write("Player 1 wins");
  }
}

// Driver Code

    // Given array of Strings
  let str = ["010", "101"];

  let N = str[0].length;

  // Function Call
  findPlayer(str, N);

</script>
```

**Output:** 

```
Player 2 wins
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)