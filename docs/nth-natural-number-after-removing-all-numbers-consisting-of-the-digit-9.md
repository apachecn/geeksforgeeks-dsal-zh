# 去掉所有数字 9 后的第 n 个自然数

> 原文:[https://www . geesforgeks . org/n-移除所有数字后的自然数-由数字 9 组成/](https://www.geeksforgeeks.org/nth-natural-number-after-removing-all-numbers-consisting-of-the-digit-9/)

给定一个正整数 **N** ，任务是在去掉所有包含数字 **9** 的自然数后，找到第 **N <sup>第</sup>T5】个自然数。**

**示例:**

> **输入:** N = 8
> **输出:** 8
> **解释:**
> 由于 9 是第一个包含数字 9 的自然数，是第 9 个自然数，因此不需要移除即可找到第 8 个<sup>第</sup>自然数，即 8。
> 
> **输入:** N = 9
> **输出:** 10
> **解释:**
> 去掉数字 9，前 9 个自然数为{1，2，3，4，5，6，7，8，10}。
> 因此，第 9 个<sup>自然数为 10。</sup>

**天真法:**解决上述问题最简单的方法是向上迭代到 **N** 并保持排除所有小于包含数字 **9 的 **N** 的数字。**最后打印得到的 **N** <sup>th</sup> 自然数。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:** 上述方法可以基于以下观察进行优化:

> *   It is understood that the number of digits of radix **2** ranges from **0** to **1** . Similarly, the number of digits of the radix **10** ranges from **0** to **9** .
> *   Therefore, the number of digits of radix **9** will vary from **0** to **8** .
> *   It can be observed that **n <sup>the</sup> th** number is equal to **n <sup>the</sup> th** number in the radix **9** after skipping the number containing the number **9** .
> *   Therefore, the task is simplified to find the base **9** which is equivalent to **n.** t42.

按照以下步骤解决问题:

*   初始化两个变量，比如 **res = 0** 和 **p = 1** 、**T5】将数字存储在基数 **9** 中并存储一个数字的位置。**
*   当 **N** 大于 **0** 时迭代，执行以下操作:
    *   将 **res** 更新为 **res = res + p*(N%9)** 。
    *   将 **N** 除以 **9** ，将 **p** 乘以 **10。**
*   完成以上步骤后，打印 **res** 的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find Nth number in base 9
long long findNthNumber(long long N)
{
    // Stores the Nth number
    long long result = 0;

    long long p = 1;

    // Iterate while N is
    // greater than 0
    while (N > 0) {

        // Update result
        result += (p * (N % 9));

        // Divide N by 9
        N = N / 9;

        // Multiply p by 10
        p = p * 10;
    }
    // Return result
    return result;
}

// Driver Code
int main()
{
    int N = 9;
    cout << findNthNumber(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to find Nth number in base 9
  static long findNthNumber(long N)
  {

    // Stores the Nth number
    long result = 0;

    long p = 1;

    // Iterate while N is
    // greater than 0
    while (N > 0) {

      // Update result
      result += (p * (N % 9));

      // Divide N by 9
      N = N / 9;

      // Multiply p by 10
      p = p * 10;
    }

    // Return result
    return result;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 9;
    System.out.print(findNthNumber(N));
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to find Nth number in base 9
def findNthNumber(N):

    # Stores the Nth number
    result = 0
    p = 1

    # Iterate while N is
    # greater than 0
    while (N > 0):

        # Update result
        result += (p * (N % 9))

        # Divide N by 9
        N = N // 9

        # Multiply p by 10
        p = p * 10
    # Return result
    return result

# Driver Code
if __name__ == '__main__':
    N = 9
    print(findNthNumber(N))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{
  // Function to find Nth number in base 9
  static long findNthNumber(long N)
  {
    // Stores the Nth number
    long result = 0;

    long p = 1;

    // Iterate while N is
    // greater than 0
    while (N > 0) {

      // Update result
      result += (p * (N % 9));

      // Divide N by 9
      N = N / 9;

      // Multiply p by 10
      p = p * 10;
    }

    // Return result
    return result;
  }

  // Driver code 
  static void Main ()
  {
    int N = 9;
    Console.Write(findNthNumber(N));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function to find Nth number in base 9
    function findNthNumber(N)
    {
      // Stores the Nth number
      let result = 0;

      let p = 1;

      // Iterate while N is
      // greater than 0
      while (N > 0) {

        // Update result
        result += (p * (N % 9));

        // Divide N by 9
        N = parseInt(N / 9, 10);

        // Multiply p by 10
        p = p * 10;
      }

      // Return result
      return result;
    }

    let N = 9;
    document.write(findNthNumber(N));

</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(log<sub>9</sub>N)*
*T8】辅助空间: O(1)*