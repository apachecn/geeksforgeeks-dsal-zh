# 寻找移除奇数或替换偶数数组元素游戏的赢家

> 原文:[https://www . geeksforgeeks . org/寻找移除奇数或替换偶数数组元素游戏的赢家/](https://www.geeksforgeeks.org/find-the-winner-of-the-game-of-removing-odd-or-replacing-even-array-elements/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。两个玩家**玩家 1** 和**玩家 2** 轮流玩，其中一个玩家可以选择以下两个动作之一:

*   将偶数数组元素转换为任何其他整数。
*   移除奇数数组元素。

不能移动的玩家输掉游戏。任务是打印游戏的获胜者。打印 **-1** 如果游戏可能永远继续。

**示例:**

> **输入:** arr[] = {3，1，9，7}
> **输出:**玩家 2
> **说明:**由于所有阵元都是奇数，所以不可能转换。
> **回合 1:** 玩家 1 删除 3。
> **回合 2:** 玩家 2 删除 1。
> **转 3:** 玩家 1 删除 9。
> **回合 4:** 玩家 2 删除 7。现在，**玩家 1** 已经没有招式了。因此**玩家 2** 赢得游戏。
> 
> **输入:** arr[]={4，8}
> **输出:** -1

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   [统计数组中出现的偶数和奇数元素的数量](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)。
*   如果偶数元素的数量为**零**，执行以下操作:
    *   如果奇数计数为偶数，则**玩家 2** 将赢得游戏。
    *   否则**玩家 1** 将赢得游戏。
*   如果奇数计数为奇数，并且数组中只有一个偶数元素，则**玩家 1** 将赢得游戏。
*   否则每次都会有平局。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to evaluate the
// winner of the game
void findWinner(int arr[], int N)
{
    // Stores count of odd
    // array elements
    int odd = 0;

    // Stores count of even
    // array elements
    int even = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If array element is odd
        if (arr[i] % 2 == 1) {

            odd++;
        }
        // Otherwise
        else {

            even++;
        }
    }

    // If count of even is zero
    if (even == 0) {

        // If count of odd is even
        if (odd % 2 == 0) {

            cout << "Player 2" << endl;
        }

        // If count of odd is odd
        else if (odd % 2 == 1) {

            cout << "Player 1" << endl;
        }
    }

    // If count of odd is odd and
    // count of even is one
    else if (even == 1 && odd % 2 == 1) {

        cout << "Player 1" << endl;
    }

    // Otherwise
    else {

        cout << -1 << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 9, 7 };
    int N = sizeof(arr)
            / sizeof(arr[0]);

    findWinner(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to evaluate the
// winner of the game
static void findWinner(int arr[], int N)
{

    // Stores count of odd
    // array elements
    int odd = 0;

    // Stores count of even
    // array elements
    int even = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If array element is odd
        if (arr[i] % 2 == 1)
        {
            odd++;
        }

        // Otherwise
        else
        {
            even++;
        }
    }

    // If count of even is zero
    if (even == 0)
    {

        // If count of odd is even
        if (odd % 2 == 0)
        {
            System.out.println("Player 2");
        }

        // If count of odd is odd
        else if (odd % 2 == 1)
        {
            System.out.println("Player 1");
        }
    }

    // If count of odd is odd and
    // count of even is one
    else if (even == 1 && odd % 2 == 1)
    {
        System.out.println("Player 1");
    }

    // Otherwise
    else
    {
        System.out.println(-1);
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 3, 1, 9, 7 };
    int N = arr.length;

    findWinner(arr, N);
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to evaluate the
# winner of the game
def findWinner(arr, N):

    # Stores count of odd
    # array elements
    odd = 0

    # Stores count of even
    # array elements
    even = 0

    # Traverse the array
    for i in range(N):

        # If array element is odd
        if (arr[i] % 2 == 1):
            odd += 1

        # Otherwise
        else:
            even += 1

    # If count of even is zero
    if (even == 0):

        # If count of odd is even
        if (odd % 2 == 0):
            print("Player 2")

        # If count of odd is odd
        elif (odd % 2 == 1):
            print("Player 1")

    # If count of odd is odd and
    # count of even is one
    elif (even == 1 and odd % 2 == 1):
        print("Player 1")

    # Otherwise
    else:
        print(-1)

# Driver code
if __name__ == '__main__':

    arr = [ 3, 1, 9, 7 ]
    N = len(arr)

    findWinner(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to evaluate the
// winner of the game
static void findWinner(int []arr, int N)
{

    // Stores count of odd
    // array elements
    int odd = 0;

    // Stores count of even
    // array elements
    int even = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If array element is odd
        if (arr[i] % 2 == 1)
        {
            odd++;
        }

        // Otherwise
        else
        {
            even++;
        }
    }

    // If count of even is zero
    if (even == 0)
    {

        // If count of odd is even
        if (odd % 2 == 0)
        {
            Console.WriteLine("Player 2");
        }

        // If count of odd is odd
        else if (odd % 2 == 1)
        {
            Console.WriteLine("Player 1");
        }
    }

    // If count of odd is odd and
    // count of even is one
    else if (even == 1 && odd % 2 == 1)
    {
        Console.WriteLine("Player 1");
    }

    // Otherwise
    else
    {
        Console.WriteLine(-1);
    }
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 1, 9, 7 };
    int N = arr.Length;

    findWinner(arr, N);
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to evaluate the
// winner of the game
function findWinner(arr, N)
{

    // Stores count of odd
    // array elements
    let odd = 0;

    // Stores count of even
    // array elements
    let even = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // If array element is odd
        if (arr[i] % 2 == 1)
        {
            odd++;
        }

        // Otherwise
        else
        {
            even++;
        }
    }

    // If count of even is zero
    if (even == 0)
    {

        // If count of odd is even
        if (odd % 2 == 0)
        {
            document.write("Player 2");
        }

        // If count of odd is odd
        else if (odd % 2 == 1)
        {
            document.write("Player 1");
        }
    }

    // If count of odd is odd and
    // count of even is one
    else if (even == 1 && odd % 2 == 1)
    {
        document.write("Player 1");
    }

    // Otherwise
    else
    {
        document.write(-1);
    }
}

// Driver Code

    let arr = [ 3, 1, 9, 7 ];
    let N = arr.length;

    findWinner(arr, N);

</script>
```

**Output:** 

```
Player 2
```

***时间复杂度:**O(N)*
T5**辅助空间** : O(1)