# 通过移除非空子串

在清空一个二进制串后找到最少为 0 的玩家

> 原文:[https://www . geeksforgeeks . org/通过移除非空子字符串来查找清空二进制字符串后计数最少为 0 的玩家/](https://www.geeksforgeeks.org/find-the-player-with-least-count-of-0s-after-emptying-a-binary-string-by-removing-non-empty-substrings/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是当两个玩家在给定字符串的交替回合中以最佳方式玩游戏时，根据以下条件确定游戏的赢家:

*   **玩家 1** 总是先开始。
*   在每一回合中，玩家从给定的字符串中移除一个非空的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)。
*   给定字符串清空后，最小计数为 **0** s 的玩家将赢得游戏。如果两个玩家的 **0** 相同，则打印“**平局**”。

**示例:**

> **输入:** S = "00011"
> **输出:**玩家 1
> **说明:**子串可以选择如下:
> 回合 1:玩家 1 移除子串 S[4…5]。因此，玩家 1 包含“11”。
> 回合 2:玩家 2 移除子串 S[0…0]。因此，播放器 2 包含“0”。
> 回合 3:玩家 1 移除子串 S[0…0]。因此，玩家 1 包含“110”。
> 回合 4:玩家 2 移除子串 S[0…0]。因此，玩家 2 包含“00”。
> 因此，玩家 1 赢得游戏。
> 
> **输入:** S = "0110011"
> **输出:**玩家 2

**方法:**根据以下观察结果可以解决问题:

*   如果字符串中 **0** s 的计数是[偶数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-given-number-is-even-or-odd/)，那么玩家 1 和玩家 2 每回合选择子字符串**“0”**，没有玩家会赢这场游戏。
*   否则，将连续 **1** s 的计数存储在一个数组中，并在该数组中应用 nim 规则的[游戏。](https://www.geeksforgeeks.org/combinatorial-game-theory-set-2-game-nim/)
*   **Nim-Sum:** 游戏任意一点每堆/堆(此处为连续 1)中硬币/石头数量的累计 XOR 值，在该点称为 Nim-Sum。

按照以下步骤解决问题:

*   初始化一个变量，比如说 **cntZero** ，将 **0** 的计数存储在字符串中。
*   初始化一个变量，比如 **cntConOne** ，来存储字符串中连续 **1** 的计数。
*   初始化一个变量，比如 **nimSum** ，来存储给定字符串的连续 **1** 的 [Nim-Sum](https://www.geeksforgeeks.org/combinatorial-game-theory-set-2-game-nim/) 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，计算 **0** s、**尼姆森**的个数。
*   最后，[检查 **cntZero** 的值是否为偶数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-given-number-is-even-or-odd/)。如果发现属实，则打印**铁**。
*   否则，检查 **nimSum** 的值是否大于 **0** 。如果发现是真的，那么打印**玩家 1** 。
*   否则打印**玩家 2** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the player
// who wins the game
void FindwinnerOfGame(string& S)
{

    // Stores total count
    // of 0s in the string
    int cntZero = 0;

    // Stores count of
    // consecutive 1s
    int cntConOne = 0;

    // Stores Nim-Sum on count
    // of consecutive 1s
    int nimSum = 0;

    // Stores length
    // of the string
    int N = S.length();

    // Traverse the string
    for (int i = 0; i < N; i++) {

        // If the current
        // character is 1
        if (S[i] == '1') {

            // Update cntConOne
            cntConOne += 1;
        }
        else {

            // Update nimSum
            nimSum ^= cntConOne;

            // Update cntConOne
            cntConOne = 0;

            // Update cntZero
            cntZero++;
        }
    }

    // Update nimSum
    nimSum ^= cntConOne;

    // If countZero is
    // an even number
    if (cntZero % 2 == 0) {
        cout << "Tie";
    }

    // nimSum is not 0
    else if (nimSum) {
        cout << "player 1";
    }

    // If nimSum is zero
    else {
        cout << "player 2";
    }
}

// Driver Code
int main()
{

    string S = "0110011";
    FindwinnerOfGame(S);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

// Function to find the player
// who wins the game
class GFG {
    public static void FindwinnerOfGame(String S)
    {

        // Stores total count
        // of 0s in the string
        int cntZero = 0;

        // Stores count of
        // consecutive 1s
        int cntConOne = 0;

        // Stores Nim-Sum on count
        // of consecutive 1s
        int nimSum = 0;

        // Stores length
        // of the string
        int N = S.length();

        // Traverse the string
        for (int i = 0; i < N; i++) {

            // If the current
            // character is 1
            if (S.charAt(i) == '1') {

                // Update cntConOne
                cntConOne += 1;
            }
            else {

                // Update nimSum
                nimSum ^= cntConOne;

                // Update cntConOne
                cntConOne = 0;

                // Update cntZero
                cntZero++;
            }
        }

        // Update nimSum
        nimSum ^= cntConOne;

        // If countZero is
        // an even number
        if (cntZero % 2 == 0) {
            System.out.print("Tie");
        }

        // nimSum is not 0
        else if (nimSum != 0) {
            System.out.print("player 1");
        }

        // If nimSum is zero
        else {
            System.out.print("player 2");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "0110011";
        FindwinnerOfGame(S);
    }
}

// This code is contributed by grand_master.
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to find the player
# who wins the game
def FindwinnerOfGame(S):

    # Stores total count
    # of 0s in the string
    cntZero = 0

    # Stores count of
    # consecutive 1s
    cntConOne = 0

    # Stores Nim-Sum on count
    # of consecutive 1s
    nimSum = 0

    # Stores length
    # of the string
    N = len(S)

    # Traverse the string
    for i in range(N):

        # If the current
        # character is 1
        if (S[i] == '1'):

            # Update cntConOne
            cntConOne += 1
        else:

            # Update nimSum
            nimSum ^= cntConOne

            # Update cntConOne
            cntConOne = 0

            # Update cntZero
            cntZero += 1

    # Update nimSum
    nimSum ^= cntConOne

    # If countZero is
    # an even number
    if (cntZero % 2 == 0):
        print("Tie")

    # nimSum is not 0
    elif(nimSum):
        print("player 1")

    # If nimSum is zero
    else:
        print("player 2")

# Driver Code
if __name__ == '__main__':
    S = "0110011"
    FindwinnerOfGame(S)

    # this code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program to implement
// the above approach
using System;

// Function to find the player
// who wins the game
class GFG {
  public static void FindwinnerOfGame(string S)
  {

    // Stores total count
    // of 0s in the string
    int cntZero = 0;

    // Stores count of
    // consecutive 1s
    int cntConOne = 0;

    // Stores Nim-Sum on count
    // of consecutive 1s
    int nimSum = 0;

    // Stores length
    // of the string
    int N = S.Length;

    // Traverse the string
    for (int i = 0; i < N; i++) {

      // If the current
      // character is 1
      if (S[i] == '1') {

        // Update cntConOne
        cntConOne += 1;
      }
      else {

        // Update nimSum
        nimSum ^= cntConOne;

        // Update cntConOne
        cntConOne = 0;

        // Update cntZero
        cntZero++;
      }
    }

    // Update nimSum
    nimSum ^= cntConOne;

    // If countZero is
    // an even number
    if (cntZero % 2 == 0) {
      Console.Write("Tie");
    }

    // nimSum is not 0
    else if (nimSum != 0) {
      Console.Write("player 1");
    }

    // If nimSum is zero
    else {
      Console.Write("player 2");
    }
  }

  // Driver Code
  public static void Main(string[] args)
  {
    string S = "0110011";
    FindwinnerOfGame(S);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Function to find the player
// who wins the game
    function FindwinnerOfGame(S)
    {

        // Stores total count
        // of 0s in the string
        let cntZero = 0;

        // Stores count of
        // consecutive 1s
        let cntConOne = 0;

        // Stores Nim-Sum on count
        // of consecutive 1s
        let nimSum = 0;

        // Stores length
        // of the string
        let N = S.length;

        // Traverse the string
        for (let i = 0; i < N; i++) {

            // If the current
            // character is 1
            if (S[i] == '1') {

                // Update cntConOne
                cntConOne += 1;
            }
            else {

                // Update nimSum
                nimSum ^= cntConOne;

                // Update cntConOne
                cntConOne = 0;

                // Update cntZero
                cntZero++;
            }
        }

        // Update nimSum
        nimSum ^= cntConOne;

        // If countZero is
        // an even number
        if (cntZero % 2 == 0) {
            document.write("Tie");
        }

        // nimSum is not 0
        else if (nimSum != 0) {
            document.write("player 1");
        }

        // If nimSum is zero
        else {
            document.write("player 2");
        }
    }

    // Driver Code

           let S = "0110011";
        FindwinnerOfGame(S);

</script>
```

**Output:** 

```
player 2
```

***时间复杂度:** O(N)，其中 N 为弦的长度*
***辅助空间:** O(1)*