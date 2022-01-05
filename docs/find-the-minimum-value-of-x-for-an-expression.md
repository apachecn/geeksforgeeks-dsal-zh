# 求一个表达式的 X 的最小值

> 原文:[https://www . geesforgeks . org/find-表达式的 x 的最小值/](https://www.geeksforgeeks.org/find-the-minimum-value-of-x-for-an-expression/)

给定数组 **arr[]** 。任务是找到 x 的值，使得表达式(a[1]–x)^2+(a[2]–x)^2+(a[3]–x)^2+……(a[n-1]–x)^2+(a[n]–x)^2)的结果最小。
**例:**

> **输入:** arr[] = {6，9，1，6，1，3，7}
> **输出:** 5
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 3

**方法:**
我们可以简化我们需要最小化的表达式。表达式可以写成

```
(A[1]^2 + A[2]^2 + A[3]^2 + … + A[n]^2) + nX^2 – 2X(A[1] + A[2] + A[3] + … + A[n])
```

通过区分上述表达式，我们得到

```
 2nX - 2(A[1] + A[2] + A[3] + … + A[n])
```

我们可以将术语(A[1] + A[2] + A[3] + … + A[n])表示为 s。我们得到

```
 2nX - 2S 
```

放 2Nx–2S = 0，我们得到

```
 X = S/N 
```

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate value of X
int valueofX(int ar[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum = sum + ar[i];
    }

    if (sum % n == 0) {
        return sum / n;
    }
    else {
        int A = sum / n, B = sum / n + 1;
        int ValueA = 0, ValueB = 0;

        // Check for both possibilities
        for (int i = 0; i < n; i++) {
            ValueA += (ar[i] - A) * (ar[i] - A);
            ValueB += (ar[i] - B) * (ar[i] - B);
        }

        if (ValueA < ValueB) {
            return A;
        }
        else {
            return B;
        }
    }
}

// Driver Code
int main()
{
    int n = 7;
    int arr[7] = { 6, 9, 1, 6, 1, 3, 7 };

    cout << valueofX(arr, n) << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to calculate value of X
static int valueofX(int ar[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
    {
        sum = sum + ar[i];
    }

    if (sum % n == 0)
    {
        return sum / n;
    }
    else
    {
        int A = sum / n, B = sum / n + 1;
        int ValueA = 0, ValueB = 0;

        // Check for both possibilities
        for (int i = 0; i < n; i++)
        {
            ValueA += (ar[i] - A) * (ar[i] - A);
            ValueB += (ar[i] - B) * (ar[i] - B);
        }

        if (ValueA < ValueB)
        {
            return A;
        }
        else
        {
            return B;
        }
    }
}

// Driver Code
public static void main(String args[])
{
    int n = 7;
    int arr[] = { 6, 9, 1, 6, 1, 3, 7 };

    System.out.println(valueofX(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to calculate value of X
def valueofX(ar, n):
    summ = sum(ar)

    if (summ % n == 0):
        return summ // n
    else:
        A = summ // n
        B = summ // n + 1
        ValueA = 0
        ValueB = 0

        # Check for both possibilities
        for i in range(n):
            ValueA += (ar[i] - A) * (ar[i] - A)
            ValueB += (ar[i] - B) * (ar[i] - B)

        if (ValueA < ValueB):
            return A
        else:
            return B

# Driver Code
n = 7
arr = [6, 9, 1, 6, 1, 3, 7]

print(valueofX(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to calculate value of X
static int valueofX(int []ar, int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
    {
        sum = sum + ar[i];
    }

    if (sum % n == 0)
    {
        return sum / n;
    }
    else
    {
        int A = sum / n, B = sum / n + 1;
        int ValueA = 0, ValueB = 0;

        // Check for both possibilities
        for (int i = 0; i < n; i++)
        {
            ValueA += (ar[i] - A) * (ar[i] - A);
            ValueB += (ar[i] - B) * (ar[i] - B);
        }

        if (ValueA < ValueB)
        {
            return A;
        }
        else
        {
            return B;
        }
    }
}

// Driver Code
public static void Main(String []args)
{
    int n = 7;
    int []arr = { 6, 9, 1, 6, 1, 3, 7 };

    Console.WriteLine(valueofX(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript implementation of above approach

// Function to calculate value of X
function valueofX(ar, n)
{
    let sum = 0;
    for (let i = 0; i < n; i++) {
        sum = sum + ar[i];
    }

    if (sum % n == 0) {
        return Math.floor(sum / n);
    }
    else {
        let A = Math.floor(sum / n), B = Math.floor(sum / n + 1);
        let ValueA = 0, ValueB = 0;

        // Check for both possibilities
        for (let i = 0; i < n; i++) {
            ValueA += (ar[i] - A) * (ar[i] - A);
            ValueB += (ar[i] - B) * (ar[i] - B);
        }

        if (ValueA < ValueB) {
            return A;
        }
        else {
            return B;
        }
    }
}

// Driver Code
    let n = 7;
    let arr = [ 6, 9, 1, 6, 1, 3, 7 ];

    document.write(valueofX(arr, n) + "<br>");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(n)