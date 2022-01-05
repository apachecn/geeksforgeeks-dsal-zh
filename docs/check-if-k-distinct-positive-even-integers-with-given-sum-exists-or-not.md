# 检查给定和的 K 个不同的正偶数是否存在

> 原文:[https://www . geesforgeks . org/check-if-k-distinct-正整数-带给定和-存在与否/](https://www.geeksforgeeks.org/check-if-k-distinct-positive-even-integers-with-given-sum-exists-or-not/)

给定两个整数 **N** 和 **K** ，任务是找出是否存在 **K** 个不同的正偶数，使得它们的和等于给定的数 N

**示例:**

> **输入:** N = 16，K = 3
> **输出:**是
> **说明:**和为 16 的三个截然不同的正偶数是 8、6 和 2。
> 既然有三个这样的数字，打印“是”。
> 
> **输入:** N = 18 K = 4
> **输出:**否
> **说明:**四个截然不同的正偶数之和不能等于 18。因此，打印“否”。

**方法:**解决这个问题的思路是观察如果 **N** **是** **奇数**，那么就不可能通过 **K** 偶数得到需要的 **N** 。如果 **N** 为偶数，则[求第一个 **K** 个偶数](https://www.geeksforgeeks.org/sum-first-n-even-numbers/)的和，如果它们的和小于或等于 **N** ，则打印“是”。否则，不存在和等于 **N** 的 **K** 相异偶数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find if the sum
// of K even integers equals N
void isPossibleN(int N, int K)
{

    // If N is odd, then its impossible
    // to obtain N from K even numbers
    if (N % 2 == 1) {
        cout << "NO" << endl;
        return;
    }

    // Sum first k even numbers
    int sum = K * (K + 1);

    // If sum is less then equal to N
    if (sum <= N) {
        cout << "YES" << endl;
    }

    // Otherwise
    else {
        cout << "No" << endl;
    }

    return;
}

// Driver Code
int main()
{

    int N = 16;
    int K = 3;

    isPossibleN(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

static void isPossibleN(int N, int K)
{

    // If N is odd, then its impossible
    // to obtain N from K even numbers
    if (N % 2 == 1) {
        System.out.println("NO");
        return;
    }

    // Sum first k even numbers
    int sum = K * (K + 1);

    // If sum is less then equal to N
    if (sum <= N) {
        System.out.println("YES");
    }

    // Otherwise
    else {
        System.out.println("No");
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 16;
    int K = 3;
    isPossibleN(N, K);
}
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find if the sum
# of K even integers equals N
def isPossibleN(N, K) :

    # If N is odd, then its impossible
    # to obtain N from K even numbers
    if (N % 2 == 1) :
        print("NO")
        return

    # Sum first k even numbers
    sum = K * (K + 1)

    # If sum is less then equal to N
    if (sum <= N) :
        print("YES")

    # Otherwise
    else :
        print("NO")

    return

# Driver Code

N = 16
K = 3

isPossibleN(N, K)
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG
{

  static void isPossibleN(int N, int K)
  {

    // If N is odd, then its impossible
    // to obtain N from K even numbers
    if (N % 2 == 1) {
      Console.WriteLine("NO");
      return;
    }

    // Sum first k even numbers
    int sum = K * (K + 1);

    // If sum is less then equal to N
    if (sum <= N) {
      Console.WriteLine("YES");
    }

    // Otherwise
    else {
      Console.WriteLine("No");
    }
  }

  // Driver Code
  public static void Main()
  {
    int N = 16;
    int K = 3;
    isPossibleN(N, K);
  }
}

// This code is contributed by jana_sayantan.
```

## java 描述语言

```
<script>
function isPossibleN( N,  K)
{

    // If N is odd, then its impossible
    // to obtain N from K even numbers
    if (N % 2 == 1) {
        document.write("NO");
        return;
    }

    // Sum first k even numbers
    let sum = K * (K + 1);

    // If sum is less then equal to N
    if (sum <= N) {
        document.write("YES");
    }

    // Otherwise
    else {
        document.write("No");
    }
}

// Driver Code

    let  N = 16;
    let  K = 3;
    isPossibleN(N, K);

//this code is contributed by sravan kumar
</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)