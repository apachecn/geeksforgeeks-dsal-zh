# 计算最多 N 个整数，可以表示为两个或多个连续数字的和

> 原文:[https://www . geesforgeks . org/count-integs-up-n-哪些可以表示为两个或多个连续数字的和/](https://www.geeksforgeeks.org/count-integers-up-to-n-which-can-be-represented-as-sum-of-two-or-more-consecutive-numbers/)

给定一个正整数 **N** ，任务是将整数的个数计数到 **N** ，可以将[表示为两个或多个连续数](https://www.geeksforgeeks.org/check-number-can-expressed-sum-consecutive-numbers/)的和。

**示例:**

> **输入:** N = 7
> **输出:** 4
> **说明:**在【1，7】范围内:{3，5，6，7}可以表示为连续数的和。
> 
> *   3 = 1 + 2
> *   5 = 2 + 3
> *   6 = 1 + 2 + 3
> *   7 = 3 + 4
> 
> **输入:**N = 15
> T3】输出: 11

**天真方法:**按照以下步骤解决问题:

1.  迭代**【1，N】**范围内的所有整数，对于每个整数，检查它是否可以表示为两个或多个连续整数的和。
2.  要检查一个数是否可以表示为两个或两个以上连续数的和，请参考[这篇](https://www.geeksforgeeks.org/check-number-can-expressed-sum-consecutive-numbers/)文章。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the number N
// can be expressed as sum of 2 or
// more consecutive numbers or not
bool isPossible(int N)
{
    return ((N & (N - 1)) && N);
}

// Function to count integers in the range
// [1, N] that can be expressed as sum of
// 2 or more consecutive numbers
void countElements(int N)
{
    // Stores the required count
    int count = 0;

    for (int i = 1; i <= N; i++) {

        if (isPossible(i))
            count++;
    }
    cout << count;
}
// Driver Code
int main()
{
    int N = 15;
    countElements(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;
class GFG
{

// Function to check if the number N
// can be expressed as sum of 2 or
// more consecutive numbers or not
static int isPossible(int N)
{
    return (((N & (N - 1)) & N));
}

// Function to count integers in the range
// [1, N] that can be expressed as sum of
// 2 or more consecutive numbers
static void countElements(int N)
{

    // Stores the required count
    int count = 0;
    for (int i = 1; i <= N; i++)
    {
        if (isPossible(i) != 0)
            count++;
    }
    System.out.println(count);
}

// Driver Code
    public static void main(String[] args)
{
    int N = 15;
    countElements(N);
}
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to check if the number N
# can be expressed as sum of 2 or
# more consecutive numbers or not
def isPossible(N):
    return ((N & (N - 1)) and N)

# Function to count integers in the range
# [1, N] that can be expressed as sum of
# 2 or more consecutive numbers
def countElements(N):

    # Stores the required count
    count = 0
    for i in range(1, N + 1):
        if (isPossible(i)):
            count += 1

    print (count)

# Driver Code
if __name__ == '__main__':
    N = 15
    countElements(N)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to check if the number N
// can be expressed as sum of 2 or
// more consecutive numbers or not
static int isPossible(int N)
{
    return (((N & (N - 1)) & N));
}

// Function to count integers in the range
// [1, N] that can be expressed as sum of
// 2 or more consecutive numbers
static void countElements(int N)
{

    // Stores the required count
    int count = 0;
    for (int i = 1; i <= N; i++)
    {
        if (isPossible(i) != 0)
            count++;
    }
    Console.Write(count);
}

// Driver Code
static public void Main()
{
    int N = 15;
    countElements(N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// JavaScript program of the above approach

    // Function to check if the number N
    // can be expressed as sum of 2 or
    // more consecutive numbers or not
    function isPossible(N) {
        return (((N & (N - 1)) & N));
    }

    // Function to count integers in the range
    // [1, N] that can be expressed as sum of
    // 2 or more consecutive numbers
    function countElements(N) {

        // Stores the required count
        var count = 0;
        for (i = 1; i <= N; i++) {
            if (isPossible(i) != 0)
                count++;
        }
        document.write(count);
    }

    // Driver Code

        var N = 15;
        countElements(N);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**要优化上述方法，请按照以下步骤解决问题

1.  [除了](https://www.geeksforgeeks.org/check-number-can-expressed-sum-consecutive-numbers/)[2 的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)以外的所有数字都可以表示为连续数字的和。
2.  计算 2 的幂次≤ **N** 并将其存储在一个变量中，k 表示**计数**
3.  打印**(N–计数)**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count integers in the range
// [1, N] that can be expressed as sum of
// 2 or more consecutive numbers
void countElements(int N)
{
    int Cur_Ele = 1;
    int Count = 0;

    // Count powers of 2 up to N
    while (Cur_Ele <= N) {

        // Increment count
        Count++;

        // Update current power of 2
        Cur_Ele = Cur_Ele * 2;
    }

    cout << N - Count;
}

// Driver Code
int main()
{
    int N = 15;
    countElements(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of the above approach
import java.util.*;
class GFG
{

  // Function to count integers in the range
  // [1, N] that can be expressed as sum of
  // 2 or more consecutive numbers
  static void countElements(int N)
  {
    int Cur_Ele = 1;
    int Count = 0;

    // Count powers of 2 up to N
    while (Cur_Ele <= N)
    {

      // Increment count
      Count++;

      // Update current power of 2
      Cur_Ele = Cur_Ele * 2;
    }

    System.out.print(N - Count);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 15;
    countElements(N);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python 3 implementation
# of the above approach

# Function to count integers in the range
# [1, N] that can be expressed as sum of
# 2 or more consecutive numbers
def countElements(N):
    Cur_Ele = 1
    Count = 0

    # Count powers of 2 up to N
    while (Cur_Ele <= N):
        # Increment count
        Count += 1

        # Update current power of 2
        Cur_Ele = Cur_Ele * 2

    print(N - Count)

# Driver Code
if __name__ == '__main__':
    N = 15
    countElements(N)
```

## C#

```
// C# implementation
// of the above approach
using System;

public class GFG
{

  // Function to count integers in the range
  // [1, N] that can be expressed as sum of
  // 2 or more consecutive numbers
  static void countElements(int N)
  {
    int Cur_Ele = 1;
    int Count = 0;

    // Count powers of 2 up to N
    while (Cur_Ele <= N)
    {

      // Increment count
      Count++;

      // Update current power of 2
      Cur_Ele = Cur_Ele * 2;
    }

    Console.Write(N - Count);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 15;
    countElements(N);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation
// of the above approach

// Function to count integers in the range
// [1, N] that can be expressed as sum of
// 2 or more consecutive numbers
function countElements(N)
{
    var Cur_Ele = 1;
    var Count = 0;

    // Count powers of 2 up to N
    while (Cur_Ele <= N)
    {

        // Increment count
        Count++;

        // Update current power of 2
        Cur_Ele = Cur_Ele * 2;
    }
    document.write(N - Count);
}

// Driver Code
var N = 15;

countElements(N);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
11
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*