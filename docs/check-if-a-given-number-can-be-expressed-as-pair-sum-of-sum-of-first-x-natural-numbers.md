# 检查给定的数是否可以表示为前 X 个自然数之和的对和

> 原文:[https://www . geeksforgeeks . org/check-如果给定的数字可以表示为第一个 x 个自然数的对和之和/](https://www.geeksforgeeks.org/check-if-a-given-number-can-be-expressed-as-pair-sum-of-sum-of-first-x-natural-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否为一对整数之和，可以表示为第一个 **X** 自然数之和，其中 **X** 可以是任意正整数。如果满足要求的条件。打印“是”。否则，打印“否”。

**示例:**

> **输入:** N = 25
> **输出:** YES
> **解释:**
> = > 10 + 15 = 25
> 由于 10 和 15 分别是前 4 和 5 个自然数的和，所以答案是 YES。
> 
> **输入:**N = 512
> T3】输出:否

**方法:**思路是选择一个小于等于 **N** 的自然数之和 **M** ，检查 **M** 和**N–M**是否为前几个自然数的序列之和。按照以下步骤解决问题:

*   循环迭代计算 **K** 个自然数之和:

> K 个自然数之和= K * (K + 1) / 2

*   然后，计算剩余总和，并通过以下等式检查总和是否为总和:

> Y = N–K 个自然数之和
> =>Y = N –( K *(K+1)/2)

*   通过计算两次数的平方根，检查上面计算的数是否满足要求的条件，并检查连续数的乘积是否等于两次数。

> M *(M+1)= 2 * Y，其中 M = √ (2 * Y)

*   如果满足上述条件，则打印“是”。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if the number
// is pair-sum of sum of first X
// natural numbers
void checkSumOfNatural(int n)
{
    int i = 1;
    bool flag = false;

    // Check if the given number
    // is sum of pair of special numbers
    while (i * (i + 1) < n * 2)
    {

        // X is the sum of first
        // i natural numbers
        int X = i * (i + 1);

        // t = 2 * Y
        int t = n * 2 - X;
        int k = sqrt(t);

        // Condition to check if
        // Y is a special number
        if (k * (k + 1) == t)
        {
            flag = true;
            break;
        }
        i += 1;
    }

    if (flag)
        cout << "YES";
    else
        cout << "NO";
}

// Driver Code
int main()
{
    int n = 25;

    // Function call
    checkSumOfNatural(n);

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to check if the number
// is pair-sum of sum of first X
// natural numbers
static void checkSumOfNatural(int n)
{
    int i = 1;
    boolean flag = false;

    // Check if the given number
    // is sum of pair of special numbers
    while (i * (i + 1) < n * 2)
    {

        // X is the sum of first
        // i natural numbers
        int X = i * (i + 1);

        // t = 2 * Y
        int t = n * 2 - X;
        int k = (int)Math.sqrt(t);

        // Condition to check if
        // Y is a special number
        if(k * (k + 1) == t)
        {
            flag = true;
            break;
        }
        i += 1;
    }

    if (flag)
        System.out.println("YES");
    else
        System.out.println("NO");
}

// Driver Code
public static void main (String[] args)
{
    int n = 25;

    // Function call
    checkSumOfNatural(n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

import math

# Function to check if the number
# is pair-sum of sum of first X
# natural numbers
def checkSumOfNatural(n):
    i = 1
    flag = False

    # Check if the given number
    # is sum of pair of special numbers
    while i*(i + 1) < n * 2:

        # X is the sum of first
        # i natural numbers
        X = i*(i + 1)

        # t = 2 * Y
        t = n * 2 - X
        k = int(math.sqrt(t))

        # Condition to check if
        # Y is a special number
        if k*(k + 1) == t:
            flag = True
            break
        i += 1

    if flag:
        print('YES')
    else:
        print('NO')

# Driver Code       
if __name__ == "__main__":
    n = 25

    # Function Call
    checkSumOfNatural(n)
```

## C#

```
// C# program of
// the above approach
using System;
class GFG{

// Function to check if the number
// is pair-sum of sum of first X
// natural numbers
static void checkSumOfNatural(int n)
{
  int i = 1;
  bool flag = false;

  // Check if the given number
  // is sum of pair of special numbers
  while (i * (i + 1) < n * 2)
  {
    // X is the sum of first
    // i natural numbers
    int X = i * (i + 1);

    // t = 2 * Y
    int t = n * 2 - X;
    int k = (int)Math.Sqrt(t);

    // Condition to check if
    // Y is a special number
    if(k * (k + 1) == t)
    {
      flag = true;
      break;
    }
    i += 1;
  }

  if (flag)
    Console.WriteLine("YES");
  else
    Console.WriteLine("NO");
}

// Driver Code
public static void Main(String[] args)
{
  int n = 25;

  // Function call
  checkSumOfNatural(n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program of the above approach// Function to check if the number
// is pair-sum of sum of first X
// natural numbers
function checkSumOfNatural(n)
{
    var i = 1;
    var flag = false;

    // Check if the given number
    // is sum of pair of special numbers
    while (i * (i + 1) < n * 2)
    {

        // X is the sum of first
        // i natural numbers
        var X = i * (i + 1);

        // t = 2 * Y
        var t = n * 2 - X;
        var k = parseInt(Math.sqrt(t));

        // Condition to check if
        // Y is a special number
        if(k * (k + 1) == t)
        {
            flag = true;
            break;
        }
        i += 1;
    }

    if (flag)
        document.write("YES");
    else
        document.write("NO");
}

// Driver Code
var n = 25;

// Function call
checkSumOfNatural(n);

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)