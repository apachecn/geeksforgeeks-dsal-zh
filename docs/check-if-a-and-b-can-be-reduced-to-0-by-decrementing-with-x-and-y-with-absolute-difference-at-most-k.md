# 检查 A 和 B 是否可以用 x 和 y 递减到 0，绝对差值最多为 K

> 原文:[https://www . geeksforgeeks . org/check-if-a-和-b-可以通过 x-和-y-与-k-的绝对差值递减来减少到 0/](https://www.geeksforgeeks.org/check-if-a-and-b-can-be-reduced-to-0-by-decrementing-with-x-and-y-with-absolute-difference-at-most-k/)

给定三个整数 **A** 、 **B** 和 **K** 。任务是检查 **A** 和 **B** 是否可以通过从 A 和 B 分别递减 **x** 和 **y** 使**ABS(x–y)≤K**而降至**零**。

**示例:**

> **输入:** A = 2，B = 7，K = 3
> **输出:**是
> **说明:**减量值如下:
> 
> *   从 A 开始递减 1，从 B 开始递减 4，这样 ABS(1–4)≤3，因此，A = 1 和 B = 3 的当前值。
> *   从 A 开始递减 1，从 B 开始递减 3，这样 ABS(1–3)≤3，当前值 A = 0，B = 0。
> 
> 因此，可以将这两个数字都减少到 0。
> 
> **输入:** A = 9，B = 8，K = 0
> T3】输出:否

**进场:**简单的**观察**就可以解决任务。想法是从 A 和 B 中找出[最小](https://www.geeksforgeeks.org/stdmin-in-cpp/)和[最大](https://www.geeksforgeeks.org/stdmax-in-cpp/) ，如果**最小**数乘以( **1+K** )比**最大值**少**，那么将 A 和 B 转换为零的可能就是**而不是**，否则可以转换为零。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to reduce A and B to zero
bool isPossibleToReduce(int A, int B, int k)
{
    // Finding minimum and maximum
    // of A and B
    int mn = min(A, B);
    int mx = max(A, B);

    // If minimum multiply by (1+k)
    // is less than maximum then
    // return false
    if (mn * (1 + k) < mx) {
        return false;
    }

    // Else return true;
    return true;
}

// Driver Code
int main()
{
    int A = 2, B = 7;
    int K = 3;

    if (isPossibleToReduce(A, B, K))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG {

    /// Function to check if it is possible
    // to reduce A and B to zero
    static boolean isPossibleToReduce(int A, int B, int k)
    {

        // Finding minimum and maximum
        // of A and B
        int mn = Math.min(A, B);
        int mx = Math.max(A, B);

        // If minimum multiply by (1+k)
        // is less than maximum then
        // return false
        if (mn * (1 + k) < mx) {
            return false;
        }

        // Else return true;
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A = 2, B = 7;
        int K = 3;

        if (isPossibleToReduce(A, B, K))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python program for the above approach

# Function to check if it is possible
# to reduce A and B to zero
def isPossibleToReduce(A, B, k):

    # Finding minimum and maximum
    # of A and B
    mn = min(A, B)
    mx = max(A, B)

    # If minimum multiply by (1+k)
    # is less than maximum then
    # return false
    if (mn * (1 + k) < mx):
        return False

    # Else return true;
    return True

# Driver Code
if __name__ == "__main__":

    A = 2
    B = 7
    K = 3

    if (isPossibleToReduce(A, B, K)):
        print("YES")

    else:
        print("NO")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    /// Function to check if it is possible
    // to reduce A and B to zero
    static bool isPossibleToReduce(int A, int B, int k)
    {

        // Finding minimum and maximum
        // of A and B
        int mn = Math.Min(A, B);
        int mx = Math.Max(A, B);

        // If minimum multiply by (1+k)
        // is less than maximum then
        // return false
        if (mn * (1 + k) < mx) {
            return false;
        }

        // Else return true;
        return true;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int A = 2, B = 7;
        int K = 3;

        if (isPossibleToReduce(A, B, K))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if it is possible
// to reduce A and B to zero
function isPossibleToReduce(A, B, k)
{

  // Finding minimum and maximum
  // of A and B
  let mn = Math.min(A, B);
  let mx = Math.max(A, B);

  // If minimum multiply by (1+k)
  // is less than maximum then
  // return false
  if (mn * (1 + k) < mx) {
    return false;
  }

  // Else return true;
  return true;
}

// Driver Code

let A = 2,
  B = 7;
let K = 3;

if (isPossibleToReduce(A, B, K)) document.write("YES");
else document.write("NO");

// This code is contributed by gfgking.
</script>
```

**Output**

```
YES
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)