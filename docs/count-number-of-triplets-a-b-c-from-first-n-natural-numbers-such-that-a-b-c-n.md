# 从前 N 个自然数中计算三胞胎(a，b，c)的数量，使得 a * b + c = N

> 原文:[https://www . geesforgeks . org/count-三胞胎数量-a-b-c-从第一个-n-自然数-这样-a-b-c-n/](https://www.geeksforgeeks.org/count-number-of-triplets-a-b-c-from-first-n-natural-numbers-such-that-a-b-c-n/)

给定一个整数 **N** ，任务是从第一个 **N** 个自然数开始计算三胞胎( **a，b，c** )，使得 **a * b + c = N** 。

**示例:**

> **输入:** N = 3
> **输出:** 3
> **说明:**
> a * b+ c = N 形式的三元组为{ (1，1，2)，(1，2，1)，(2，1，1) }
> 因此，需要的输出为 3。
> 
> **输入:**N = 100
> T3】输出: 473

**方法:**根据以下观察可以解决问题:

> 对于每一个可能的对(a，b)，如果 a * b < N，那么只有 c 存在。因此，计算乘积小于 n 的对(a，b)

按照以下步骤解决问题:

*   初始化一个变量，比如说**个三元组**，来存储满足给定条件的第一个 **N 个**自然数的三元组计数。
*   使用变量 **i** 迭代范围**【1，N–1】**，检查 **N % i == 0** 与否。如果发现为真，则更新**碳三元组+=(不适用)–1**。
*   否则，更新**碳三元组+= (N / i)。**
*   最后，打印**碳三元组**的值。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// triplets (a, b, c) with a * b + c = N
int findCntTriplet(int N)
{
    // Stores count of triplets of 1st
    // N natural numbers which are of
    // the form a * b + c = N
    int cntTriplet = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i < N; i++) {

        // If N is divisible by i
        if (N % i != 0) {

            // Update cntTriplet
            cntTriplet += N / i;
        }
        else {

            // Update cntTriplet
            cntTriplet += (N / i) - 1;
        }
    }
    return cntTriplet;
}

// Driver Code
int main()
{
    int N = 3;
    cout << findCntTriplet(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find the count of
  // triplets (a, b, c) with a * b + c = N
  static int findCntTriplet(int N)
  {

    // Stores count of triplets of 1st
    // N natural numbers which are of
    // the form a * b + c = N
    int cntTriplet = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i < N; i++)
    {

      // If N is divisible by i
      if (N % i != 0)
      {

        // Update cntTriplet
        cntTriplet += N / i;
      }
      else
      {

        // Update cntTriplet
        cntTriplet += (N / i) - 1;
      }
    }
    return cntTriplet;
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 3;
    System.out.println(findCntTriplet(N));
  }
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the count of
# triplets (a, b, c) with a * b + c = N
def findCntTriplet(N):

    # Stores count of triplets of 1st
    # N natural numbers which are of
    # the form a * b + c = N
    cntTriplet = 0;

    # Iterate over the range [1, N]
    for i in range(1, N):

        # If N is divisible by i
        if (N % i != 0):

            # Update cntTriplet
            cntTriplet += N // i;
        else:

            # Update cntTriplet
            cntTriplet += (N // i) - 1;

    return cntTriplet;

# Driver code
if __name__ == '__main__':
    N = 3;
    print(findCntTriplet(N));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find the count of
  // triplets (a, b, c) with a * b + c = N
  static int findCntTriplet(int N)
  {

    // Stores count of triplets of 1st
    // N natural numbers which are of
    // the form a * b + c = N
    int cntTriplet = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i < N; i++)
    {

      // If N is divisible by i
      if (N % i != 0)
      {

        // Update cntTriplet
        cntTriplet += N / i;
      }
      else
      {

        // Update cntTriplet
        cntTriplet += (N / i) - 1;
      }
    }
    return cntTriplet;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int N = 3;
    Console.WriteLine(findCntTriplet(N));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

  // Function to find the count of
  // triplets (a, b, c) with a * b + c = N
  function findCntTriplet(N)
  {

    // Stores count of triplets of 1st
    // N natural numbers which are of
    // the form a * b + c = N
    let cntTriplet = 0;

    // Iterate over the range [1, N]
    for (let i = 1; i < N; i++)
    {

      // If N is divisible by i
      if (N % i != 0)
      {

        // Update cntTriplet
        cntTriplet += Math.floor(N / i);
      }
      else
      {

        // Update cntTriplet
        cntTriplet += Math.floor(N / i) - 1;
      }
    }
    return cntTriplet;
  }

// Driver Code

    let N = 3;
    document.write(findCntTriplet(N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)