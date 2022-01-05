# 通过将 arr[i]替换为(arr[i-1]+1) % M

来重构数组

> 原文:[https://www . geeksforgeeks . org/通过用 arri-11-m 替换 arri 来重建阵列/](https://www.geeksforgeeks.org/reconstruct-the-array-by-replacing-arri-with-arri-11-m/)

给定一个由 N 个元素和一个整数 m 组成的数组。现在，通过用-1 替换一些数组元素来修改数组。任务是打印原始数组。
在**原始数组**中的元素是相关的，对于每个索引 I， **a[i] = (a[i-1]+1)% M** 。
保证数组中有一个非零值。

**示例**:

```
Input: arr[] = {5, -1, -1, 1, 2, 3}, M = 7
Output: 5 6 0 1 2 3
M = 7, so value at index 2 should be (5+1) % 7 = 6
value at index 3 should be (6+1) % 7 = 0

Input: arr[] = {5, -1, 7, -1, 9, 0}, M = 10
Output: 5 6 7 8 9 0 
```

**做法:**先找到非负值指标 I 的指标，然后简单的往两个方向走，即从 i-1 到 0，i+1 到 n。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

void construct(int n, int m, int a[])
{
    int ind = 0;

    // Finding the index which is not -1
    for (int i = 0; i < n; i++)
    {
        if (a[i] != -1)
        {
            ind = i;
            break;
        }
    }

    // Calculating the values of
    // the indexes ind-1 to 0
    for (int i = ind - 1; i > -1; i--)
    {
        if (a[i] == -1)
            a[i] = (a[i + 1] - 1 + m) % m;
    }

    // Calculating the values of
    // the indexes ind + 1 to n
    for (int i = ind + 1; i < n; i++)
    {
        if (a[i] == -1)
            a[i] = (a[i - 1] + 1) % m;
    }
    for (int i = 0; i < n; i++)
    {
        cout<< a[i] << " ";
    }

}

// Driver code
int main()
{

    int n = 6, m = 7;
    int a[] = { 5, -1, -1, 1, 2, 3 };
    construct(n, m, a);
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    static void construct(int n, int m, int[] a)
    {
        int ind = 0;

        // Finding the index which is not -1
        for (int i = 0; i < n; i++)
        {
            if (a[i] != -1)
            {
                ind = i;
                break;
            }
        }

        // Calculating the values of
        // the indexes ind-1 to 0
        for (int i = ind - 1; i > -1; i--)
        {
            if (a[i] == -1)
                a[i] = (a[i + 1] - 1 + m) % m;
        }

        // Calculating the values of
        // the indexes ind + 1 to n
        for (int i = ind + 1; i < n; i++)
        {
            if (a[i] == -1)
                a[i] = (a[i - 1] + 1) % m;
        }
        for (int i = 0; i < n; i++)
        {
            System.out.print(a[i] + " ");
        }

    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 6, m = 7;
        int[] a = { 5, -1, -1, 1, 2, 3 };
        construct(n, m, a);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the above approach
def construct(n, m, a):
    ind = 0

    # Finding the index which is not -1
    for i in range(n):
        if (a[i]!=-1):
            ind = i
            break

    # Calculating the values of the indexes ind-1 to 0
    for i in range(ind-1, -1, -1):
        if (a[i]==-1):
            a[i]=(a[i + 1]-1 + m)% m

    # Calculating the values of the indexes ind + 1 to n
    for i in range(ind + 1, n):
        if(a[i]==-1):
            a[i]=(a[i-1]+1)% m
    print(*a)

# Driver code
n, m = 6, 7
a =[5, -1, -1, 1, 2, 3]
construct(n, m, a)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static void construct(int n, int m, int[] a)
    {
        int ind = 0;

        // Finding the index which is not -1
        for (int i = 0; i < n; i++)
        {
            if (a[i] != -1)
            {
                ind = i;
                break;
            }
        }

        // Calculating the values of
        // the indexes ind-1 to 0
        for (int i = ind - 1; i > -1; i--)
        {
            if (a[i] == -1)
                a[i] = (a[i + 1] - 1 + m) % m;
        }

        // Calculating the values of
        // the indexes ind + 1 to n
        for (int i = ind + 1; i < n; i++)
        {
            if (a[i] == -1)
                a[i] = (a[i - 1] + 1) % m;
        }
        for (int i = 0; i < n; i++)
        {
            Console.Write(a[i] + " ");
        }

    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 6, m = 7;
        int[] a = { 5, -1, -1, 1, 2, 3 };
        construct(n, m, a);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

function construct(n, m, a)
{
    var ind = 0;

    // Finding the index which is not -1
    for (var i = 0; i < n; i++)
    {
        if (a[i] != -1)
        {
            ind = i;
            break;
        }
    }

    // Calculating the values of
    // the indexes ind-1 to 0
    for (var i = ind - 1; i > -1; i--)
    {
        if (a[i] == -1)
            a[i] = (a[i + 1] - 1 + m) % m;
    }

    // Calculating the values of
    // the indexes ind + 1 to n
    for (var i = ind + 1; i < n; i++)
    {
        if (a[i] == -1)
            a[i] = (a[i - 1] + 1) % m;
    }
    for (var i = 0; i < n; i++)
    {
        document.write( a[i] + " ");
    }

}

// Driver code
var n = 6, m = 7;
var a = [5, -1, -1, 1, 2, 3];
construct(n, m, a);

</script>
```

**Output:** 

```
5 6 0 1 2 3
```