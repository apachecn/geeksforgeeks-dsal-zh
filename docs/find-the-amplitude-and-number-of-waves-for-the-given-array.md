# 求给定阵列的振幅和波数

> 原文:[https://www . geesforgeks . org/find-给定阵列的振幅和波数/](https://www.geeksforgeeks.org/find-the-amplitude-and-number-of-waves-for-the-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到给定数组的波的振幅和数量。如果[阵列不是波阵](https://www.geeksforgeeks.org/check-if-an-array-is-wave-array/)，则打印 **-1** 。

> **波阵:**如果一个阵是连续严格递增和递减的，反之亦然，那么这个阵就是波阵。
> **振幅**定义为连续数的最大差值。

**示例:**

> **输入:** arr[] = {1，2，1，5，0，7，-6}
> **输出:**振幅= 13，波浪= 3
> **解释:**
> 对于阵列观察模式 1- > 2(增加)，2- > 1(减少)，1- > 5(增加)，5- > 0(减少)，0- > 7(增加)，7- > -6(减少)。振幅= 13(在 7 和-6 之间)和总波= 3
> **输入:** arr[] = {1，2，1，5，0，7，7}
> **输出:** -1
> **解释:**
> 由于数组的最后两个元素相等，所以数组不是波浪数组，因此答案是-1。

**方法:**
想法是检查相邻元素的两侧，其中两者都必须小于或大于当前元素。如果满足该条件，则计算波数，否则打印 **-1** ，其中波数为**(n–1)/2**。遍历数组时，不断更新连续元素之间的最大差值，得到**给定波阵的振幅**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the amplitude and
// number of waves for the given array
bool check(int a[], int n)
{
    int ma = a[1] - a[0];

    // Check for both sides adjacent
    // elements that both must be less
    // or both must be greater
    // than current element
    for (int i = 1; i < n - 1; i++) {

        if ((a[i] > a[i - 1]
             && a[i + 1] < a[i])
            || (a[i] < a[i - 1]
                && a[i + 1] > a[i]))

            // Update amplitude with max value
            ma = max(ma, abs(a[i] - a[i + 1]));

        else
            return false;
    }

    // Print the Amplitude
    cout << "Amplitude = " << ma;
    cout << endl;
    return true;
}

// Driver Code
int main()
{
    // Given array a[]
    int a[] = { 1, 2, 1, 5, 0, 7, -6 };
    int n = sizeof a / sizeof a[0];

    // Calculate number of waves
    int wave = (n - 1) / 2;

    // Function Call
    if (check(a, n))
        cout << "Waves = " << wave;
    else
        cout << "-1";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the amplitude and
// number of waves for the given array
static boolean check(int a[], int n)
{
    int ma = a[1] - a[0];

    // Check for both sides adjacent
    // elements that both must be less
    // or both must be greater
    // than current element
    for (int i = 1; i < n - 1; i++)
    {
        if ((a[i] > a[i - 1] &&
             a[i + 1] < a[i]) ||
            (a[i] < a[i - 1] &&
             a[i + 1] > a[i]))

            // Update amplitude with max value
            ma = Math.max(ma, Math.abs(a[i] - a[i + 1]));

        else
            return false;
    }

    // Print the Amplitude
    System.out.print("Amplitude = " +  ma);
    System.out.println();
    return true;
}

// Driver Code
public static void main(String[] args)
{
    // Given array a[]
    int a[] = { 1, 2, 1, 5, 0, 7, -6 };
    int n = a.length;

    // Calculate number of waves
    int wave = (n - 1) / 2;

    // Function Call
    if (check(a, n))
        System.out.print("Waves = " +  wave);
    else
        System.out.print("-1");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the amplitude and
# number of waves for the given array
def check(a, n):
    ma = a[1] - a[0]

    # Check for both sides adjacent
    # elements that both must be less
    # or both must be greater
    # than current element
    for i in range(1, n - 1):

        if ((a[i] > a[i - 1] and
             a[i + 1] < a[i]) or
            (a[i] < a[i - 1] and
             a[i + 1] > a[i])):

            # Update amplitude with max value
            ma = max(ma, abs(a[i] - a[i + 1]))

        else:
            return False

    # Prthe Amplitude
    print("Amplitude = ", ma)
    return True

# Driver Code
if __name__ == '__main__':

    # Given array a[]
    a = [1, 2, 1, 5, 0, 7, -6]
    n = len(a)

    # Calculate number of waves
    wave = (n - 1) // 2

    # Function Call
    if (check(a, n)):
        print("Waves = ",wave)
    else:
        print("-1")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the amplitude and
// number of waves for the given array
static bool check(int []a, int n)
{
    int ma = a[1] - a[0];

    // Check for both sides adjacent
    // elements that both must be less
    // or both must be greater
    // than current element
    for (int i = 1; i < n - 1; i++)
    {
        if ((a[i] > a[i - 1] &&
             a[i + 1] < a[i]) ||
            (a[i] < a[i - 1] &&
             a[i + 1] > a[i]))

            // Update amplitude with max value
            ma = Math.Max(ma, Math.Abs(a[i] - a[i + 1]));
        else
            return false;
    }

    // Print the Amplitude
    Console.Write("Amplitude = " + ma);
    Console.WriteLine();
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []a
    int []a = { 1, 2, 1, 5, 0, 7, -6 };
    int n = a.Length;

    // Calculate number of waves
    int wave = (n - 1) / 2;

    // Function Call
    if (check(a, n))
        Console.Write("Waves = " + wave);
    else
        Console.Write("-1");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the amplitude and
// number of waves for the given array
function check(a, n)
{
    let ma = a[1] - a[0];

    // Check for both sides adjacent
    // elements that both must be less
    // or both must be greater
    // than current element
    for (let i = 1; i < n - 1; i++)
    {
        if ((a[i] > a[i - 1] &&
             a[i + 1] < a[i]) ||
            (a[i] < a[i - 1] &&
             a[i + 1] > a[i]))

            // Update amplitude with max value
            ma = Math.max(ma, Math.abs(a[i] - a[i + 1]));

        else
            return false;
    }

    // Prlet the Amplitude
    document.write("Amplitude = " +  ma);
    document.write("<br/>");
    return true;
}

// Driver Code

           // Given array a[]
    let a = [ 1, 2, 1, 5, 0, 7, -6 ];
    let n = a.length;

    // Calculate number of waves
    let wave = (n - 1) / 2;

    // Function Call
    if (check(a, n))
        document.write("Waves = " +  wave);
    else
        document.write("-1");

</script>
```

**Output:** 

```
Amplitude = 13
Waves = 3
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*