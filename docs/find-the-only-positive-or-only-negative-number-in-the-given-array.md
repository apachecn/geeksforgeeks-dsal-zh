# 找出给定数组中唯一的正数或唯一的负数

> 原文:[https://www . geesforgeks . org/find-唯一正或唯一负的给定数组中的数字/](https://www.geeksforgeeks.org/find-the-only-positive-or-only-negative-number-in-the-given-array/)

给定一个除了一个数字之外的全正整数或全负整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找到那个号码。

**示例**:

> **输入** : arr[] = {3，5，2，8，-7，6，9}
> **输出** : -7
> **说明:**除-7 外，arr[]中的所有数字都是正整数。
> 
> **输入** : arr[] = {-3，5，-9}
> 输出 : 5

**逼近**:给定的问题只需要比较 arr[]的前三个数字就可以解决。之后应用[线性搜索](https://www.geeksforgeeks.org/linear-search/)找到号码。按照以下步骤解决问题。

*   如果 **arr[]** 的尺寸小于 **3** ，则返回 **0** 。
*   初始化变量 **Cp** 和 **Cn** 。
*   其中 **Cp =正整数计数**和 **Cn =负整数计数**。
*   迭代第一个 **3** 元素
    *   如果 **(arr[i] > 0)** ，将 **Cp** 增加 **1** 。
    *   否则用 **1** 增加 **Cn** 。
*   **Cp** 可以是 **2** 或 **3** ，同样， **Cn** 也可以是 **2** 或 **3** 。
*   如果 **Cp < Cn** ，那么单个元素为正，应用线性搜索找到。
*   如果 **Cn < Cp** ，则单个元素为负，应用线性搜索找到。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to return the single element
int find(int* a, int N)
{
    // Size can not be smaller than 3
    if (N < 3)
        return 0;

    // Initialize the variable
    int i, Cp = 0, Cn = 0;

    // Check the single element is
    // positive or negative
    for (i = 0; i < 3; i++) {

        if (a[i] > 0)
            Cp++;
        else
            Cn++;
    }

    // Check for positive single element
    if (Cp < Cn) {
        for (i = 0; i < N; i++)
            if (a[i] > 0)
                return a[i];
    }

    // Check for negative single element
    else {
        for (i = 0; i < N; i++)
            if (a[i] < 0)
                return a[i];
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 2, 8, -7, 6, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << find(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG {

// Function to return the single element
static int find(int []a, int N)
{
    // Size can not be smaller than 3
    if (N < 3)
        return 0;

    // Initialize the variable
    int i, Cp = 0, Cn = 0;

    // Check the single element is
    // positive or negative
    for (i = 0; i < 3; i++) {

        if (a[i] > 0)
            Cp++;
        else
            Cn++;
    }

    // Check for positive single element
    if (Cp < Cn) {
        for (i = 0; i < N; i++)
            if (a[i] > 0)
                return a[i];
    }

    // Check for negative single element
    else {
        for (i = 0; i < N; i++)
            if (a[i] < 0)
                break;
    }
    return a[i];
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 3, 5, 2, 8, -7, 6, 9 };
    int N = arr.length;
    System.out.println(find(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to return the single element
def find(a, N):

    # Size can not be smaller than 3
    if (N < 3):
        return 0

    # Initialize the variable
    Cp = 0
    Cn = 0

    # Check the single element is
    # positive or negative
    for i in range(0, 3):

        if (a[i] > 0):
            Cp += 1
        else:
            Cn += 1

        # Check for positive single element
    if (Cp < Cn):
        for i in range(0, N):
            if (a[i] > 0):
                return a[i]

        # Check for negative single element
    else:
        for i in range(0, N):
            if (a[i] < 0):
                return a[i]

# Driver Code
if __name__ == "__main__":

    arr = [3, 5, 2, 8, -7, 6, 9]
    N = len(arr)

    print(find(arr, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {

// Function to return the single element
static int find(int []a, int N)
{
    // Size can not be smaller than 3
    if (N < 3)
        return 0;

    // Initialize the variable
    int i, Cp = 0, Cn = 0;

    // Check the single element is
    // positive or negative
    for (i = 0; i < 3; i++) {

        if (a[i] > 0)
            Cp++;
        else
            Cn++;
    }

    // Check for positive single element
    if (Cp < Cn) {
        for (i = 0; i < N; i++)
            if (a[i] > 0)
                return a[i];
    }

    // Check for negative single element
    else {
        for (i = 0; i < N; i++)
            if (a[i] < 0)
                break;
    }
    return a[i];
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 5, 2, 8, -7, 6, 9 };
    int N = arr.Length;
    Console.Write(find(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to return the single element
function find(a, N)
{
    // Size can not be smaller than 3
    if (N < 3)
        return 0;

    // Initialize the variable
    let i, Cp = 0, Cn = 0;

    // Check the single element is
    // positive or negative
    for (i = 0; i < 3; i++) {

        if (a[i] > 0)
            Cp++;
        else
            Cn++;
    }

    // Check for positive single element
    if (Cp < Cn) {
        for (i = 0; i < N; i++)
            if (a[i] > 0)
                return a[i];
    }

    // Check for negative single element
    else {
        for (i = 0; i < N; i++)
            if (a[i] < 0)
                return a[i];
    }
}

// Driver Code
let arr = [ 3, 5, 2, 8, -7, 6, 9 ];
let N = arr.length;

document.write(find(arr, N));

// This code is contributed Samim Hossain Mondal.
</script>
```

**Output**

```
-7
```

**时间** **复杂度**:O(N)
T5】辅助 **空间** : O(1)