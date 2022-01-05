# 检查数组的任何排列是否包含不能被 3 整除的每个相邻对的和

> 原文:[https://www . geeksforgeeks . org/check-if-any-array-array-contains-sum-of-near-pair-not-除尽-3/](https://www.geeksforgeeks.org/check-if-any-permutation-of-array-contains-sum-of-every-adjacent-pair-not-divisible-by-3/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查数组元素是否存在任何排列，其中每对相邻元素的和不能被 **3** 整除。如果可能，则打印“**是”**。否则，打印“**否”**。

**示例:**

> **输入:** arr[] = {1，2，3，3}
> **输出:**是
> **解释:**
> 因为至少存在一个组合{3，2，3，1}，其中每个相邻对的和不能被 3 整除。
> 
> **输入:** arr[] = {3，6，1，9}
> **输出:**否

**天真方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有排列，并检查是否存在没有两个相邻元素之和可被 **3** 整除的排列。如果发现是真的，则打印“**是”**。否则，打印“**否”**。

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，其思想是观察所有数组元素的唯一可能余数，即 **{0，1，2}** 。用两个相邻元素的和不能被 3 整除的方式分隔这三个数字。请遵循以下步骤:

1.  将所有数字分成三部分，剩余部分为 **0** 、 **1** 和 **2** 。让计数分别为 **a** 、 **b** 和 **c** 。
2.  现在将余数为 **0** 的数字与余数为 **1** 或 **2** 的数字排列在一起，这样它们的和就不能被 3 整除。以下是该条件成立的条件:
    *   如果**a≥1****a≤b+ c+1**
    *   如果 **a 和 b** 都等于 **0** 和 **c > 0**
    *   如果 **a 和 c** 都等于 **0** 和 **b > 0**
3.  如果没有办法以上述方式排列所有的数字，那么就没有排列使得它们的相邻元素之和不能被 3 整除。因此，打印“**否”**。
4.  如果**步骤 2** 中的条件为真，则打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to checks if any permutation
// of the array exists whose sum of
// adjacent pairs is not divisible by 3
void factorsOf3(int arr[], int N)
{
    int a = 0, b = 0, c = 0;
    for (int i = 0; i < N; i++) {

        // Count remainder 0
        if (arr[i] % 3 == 0)
            a++;

        // Count remainder 1
        else if (arr[i] % 3 == 1)
            b++;

        // Count remainder 2
        else if (arr[i] % 3 == 2)
            c++;
    }

    // Condition for valid arrangements
    if (a >= 1 && a <= b + c + 1)
        cout << "Yes" << endl;
    else if (a == 0 && b == 0 && c > 0)
        cout << "Yes" << endl;
    else if (a == 0 && c == 0 && b > 0)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    factorsOf3(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

// Function to checks if any permutation
// of the array exists whose sum of
// adjacent pairs is not divisible by 3
static void factorsOf3(int arr[], int N)
{
  int a = 0, b = 0, c = 0;
  for (int i = 0; i < N; i++)
  {
    // Count remainder 0
    if (arr[i] % 3 == 0)
      a++;

    // Count remainder 1
    else if (arr[i] % 3 == 1)
      b++;

    // Count remainder 2
    else if (arr[i] % 3 == 2)
      c++;
  }

  // Condition for valid arrangements
  if (a >= 1 && a <= b + c + 1)
    System.out.print("Yes" + "\n");
  else if (a == 0 && b == 0 && c > 0)
    System.out.print("Yes" + "\n");
  else if (a == 0 && c == 0 && b > 0)
    System.out.print("Yes" + "\n");
  else
    System.out.print("No" + "\n");
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {1, 2, 3, 3};

  int N = arr.length;

  // Function Call
  factorsOf3(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to checks if any permutation
# of the array exists whose sum of
# adjacent pairs is not divisible by 3
def factorsOf3(arr, N):

    a = 0
    b = 0
    c = 0

    for i in range(N):

        # Count remainder 0
        if (arr[i] % 3 == 0):
            a += 1
        # Count remainder 1
        elif (arr[i] % 3 == 1):
            b += 1
        # Count remainder 2
        elif (arr[i] % 3 == 2):
            c += 1

    # Condition for valid arrangements
    if (a >= 1 and a <= b + c + 1):
        print("Yes")
    elif (a == 0 and b == 0 and c > 0):
        print("Yes")
    elif (a == 0 and c == 0 and b > 0):
        print("Yes")
    else:
        print("No")

# Driver Code

# Given array arr[]
arr = [ 1, 2, 3, 3 ]
N = len(arr)

# Function call
factorsOf3(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to checks if any
// permutation of the array
// exists whose sum of
// adjacent pairs is not
// divisible by 3
static void factorsOf3(int []arr,
                       int N)
{
  int a = 0, b = 0, c = 0;
  for (int i = 0; i < N; i++)
  {
    // Count remainder 0
    if (arr[i] % 3 == 0)
      a++;

    // Count remainder 1
    else if (arr[i] % 3 == 1)
      b++;

    // Count remainder 2
    else if (arr[i] % 3 == 2)
      c++;
  }

  // Condition for valid arrangements
  if (a >= 1 && a <= b + c + 1)
    Console.Write("Yes" + "\n");
  else if (a == 0 && b == 0 && c > 0)
    Console.Write("Yes" + "\n");
  else if (a == 0 && c == 0 && b > 0)
    Console.Write("Yes" + "\n");
  else
    Console.Write("No" + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 2, 3, 3};

  int N = arr.Length;

  // Function Call
  factorsOf3(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to checks if any permutation
// of the array exists whose sum of
// adjacent pairs is not divisible by 3
function factorsOf3(arr, N)
{
    let a = 0, b = 0, c = 0;
    for(let i = 0; i < N; i++)
    {

        // Count remainder 0
        if (arr[i] % 3 == 0)
            a++;

        // Count remainder 1
        else if (arr[i] % 3 == 1)
            b++;

        // Count remainder 2
        else if (arr[i] % 3 == 2)
            c++;
    }

    // Condition for valid arrangements
    if (a >= 1 && a <= b + c + 1)
        document.write("Yes" + "<br/>");
    else if (a == 0 && b == 0 && c > 0)
        document.write("Yes" + "<br/>");
    else if (a == 0 && c == 0 && b > 0)
        document.write("Yes" + "<br/>");
    else
        document.write("No" + "<br/>");
}

// Driver Code

// Given array arr[]
let arr = [ 1, 2, 3, 3 ];

let N = arr.length;

// Function Call
factorsOf3(arr, N);

// This code is contributed by chinmoy1997pal 

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)