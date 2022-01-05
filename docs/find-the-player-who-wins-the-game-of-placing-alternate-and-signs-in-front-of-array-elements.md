# 找到在阵元前放置交替+和–符号的游戏中获胜的玩家

> 原文:[https://www . geeksforgeeks . org/find-在阵列元素前放置交替和标记游戏中获胜的玩家/](https://www.geeksforgeeks.org/find-the-player-who-wins-the-game-of-placing-alternate-and-signs-in-front-of-array-elements/)

给定一个长度为 **N** 的[阵](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是通过执行以下操作来最佳地找到由两个玩家 **A** 和 **B** 玩的游戏的获胜者:

*   玩家 **A** 先动。
*   玩家需要轮流在阵元前交替放置 **+** 和**–**符号。
*   在所有数组元素前放置符号后，如果所有元素的差为偶数，玩家 **A** 获胜。
*   否则，玩家 **B** 获胜。

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** B
> **解释:**
> 游戏可以进行的所有可能方式为:
> (+1)–(+2)=-1
> (1)–(+2)=-3
> (+1)–(-2)= 3
> (-1)–(-2)= 1
> 由于所有可能性的差异都是奇数，B 获胜。
> 
> **输入:** arr[] = {1，1， 2}
> **输出:** A
> **说明:**
> 游戏可以玩出的所有可能方式有:
> (1)–(1)–(2)=-2
> (1)–(2)=-2
> (1)–(1)–(2)= 0
> (1)–(1)–(2)= 4
> (-1)–(2)=-4【T14

**天真法:**最简单的方法是生成所有可能的 2 <sup>N</sup> 组合，其中的符号可以放在数组中并检查每个组合，检查玩家 A 是否能赢。如果发现任何排列都为真，则打印 **A.** 否则，玩家 **B** 获胜。

***时间复杂度:**O(2<sup>N</sup>* N)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤优化上述方法:

*   初始化一个变量，比如 **diff** ，来存储数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，在索引**【1，N】**的范围内，通过减去 **arr[i]** 来更新 **diff** 。
*   如果发现**差值% 2** 等于 **0** ，则打印**‘A’**。否则，打印**【B】**。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check which
// player wins the game
void checkWinner(int arr[], int N)
{
    // Stores the difference between
    // +ve and -ve array elements
    int diff = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        // Update diff
        diff -= arr[i];
    }

    // Checks if diff is even
    if (diff % 2 == 0) {
        cout << "A";
    }
    else {
        cout << "B";
    }
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to check
    // which player wins the game
    checkWinner(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check which
# player wins the game
def checkWinner(arr, N):

    # Stores the difference between
    # +ve and -ve array elements
    diff = 0

    # Traverse the array
    for i in range(N):
        # Update diff
        diff -= arr[i]

    # Checks if diff is even
    if (diff % 2 == 0):
        print("A")

    else:
        print("B")

# Driver Code
if __name__ == "__main__":

    # Given Input
    arr = [1, 2]
    N = len(arr)

    # Function call to check
    # which player wins the game
    checkWinner(arr, N)

    # This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG
{
// Function to check which
// player wins the game
static void checkWinner(int arr[], int N)
{
    // Stores the difference between
    // +ve and -ve array elements
    int diff = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        // Update diff
        diff -= arr[i];
    }

    // Checks if diff is even
    if (diff % 2 == 0) {
        System.out.println("A");
    }
    else {
        System.out.println("B");
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given Input
    int arr[] = { 1, 2 };
    int N = arr.length;
    // Function call to check
    // which player wins the game
    checkWinner(arr, N);
}
}

// This code is contributed by Stream-Cipher
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check which
// player wins the game
static void checkWinner(int[] arr, int N)
{

    // Stores the difference between
    // +ve and -ve array elements
    int diff = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update diff
        diff -= arr[i];
    }

    // Checks if diff is even
    if (diff % 2 == 0)
    {
        Console.Write("A");
    }
    else
    {
        Console.Write("B");
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    int[] arr = { 1, 2 };
    int N = arr.Length;

    // Function call to check
    // which player wins the game
    checkWinner(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to check which
// player wins the game
function checkWinner(arr, N)
{
    // Stores the difference between
    // +ve and -ve array elements
    let diff = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {
        // Update diff
        diff -= arr[i];
    }

    // Checks if diff is even
    if (diff % 2 == 0) {
        document.write("A");
    }
    else {
        document.write("B");
    }
}

// Driver Code

     // Given Input
    let arr = [ 1, 2 ];
    let N = arr.length;
    // Function call to check
    // which player wins the game
    checkWinner(arr, N);

</script>
```

**Output:** 

```
B
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)