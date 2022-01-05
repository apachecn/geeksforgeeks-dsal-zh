# 检查二进制数组的所有元素是否都可以做成 1

> 原文:[https://www . geesforgeks . org/check-if-all-elements-of-binary-array-can-make-1/](https://www.geeksforgeeks.org/check-if-all-elements-of-binary-array-can-be-made-1/)

给定一个二进制数组 **Arr** 和一个整数 **K** 。如果索引 **i** 处的值为 **1** ，则可以在**(I–K)至(i + K )** 的范围内将 **0** 更改为 **1** 。
任务是判断数组的所有元素是否可以做成 **1** 。
**举例:**

> **输入:** Arr = { 0，1，0，1 }，K = 2
> **输出:** 2
> **输入:** Arr = { 1，0，0，0，0，0，1 }，K = 2
> **输出:** 0
> 不可能让所有元素都等于 1

**进场:**
这里另一个阵被用来标记为 **1** 如果我们能达到那个指数。
对于 **1 到 N** 范围内的每个指标，如果 Arr[i]的值为 **1** ，则进行从**(I–K)到(i + K)** 的循环，并将 b[i]更新为 **1** 。
最后检查 b[i]的条目，每一个 **i** 应该是 **1** ，如果是则打印 **1** 否则打印 **0** 。
以下是上述方法的实施:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Function to print 1 if the
// it is possible to make all array
// element equal to 1 else 0
void checkAllOnes(int arr[], int n,
                 int k)
{

    int brr[n];

    // Iterating over the array
    for (int i = 0; i < n; i++) {

        // If element is 1
        if (arr[i] == 1) {

            int h = k + 1;
            int j = i;

            // Put b[j...j-k] = 0
            while (j >= 0 && (h--)) {
                brr[j] = 1;
                j--;
            }

            h = k + 1;
            j = i;

            // Put b[j...j+k] = 0
            while (j < n && (h--)) {
                brr[j] = 1;
                j++;
            }
        }
    }

    int flag = 0;

    // If any value in aux
    // array equal to 0
    // then set flag
    for (int i = 0; i < n; i++) {
        if (brr[i] == 0) {
            flag = 1;
            break;
        }
    }

    // If flag is set this
    // means array after
    // conversion contains
    // 0 so print 0
    if (flag == 1)
        cout << "0";

    // else print 1
    else
        cout << "1\n";
}

// Driver Code
int main()
{

    int arr[] = { 1, 0, 1, 0 };
    int k = 2;
    int n = sizeof(arr) / sizeof(arr[0]);

    checkAllOnes(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to print 1 if the
// it is possible to make all array
// element equal to 1 else 0
static void checkAllOnes(int arr[],
                         int n, int k)
{
    int brr[] = new int[n];

    // Iterating over the array
    for (int i = 0; i < n; i++)
    {

        // If element is 1
        if (arr[i] == 1)
        {
            int h = k + 1;
            int j = i;

            // Put b[j...j-k] = 0
            while ((j >= 0) && (h-- != 0))
            {
                brr[j] = 1;
                j--;
            }

            h = k + 1;
            j = i;

            // Put b[j...j+k] = 0
            while ((j < n) && (h-- != 0))
            {
                brr[j] = 1;
                j++;
            }
        }
    }

    int flag = 0;

    // If any value in aux
    // array equal to 0
    // then set flag
    for (int i = 0; i < n; i++)
    {
        if (brr[i] == 0)
        {
            flag = 1;
            break;
        }
    }

    // If flag is set this
    // means array after
    // conversion contains
    // 0 so print 0
    if (flag == 1)
        System.out.println("0");

    // else print 1
    else
        System.out.println("1");
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 1, 0, 1, 0 };
    int k = 2;
    int n = arr.length;

    checkAllOnes(arr, n, k);
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation

# Function to print 1 if the
# it is possible to make all array
# element equal to 1 else 0
def checkAllOnes(arr, n, k):

    brr = [0 for i in range(n)]

    # Iterating over the array
    for i in range(n):

        # If element is 1
        if (arr[i] == 1):

            h = k + 1
            j = i

            # Put b[j...j-k] = 0
            while (j >= 0 and (h)):
                brr[j] = 1
                h -= 1
                j -= 1

            h = k + 1
            j = i

            # Put b[j...j+k] = 0
            while (j < n and (h)):
                brr[j] = 1
                j += 1
                h -= 1

    flag = 0

    # If any value in aux
    # array equal to 0
    # then set flag
    for i in range(n):
        if (brr[i] == 0):
            flag = 1
            break

    # If flag is set this
    # means array after
    # conversion contains
    # 0 so pr0
    if (flag == 1):
        print("0")

    # else pr1
    else:
        print("1")

# Driver Code
arr = [1, 0, 1, 0]
k = 2
n = len(arr)

checkAllOnes(arr, n, k)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to print 1 if the
// it is possible to make all array
// element equal to 1 else 0
static void checkAllOnes(int []arr,
                         int n, int k)
{
    int []brr = new int[n];

    // Iterating over the array
    for (int i = 0; i < n; i++)
    {

        // If element is 1
        if (arr[i] == 1)
        {
            int h = k + 1;
            int j = i;

            // Put b[j...j-k] = 0
            while ((j >= 0) && (h-- != 0))
            {
                brr[j] = 1;
                j--;
            }

            h = k + 1;
            j = i;

            // Put b[j...j+k] = 0
            while ((j < n) && (h-- != 0))
            {
                brr[j] = 1;
                j++;
            }
        }
    }

    int flag = 0;

    // If any value in aux
    // array equal to 0
    // then set flag
    for (int i = 0; i < n; i++)
    {
        if (brr[i] == 0)
        {
            flag = 1;
            break;
        }
    }

    // If flag is set this
    // means array after
    // conversion contains
    // 0 so print 0
    if (flag == 1)
        Console.WriteLine("0");

    // else print 1
    else
        Console.WriteLine("1");
}

// Driver Code
public static void Main (String[] args)
{
    int []arr = { 1, 0, 1, 0 };
    int k = 2;
    int n = arr.Length;

    checkAllOnes(arr, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation

// Function to print 1 if the
// it is possible to make all array
// element equal to 1 else 0
function checkAllOnes(arr, n, k)
{

    let brr = new Array(n);

    // Iterating over the array
    for (let i = 0; i < n; i++) {

        // If element is 1
        if (arr[i] == 1) {

            let h = k + 1;
            let j = i;

            // Put b[j...j-k] = 0
            while (j >= 0 && (h--)) {
                brr[j] = 1;
                j--;
            }

            h = k + 1;
            j = i;

            // Put b[j...j+k] = 0
            while (j < n && (h--)) {
                brr[j] = 1;
                j++;
            }
        }
    }

    let flag = 0;

    // If any value in aux
    // array equal to 0
    // then set flag
    for (let i = 0; i < n; i++) {
        if (brr[i] == 0) {
            flag = 1;
            break;
        }
    }

    // If flag is set this
    // means array after
    // conversion contains
    // 0 so print 0
    if (flag == 1)
        document.write("0");

    // else print 1
    else
        document.write("1");
}

// Driver Code

    let arr = [ 1, 0, 1, 0 ];
    let k = 2;
    let n = arr.length;

    checkAllOnes(arr, n, k);

</script>
```

**输出:**

```
1
```