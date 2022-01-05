# 给定数组所有可能的非空子集的值的乘积

> 原文:[https://www . geeksforgeeks . org/给定数组的所有可能非空子集的值的乘积/](https://www.geeksforgeeks.org/product-of-values-of-all-possible-non-empty-subsets-of-given-array/)

给定一个大小为 n 的数组，任务是找出给定数组中所有可能的非空子集的值的乘积。
**例:**

> **输入:** N = 2，arr[] = {3，7}
> **输出:** 441
> 所有非空子集为:
> 3
> 7
> 3，7
> 积= 3 * 7 * 3 * 7 = 441
> **输入:** N = 1，arr[] = {4}
> **输出:** 4

**方法:**仔细观察，可以推断出所有子集内每个元素的出现次数为**2<sup>N-1</sup>T5。因此，在最终的乘积中，数组中的每个元素都将乘以 **2 <sup>N-1</sup>** 次。** 

```
Product = a[0]2N-1*a[1]2N-1********a[N-1]2N-1
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find product of all elements
// in all subsets
int product(int a[], int n)
{
    int ans = 1;
    int val = pow(2, n - 1);

    for (int i = 0; i < n; i++) {
        ans *= pow(a[i], val);
    }

    return ans;
}

// Driver Code
int main()
{
    int n = 2;
    int a[] = { 3, 7 };

    cout << product(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find product of all elements
    // in all subsets
    static int product(int a[], int n)
    {
        int ans = 1;
        int val = (int)Math.pow(2, n - 1);

        for (int i = 0; i < n; i++)
        {
            ans *= (int)Math.pow(a[i], val);
        }
        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 2;
        int a[] = { 3, 7 };

        System.out.println(product(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find product of
# all elements in all subsets
def product(a, n):
    ans = 1
    val = pow(2, n - 1)

    for i in range(n):
        ans *= pow(a[i], val)

    return ans

# Driver Code
n = 2
a = [3, 7]

print(product(a, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find product of all elements
    // in all subsets
    static int product(int []a, int n)
    {
        int ans = 1;
        int val = (int)Math.Pow(2, n - 1);

        for (int i = 0; i < n; i++)
        {
            ans *= (int)Math.Pow(a[i], val);
        }
        return ans;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 2;
        int []a = { 3, 7 };

        Console.WriteLine(product(a, n));
    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find product of all elements
// in all subsets
function product(a, n)
{
    var ans = 1;
    var val = Math.pow(2, n - 1);

    for (var i = 0; i < n; i++) {
        ans *= Math.pow(a[i], val);
    }

    return ans;
}

// Driver Code
var n = 2;
a = [ 3, 7 ]

document.write(product(a, n));

</script>
```

**Output:** 

```
441
```

**时间复杂度:** O(N)