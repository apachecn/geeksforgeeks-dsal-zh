# 将阵列反转到给定位置

> 原文:[https://www . geeksforgeeks . org/reverse-a-array-up-a-给定位置/](https://www.geeksforgeeks.org/reverse-an-array-upto-a-given-position/)

给定数组 arr[]和数组 k 中的一个位置，写一个函数名 reverse (a[]，k)，这样它就可以反转子数组 arr[0..k-1]。使用的额外空间应为 0(1)，时间复杂度应为 0(k)。
例:

```
Input:
arr[] = {1, 2, 3, 4, 5, 6}
    k = 4

Output:
arr[] = {4, 3, 2, 1, 5, 6} 
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
下图为同一个实施。

## C++

```
// C++ program to reverse a subarray arr[0..k-1]
#include <bits/stdc++.h>
using namespace std;

// Reverse subarray a[0..k-1]
void reverse(int a[], int n, int k)
{
    if (k > n)
    {
        cout << "Invalid k";
        return;
    }

    // One by one reverse first and last elements of a[0..k-1]
    for (int i = 0; i < k/2; i++)
        swap(a[i], a[k-i-1]);
}

// Driver program
int main()
{
    int a[] = {1, 2, 3, 4, 5, 6};
    int n = sizeof(a) / sizeof(int), k = 4;

    reverse(a, n, k);

    for (int i = 0; i < n; ++i)
        printf("%d ", a[i]);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to reverse a
// subarray arr[0..k-1]

public class GFG {

    // Reverse subarray a[0..k-1]
    static void reverse(int []a, int n, int k)
    {
        if (k > n)
        {
            System.out.println( "Invalid k");
            return;
        }

        // One by one reverse first
        // and last elements of a[0..k-1]
        for (int i = 0; i < k / 2; i++)
        {
            int tempswap = a[i];
                a[i] = a[k - i - 1];
                a[k - i - 1] = tempswap;            
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int []a = {1, 2, 3, 4, 5, 6};
        int n = a.length, k = 4;
        reverse(a, n, k);
        for (int i = 0; i < n; ++i)
            System.out.print(a[i] + " ");
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# python program to reverse a subarray
# arr[0..k-1]
from __future__ import print_function

# Reverse subarray a[0..k-1]
def reverse(a, n, k):

    if (k > n):
        print( "Invalid k")
        return

    # One by one reverse first and
    # last elements of a[0..k-1]
    for i in range(0, (int)(k/2)):
        temp = a[i]
        a[i] = a[k-i-1]
        a[k-i-1] = temp

# Driver program
a = [1, 2, 3, 4, 5, 6]
n = len(a)
k = 4

reverse(a, n, k);

for i in range(0, n):
    print(a[i], end=" ")

# This code is contributed by Sam007.
```

## C#

```
// C# program to reverse a
// subarray arr[0..k-1]
using System;

class GFG {

static void SwapNum(ref int x, ref int y)
{
    int tempswap = x;
    x = y;
    y = tempswap;            
}

// Reverse subarray a[0..k-1]
static void reverse(int []a, int n,
                             int k)
{
    if (k > n)
    {
        Console.Write( "Invalid k");
        return;
    }

    // One by one reverse first
    // and last elements of a[0..k-1]
    for (int i = 0; i < k / 2; i++)
        SwapNum(ref a[i], ref a[k - i - 1]);

}

// Driver Code
public static void Main()
{
    int []a = {1, 2, 3, 4, 5, 6};
    int n = a.Length, k = 4;

    reverse(a, n, k);

    for (int i = 0; i < n; ++i)
        Console.Write(a[i] + " ");
}
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

// Javascript program to reverse
// a subarray arr[0..k-1]

// Reverse subarray a[0..k-1]
function reverse( a, n, k)
{
    if (k > n)
    {
        document.write("Invalid k");
        return;
    }

    // One by one reverse first
    // and last elements of a[0..k-1]
    for (let i = 0; i < Math.floor(k/2); i++)
    {
      let temp = a[i] ;
      a[i] = a[k-i-1] ;
      a[k-i-1] = temp ;
    }

}
    // driver code

    let a = [1, 2, 3, 4, 5, 6];
    let n = a.length, k = 4;

    reverse(a, n, k);

    for (let i = 0; i < n; ++i)
        document.write(a[i] + " ");

</script>
```

**输出:**

```
4 3 2 1 5 6
```

时间复杂度:O(k)
如果发现有不正确的地方，或者想分享更多以上讨论话题的信息请写评论