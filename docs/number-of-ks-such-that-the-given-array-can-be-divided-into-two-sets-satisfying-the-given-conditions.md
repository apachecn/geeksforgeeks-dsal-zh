# K 的个数，使得给定的数组可以分成满足给定条件的两组

> 原文:[https://www . geeksforgeeks . org/k-number-of-ks-so-给定数组可以被分成满足给定条件的两个集合/](https://www.geeksforgeeks.org/number-of-ks-such-that-the-given-array-can-be-divided-into-two-sets-satisfying-the-given-conditions/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是找到 **K** 的数量，这样如果一个集合中有少于 **K** 的元素，而其余的元素在另一个集合中，那么这个数组就可以被分成包含相同数量元素的两个集合。
**注** : **N** 始终为偶数。

**示例:**

> **输入:** arr[] = {9，1，4，4，6，7}
> **输出:** 2
> {1，4，4}和{6，7，9}是两套。
> K 可以是 5 或 6。
> **输入:** arr[] = {1，2，3，3，4，5}
> **输出:** 0

**方法:**一个有效的方法是[排序](https://www.geeksforgeeks.org/merge-sort/)数组。那么如果两个中间数相同，那么答案是零，否则答案是两个数之差。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of K's
// such that the array can be divided
// into two sets containing equal number
// of elements when all the elements less
// than K are in one set and the rest
// of the elements are in the other set
int two_sets(int a[], int n)
{
    // Sort the given array
    sort(a, a + n);

    // Return number of such Ks
    return a[n / 2] - a[(n / 2) - 1];
}

// Driver code
int main()
{
    int a[] = { 1, 4, 4, 6, 7, 9 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << two_sets(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of K's
// such that the array can be divided
// into two sets containing equal number
// of elements when all the elements less
// than K are in one set and the rest
// of the elements are in the other set
static int two_sets(int a[], int n)
{
    // Sort the given array
    Arrays.sort(a);

    // Return number of such Ks
    return a[n / 2] - a[(n / 2) - 1];
}

// Driver code
public static void main(String []args)
{
    int a[] = { 1, 4, 4, 6, 7, 9 };
    int n = a.length;

    System.out.println(two_sets(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of K's
# such that the array can be divided
# into two sets containing equal number
# of elements when all the elements less
# than K are in one set and the rest
# of the elements are in the other set
def two_sets(a, n) :

    # Sort the given array
    a.sort();

    # Return number of such Ks
    return (a[n // 2] - a[(n // 2) - 1]);

# Driver code
if __name__ == "__main__" :

    a = [ 1, 4, 4, 6, 7, 9 ];
    n = len(a);

    print(two_sets(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of K's
// such that the array can be divided
// into two sets containing equal number
// of elements when all the elements less
// than K are in one set and the rest
// of the elements are in the other set
static int two_sets(int []a, int n)
{
    // Sort the given array
    Array.Sort(a);

    // Return number of such Ks
    return a[n / 2] - a[(n / 2) - 1];
}

// Driver code
public static void Main(String []args)
{
    int []a = { 1, 4, 4, 6, 7, 9 };
    int n = a.Length;

    Console.WriteLine(two_sets(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the count of K's
    // such that the array can be divided
    // into two sets containing equal number
    // of elements when all the elements less
    // than K are in one set and the rest
    // of the elements are in the other set
    function two_sets(a , n) {
        // Sort the given array
        a.sort();

        // Return number of such Ks
        return a[n / 2] - a[(n / 2) - 1];
    }

    // Driver code

        var a = [ 1, 4, 4, 6, 7, 9 ];
        var n = a.length;

        document.write(two_sets(a, n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
2
```