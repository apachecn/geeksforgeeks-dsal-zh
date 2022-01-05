# 给定范围内 AP 元素的总和

> 原文:[https://www . geeksforgeeks . org/给定范围内 ap 元素之和/](https://www.geeksforgeeks.org/sum-of-elements-of-an-ap-in-the-given-range/)

在 **arr** 和 **Q** 中给定一个算术数列，以**【L，R】**的形式查询，其中 **L** 是范围的左边界， **R** 是右边界。任务是[求给定范围内 AP](https://www.geeksforgeeks.org/program-sum-arithmetic-series/) 元素的和。
**注:**范围为 1-索引，1 ≤ L，R ≤ N，其中 N 为 arr 的大小。
**举例:**

> **输入:** arr[] = {2，4，6，8，10，12，14，16}，Q = [[2，4]，[2，6]，[5，8]]
> **输出:**
> 18
> 40
> 52
> **说明:**
> 范围 1: arr = {4，6，8}。因此总和= 18
> 范围 2: arr = {4，6，8，10，12}。因此总和= 40
> 范围 3: arr = {10，12，14，16}。因此 sum = 52
> **输入:** arr[] = {7，14，21，28，35，42}，Q = [[1，6]，[2，4]，[3，3]]
> **输出:**
> 147
> 63
> 21
> **解释:**
> 范围 1: arr = {7，14，21，28，35 因此总和= 147
> 范围 2: arr = {14，21，28}。因此总和= 63
> 范围 3: arr = {21}。因此总和= 21

**逼近**:由于给定的序列是一个[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)，所以可以很容易地分两步高效地求出总和:

1.  将范围的第一个元素乘以范围中的元素数。
2.  加上 **(d*k*(k+1))/2** ，其中 **d** 是 AP 和 **k** 的公差，对应的是间隙数(范围内的元素数–1)。

**例如:**
假设 a[i]是范围的第一个元素， **d** 是 AP 和 **k+1** 的共同区别，是给定范围内的元素个数。
那么范围的总和就是

> = a[i] + a[i+1] + a[i+2] + …..+a[I+k]
> = a[I]+a[I]+d+a[I]+2 * d+…。+a[I]+k * d
> = a[I]*(k+1)+d *(1+2+…+k)
> = a[I]*(k+1)+(d * k *(k+1))/2

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the sum of elements
// of an AP in the given range

#include <bits/stdc++.h>
using namespace std;

// Function to find sum in the given range
int findSum(int* arr, int n,
            int left, int right)
{
    // Find the value of k
    int k = right - left;

    // Find the common difference
    int d = arr[1] - arr[0];

    // Find the sum
    int ans = arr[left - 1] * (k + 1);
    ans = ans + (d * (k * (k + 1))) / 2;

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6, 8, 10, 12, 14, 16 };
    int queries = 3;
    int q[queries][2] = { { 2, 4 },
                          { 2, 6 },
                          { 5, 6 } };
    int n = sizeof(arr) / sizeof(arr[0]);

    for (int i = 0; i < queries; i++)
        cout << findSum(arr, n, q[i][0], q[i][1])
             << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of elements
// of an AP in the given range
class GFG{

// Function to find sum in the given range
static int findSum(int []arr, int n,
            int left, int right)
{
    // Find the value of k
    int k = right - left;

    // Find the common difference
    int d = arr[1] - arr[0];

    // Find the sum
    int ans = arr[left - 1] * (k + 1);
    ans = ans + (d * (k * (k + 1))) / 2;

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 6, 8, 10, 12, 14, 16 };
    int queries = 3;
    int q[][] = { { 2, 4 },
                          { 2, 6 },
                          { 5, 6 } };
    int n = arr.length;

    for (int i = 0; i < queries; i++)
        System.out.print(findSum(arr, n, q[i][0], q[i][1])
             +"\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program to find the sum of elements
# of an AP in the given range

# Function to find sum in the given range
def findSum(arr, n, left, right):

    # Find the value of k
    k = right - left;

    # Find the common difference
    d = arr[1] - arr[0];

    # Find the sum
    ans = arr[left - 1] * (k + 1);
    ans = ans + (d * (k * (k + 1))) // 2;

    return ans;

# Driver code
if __name__ == '__main__':
    arr = [ 2, 4, 6, 8, 10, 12, 14, 16 ];
    queries = 3;
    q = [[ 2, 4 ],[ 2, 6 ],[ 5, 6 ]];
    n = len(arr);

    for i in range(queries):
        print(findSum(arr, n, q[i][0], q[i][1]));

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program to find the sum of elements
// of an AP in the given range
using System;

class GFG{

// Function to find sum in the given range
static int findSum(int []arr, int n,
            int left, int right)
{
    // Find the value of k
    int k = right - left;

    // Find the common difference
    int d = arr[1] - arr[0];

    // Find the sum
    int ans = arr[left - 1] * (k + 1);
    ans = ans + (d * (k * (k + 1))) / 2;

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 4, 6, 8, 10, 12, 14, 16 };
    int queries = 3;
    int [,]q = { { 2, 4 },
                          { 2, 6 },
                          { 5, 6 } };
    int n = arr.Length;

    for (int i = 0; i < queries; i++)
        Console.Write(findSum(arr, n, q[i,0], q[i,1])
             +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find the sum of elements
// of an AP in the given range

// Function to find sum in the given range
function findSum(arr, n, left, right)
{
    // Find the value of k
    let k = right - left;

    // Find the common difference
    let d = arr[1] - arr[0];

    // Find the sum
    let ans = arr[left - 1] * (k + 1);
    ans = ans + (d * (k * (k + 1))) / 2;

    return ans;
}

// Driver Code

    let arr = [ 2, 4, 6, 8, 10, 12, 14, 16 ];
    let queries = 3;
    let q = [[ 2, 4 ],
             [ 2, 6 ],
             [ 5, 6 ]];
    let n = arr.length;

    for (let i = 0; i < queries; i++)
        document.write(findSum(arr, n, q[i][0], q[i][1])
             +"<br/>");

</script>
```

**Output:** 

```
18
40
22
```

***时间复杂度:** O(1)*
***空间复杂度:** O(1)*