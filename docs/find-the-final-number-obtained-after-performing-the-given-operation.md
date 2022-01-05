# 求执行给定操作后得到的最终数字

> 原文:[https://www . geeksforgeeks . org/find-执行给定操作后获得的最终号码/](https://www.geeksforgeeks.org/find-the-final-number-obtained-after-performing-the-given-operation/)

给定一个正的不同整数的数组 **arr[]** ，任务是通过对数组的元素执行以下操作来找到最终的数:
**操作:**取两个不相等的数，用它们的差替换较大的数，直到所有的数都相等。
**例:**

> **输入:** arr[] = {5，2，3}
> **输出:**1
> 5–3 = 2，arr[] = {2，2，3 }
> 3–2 = 1，arr[] = {2，2，1 }
> 2–1 = 1，arr[] = {2，1，1 }
> 2–1 = 1，arr[] = {1，1，1}
> **输入:** arr[] = {3，9

**天真的方法:**由于最终答案总是截然不同的，人们可以只[排序](https://www.geeksforgeeks.org/merge-sort/)数组，用两个最大元素的差替换最大的项，并重复这个过程，直到所有的数字变得相等。
**高效途径:**从[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)可知 **gcd(a，b)= gcd(a–b，b)** 。这可以扩展到 **gcd(A <sub>1</sub> 、A <sub>2</sub> 、A <sub>3</sub> 、…、A<sub>n</sub>)= gcd(A<sub>1</sub>–A<sub>2</sub>、A <sub>2</sub> 、A <sub>3</sub> 、…、A <sub>n</sub> )** 。
同样，假设应用给定的运算后，得到的最终数为 K，因此，从扩展的算法中，可以说 **gcd(A <sub>1</sub> ，A <sub>2</sub> ，A <sub>3</sub> ，…，A <sub>n</sub> ) = gcd(K，K，…，n 次)**。由于 **gcd(K，K，…，n 次)= K** ，给定问题的解可以通过求数组所有元素的 gcd 来求
。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the final number
// obtained after performing the
// given operation
int finalNum(int arr[], int n)
{

    // Find the gcd of the array elements
    int result = 0;
    for (int i = 0; i < n; i++) {
        result = __gcd(result, arr[i]);
    }
    return result;
}

// Driver code
int main()
{
    int arr[] = { 3, 9, 6, 36 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << finalNum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the final number
// obtained after performing the
// given operation
static int finalNum(int arr[], int n)
{

    // Find the gcd of the array elements
    int result = 0;
    for (int i = 0; i < n; i++)
    {
        result = __gcd(result, arr[i]);
    }
    return result;
}

static int __gcd(int a, int b)
{
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 9, 6, 36 };
    int n = arr.length;

    System.out.print(finalNum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd

# Function to return the final number
# obtained after performing the
# given operation
def finalNum(arr, n):

    # Find the gcd of the array elements
    result = arr[0]
    for i in arr:
        result = __gcd(result, i)
    return result

# Driver code
arr = [3, 9, 6, 36]
n = len(arr)

print(finalNum(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the readonly number
// obtained after performing the
// given operation
static int finalNum(int []arr, int n)
{

    // Find the gcd of the array elements
    int result = 0;
    for (int i = 0; i < n; i++)
    {
        result = __gcd(result, arr[i]);
    }
    return result;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 9, 6, 36 };
    int n = arr.Length;

    Console.Write(finalNum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the final number
    // obtained after performing the
    // given operation
    function finalNum(arr , n) {

        // Find the gcd of the array elements
        var result = 0;
        for (i = 0; i < n; i++) {
            result = __gcd(result, arr[i]);
        }
        return result;
    }

    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code

        var arr = [ 3, 9, 6, 36 ];
        var n = arr.length;

        document.write(finalNum(arr, n));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
3
```