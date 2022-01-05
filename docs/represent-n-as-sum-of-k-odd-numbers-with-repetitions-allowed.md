# 将 N 表示为 K 个奇数的和，允许重复

> 原文:[https://www . geesforgeks . org/representative-n-as-sum-k-奇数-允许重复/](https://www.geeksforgeeks.org/represent-n-as-sum-of-k-odd-numbers-with-repetitions-allowed/)

给定两个整数 **N** 和 **K** ，任务是将 **N** 表示为 **K** 奇数的和。如果无法创建总和，则输出 **-1** 。
***注:**表示可能包含重复的奇数。*
**例:**

> **输入:** N = 5，K = 3
> **输出:** 1，1，3
> **解释:**
> 给定数字 N 可以表示为 1 + 1 + 3 = 5
> **输入:** N = 7，K = 5
> **输出:** 1，1，1，1，3
> **解释:**
> 给定数字 N 可以表示为 1 + 1

**方法:**
要解决上述问题，一个简单的解决方案是**最大化 1** 的出现，这是可能的最小奇数。将数字 N 表示为 K 个奇数的必要条件是:

*   **(K–1)**必须小于 n
*   **N –( K–1)**必须是奇数。

以下是上述方法的实现:

## C++

```
// C++ implementation to represent
// N as sum of K even numbers

#include <bits/stdc++.h>

using namespace std;

// Function to print the representation
void sumOddNumbers(int N, int K)
{
    int check = N - (K - 1);

    // N must be greater than equal to 2*K
    // and must be odd
    if (check > 0 && check % 2 == 1) {
        for (int i = 0; i < K - 1; i++) {
            cout << "1 ";
        }
        cout << check;
    }
    else
        cout << "-1";
}

// Driver Code
int main()
{

    int N = 5;
    int K = 3;

    sumOddNumbers(N, K);
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
static void sumOddNumbers(int N, int K)
{
    int check = N - (K - 1);

    // N must be greater than equal 
    // to 2*K and must be odd
    if (check > 0 && check % 2 == 1)
    {
        for(int i = 0; i < K - 1; i++)
        {
           System.out.print("1 ");
        }
        System.out.print(+check);
    }
    else
        System.out.println("-1 ");
}

// Driver Code
public static void main(String args[])
{
    int N = 5;
    int K = 3;

    sumOddNumbers(N, K);
}
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 implementation to represent 
# N as sum of K even numbers 

# Function to print the representation 
def sumOddNumbers(N, K):

    check = N - (K - 1) 

    # N must be greater than equal  
    # to 2*K and must be odd 
    if (check > 0 and check % 2 == 1): 
        for i in range(0, K - 1): 
            print("1", end = " ") 

        print(check, end = " ") 

    else:
        print("-1") 

# Driver Code 
N = 5
K = 3; 

sumOddNumbers(N, K) 

# This code is contributed by PratikBasu    
```

## C#

```
// C# implementation to represent
// N as sum of K even numbers
using System;

class GFG{

// Function to print the representation
static void sumOddNumbers(int N, int K)
{
    int check = N - (K - 1);

    // N must be greater than equal 
    // to 2*K and must be odd
    if (check > 0 && check % 2 == 1)
    {
        for(int i = 0; i < K - 1; i++)
        {
           Console.Write("1 ");
        }
        Console.Write(+check);
    }
    else
        Console.WriteLine("-1 ");
}

// Driver Code
public static void Main()
{
    int N = 5;
    int K = 3;

    sumOddNumbers(N, K);
}
}

// This code is contributed by Code_Mech
```

## Java Script 语言

```
<script>

// Javascript implementation to represent
// N as sum of K even numbers

// Function to print the representation
function sumOddNumbers(N, K)
{
    var check = N - (K - 1);
    var i;

    // N must be greater than equal to 2*K
    // and must be odd
    if (check > 0 && check % 2 == 1) {
        for (i = 0; i < K - 1; i++) {
             document.write("1,"+" ");
        }
        document.write(check + " ");
    }
    else
        document.write("-1");
}

// Driver Code
    var N = 5;
    var K = 3;

    sumOddNumbers(N, K);

</script>
```

**Output:** 

```
1 1 3
```

***时间复杂度:**O(K)*T4】