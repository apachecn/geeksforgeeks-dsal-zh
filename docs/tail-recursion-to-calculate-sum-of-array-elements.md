# 尾部递归计算数组元素之和。

> 原文:[https://www . geeksforgeeks . org/tail-计算数组元素和的递归/](https://www.geeksforgeeks.org/tail-recursion-to-calculate-sum-of-array-elements/)

给定一个数组 A[]，我们需要用[尾递归法](https://www.geeksforgeeks.org/tail-recursion/)求其元素的和。我们通常希望实现尾部递归(递归调用是函数做的最后一件事的递归函数)，以便编译器可以优化代码。基本上，如果递归调用是最后一条语句，编译器不需要保存父调用的状态。
示例:

```
Input : A[] = {1, 8, 9}
Output : 18

Input : A[] = {2, 55, 1, 7}
Output : 65
```

对于线性递归方法，请参考:https://www . geeksforgeeks . org/sum-array-elements-use-Recursion/
逻辑:这里尾部递归的关键是无论函数调用应用了什么操作，都将其作为单独的函数参数维护。
所以，保留最后 K 个元素的和作为函数参数，K=0 时返回和。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Tail recursive function
int arrSum(int* array, int size, int sum = 0)
{
    // Base Case
    if (size == 0)
        return sum;

    // Function Call Observe sum+array[size-1]
    // to maintain sum of elements
    return arrSum(array, size - 1, sum + array[size - 1]);
}

int main()
{
    int array[] = { 2, 55, 1, 7 };
    int size = sizeof(array) / sizeof(array[0]);
    cout << arrSum(array, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the given approach.
class GFG
{

// Tail recursive function
static int arrSum(int []array, int size, int sum)
{
    // Base Case
    if (size == 0)
        return sum;

    // Function Call Observe sum+array[size-1]
    // to maintain sum of elements
    return arrSum(array, size - 1, sum + array[size - 1]);
}

// Driver code
public static void main(String[] args)
{
    int array[] = { 2, 55, 1, 7 };
    int size = array.length;
    System.out.print(arrSum(array, size, 0));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the given approach.

# Tail recursive function
def arrSum(array, size, Sum = 0):

    # Base Case
    if size == 0:
        return Sum

    # Function Call Observe sum+array[size-1]
    # to maintain sum of elements
    return arrSum(array, size - 1,
            Sum + array[size - 1])

# Driver Code
if __name__ == "__main__":

    array = [2, 55, 1, 7]
    size = len(array)
    print(arrSum(array, size))

# This code is contributed by Rituraj Jain
```

## C#

```

// C# implementation of the given approach.
using System;

class GFG
{

// Tail recursive function
static int arrSum(int []array, int size, int sum)
{
    // Base Case
    if (size == 0)
        return sum;

    // Function Call Observe sum+array[size-1]
    // to maintain sum of elements
    return arrSum(array, size - 1, sum + array[size - 1]);
}

// Driver code
public static void Main(String[] args)
{
    int []array = { 2, 55, 1, 7 };
    int size = array.Length;
    Console.WriteLine(arrSum(array, size, 0));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Tail recursive function
function arrSum(array, size, sum = 0)
{
    // Base Case
    if (size == 0)
        return sum;

    // Function Call Observe sum+array[size-1]
    // to maintain sum of elements
    return arrSum(array, size - 1, sum + array[size - 1]);
}

var array = [2, 55, 1, 7];
var size = array.length;
document.write( arrSum(array, size));

</script>   
```

**Output:** 

```
65
```

**时间复杂度:** O(n)