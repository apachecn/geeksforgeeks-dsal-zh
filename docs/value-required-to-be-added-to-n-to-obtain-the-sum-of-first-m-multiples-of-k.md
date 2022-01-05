# 需要加到 N 的值，得到 K 的前 M 倍之和

> 原文:[https://www . geesforgeks . org/value-required-to-n-to-get-first-m-倍数之和 k/](https://www.geeksforgeeks.org/value-required-to-be-added-to-n-to-obtain-the-sum-of-first-m-multiples-of-k/)

给定三个正整数 **N** 、 **K** 和 **M** ，任务是找到要加到 **N** 上的数，得到 **K** 的第一个 **M** 倍数之和。

**示例:**

> **输入:** N = 17，K = 3，M = 4
> **输出:** 13
> **说明:**
> 3 的前 4 倍数之和= (3 + 6 + 9 + 12) = 30。
> 因此，要加到 17 上的值是(30–17)= 13。
> 因此，要求的输出是 13。
> 
> **输入:** N = 5，K = 2，M = 1
> **输出:** -3
> **说明:**
> 2 的前 1 倍数之和为 2。
> 加 5 得到 2 的值是(2–5)=-3

**方法:**按照以下步骤解决问题:

1.  计算第一个 **M** 的倍数 **K** 的**和**，等于**K *(1+2+3+…M)**=**K * M *(M+1)/2**。
2.  初始化一个变量，比如 **res** ，存储需要添加到 **N** 的数字，得到**和**。
3.  因此， **res** 将等于**sum–N**。打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to print the value
// to be added to N to obtain
// sum of first M multiples of K
static int printNumber(int N, int K, int M)
{

    // Store the sum of the
    // first M multiples of K
    int sum = K * (M * (M + 1) / 2);

    // Store the value to be
    // added to obtain N
    return sum - N;
}

// Driver Code
int main()
{
    // Input
    int N = 17;
    int K = 3;
    int M = 4;
    cout << printNumber(N, K, M);
    return 0;
}

// This code is contributed by shubhamsingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code of above approach
import java.util.*;
class GFG
{

  // Function to print the value
  // to be added to N to obtain
  // sum of first M multiples of K
  static int printNumber(int N, int K, int M)
  {

    // Store the sum of the
    // first M multiples of K
    int sum = K * (M * (M + 1) / 2);

    // Store the value to be
    // added to obtain N
    return sum - N;
  }

  // Driver code
  public static void main(String[] args)
  {
    // Input
    int N = 17;
    int K = 3;
    int M = 4;
    System.out.print(printNumber(N, K, M));
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the value
# to be added to N to obtain
# sum of first M multiples of K
def printNumber(N, K, M):

    # Store the sum of the
    # first M multiples of K
    sum = K * (M * (M + 1) / 2)

    # Store the value to be
    # added to obtain N
    return sum - N

# Driver Code

# Input
N = 17
K = 3
M = 4

print(int(printNumber(N, K, M)))
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to print the value
  // to be added to N to obtain
  // sum of first M multiples of K
  static int printNumber(int N, int K, int M)
  {

    // Store the sum of the
    // first M multiples of K
    int sum = K * (M * (M + 1) / 2);

    // Store the value to be
    // added to obtain N
    return sum - N;
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Input
    int N = 17;
    int K = 3;
    int M = 4;
    Console.Write(printNumber(N, K, M));
  }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the value
// to be added to N to obtain
// sum of first M multiples of K
function printNumber(N, K, M)
{

    // Store the sum of the
    // first M multiples of K
    var sum = K * ((M * (M + 1)) / 2);

    // Store the value to be
    // added to obtain N
    return sum - N;
}

// Driver Code

// Input
var N = 17;
var K = 3;
var M = 4;

document.write(printNumber(N, K, M));

// This code is contributed by rdtank

</script>
```

**Output**

```
13
```

***时间复杂度:*** O(1)
***辅助空间:*** O(1)