# 检查圆形阵列的所有元素是否可以通过相邻对的增量变得相等

> 原文:[https://www . geeksforgeeks . org/check-如果一个圆形数组中的所有元素都可以通过相邻对的增量来相等/](https://www.geeksforgeeks.org/check-if-all-elements-of-a-circular-array-can-be-made-equal-by-increments-of-adjacent-pairs/)

给定大小为 **N、**的圆形数组 **arr[]** ，任务是检查是否有可能通过将相邻元素对增加 **1** 来使[圆形数组](https://www.geeksforgeeks.org/circular-array/)的所有数组元素相等。

**示例:**

> **输入:** N = 4，arr[] = {2，1，3，4}
> **输出:**是
> **解释:**
> 步骤 1: { **2，1** ，3，4} - > { **3，2** ，3，4}
> 步骤 2: { **3，2** ，3，4} - > { **4**

**方法:**为了解决这个问题，可以观察到由要递增的元素组成的两个指标，一个是 ***偶数*** ，另一个是 ***奇数*** 。因此，如果我们增加偶数索引元素的值，那么奇数索引元素也会增加。因此，只有当奇数索引元素和偶数索引元素的总和相等时，才能使所有数组元素相等。按照以下步骤解决问题:

1.  计算所有偶数索引数的和，即***【sumever】**。*
2.  计算所有奇数索引数的和，即 ***和**。*
3.  如果发现 ***sumEven*** 和 ***sumOdd*** 相等，则打印“**是**”否则“**否**”。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if all array
// elements can be made equal
bool checkEquall(int arr[], int N)
{
    // Stores the sum of even and
    // odd array elements
    int sumEven = 0, sumOdd = 0;
    for (int i = 0; i < N; i++) {

        // If index is odd
        if (i & 1)
            sumOdd += arr[i];
        else
            sumEven += arr[i];
    }

    if (sumEven == sumOdd)
        return true;
    else
        return false;
}

// Driver Code
int main()
{

    int arr[] = { 2, 7, 3, 5, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    if (checkEquall(arr, N))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if all array
// elements can be made equal
static boolean checkEquall(int arr[], int N)
{

    // Stores the sum of even and
    // odd array elements
    int sumEven = 0, sumOdd = 0;

    for(int i = 0; i < N; i++)
    {

        // If index is odd
        if (i % 2 == 1)
            sumOdd += arr[i];
        else
            sumEven += arr[i];
    }

    if (sumEven == sumOdd)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 7, 3, 5, 7 };
    int N = arr.length;

    if (checkEquall(arr, N))
        System.out.print("YES" + "\n");
    else
        System.out.print("NO" + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if all array
# elements can be made equal
def checkEquall(arr, N):

    # Stores the sum of even and
    # odd array elements
    sumEven, sumOdd = 0, 0

    for i in range(N):

        # If index is odd
        if (i & 1):
            sumOdd += arr[i]
        else:
            sumEven += arr[i]

    if (sumEven == sumOdd):
        return True
    else:
        return False

# Driver Code
if __name__ == "__main__":

    arr = [ 2, 7, 3, 5, 7 ]
    N = len(arr)

    if (checkEquall(arr, N)):
        print("YES")
    else:
        print("NO")

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to check if all array
// elements can be made equal
static bool checkEquall(int []arr, int N)
{

    // Stores the sum of even and
    // odd array elements
    int sumEven = 0, sumOdd = 0;

    for(int i = 0; i < N; i++)
    {

        // If index is odd
        if (i % 2 == 1)
            sumOdd += arr[i];
        else
            sumEven += arr[i];
    }

    if (sumEven == sumOdd)
        return true;
    else
        return false;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 7, 3, 5, 7 };
    int N = arr.Length;

    if (checkEquall(arr, N))
        Console.Write("YES" + "\n");
    else
        Console.Write("NO" + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if all array
// elements can be made equal
function checkEquall(arr, N)
{

    // Stores the sum of even and
    // odd array elements
    let sumEven = 0, sumOdd = 0;

    for(let i = 0; i < N; i++)
    {

        // If index is odd
        if (i % 2 == 1)
            sumOdd += arr[i];
        else
            sumEven += arr[i];
    }

    if (sumEven == sumOdd)
        return true;
    else
        return false;
}

// Driver Code

    let arr = [ 2, 7, 3, 5, 7 ];
    let N = arr.length;

    if (checkEquall(arr, N))
        document.write("YES" );
    else
        document.write("NO");

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)