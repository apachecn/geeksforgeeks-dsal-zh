# 将 N 表示为 K 个偶数的和

> 原文:[https://www . geesforgeks . org/represent-n-as-sum-k-偶数/](https://www.geeksforgeeks.org/represent-n-as-sum-of-k-even-numbers/)

给定两个整数 **N** 和 **K** ，任务是将 N 表示为 K 个偶数的和。如果无法表示数字，请打印-1。
***注意:**表示可能包含重复的偶数。*

**示例:**

> **输入:** N = 6，K = 3
> **输出:** 2 2 2
> **解释:**
> 给定数字 6 可以表示为 2 + 2 + 2 = 6
> **输入:** N = 8，K = 2
> **输出:** 2 6
> **解释:**
> 给定数字 3 可以表示为 2 + 6 = 8

**方法:**解决上述问题的一个简单方法是最大化最小偶数 2 的出现。将 N 表示为 K 个数之和的必要条件是:

*   **(K–1)* 2**必须小于 n
*   **N –( K–1)* 2**必须为偶数。

下面是上述方法的实现:

## C++

```
// C++ implementation to represent
// N as sum of K even numbers

#include <bits/stdc++.h>
using namespace std;

// Function to print the representation
void sumEvenNumbers(int N, int K)
{
    int check = N - 2 * (K - 1);

    // N must be greater than equal to 2*K
    // and must be even
    if (check > 0 && check % 2 == 0) {
        for (int i = 0; i < K - 1; i++) {
            cout << "2 ";
        }
        cout << check;
    }
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    int N = 8;
    int K = 2;

    sumEvenNumbers(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to represent
// N as sum of K even numbers
import java.util.*;

class GFG{

// Function to print the representation
static void sumEvenNumbers(int N, int K)
{
    int check = N - 2 * (K - 1);

    // N must be greater than equal to 2 * K
    // and must be even
    if (check > 0 && check % 2 == 0)
    {
        for(int i = 0; i < K - 1; i++)
        {
           System.out.print("2 ");
        }
        System.out.println(check);
    }
    else
    {
        System.out.println("-1");
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 8;
    int K = 2;

    sumEvenNumbers(N, K);
}
}

// This code is contributed by ANKITKUMAR34
```

## 蟒蛇 3

```
# Python3 implementation to represent
# N as sum of K even numbers

# Function to print the representation
def sumEvenNumbers(N, K):

    check = N - 2 * (K - 1)

    # N must be greater than equal to 2 * K
    # and must be even
    if (check > 0 and check % 2 == 0):
        for i in range(K - 1):
            print("2 ", end = "")

        print(check)
    else:
        print("-1")

# Driver Code
N = 8
K = 2
sumEvenNumbers(N, K)

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# implementation to represent
// N as sum of K even numbers
using System;

class GFG{

// Function to print the representation
static void sumEvenNumbers(int N, int K)
{
    int check = N - 2 * (K - 1);

    // N must be greater than equal to
    //  2 * K and must be even
    if (check > 0 && check % 2 == 0)
    {
        for(int i = 0; i < K - 1; i++)
        {
           Console.Write("2 ");
        }
        Console.WriteLine(check);
    }
    else
    {
        Console.WriteLine("-1");
    }
}

// Driver Code
static public void Main(String []args)
{
    int N = 8;
    int K = 2;

    sumEvenNumbers(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to represent
// N as sum of K even numbers

// Function to prlet the representation
function sumEvenNumbers(N, K)
{
    let check = N - 2 * (K - 1);

    // N must be greater than equal to 2 * K
    // and must be even
    if (check > 0 && check % 2 == 0)
    {
        for(let i = 0; i < K - 1; i++)
        {
           document.write("2 ");
        }
        document.write(check);
    }
    else
    {
        document.write("-1");
    }
}

// Driver Code

       let N = 8;
    let K = 2;

    sumEvenNumbers(N, K);

</script>
```

**Output:** 

```
2 6
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*