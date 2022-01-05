# 数组中的减法

> 原文:[https://www.geeksforgeeks.org/subtraction-in-the-array/](https://www.geeksforgeeks.org/subtraction-in-the-array/)

给定一个整数 **k** 和一个数组**arr【】**，任务是精确地重复以下操作 **k** 次:
找到数组中的最小非零元素，打印出来，然后从数组的所有非零元素中减去这个数。如果数组的所有元素都是 **< 0** ，只需打印 **0** 。
**举例:**

> **输入:** arr[] = {3，6，4，2}，k = 5
> T3】输出:2 1 2 0
> k = 1；选择 2 并更新 arr[] = {1，4，2，0 }
> k = 2；Pick 1，arr[] = {0，3，1，0 }
> k = 3；Pick 1，arr[] = {0，2，0，0 }
> k = 4；Pick 2，arr[] = {0，0，0，0 }
> k = 5；没什么可挑的所以打印 0
> **输入:** arr[] = {1，2}，k = 3
> **输出:** 1 1 0

**方法:**对数组进行排序，取一个名为 **sum** 的额外变量，该变量将存储**之前的元素**，该元素变为 **0** 。
取 **arr[] = {3，6，4，2}** 并在数组排序后初始 **sum = 0** ，则变为 **arr[] = {2，3，4，6}** 。
现在 **sum = 0** ，我们打印第一个非零元素即 **2** ，赋值 **sum = 2** 。
在下一次迭代中，选择第二个元素即 **3** 并打印**3–sum**即 **1** ，因为 **2** 已经从所有其他非零元素中减去。精确重复这些步骤 **k** 次。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to perform the given operation on arr[]
void operations(int arr[], int n, int k)
{
    sort(arr, arr + n);
    ll i = 0, sum = 0;
    while (k--) {

        // Skip elements which are 0
        while (i < n && arr[i] - sum == 0)
            i++;

        // Pick smallest non-zero element
        if (i < n && arr[i] - sum > 0) {
            cout << arr[i] - sum << " ";
            sum = arr[i];
        }

        // If all the elements of arr[] are 0
        else
            cout << 0 << endl;
    }
}

// Driver code
int main()
{
    int k = 5;
    int arr[] = { 3, 6, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    operations(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to perform the given operation on arr[]
static void operations(int arr[], int n, int k)
{
    Arrays.sort(arr);
    int i = 0, sum = 0;
    while (k-- > 0)
    {

        // Skip elements which are 0
        while (i < n && arr[i] - sum == 0)
            i++;

        // Pick smallest non-zero element
        if (i < n && arr[i] - sum > 0)
        {
            System.out.print(arr[i] - sum + " ");
            sum = arr[i];
        }

        // If all the elements of arr[] are 0
        else
            System.out.println("0");
    }
}

// Driver code
public static void main(String args[])
{
    int k = 5;
    int arr[] = { 3, 6, 4, 2 };
    int n = arr.length;
    operations(arr, n, k);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```

# Python implementation of the approach

# Function to perform the given operation on arr[]
def operations(arr, n, k):
    arr.sort();
    i = 0; sum = 0;
    while (k > 0):

        # Skip elements which are 0
        while (i < n and arr[i] - sum == 0):
            i+=1;

        # Pick smallest non-zero element
        if (i < n and arr[i] - sum > 0):
            print(arr[i] - sum, end= " ");
            sum = arr[i];

        # If all the elements of arr[] are 0
        else:
            print(0);
        k-=1;

# Driver code
k = 5;
arr = [ 3, 6, 4, 2 ];
n = len(arr);
operations(arr, n, k);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to perform the given operation on arr[]
static void operations(int []arr, int n, int k)
{
    Array.Sort(arr);
    int i = 0, sum = 0;
    while (k-- > 0)
    {

        // Skip elements which are 0
        while (i < n && arr[i] - sum == 0)
            i++;

        // Pick smallest non-zero element
        if (i < n && arr[i] - sum > 0)
        {
            Console.Write(arr[i] - sum + " ");
            sum = arr[i];
        }

        // If all the elements of arr[] are 0
        else
            Console.WriteLine("0");
    }
}

// Driver code
public static void Main(String []args)
{
    int k = 5;
    int []arr = { 3, 6, 4, 2 };
    int n = arr.Length;
    operations(arr, n, k);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program implementation of the approach

// Function to perform the given operation on arr[]
function operations(arr, n, k)
{
    arr.sort();
    let i = 0, sum = 0;
    while (k-- > 0)
    {

        // Skip elements which are 0
        while (i < n && arr[i] - sum == 0)
            i++;

        // Pick smallest non-zero element
        if (i < n && arr[i] - sum > 0)
        {
            document.write(arr[i] - sum + " ");
            sum = arr[i];
        }

        // If all the elements of arr[] are 0
        else
            document.write("0");
    }
}

// Driver code

    let k = 5;
    let arr = [ 3, 6, 4, 2 ];
    let n = arr.length;
    operations(arr, n, k);  

</script>
```

**Output:** 

```
2 1 1 2 0
```