# 计算 L 到 R 范围内数字总和的总和

> 原文:[https://www . geesforgeks . org/calculate-sum-of-numbers-in-l-to-r/](https://www.geeksforgeeks.org/calculate-the-sum-of-sum-of-numbers-in-range-l-to-r/)

给定两个数字 **L** 和 **R** 。任务是找出范围 **L** 到 **R** 内的数字之和。

**示例:**

> **输入:** L = 3，R = 6
> T3】输出:40
> T6】说明: 3 + 3+4 + 3+4+5 + 3+4+5+6 = 40
> 
> **输入:** L = 5，R = 6
> T3】输出: 16

**做法:**这个问题是基于公式的。对于下面给出的示例，观察每个数字在总和中重复的次数，并据此计算最终总和。

插图: **L** = 3， **R** = 6

总和= 3+3+4+3+4+5+3+4+5+6 = 3+3+3+3+4+4+4+5+5+6(分组时)
即等于 3*4 + 4*3 + 5*2 + 6*1

因此，对于 L 至 R 的任何范围，总和可以计算为:

**L * D+(L+1)*(D-1)+(L+2)*(D-2)+……+(R-1)*(2)+R * 1**

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

// Function to return sum
int findSum(int L, int R)
{
    // Initializing the variables
    int sum = 0, d = R - L + 1;

    for (int i = L; i <= R; i++) {
        sum += (i * d);
        d--;
    }

    // Return Sum as the final result.
    return sum;
}

// Driver Code
int main()
{
    int L = 3, R = 6;

    // Function call
    cout << findSum(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
public class GFG {

// Function to return sum
static int findSum(int L, int R)
{

    // Initializing the variables
    int sum = 0, d = R - L + 1;

    for (int i = L; i <= R; i++) {
        sum += (i * d);
        d--;
    }

    // Return Sum as the final result.
    return sum;
}

// Driver code
public static void main(String args[])
{
    int L = 3, R = 6;

    // Function call
    System.out.println(findSum(L, R));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## 计算机编程语言

```
# Pyhton program for above approach

# Function to return sum
def findSum(L, R):

    # Initializing the variables
    sum = 0
    d = R - L + 1

    for i in range(L, R + 1):
        sum += (i * d)
        d = d - 1

    # Return Sum as the final result.
    return sum

# Driver Code
L = 3
R = 6

# Function call
print(findSum(L, R))

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to implement above approach
using System;
public class GFG {

  // Function to return sum
  static int findSum(int L, int R)
  {

    // Initializing the variables
    int sum = 0, d = R - L + 1;

    for (int i = L; i <= R; i++) {
      sum += (i * d);
      d--;
    }

    // Return Sum as the final result.
    return sum;
  }

  // Driver code
  public static void Main()
  {
    int L = 3, R = 6;

    // Function call
    Console.WriteLine(findSum(L, R));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach

   // Function to return sum
   function findSum(L, R) {
     // Initializing the variables
     let sum = 0, d = R - L + 1;

     for (let i = L; i <= R; i++) {
       sum += (i * d);
       d--;
     }

     // Return Sum as the final result.
     return sum;
   }

   // Driver Code

   let L = 3, R = 6;

   // Function call
   document.write(findSum(L, R));
 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
40
```

**时间复杂度:** O(R-L+1)

**辅助空间:** O(1)