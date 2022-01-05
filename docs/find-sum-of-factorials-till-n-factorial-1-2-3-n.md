# 求阶乘之和直到 N 阶乘(1！+ 2!+ 3!+ … + N！)

> 原文:[https://www . geesforgeks . org/find-阶乘和-till-n-阶乘-1-2-3-n/](https://www.geeksforgeeks.org/find-sum-of-factorials-till-n-factorial-1-2-3-n/)

给定正整数 **N** 。任务是从 1 开始计算阶乘的和！去 N！， **1！+ 2!+ 3!+ … + N！**。

**示例**:

> **输入** : N = 5
> **输出** : 153
> **解释** : 1！+ 2!+ 3!+ 4!+ 5!= 1 + 2 + 6 + 24 + 120 = 153.
> 
> **输入** : N = 1
> 输出 : 1

**天真的做法**:解决这个问题的基本方法是找到所有数字直到 1 到 N 的阶乘，并计算它们的和。
***时间复杂度** : O(N^2)*
***辅助空间** : O(1)*

**方法**:一个有效的方法是在同一个循环中计算阶乘和和，使时间为 O(N)。遍历从 1 到 N 的数字，对于每个数字 i:

*   将 I 乘以先前的阶乘(最初为 1)。
*   将这个新阶乘加到一个集合和上

最后，打印这个集体总和。

下面是上述方法的实现。

## C++

```
// C++ program to compute sum of series
// 1! + 2! + 3! + ... + N!
#include <iostream>
using namespace std;

// Function to return sum
// of 1!, 2! upto N!
int findFactSum(int N)
{
    // Initializing the variables
    int f = 1, Sum = 0;

    // Calculate the factorial and sum
    // in the same loop
    for (int i = 1; i <= N; i++) {

        f = f * i;
        Sum += f;
    }

    // Return Sum as the final result.
    return Sum;
}

// Driver Code
int main()
{
    int N = 5;

    // Function call
    cout << findFactSum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
class GFG {

    // Function to return sum
    // of 1!, 2! upto N!
    static int findFactSum(int N)
    {

        // Initializing the variables
        int f = 1, Sum = 0;

        // Calculate the factorial and sum
        // in the same loop
        for (int i = 1; i <= N; i++) {

            f = f * i;
            Sum += f;
        }

        // Return Sum as the final result.
        return Sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 5;
        System.out.print(findFactSum(N));
    }
}

// This code is contributed ukasp.
```

## 蟒蛇 3

```
# python program to compute sum of series
# 1! + 2! + 3! + ... + N!

# Function to return sum
# of 1!, 2! upto N!
def findFactSum(N):

    # Initializing the variables
    f = 1
    Sum = 0

    # Calculate the factorial and sum
    # in the same loop
    for i in range(1, N + 1):
        f = f * i
        Sum += f

    # Return Sum as the final result.
    return Sum

# Driver Code
if __name__ == "__main__":
    N = 5

    # Function call
    print(findFactSum(N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code to implement above approach
using System;
class GFG
{

  // Function to return sum
  // of 1!, 2! upto N!
  static int findFactSum(int N)
  {

    // Initializing the variables
    int f = 1, Sum = 0;

    // Calculate the factorial and sum
    // in the same loop
    for (int i = 1; i <= N; i++) {

      f = f * i;
      Sum += f;
    }

    // Return Sum as the final result.
    return Sum;
  }

  // Driver code
  public static void Main()
  {
    int N = 5;
    Console.Write(findFactSum(N));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to return sum
    // of 1!, 2! upto N!
    function findFactSum(N)
    {

      // Initializing the variables
      let f = 1, Sum = 0;

      // Calculate the factorial and sum
      // in the same loop
      for (let i = 1; i <= N; i++) {

        f = f * i;
        Sum += f;
      }

      // Return Sum as the final result.
      return Sum;
    }

    // Driver Code
    let N = 5;

    // Function call
    document.write(findFactSum(N));

  // This code is contributed by Potta Lokesh
  </script>
```

**Output:** 

```
153
```

**时间复杂度** : O(N)
**辅助空间** : O(1)