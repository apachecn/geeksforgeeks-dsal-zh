# 找到最后修改字符串的玩家，使得字符串中剩下偶数个辅音，没有元音

> 原文:[https://www . geesforgeks . org/find-the-player-to-last-modify-a-string-so-偶数个辅音和非元音都留在字符串中/](https://www.geeksforgeeks.org/find-the-player-to-last-modify-a-string-such-that-even-number-of-consonants-and-no-vowels-are-left-in-the-string/)

给定一个长度为 **N** 的包含小写字母的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 。两名玩家 **A** 和 **B** 从玩家 A 开始，轮流进行一场最佳游戏，在每一步中，可以执行以下任一操作:

*   从弦上去掉一个辅音。
*   如果任何[字符是元音](https://www.geeksforgeeks.org/program-find-character-vowel-consonant/)，那么将其转换成任何其他字母表。

如果字符串中有偶数个辅音，没有元音，玩家就输了。任务是确定比赛的获胜者。在抽签的情况下，打印 **D** 。
**例:**

> **输入:**S =“ABCD”
> T3】输出:玩家 A
> **说明:**
> 玩家 A 可以通过执行以下招式获胜:
> 招式 1: A 变 A 为 f，因此 S =“fbcd”
> 招式 2: B 移 f，因此 S =“BCD”。
> 移 3: A 移 b，因此，S =“CD”。
> 移动 4: B 移除 c，因此，S =“d”。
> 移 5: A 移 d，故 S =“”。
> 现在轮到 B 了，S 没有元音，有偶数个辅音即 0。
> 
> **输入:**S = " abcde "
> T3】输出: D

**方法:**要解决问题，观察以下情况:

*   如果字符串中没有元音和偶数个辅音，则开始游戏的玩家**输掉游戏**，即玩家 **B** 获胜。
*   如果字符串中没有元音和奇数个辅音，则开始游戏的玩家**赢得游戏**，即玩家 A 获胜。
*   如果单个元音和奇数个辅音出现在给定的字符串**中，玩家 A** 可以获胜。
*   如果字符串中有多个元音，那就是平局。

按照以下步骤解决问题:

*   [统计给定字符串](https://www.geeksforgeeks.org/count-consonants-string-iterative-recursive-methods/) **S** 中的辅音数量，并将其存储在一个变量中，比如 **X** 。
*   因此，给定字符串 **S** 中元音的[计数等于**N–X**。](https://www.geeksforgeeks.org/program-count-vowels-string-iterative-recursive/)
*   如果**N–X**大于 **1** ，则打印 **D** 。
*   如果**N–X**为**0****X**为偶数，则打印**玩家 B** 。
*   否则打印**玩家 A** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find a winner of the game
// if both the player plays optimally
void findWinner(string s)
{
    // Stores the count of vowels
    // and consonants
    int vowels_count = 0,
        consonants_count = 0;

    // Traverse the string
    for (int i = 0; i < s.size(); i++) {

        // Check if character is vowel
        if (s[i] == 'a'
            || s[i] == 'e'
            || s[i] == 'i'
            || s[i] == 'o'
            || s[i] == 'u') {

            // Increment vowels count
            vowels_count++;
        }

        // Otherwise increment the
        // consonants count
        else {
            consonants_count++;
        }
    }

    if (vowels_count == 0) {

        // Check if Player B wins
        if (consonants_count % 2 == 0) {
            cout << "Player B";
        }

        // Check if Player A wins
        else {
            cout << "Player A";
        }
    }

    // Check if Player A wins
    else if (vowels_count == 1
             && consonants_count % 2 != 0) {
        cout << "Player A";
    }

    // If game ends in a Draw
    else {
        cout << "D";
    }
}

// Driver Code
int main()
{
    // Given string s
    string s = "abcd";

    // Function Call
    findWinner(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
class GFG{

// Function to find a winner
// of the game if both the
// player plays optimally
static void findWinner(char[] s)
{
  // Stores the count of vowels
  // and consonants
  int vowels_count = 0,
  consonants_count = 0;

  // Traverse the String
  for (int i = 0; i < s.length; i++)
  {
    // Check if character is vowel
    if (s[i] == 'a' ||
        s[i] == 'e' ||
        s[i] == 'i' ||
        s[i] == 'o' ||
        s[i] == 'u')
    {
      // Increment vowels count
      vowels_count++;
    }

    // Otherwise increment the
    // consonants count
    else
    {
      consonants_count++;
    }
  }

  if (vowels_count == 0)
  {
    // Check if Player B wins
    if (consonants_count % 2 == 0)
    {
      System.out.print("Player B");
    }

    // Check if Player A wins
    else
    {
      System.out.print("Player A");
    }
  }

  // Check if Player A wins
  else if (vowels_count == 1 &&
           consonants_count % 2 != 0)
  {
    System.out.print("Player A");
  }

  // If game ends in a Draw
  else
  {
    System.out.print("D");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given String s
  String s = "abcd";

  // Function Call
  findWinner(s.toCharArray());
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find a winner of the game
# if both the player plays optimally
def findWinner(s):

    # Stores the count of
    # vowels and consonants
    vowels_count = 0
    consonants_count = 0

    # Traverse the string
    p = len(s)

    for i in range(0, p):

        # Check if character is vowel
        if (s[i] == 'a' or s[i] == 'e' or
            s[i] == 'i' or s[i] == 'o' or
            s[i] == 'u'):

            # Increment vowels count
            vowels_count = vowels_count + 1

        # Otherwise increment the
        # consonants count
        else:
            consonants_count = consonants_count + 1

    if (vowels_count == 0):

        # Check if Player B wins
        if (consonants_count % 2 == 0):
            print("Player B")

        # Check if Player A wins
        else:
            print("Player A")

    # Check if Player A wins
    elif (vowels_count == 1 and
       consonants_count % 2 != 0):
        print("Player A")

    # If game ends in a Draw
    else:
        print("D")

# Driver Code
s = "abcd"

findWinner(s)

# This code is contributed by sallagondaavinashreddy7
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find a winner
// of the game if both the
// player plays optimally
static void findWinner(char[] s)
{
  // Stores the count of vowels
  // and consonants
  int vowels_count = 0,
  consonants_count = 0;

  // Traverse the String
  for (int i = 0; i < s.Length; i++)
  {
    // Check if character is vowel
    if (s[i] == 'a' ||
        s[i] == 'e' ||
        s[i] == 'i' ||
        s[i] == 'o' ||
        s[i] == 'u')
    {
      // Increment vowels count
      vowels_count++;
    }

    // Otherwise increment the
    // consonants count
    else
    {
      consonants_count++;
    }
  }

  if (vowels_count == 0)
  {
    // Check if Player B wins
    if (consonants_count % 2 == 0)
    {
      Console.Write("Player B");
    }

    // Check if Player A wins
    else
    {
      Console.Write("Player A");
    }
  }

  // Check if Player A wins
  else if (vowels_count == 1 &&
           consonants_count % 2 != 0)
  {
    Console.Write("Player A");
  }

  // If game ends in a Draw
  else
  {
    Console.Write("D");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given String s
  String s = "abcd";

  // Function Call
  findWinner(s.ToCharArray());
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to find a winner of the game
      // if both the player plays optimally
      function findWinner(s)
      {

        // Stores the count of vowels
        // and consonants
        var vowels_count = 0,
          consonants_count = 0;

        // Traverse the string
        for (var i = 0; i < s.length; i++)
        {

          // Check if character is vowel
          if (
            s[i] === "a" ||
            s[i] === "e" ||
            s[i] === "i" ||
            s[i] === "o" ||
            s[i] === "u"
          )
          {

            // Increment vowels count
            vowels_count++;
          }

          // Otherwise increment the
          // consonants count
          else
          {
            consonants_count++;
          }
        }

        if (vowels_count === 0)
        {

          // Check if Player B wins
          if (consonants_count % 2 === 0)
          {
            document.write("Player B");
          }

          // Check if Player A wins
          else
          {
            document.write("Player A");
          }
        }

        // Check if Player A wins
        else if (vowels_count === 1 && consonants_count % 2 !== 0) {
          document.write("Player A");
        }

        // If game ends in a Draw
        else {
          document.write("D");
        }
      }

      // Driver Code

      // Given string s
      var s = "abcd";

      // Function Call
      findWinner(s);

      // This codeis contributed by rdtank.
    </script>
```

**Output**

```
Player A
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)