# 检查是否存在前 N 个自然数的排列，相邻元素的位“与”非零

> 原文:[https://www . geeksforgeeks . org/check-first-n-自然数的排列是否存在-相邻元素的按位和-非零/](https://www.geeksforgeeks.org/check-if-permutation-of-first-n-natural-numbers-exists-having-bitwise-and-of-adjacent-elements-non-zero/)

给定一个整数 **N** ，任务是检查第一个 **N** 自然数**【1，N】**是否存在任何排列，使得任何一对连续元素的[位与](https://www.geeksforgeeks.org/bitwise-and-or-of-a-range/)不等于 **0** 。如果存在这样的排列，打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** 5
> **输出:**是
> **说明:**排列{2，3，1，5，4}满足条件。
> 
> **输入:** 4
> **输出:**否
> **说明:**因为 4 和 3 的按位 AND 等于 0，所以不能相邻放置。类似地，2 和 4，1 和 2，1 和 4 不能相邻放置。因此，不存在这样的排列。

**方法:**根据以下观察结果可以解决问题:

*   如果 **N** 是两个的[幂，那么**N&(N–1)**等于 **0** 。因此，不存在可能的解决方案。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)
*   否则，置换是存在的。

所以要解决问题，只需[检查 **N** 是 **2** 的幂还是不是](https://www.geeksforgeeks.org/java-program-to-find-whether-a-no-is-power-of-two/)的幂。如果发现是假的，打印“**是**”。否则，打印“**否**”。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a permutation
// of first N natural numbers exist
// with Bitwise AND of adjacent
// elements not equal to 0
void check(int n)
{
    // If n is a power of 2
    if ((n & n - 1) != 0)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}

// Driver Code
int main()
{

    int n = 5;
    check(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class solution{

// Function to check if a
// permutation of first N
// natural numbers exist
// with Bitwise AND of adjacent
// elements not equal to 0
static void check(int n)
{
  // If n is a power of 2
  if ((n & n - 1) != 0)
    System.out.println("YES");
  else
    System.out.println("NO");
}

// Driver Code
public static void main(String args[])
{
  int n = 5;
  check(n);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a permutation
# of first N natural numbers exist
# with Bitwise AND of adjacent
# elements not equal to 0
def check(n):

    # If n is a power of 2
    if ((n & n - 1) != 0):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':

    n = 5

    check(n)

# This code is contributed by bgangwar59
```

## C#

```
// C# Program to implement
// the above approach
using System;
class solution{

// Function to check if a
// permutation of first N
// natural numbers exist
// with Bitwise AND of adjacent
// elements not equal to 0
static void check(int n)
{
  // If n is a power of 2
  if ((n & n - 1) != 0)
    Console.WriteLine("YES");
  else
    Console.WriteLine("NO");
}

// Driver Code
public static void Main(String []args)
{
  int n = 5;
  check(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if a
// permutation of first N
// natural numbers exist
// with Bitwise AND of adjacent
// elements not equal to 0
function check(n)
{

    // If n is a power of 2
    if ((n & n - 1) != 0)
        document.write("YES");
    else
        document.write("NO");
}

// Driver Code
var n = 5;

check(n);

// This code is contributed by umadevi9616

</script>
```

**Output**

```
YES
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)