# 安排作业，使每台服务器获得相等的负载

> 原文:[https://www . geesforgeks . org/schedule-jobs-server-get-equal-load/](https://www.geeksforgeeks.org/schedule-jobs-server-gets-equal-load/)

有 n 台服务器。每个服务器 I 当前正在处理(I)数量的请求。还有另一个数组 b，其中 b(i)表示调度到服务器 I 的传入请求的数量。重新调度传入请求，使每个服务器 I 在重新调度后持有相等数量的请求。对服务器 I 的传入请求只能重新安排到服务器 i-1、I、i+1。如果没有这种重新调度的可能，则输出-1 否则打印重新调度后每个服务器保持的请求数。
**例:**

```
Input : a = {6, 14, 21, 1}
        b = {15, 7, 10, 10}
Output : 21
b(0) scheduled to a(0) --> a(0) = 21
b(1) scheduled to a(1) --> a(1) = 21
b(2) scheduled to a(3) --> a(3) = 11
b(3) scheduled to a(3) --> a(3) = 21
a(2) remains unchanged --> a(2) = 21

Input : a = {1, 2, 3}
        b = {1, 100, 3}
Output : -1
No rescheduling will result in equal requests.
```

[Recommended : Please try your approach first on IDE and then look at the solution](https://ide.geeksforgeeks.org/)

**方法:**观察数组 b 的每个元素总是恰好加到数组 a 的任何一个元素上一次。因此，数组 b 的所有元素之和+旧数组 a 的所有元素之和=新数组 a 的所有元素之和，设这个和为 s，新数组 a 的所有元素也相等。假设每个新元素是 x，如果数组 a 有 n 个元素，这就得到

```
 x * n = S
  => x = S/n     ....(1)
```

因此，新数组 a 的所有相等元素由等式(1)给出。现在要使每个 a(i)等于 x，我们需要给每个元素加上 x-a(i)。我们将迭代整个数组 a，并检查 a(i)是否可以等于 x。有多种可能性:
1。a(i) > x:在这种情况下，a(i)永远不能等于 x，所以输出-1。
2。a(i) + b(i) + b(i+1) = x .只需将 b(i) + b(i+1)添加到 a(i)中，并将 b(i)、b(i+1)更新为零。
3。a(i) + b(i) = x .将 b(i)添加到 a(i)并将 b(i)更新为零。
4。a(i) + b(i+1) = x .将 b(i+1)添加到 a(i)并将 b(i+1)更新为零。
数组 a 遍历完毕后，检查数组 b 的所有元素是否为零。如果是，则打印一个(0)，否则打印-1。
**为什么 b(i)相加后更新为零？**
考虑一个测试用例，其中 b(i)既没有被添加到 a(i-1)，也没有被添加到 a(i)。在这种情况下，我们必须把 b(i)加到 a(i+1)上。因此，当我们开始对元素 a(i)执行计算时，在对数组 a 进行迭代时，首先我们将元素 b(i-1)添加到 a(i)中，以考虑上述可能性。如果 b(i-1)已经被加到 a(i-1)或 a(i-2)上，那么，在这种情况下，它就不能被加到 a(i)上。所以为了避免 b(i)的双重加法，它被更新为零。
逐步算法为:

```
1\. Compute sum S and find x = S / n
2\. Iterate over array a
3\. for each element a(i) do:
   a(i) += b(i-1)
   b(i-1) = 0;
   if a(i) > x:
      break
   else:
     check for other three possibilities
     and update a(i) and b(i).
4\. Check whether all elements of b(i) are
   zero or not.
```

**执行:**

## C++

```
// CPP program to schedule jobs so that
// each server gets equal load.
#include <bits/stdc++.h>
using namespace std;

// Function to find new array a
int solve(int a[], int b[], int n)
{
    int i;
    long long int s = 0;

    // find sum S of both arrays a and b.
    for (i = 0; i < n; i++)
        s += (a[i] + b[i]);   

    // Single element case.
    if (n == 1)
        return a[0] + b[0];

    // This checks whether sum s can be divided
    // equally between all array elements. i.e.
    // whether all elements can take equal value
    // or not.
    if (s % n != 0)
        return -1;

    // Compute possible value of new array
    // elements.
    int x = s / n;

    for (i = 0; i < n; i++) {

        // Possibility 1
        if (a[i] > x)
            return -1;     

        // ensuring that all elements of
        // array b are used.
        if (i > 0) {
            a[i] += b[i - 1];
            b[i - 1] = 0;
        }

        // If a(i) already updated to x
        // move to next element in array a.
        if (a[i] == x)
            continue;

        // Possibility 2
        int y = a[i] + b[i];
        if (i + 1 < n)
            y += b[i + 1];
        if (y == x) {
            a[i] = y;
            b[i] = b[i + 1] = 0;
            continue;
        }

        // Possibility 3
        if (a[i] + b[i] == x) {
            a[i] += b[i];
            b[i] = 0;
            continue;
        }

        // Possibility 4
        if (i + 1 < n &&
            a[i] + b[i + 1] == x) {
            a[i] += b[i + 1];
            b[i + 1] = 0;
            continue;
        }

        // If a(i) can not be made equal
        // to x even after adding all
        // possible elements from b(i)
        // then print -1.
        return -1;
    }

    // check whether all elements of b
    // are used.
    for (i = 0; i < n; i++)
        if (b[i] != 0)
            return -1;   

    // Return the new array element value.
    return x;
}

int main()
{
    int a[] = { 6, 14, 21, 1 };
    int b[] = { 15, 7, 10, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << solve(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to schedule jobs so that
// each server gets equal load.
class GFG
{

// Function to find new array a
static int solve(int a[], int b[], int n)
{
    int i;
    int s = 0;

    // find sum S of both arrays a and b.
    for (i = 0; i < n; i++)
        s += (a[i] + b[i]);

    // Single element case.
    if (n == 1)
        return a[0] + b[0];

    // This checks whether sum s can be divided
    // equally between all array elements. i.e.
    // whether all elements can take equal value
    // or not.
    if (s % n != 0)
        return -1;

    // Compute possible value of new array
    // elements.
    int x = s / n;

    for (i = 0; i < n; i++)
    {

        // Possibility 1
        if (a[i] > x)
            return -1;    

        // ensuring that all elements of
        // array b are used.
        if (i > 0)
        {
            a[i] += b[i - 1];
            b[i - 1] = 0;
        }

        // If a(i) already updated to x
        // move to next element in array a.
        if (a[i] == x)
            continue;

        // Possibility 2
        int y = a[i] + b[i];
        if (i + 1 < n)
            y += b[i + 1];
        if (y == x)
        {
            a[i] = y;
            b[i]= 0;
            continue;
        }

        // Possibility 3
        if (a[i] + b[i] == x)
        {
            a[i] += b[i];
            b[i] = 0;
            continue;
        }

        // Possibility 4
        if (i + 1 < n &&
            a[i] + b[i + 1] == x)
        {
            a[i] += b[i + 1];
            b[i + 1] = 0;
            continue;
        }

        // If a(i) can not be made equal
        // to x even after adding all
        // possible elements from b(i)
        // then print -1.
        return -1;
    }

    // check whether all elements of b
    // are used.
    for (i = 0; i < n; i++)
        if (b[i] != 0)
            return -1;

    // Return the new array element value.
    return x;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 6, 14, 21, 1 };
    int b[] = { 15, 7, 10, 10 };
    int n = a.length;
    System.out.println(solve(a, b, n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to schedule jobs so that
# each server gets an equal load.

# Function to find new array a
def solve(a, b, n):

    s = 0

    # find sum S of both arrays a and b.
    for i in range(0, n):
        s += a[i] + b[i]    

    # Single element case.
    if n == 1:
        return a[0] + b[0]

    # This checks whether sum s can be divided
    # equally between all array elements. i.e.
    # whether all elements can take equal value
    # or not.
    if s % n != 0:
        return -1

    # Compute possible value of new
    # array elements.
    x = s // n

    for i in range(0, n):

        # Possibility 1
        if a[i] > x:
            return -1   

        # ensuring that all elements of
        # array b are used.
        if i > 0:
            a[i] += b[i - 1]
            b[i - 1] = 0

        # If a(i) already updated to x
        # move to next element in array a.
        if a[i] == x:
            continue

        # Possibility 2
        y = a[i] + b[i]
        if i + 1 < n:
            y += b[i + 1]

        if y == x:
            a[i] = y
            b[i] = 0
            if i + 1 < n: b[i + 1] = 0
            continue

        # Possibility 3
        if a[i] + b[i] == x:
            a[i] += b[i]
            b[i] = 0
            continue

        # Possibility 4
        if i + 1 < n and a[i] + b[i + 1] == x:
            a[i] += b[i + 1]
            b[i + 1] = 0
            continue

        # If a(i) can not be made equal
        # to x even after adding all
        # possible elements from b(i)
        # then print -1.
        return -1

    # check whether all elements of b
    # are used.
    for i in range(0, n):
        if b[i] != 0:
            return -1   

    # Return the new array element value.
    return x

# Driver Code
if __name__ == "__main__":

    a = [6, 14, 21, 1]
    b = [15, 7, 10, 10]
    n = len(a)
    print(solve(a, b, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to schedule jobs so that
// each server gets equal load.
using System;

class GFG
{

// Function to find new array a
static int solve(int []a, int []b, int n)
{
    int i;
    int s = 0;

    // find sum S of both arrays a and b.
    for (i = 0; i < n; i++)
        s += (a[i] + b[i]);

    // Single element case.
    if (n == 1)
        return a[0] + b[0];

    // This checks whether sum s can be divided
    // equally between all array elements. i.e.
    // whether all elements can take equal value
    // or not.
    if (s % n != 0)
        return -1;

    // Compute possible value of new array
    // elements.
    int x = s / n;

    for (i = 0; i < n; i++)
    {

        // Possibility 1
        if (a[i] > x)
            return -1;

        // ensuring that all elements of
        // array b are used.
        if (i > 0)
        {
            a[i] += b[i - 1];
            b[i - 1] = 0;
        }

        // If a(i) already updated to x
        // move to next element in array a.
        if (a[i] == x)
            continue;

        // Possibility 2
        int y = a[i] + b[i];
        if (i + 1 < n)
            y += b[i + 1];
        if (y == x)
        {
            a[i] = y;
            b[i]= 0;
            continue;
        }

        // Possibility 3
        if (a[i] + b[i] == x)
        {
            a[i] += b[i];
            b[i] = 0;
            continue;
        }

        // Possibility 4
        if (i + 1 < n &&
            a[i] + b[i + 1] == x)
        {
            a[i] += b[i + 1];
            b[i + 1] = 0;
            continue;
        }

        // If a(i) can not be made equal
        // to x even after adding all
        // possible elements from b(i)
        // then print -1.
        return -1;
    }

    // check whether all elements of b
    // are used.
    for (i = 0; i < n; i++)
        if (b[i] != 0)
            return -1;

    // Return the new array element value.
    return x;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 6, 14, 21, 1 };
    int []b = { 15, 7, 10, 10 };
    int n = a.Length;
    Console.WriteLine(solve(a, b, n));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to schedule jobs so that
// each server gets equal load.

 // Function to find new array a
function solve(a, b, n)
{
    let i;
    let s = 0;

    // find sum S of both arrays a and b.
    for (i = 0; i < n; i++)
        s += (a[i] + b[i]);

    // Single element case.
    if (n == 1)
        return a[0] + b[0];

    // This checks whether sum s can be divided
    // equally between all array elements. i.e.
    // whether all elements can take equal value
    // or not.
    if (s % n != 0)
        return -1;

    // Compute possible value of new array
    // elements.
    let x = s / n;

    for (i = 0; i < n; i++)
    {

        // Possibility 1
        if (a[i] > x)
            return -1;    

        // ensuring that all elements of
        // array b are used.
        if (i > 0)
        {
            a[i] += b[i - 1];
            b[i - 1] = 0;
        }

        // If a(i) already updated to x
        // move to next element in array a.
        if (a[i] == x)
            continue;

        // Possibility 2
        let y = a[i] + b[i];
        if (i + 1 < n)
            y += b[i + 1];
        if (y == x)
        {
            a[i] = y;
            b[i]= 0;
            continue;
        }

        // Possibility 3
        if (a[i] + b[i] == x)
        {
            a[i] += b[i];
            b[i] = 0;
            continue;
        }

        // Possibility 4
        if (i + 1 < n &&
            a[i] + b[i + 1] == x)
        {
            a[i] += b[i + 1];
            b[i + 1] = 0;
            continue;
        }

        // If a(i) can not be made equal
        // to x even after adding all
        // possible elements from b(i)
        // then print -1.
        return -1;
    }

    // check whether all elements of b
    // are used.
    for (i = 0; i < n; i++)
        if (b[i] != 0)
            return -1;

    // Return the new array element value.
    return x;
}

// Driver Code
    let a = [6, 14, 21, 1];
    let b = [15, 7, 10, 10];
    let n = a.length;
    document.write(solve(a, b, n));

// This code is contributed by avijitmondal1998.
</script>
```

**输出:**

```
21
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)如果不允许我们修改原始数组，那么 O(n)