# 给定数组中修改的范围和，不更新

> 原文:[https://www . geesforgeks . org/修改范围-给定数组中的总和-无更新/](https://www.geeksforgeeks.org/modified-range-sum-in-a-given-array-without-updates/)

给定一个大小为 **N** 的数组 **arr[]** ，该数组包含从 1 到 N 的任意顺序的不同数字，任务是根据以下规则在该数组中执行修改后的范围和。
对于数组 **arr** 中的每个索引“**I**:

*   范围“ **L** 的起始指数选择为 **i +** 1
*   范围“ **R** 的结束指数选择为:
    *   **min(arr[i]，N-1)**；>如果我
    *   **最大值(i+1，arr[I])**；if arr[i] < i+1
*   对于更新，范围 arr[L]到 arr[R]中的值增加 1。
*   使用输入数组而不是更新后的数组找到范围

**例:**

> **输入:** arr[] = {4，1，3，2}
> **输出:** 4 2 5 4
> **解释:**
> For i = 0 - >输入数组中的元素= 4。因此，L = 1，R = min(4，N-1) = 3。因此，从 arr[1]到 arr[3]的所有元素都增加 1。更新操作后的元素是{4，2，4，3}。
> 对于 i = 1 - >输入数组中的元素= 1。因此 L = 2，R = max(1，i+1) = 2。因此，从 arr[2]到 arr[2]的所有元素都增加 1。更新操作后的元素是{4，2，5，3}。
> 对于 i = 2 - >输入数组中的元素= 3。因此，L = 3，R = min(3，N-1) = 3。因此，从 arr[3]到 arr[3]的所有元素都增加 1。更新操作后的元素是{4，2，5，4}。
> 对于 i = 3 - >数组不受影响。因此，更新操作后的元素是{4，2，5，4}。
> 得到的数组是{4，2，5，4}。
> **输入:** arr[] = {2，1}
> **输出:** {2，2}
> **解释:**
> 第一个元素是 2。所以 arr[1]加 1。因此，得到的数组是{2，2}。

**天真方法:**天真方法是为每个元素运行一个循环，并将 arr[i+1]到 arr[min(i+arr[i]，N-1)]的所有值增加 1。这个方法的时间复杂度是 **O(N <sup>2</sup> )** 。
**有效途径:**这个问题可以通过使用 O(N)的额外空间在 O(N)中解决。其思路是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念。按照以下步骤计算答案:

*   声明一个大小为 **N + 1** 的数组 **b[]** ，所有元素都用 0 初始化。
*   对于给定数组中的每个元素 arr[i]，1 被加到 **b[i+1]** 上，并从 **b[min(i + arr[i]，N–1)+1]【T3]中减去。**
*   然后，计算数组 **b[]** 的前缀和。
*   最后，arr 更新为 **arr[i] = arr[i] + b[i]** 。

以下是上述方法的实现:

## C++

```
// C++ program to find elements in an array
// after performing range updates.

#include <bits/stdc++.h>
using namespace std;

// Function to perform the update on the given
// input array arr[].
void update(vector<int>& arr,
            vector<int>& d, int n)
{

    // A new array of size N+1 is defined
    // and 1's are added in that array
    for (int i = 0; i < n - 1; i++) {
        d[i + 1] += 1;
        d[min(i + arr[i], n - 1) + 1] -= 1;
    }

    // Loop to perform the prefix sum
    // on the array d[].
    for (int i = 1; i < n; i++) {
        d[i] = d[i] + d[i - 1];
    }
}

// Function to print the final
// array after updation
void print(vector<int>& arr,
           vector<int>& d, int n)
{

    // Loop to add the values of d[i]
    // to arr[i]
    for (int i = 0; i < n; i++)
        cout << arr[i] + d[i] << " ";
}

// Function to perform modified range sum
void modifiedRangeSum(vector<int>& arr, int n)
{

    vector<int> d;

    // Loop to add N+1 0's in array d[]
    for (int i = 0; i <= n; i++)
        d.push_back(0);

    update(arr, d, n);
    print(arr, d, n);
}

// Driver code
int main()
{
    vector<int> arr = { 5, 4, 1, 3, 2 };
    int n = 5;

    modifiedRangeSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find elements in an array
// after performing range updates.
import java.util.*;

class GFG{

static ArrayList<Integer> arr = new
        ArrayList<Integer>(Arrays.asList(5, 4, 1, 3, 2));
static int n = 5;

// Function to perform the update on the given
// input array arr[].
static void update(ArrayList<Integer> d)
{

    // A new array of size N+1 is defined
    // and 1's are added in that array
    for (int i = 0; i < n - 1; i++) {
        d.set(i + 1,d.get(i+1)+1);
        int x = Math.min(i + arr.get(i), n - 1)+ 1;
        d.set(x,d.get(x)-1);
    }

    // Loop to perform the prefix sum
    // on the array d[].
    for (int i = 1; i < n; i++) {
        d.set(i,d.get(i)+d.get(i - 1));
    }
}

// Function to print the final
// array after updation
static void print(ArrayList<Integer> d)
{

    // Loop to add the values of d[i]
    // to arr[i]
    for (int i = 0; i < n; i++)
        System.out.print(arr.get(i) + d.get(i)+ " ");
}

// Function to perform modified range sum
static void modifiedRangeSum()
{

    ArrayList<Integer> d = new ArrayList<Integer>();

    // Loop to add N+1 0's in array d[]
    for (int i = 0; i <= n; i++)
        d.add(0);

    update(d);
    print(d);
}

// Driver code
public static void main(String args[])
{
    modifiedRangeSum();
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find elements in an array
# after performing range updates.
arr = []
d = []

# Function to perform the update on the given
# input array arr[].
def update( n):

    global d
    global arr

    # A new array of size N+1 is defined
    # and 1's are added in that array
    for i in range(n - 1):
        d[i + 1] += 1
        d[min(i + arr[i], n - 1) + 1] -= 1

    # Loop to perform the prefix sum
    # on the array d[].
    for i in range(n):
        d[i + 1] = d[i + 1] + d[i ]

# Function to print the final
# array after updation
def print_( n):

    global d
    global arr

    # Loop to add the values of d[i]
    # to arr[i]
    for i in range(n):
        x = (arr[i] + d[i] )
        print(x, end = " ")

# Function to perform modified range sum
def modifiedRangeSum( n):

    global d
    global arr

    d = []

    # Loop to add N+1 0's in array d[]
    for i in range(n + 1):
        d.append(0)

    update( n)
    print_(n)

# Driver code
arr = [5, 4, 1, 3, 2]
n = 5

modifiedRangeSum( n)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to find elements in an array
// after performing range updates.

using System;

class GFG {

// Function to perform the update on the given
// input array arr[].
static void update(int []arr,int [] d, int n){

    // A new array of size N+1 is defined
    // and 1's are added in that array
    for (int i = 0; i < n - 1; i++) {
        d[i + 1] += 1;
        d[Math.Min(i + arr[i], n - 1) + 1] -= 1;
    }

    // Loop to perform the prefix sum
    // on the array d[].
    for (int i = 1; i < n; i++) {
        d[i] = d[i] + d[i - 1];
    }
}

// Function to print the final
// array after updation
static void print(int []arr,int []d, int n)
{

    // Loop to add the values of d[i]
    // to arr[i]
    for (int i = 0; i < n; i++)
        Console.Write((arr[i] + d[i])+" ");
}

// Function to perform modified range sum
static void modifiedRangeSum(int []arr, int n)
{
    int []d= new int[n+1];

    // Loop to add N+1 0's in array d[]
    for (int i = 0; i <= n; i++)
        d[i]=0;

    update(arr, d, n);
    print(arr, d, n);
}

// Driver code
public static void Main()
  {
    int [] arr = { 5, 4, 1, 3, 2 };
    int n = 5;

    modifiedRangeSum(arr, n);
  }
} 

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program to find elements in an array
// after performing range updates.

// Function to perform the update on the given
// input array arr[].
function update(arr, d, n)
{

    // A new array of size N+1 is defined
    // and 1's are added in that array
    for (var i = 0; i < n - 1; i++) {
        d[i + 1] += 1;
        d[Math.min(i + arr[i], n - 1) + 1] -= 1;
    }

    // Loop to perform the prefix sum
    // on the array d[].
    for (var i = 1; i < n; i++) {
        d[i] = d[i] + d[i - 1];
    }
}

// Function to print the final
// array after updation
function print(arr, d, n)
{

    // Loop to add the values of d[i]
    // to arr[i]
    for (var i = 0; i < n; i++)
        document.write( arr[i] + d[i] + " ");
}

// Function to perform modified range sum
function modifiedRangeSum(arr, n)
{

    var d = [];

    // Loop to add N+1 0's in array d[]
    for (var i = 0; i <= n; i++)
        d.push(0);

    update(arr, d, n);
    print(arr, d, n);
}

// Driver code
var arr = [5, 4, 1, 3, 2];
var n = 5;
modifiedRangeSum(arr, n);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
5 5 3 6 5
```