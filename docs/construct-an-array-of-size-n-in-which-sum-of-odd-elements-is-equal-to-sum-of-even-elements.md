# 构造一个大小为 N 的数组，其中奇数元素的和等于偶数元素的和

> 原文:[https://www . geesforgeks . org/construct-一个大小为 n 的数组，其中奇数元素的和等于偶数元素的和/](https://www.geeksforgeeks.org/construct-an-array-of-size-n-in-which-sum-of-odd-elements-is-equal-to-sum-of-even-elements/)

给定一个总是偶数的**整数 N** ，任务是创建一个大小为 **N** 的数组，该数组包含 **N/2 个偶数**和 **N/2 个奇数**。数组的所有元素应该是不同的，偶数的和等于奇数的和。如果不存在这样的数组，那么打印-1。
**举例:**

> **输入:** N = 8
> **输出:** 2 4 6 8 1 3 5 11
> **说明:**
> 数组有 8 个不同的元素，它们的奇数和偶数之和相等，即(2 + 4 + 6 + 8 = 1 + 3 + 5 + 11)。
> **输入:** N = 10
> **输出:** -1
> **解释:**
> 无法构造大小为 10 的数组。

**方法:**解决上述问题的第一个观察是*不可能创建大小为 2 的倍数而不是 4 的倍数的数组*。因为，如果发生这种情况，那么包含奇数的一半的总和将总是奇数，而包含偶数的另一半的总和将总是偶数，因此两个一半的总和不可能相同。
因此，满足问题陈述的数组应该总是有一个**大小 N，它是 4** 的倍数。方法是首先从 2 开始构造 N/2 个偶数，这是数组的前半部分。然后从 1 开始创建数组的另一部分，最后计算最后一个奇数元素，使两部分相等。为此，奇数的最后一个元素**应该是(N/2)–1+N**。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to Create an array
// of size N consisting of distinct
// elements where sum of odd elements
// is equal to sum of even elements

#include <bits/stdc++.h>
using namespace std;

// Function to construct the required array
void arrayConstruct(int N)
{

    // To construct first half,
    // distinct even numbers
    for (int i = 2; i <= N; i = i + 2)
        cout << i << " ";

    // To construct second half,
    // distinct odd numbers
    for (int i = 1; i < N - 1; i = i + 2)
        cout << i << " ";

    // Calculate the last number of second half
    // so as to make both the halves equal
    cout << N - 1 + (N / 2) << endl;
}

// Function to construct the required array
void createArray(int N)
{

    // check if size is multiple of 4
    // then array exist
    if (N % 4 == 0)

        // function call to construct array
        arrayConstruct(N);

    else
        cout << -1 << endl;
}

// Driver code
int main()
{

    int N = 8;

    createArray(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Create an array
// of size N consisting of distinct
// elements where sum of odd elements
// is equal to sum of even elements
class GFG{

// Function to construct the required array
static void arrayConstruct(int N)
{

    // To confirst half,
    // distinct even numbers
    for (int i = 2; i <= N; i = i + 2)
        System.out.print(i+ " ");

    // To consecond half,
    // distinct odd numbers
    for (int i = 1; i < N - 1; i = i + 2)
        System.out.print(i+ " ");

    // Calculate the last number of second half
    // so as to make both the halves equal
    System.out.print(N - 1 + (N / 2) +"\n");
}

// Function to construct the required array
static void createArray(int N)
{

    // check if size is multiple of 4
    // then array exist
    if (N % 4 == 0)

        // function call to conarray
        arrayConstruct(N);

    else
        System.out.print(-1 +"\n");
}

// Driver code
public static void main(String[] args)
{
    int N = 8;

    createArray(N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# python3 program to Create an array
# of size N consisting of distinct
# elements where sum of odd elements
# is equal to sum of even elements

# Function to construct the required array
def arrayConstruct(N):

    # To construct first half,
    # distinct even numbers
    for i in range(2, N + 1, 2):
        print(i,end=" ")

    # To construct second half,
    # distinct odd numbers
    for i in range(1, N - 1, 2):
        print(i, end=" ")

    # Calculate the last number of second half
    # so as to make both the halves equal
    print(N - 1 + (N // 2))

# Function to construct the required array
def createArray(N):

    # check if size is multiple of 4
    # then array exist
    if (N % 4 == 0):

        # function call to construct array
        arrayConstruct(N)

    else:
        cout << -1 << endl

# Driver code
if __name__ == '__main__':

    N = 8

    createArray(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to Create an array
// of size N consisting of distinct
// elements where sum of odd elements
// is equal to sum of even elements
using System;

class GFG{

// Function to construct the required array
static void arrayConstruct(int N)
{

    // To confirst half,
    // distinct even numbers
    for (int i = 2; i <= N; i = i + 2)
        Console.Write(i + " ");

    // To consecond half,
    // distinct odd numbers
    for (int i = 1; i < N - 1; i = i + 2)
        Console.Write(i + " ");

    // Calculate the last number of second half
    // so as to make both the halves equal
    Console.Write(N - 1 + (N / 2) +"\n");
}

// Function to construct the required array
static void createArray(int N)
{

    // check if size is multiple of 4
    // then array exist
    if (N % 4 == 0)

        // function call to conarray
        arrayConstruct(N);

    else
        Console.Write(-1 +"\n");
}

// Driver code
public static void Main(String[] args)
{
    int N = 8;

    createArray(N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program to Create an array
// of size N consisting of distinct
// elements where sum of odd elements
// is equal to sum of even elements

// Function to construct the required array
function arrayConstruct(N)
{

    // To construct first half,
    // distinct even numbers
    for (let i = 2; i <= N; i = i + 2)
        document.write(i + " ");

    // To construct second half,
    // distinct odd numbers
    for (let i = 1; i < N - 1; i = i + 2)
        document.write(i + " ");

    // Calculate the last number of second half
    // so as to make both the halves equal
    document.write(N - 1 + (N / 2) + "<br>");
}

// Function to construct the required array
function createArray(N)
{

    // check if size is multiple of 4
    // then array exist
    if (N % 4 == 0)

        // function call to construct array
        arrayConstruct(N);
    else
        document.write(-1 + "<br>");
}

// Driver code
    let N = 8;
    createArray(N);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
2 4 6 8 1 3 5 11
```

时间复杂度:0(N)

辅助空间:0(1)