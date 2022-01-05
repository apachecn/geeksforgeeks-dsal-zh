# 计算给定素数 P 等于自身时具有模逆的数组元素

> 原文:[https://www . geesforgeks . org/count-array-elements-having-modular-inverse-欠给定质数-p-equal-to-self/](https://www.geeksforgeeks.org/count-array-elements-having-modular-inverse-under-given-prime-number-p-equal-to-itself/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个[质数](https://www.geeksforgeeks.org/prime-numbers/) **P** ，任务是对数组元素进行计数，使得在模 P 下元素的[模乘逆等于元素本身。](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)

**示例:**

> **输入:** arr[] = {1，6，4，5}，P = 7
> **输出:** 2
> **解释:**
> 模 P(= 7)下 arr[0](=1)的模乘逆本身就是 arr[0](= 1)。
> 模 P(= 7)下 arr[1](= 6)的模乘逆本身就是 arr[1](= 6)。
> 因此，要求输出为 2。
> 
> **输入:** arr[] = {1，3，8，12，12}，P = 13
> T3】输出: 3

**天真法:**解决这个问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并打印数组元素的计数，使得[模 P 下元素的模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)等于元素本身。

***时间复杂度:** O(N * log P)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 如果 X 和 Y 是两个数字使得 **(X × Y) % P = 1** ，那么 **Y** 是 **X** 的模逆。
> 所以如果 **Y** 是 **X** 本身，那么 **(X × X) % P** 一定是 **1。**

按照以下步骤解决问题:

*   初始化一个变量，比如 **cntElem** 来存储满足给定条件的元素计数。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查 **(arr[i] * arr[i]) % P** 是否等于 **1** 。如果发现为真，则将**计数增加**1。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the count
// of elements that satisfy
// the given condition.
int equvInverse(int arr[],
                int N, int P)
{
    // Stores count of elements
    // that satisfy the condition
    int cntElem = 0;

    // Traverse the given array.
    for (int i = 0; i < N; i++) {

        // If square of current
        // element is equal to 1
        if ((arr[i] * arr[i]) % P
            == 1) {
            cntElem++;
        }
    }
    return cntElem;
}

// Driver Code
int main()
{
    int arr[] = { 1, 6, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int P = 7;
    cout << equvInverse(arr, N, P);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to get the count
// of elements that satisfy
// the given condition.
static int equvInverse(int[] arr,
                       int N, int P)
{

    // Stores count of elements
    // that satisfy the condition
    int cntElem = 0;

    // Traverse the given array.
    for(int i = 0; i < N; i++)
    {

        // If square of current
        // element is equal to 1
        if ((arr[i] * arr[i]) % P == 1)
        {
            cntElem++;
        }
    }
    return cntElem;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 6, 4, 5 };
    int N = arr.length;
    int P = 7;

    System.out.println(equvInverse(arr, N, P));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to get the count
# of elements that satisfy
# the given condition.
def equvInverse(arr, N, P):

    # Stores count of elements
    # that satisfy the condition
    cntElem = 0

    # Traverse the given array.
    for i in range(0, N):

        # If square of current
        # element is equal to 1
        if ((arr[i] * arr[i]) % P == 1):
            cntElem = cntElem + 1

    return cntElem

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 6, 4, 5 ]
    N = len(arr)
    P = 7

    print(equvInverse(arr, N, P))

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to get the count
// of elements that satisfy
// the given condition.
static int equvInverse(int[] arr, int N, int P)
{

    // Stores count of elements
    // that satisfy the condition
    int cntElem = 0;

    // Traverse the given array.
    for(int i = 0; i < N; i++)
    {

        // If square of current
        // element is equal to 1
        if ((arr[i] * arr[i]) % P == 1)
        {
            cntElem++;
        }
    }
    return cntElem;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 6, 4, 5 };
    int N = arr.Length;
    int P = 7;

    Console.WriteLine(equvInverse(arr, N, P));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to get the count
// of elements that satisfy
// the given condition.
function equvInverse(arr, N, P)
{
    // Stores count of elements
    // that satisfy the condition
    let cntElem = 0;

    // Traverse the given array.
    for (let i = 0; i < N; i++) {

        // If square of current
        // element is equal to 1
        if ((arr[i] * arr[i]) % P
            == 1) {
            cntElem++;
        }
    }
    return cntElem;
}

// Driver Code
let arr = [ 1, 6, 4, 5 ];
let N = arr.length;
let P = 7;
document.write(equvInverse(arr, N, P));

// This code is contributed by subham348.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)