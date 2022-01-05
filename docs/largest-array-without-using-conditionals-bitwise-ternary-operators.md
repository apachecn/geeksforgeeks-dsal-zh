# 不使用条件/按位/三元运算符时数组中最大的值

> 原文:[https://www . geeksforgeeks . org/不使用条件的最大数组-按位三元运算符/](https://www.geeksforgeeks.org/largest-array-without-using-conditionals-bitwise-ternary-operators/)

定义一个函数 int max(int a[]，int n)，该函数从由 n 个元素组成的整数数组中返回最大的整数(不使用条件/按位/三元运算符/库函数来查找最大的
**示例:**

```
Input : arr[] = {16, 14, 15, 17, 9}
Output : 17

Input : arr[] = {10, 13, 11, 13}
Output : 13
```

思路类似[最大四个数](https://www.geeksforgeeks.org/maximum-four-numbers-without-using-conditional-bitwise-operator/)。
我们使用“(x–y+ABS(x–y))”的值将是 0 的事实，x 小于或等于 y。我们使用该值作为大小为 2 的数组中的索引来选择最大值。一旦我们找到了两个元素的最大值，我们就可以使用相同的技术来找到所有元素的最大值。

## C++

```
// CPP program to find largest in an array
// without conditional/bitwise/ternary/ operators
// and without library functions.
#include <bits/stdc++.h>
using namespace std;

int maxArray(int a[], int n)
{
    int tmp[2];
    tmp[0] = a[0];
    for (int i = 1; i < n; i++) {
        tmp[1] = a[i];
        swap(tmp[0], tmp[bool(abs(tmp[1] - tmp[0]) +
                                  tmp[1] - tmp[0])]);
    }
    return tmp[0];
}

// Driver code
int main()
{
    int a[] = { 15, 11, 17, 16, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << maxArray(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find largest in an array
// without conditional/bitwise/ternary/ operators
// and without library functions.
import java.util.*;
class GFG
{

static int maxArray(int a[], int n)
{
    int []tmp = new int[2];
    tmp[0] = a[0];
    for (int i = 1; i < n-1; i++) {
        tmp[1] = a[i];

        int temp = tmp[0];
        tmp[0] = tmp[(Math.abs(tmp[1] - tmp[0]) +
                tmp[1] - tmp[0])%2+1];
        tmp[(Math.abs(tmp[1] - tmp[0]) +
                tmp[1] - tmp[0])%2+1] = temp;
    }
    return tmp[1];
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 15, 11, 17, 16, 10 };
    int n =a.length;
    System.out.print(maxArray(a, n));
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python 3 program to find largest in an array
# without conditional/bitwise/ternary/ operators
# and without library functions.

def maxArray(a, n):
    tmp = [a[i] for i in range(len(a))]
    tmp[0] = a[0]
    for i in range(1,n,1):
        tmp[1] = a[i]
        temp = tmp[int(bool(abs(tmp[1] - tmp[0]) +
                                tmp[1] - tmp[0]))]
        tmp[int(bool(abs(tmp[1] - tmp[0]) +
                         tmp[1] - tmp[0]))] = tmp[0]
        tmp[0] = temp

    return tmp[0]

# Driver code
if __name__ == '__main__':
    a = [15, 11, 17, 16, 10]
    n = len(a)
    print(maxArray(a, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find largest in an array
// without conditional/bitwise/ternary/ operators
// and without library functions.
using System;

public class GFG {

    static int maxArray(int[] a, int n)
    {
        int[] tmp = new int[2];
        tmp[0] = a[0];
        for (int i = 1; i < n - 1; i++) {
            tmp[1] = a[i];

            int temp = tmp[0];
            tmp[0] = tmp[(Math.Abs(tmp[1] - tmp[0]) + tmp[1]
                          - tmp[0]) % 2 + 1];
            tmp[(Math.Abs(tmp[1] - tmp[0]) + tmp[1]
                 - tmp[0]) % 2 + 1] = temp;
        }
        return tmp[1];
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 15, 11, 17, 16, 10 };
        int n = a.Length;
        Console.Write(maxArray(a, n));
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>

// JavaScript program to find largest in an array
// without conditional/bitwise/ternary/ operators
// and without library functions.
function maxArray(a, n)
{
    var tmp = new Array(2);
    tmp[0] = a[0];
    for (var i = 1; i < n-1; i++) {
        tmp[1] = a[i];

        var temp = tmp[0];
        tmp[0] = tmp[(Math.abs(tmp[1] - tmp[0]) +
                tmp[1] - tmp[0])%2+1];
        tmp[(Math.abs(tmp[1] - tmp[0]) +
                tmp[1] - tmp[0])%2+1] = temp;
    }
    return tmp[1];
}

// Driver code
    var a = [ 15, 11, 17, 16, 10 ];
    var n =a.length;
    document.write(maxArray(a, n));

// This code is contributed by shivanisinghss2110
</script>
```

**输出:**

```
17
```