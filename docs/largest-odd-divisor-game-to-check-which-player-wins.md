# 最大奇数除数游戏检查哪个玩家赢

> 原文:[https://www . geesforgeks . org/最大奇数除数游戏检查哪个玩家获胜/](https://www.geeksforgeeks.org/largest-odd-divisor-game-to-check-which-player-wins/)

两个玩家正在玩一个以**数字 n** 开始的游戏。在每一回合中，玩家可以进行任何一个后续动作:

*   将 n 除以大于 1 的任何奇数除数。数的除数包括数本身。
*   如果 n > k，从 n 中减去 1，其中 k < n。

玩家 1 进行主要移动，如果玩家 1 获胜，则打印“是”,否则如果两者都以最佳方式玩，则打印“否”。不能移动的玩家输掉游戏。
**例:**

> **输入:** n = 12，k = 1
> **输出:**是
> **解释:**
> 玩家 1 第一步= 12 / 3 = 4
> 玩家 2 第一步= 4–1 = 3
> 玩家 1 第二步= 3 / 3 = 1
> 玩家 2 第二步可以完成，因此他输了。
> **输入:** n = 1，k = 1
> **输出:**否
> **说明:**
> 1 号玩家第一招不可能，因为 n = k，因此 1 号玩家输。

**方法:**思路是针对以下 3 种情况分析问题:

*   当整数 **n 为奇数**时，玩家 1 可以自己除 n，因为它是奇数，所以 n / n = 1，玩家 2 输。注意这里 n = 1 是个例外。
*   当整数 **n 是偶数并且没有大于 1 的奇数除数**时，则 n 的形式为 2 <sup>x</sup> 。玩家 1 必然会用 1 减去 n，使 n 为奇数。所以如果 x > 1，玩家 2 赢。请注意，对于 x = 1，n–1 等于 1，因此玩家 1 获胜。
*   当**整数 n 是偶数并且有奇数除数**时，任务仍然是检查 n 是否能被 4 整除，然后玩家 1 可以用它最大的奇数因子除 n，之后 n 变成形式 2 <sup>x</sup> ，其中 x > 1，所以玩家 1 再次获胜。
*   否则，n 必须是 **2 * p** 的形式，其中 p 为奇数。如果 **p 是质数**，玩家 1 输了，因为他可以将 n 减 1 或者除以 p，这两种情况对他来说都是输的。如果 **p 不是质数**，那么 p 必须是 p1 * p2 的形式，其中 p1 是质数，p2 是任意奇数> 1，玩家 1 可以通过 n 除以 p2 获胜。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// Largest Odd Divisor Game to
// check which player wins
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Largest Odd Divisor Game to
// check which player wins
void findWinner(int n, int k)
{
    int cnt = 0;

    // Check if n == 1 then
    // player 2 will win
    if (n == 1)
        cout << "No" << endl;

    // Check if n == 2 or n is odd
    else if ((n & 1) or n == 2)
        cout << "Yes" << endl;

    else {
        int tmp = n;
        int val = 1;

        // While n is greater than k and
        // divisible by 2 keep
        // incrementing tha val
        while (tmp > k and tmp % 2 == 0) {
            tmp /= 2;
            val *= 2;
        }

        // Loop to find greatest
        // odd divisor
        for (int i = 3; i <= sqrt(tmp); i++) {
            while (tmp % i == 0) {
                cnt++;
                tmp /= i;
            }
        }
        if (tmp > 1)
            cnt++;

        // Check if n is a power of 2
        if (val == n)
            cout << "No" << endl;

        else if (n / tmp == 2 and cnt == 1)
            cout << "No" << endl;

        // Check if cnt is not one
        // then player 1 wins
        else
            cout << "Yes" << endl;
    }
}

// Driver code
int main()
{
    long long n = 1, k = 1;
    findWinner(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Largest Odd Divisior Game to
// check which player wins
import java.util.*;

class GFG{

// Function to find the
// Largest Odd Divisior Game to
// check which player wins
public static void findWinner(int n, int k)
{
    int cnt = 0;

    // Check if n == 1 then
    // player 2 will win
    if (n == 1)
        System.out.println("No");

    // Check if n == 2 or n is odd
    else if ((n & 1) != 0 || n == 2)
        System.out.println("Yes");

    else
    {
        int tmp = n;
        int val = 1;

        // While n is greater than k and
        // divisible by 2 keep
        // incrementing tha val
        while (tmp > k && tmp % 2 == 0)
        {
            tmp /= 2;
            val *= 2;
        }

        // Loop to find greatest
        // odd divisor
        for(int i = 3;
                i <= Math.sqrt(tmp); i++)
        {
           while (tmp % i == 0)
           {
               cnt++;
               tmp /= i;
           }
        }
        if (tmp > 1)
            cnt++;

        // Check if n is a power of 2
        if (val == n)
            System.out.println("No");

        else if (n / tmp == 2 && cnt == 1)
            System.out.println("No");

        // Check if cnt is not one
        // then player 1 wins
        else
            System.out.println("Yes");
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 1, k = 1;

    findWinner(n, k);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 implementation to find 
# the Largest Odd Divisor Game
# to check which player wins
import math 

# Function to find the Largest
# Odd Divisor Game to check
# which player wins
def findWinner(n, k):

    cnt = 0;

    # Check if n == 1 then
    # player 2 will win
    if (n == 1):
        print("No");

    # Check if n == 2 or n is odd
    elif ((n & 1) or n == 2):
        print("Yes");

    else:
        tmp = n;
        val = 1;

        # While n is greater than k and
        # divisible by 2 keep
        # incrementing tha val
        while (tmp > k and tmp % 2 == 0):
            tmp //= 2;
            val *= 2;

        # Loop to find greatest
        # odd divisor
        for i in range(3, int(math.sqrt(tmp)) + 1):
            while (tmp % i == 0):
                cnt += 1;
                tmp //= i;

        if (tmp > 1):
            cnt += 1;

        # Check if n is a power of 2
        if (val == n):
            print("No");

        elif (n / tmp == 2 and cnt == 1):
            print("No");

        # Check if cnt is not one
        # then player 1 wins
        else:
            print("Yes");

# Driver code
if __name__ == "__main__":

    n = 1; k = 1;

    findWinner(n, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// Largest Odd Divisior Game to
// check which player wins
using System;

class GFG{

// Function to find the
// Largest Odd Divisior Game to
// check which player wins
public static void findWinner(int n, int k)
{
    int cnt = 0;

    // Check if n == 1 then
    // player 2 will win
    if (n == 1)
        Console.Write("No");

    // Check if n == 2 or n is odd
    else if ((n & 1) != 0 || n == 2)
        Console.Write("Yes");

    else
    {
        int tmp = n;
        int val = 1;

        // While n is greater than k and
        // divisible by 2 keep
        // incrementing tha val
        while (tmp > k && tmp % 2 == 0)
        {
            tmp /= 2;
            val *= 2;
        }

        // Loop to find greatest
        // odd divisor
        for(int i = 3;
                i <= Math.Sqrt(tmp); i++)
        {
           while (tmp % i == 0)
           {
               cnt++;
               tmp /= i;
           }
        }
        if (tmp > 1)
            cnt++;

        // Check if n is a power of 2
        if (val == n)
            Console.Write("No");

        else if (n / tmp == 2 && cnt == 1)
            Console.Write("No");

        // Check if cnt is not one
        // then player 1 wins
        else
            Console.Write("Yes");
    }
}

// Driver code
public static void Main(string[] args)
{
    int n = 1, k = 1;

    findWinner(n, k);
}
}
// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// Largest Odd Divisior Game to
// check which player wins

// Function to find the
// Largest Odd Divisior Game to
// check which player wins
function findWinner(n, k)
{
    let cnt = 0;

    // Check if n == 1 then
    // player 2 will win
    if (n == 1)
        document.write("No");

    // Check if n == 2 or n is odd
    else if ((n & 1) != 0 || n == 2)
        document.write("Yes");

    else
    {
        let tmp = n;
        let val = 1;

        // While n is greater than k and
        // divisible by 2 keep
        // incrementing tha val
        while (tmp > k && tmp % 2 == 0)
        {
            tmp /= 2;
            val *= 2;
        }

        // Loop to find greatest
        // odd divisor
        for(let i = 3;
                i <= Math.sqrt(tmp); i++)
        {
           while (tmp % i == 0)
           {
               cnt++;
               tmp /= i;
           }
        }
        if (tmp > 1)
            cnt++;

        // Check if n is a power of 2
        if (val == n)
            document.write("No");

        else if (n / tmp == 2 && cnt == 1)
            document.write("No");

        // Check if cnt is not one
        // then player 1 wins
        else
            document.write("Yes");
    }
}

// Driver Code

    let n = 1, k = 1;

    findWinner(n, k);

   // This code is contributed by splevel62.
</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(sqrt(n))*
***辅助空间:** O(1)*