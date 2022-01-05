# 使用二进制提升的 N 个数字的前缀和中大于或等于 X 的第一个元素

> 原文:[https://www . geesforgeks . org/first-element-大于或等于-x-in-prefix-sum-n-numbers-use-binary-lifting/](https://www.geeksforgeeks.org/first-element-greater-than-or-equal-to-x-in-prefix-sum-of-n-numbers-using-binary-lifting/)

给定一个由 N 个整数和一个数字 X 组成的数组，任务是在 N 个数字的前缀和中找到大于或等于 X 的第一个元素的索引。

**示例:**

> **输入:** arr[] = { 2，5，7，1，6，9，12，4，6 }和 x = 8
> **输出:** 2
> 形成的前缀和数组是{ 2，7，14，15，21，30，42，46，52}，因此 14 是索引为 2 的数
> 
> **输入:** arr[] = { 2，5，7，1，6，9，12，4，6 }和 x = 30
> **输出:** 5

**方法:**使用二分搜索法中的[下界函数可以解决问题。但是在这篇文章中，这个问题将使用**二元提升**来解决。在二进制提升中，值以 2 的幂增加(或提升)，从 *2(log(N))的最高可能幂开始，直到最低幂(0)。*](https://www.geeksforgeeks.org/lower_bound-in-cpp/)

*   初始化位置= 0，并设置位置的每个位，从最高有效位到最低有效位。
*   每当一个位被设置为 1 时，位置的值增加(或提升)。
*   增加或提升位置时，确保前缀和直到位置应小于 v。
*   这里，对于“位置”**(从第(N)个对数比特到第 0 个比特)的所有可能值，需要第(N)个对数比特。**
*   确定第 I 位的值。首先，检查设置第 I 位是否不会使“位置”大于 N，N 是数组的大小。在提升到新的“位置”之前，检查该新“位置”的值是否小于 X。
*   如果该条件为真，则目标位置位于**“位置”+ 2^i** 之上，但低于“位置”+ 2^(i+1).这是因为如果目标位置高于**“位置”+ 2^(i+1)，那么**位置已经被 **2^(i+1)** 提升了(这个逻辑类似于树中的二元提升)。
*   如果为假，则目标值位于**“位置”和“位置”+ 2^i** 之间，因此尝试以较低的 2 次方提升。最后，循环将结束，使得该位置的值小于 x。这里，在这个问题中，要求下限。所以，返回**‘位置’+1**。

下面是上述方法的实现:

## C++

```
// CPP program to find lower_bound of x in
// prefix sums array using binary lifting.
#include <bits/stdc++.h>
using namespace std;

// function to make prefix sums array
void MakePreSum(int arr[], int presum[], int n)
{
    presum[0] = arr[0];
    for (int i = 1; i < n; i++)
        presum[i] = presum[i - 1] + arr[i];
}

// function to find lower_bound of x in
// prefix sums array using binary lifting.
int BinaryLifting(int presum[], int n, int x)
{
    // initialize position
    int pos = 0;

    // find log to the base 2 value of n.
    int LOGN = log2(n);

    // if x less than first number.
    if (x <= presum[0])
        return 0;

    // starting from most significant bit.
    for (int i = LOGN; i >= 0; i--) {

        // if value at this position less
        // than x then updateposition
        // Here (1<<i) is similar to 2^i.
        if (pos + (1 << i) < n &&
            presum[pos + (1 << i)] < x) {
            pos += (1 << i);
        }
    }

    // +1 because 'pos' will have position
    // of largest value less than 'x'
    return pos + 1;
}

// Driver code
int main()
{
    // given array
    int arr[] = { 2, 5, 7, 1, 6, 9, 12, 4, 6 };

    // value to find
    int x = 8;

    // size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    // to store prefix sum
    int presum[n] = { 0 };

    // call for prefix sum
    MakePreSum(arr, presum, n);

    // function call
    cout << BinaryLifting(presum, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find lower_bound of x in
// prefix sums array using binary lifting.
import java.util.*;

class solution
{

// function to make prefix sums array
static void MakePreSum(int []arr, int []presum, int n)
{
    presum[0] = arr[0];
    for (int i = 1; i < n; i++)
        presum[i] = presum[i - 1] + arr[i];
}

// function to find lower_bound of x in
// prefix sums array using binary lifting.
static int BinaryLifting(int []presum, int n, int x)
{
    // initialize position
    int pos = 0;

    // find log to the base 2 value of n.
    int LOGN = (int)Math.log(n);

    // if x less than first number.
    if (x <= presum[0])
        return 0;

    // starting from most significant bit.
    for (int i = LOGN; i >= 0; i--) {

        // if value at this position less
        // than x then updateposition
        // Here (1<<i) is similar to 2^i.
        if (pos + (1 << i) < n &&
            presum[pos + (1 << i)] < x) {
            pos += (1 << i);
        }
    }

    // +1 because 'pos' will have position
    // of largest value less than 'x'
    return pos + 1;
}

// Driver code
public static void main(String args[])
{
    // given array
    int []arr = { 2, 5, 7, 1, 6, 9, 12, 4, 6 };

    // value to find
    int x = 8;

    // size of array
    int n = arr.length;

    // to store prefix sum
    int []presum = new int[n];
    Arrays.fill(presum,0);

    // call for prefix sum
    MakePreSum(arr, presum, n);

    // function call
    System.out.println(BinaryLifting(presum, n, x));

}

}
```

## 蟒蛇 3

```
# Python 3 program to find
# lower_bound of x in prefix
# sums array using binary lifting.
import math

# function to make prefix
# sums array
def MakePreSum( arr, presum, n):

    presum[0] = arr[0]
    for i in range(1, n):
        presum[i] = presum[i - 1] + arr[i]

# function to find lower_bound of x in
# prefix sums array using binary lifting.
def BinaryLifting(presum, n, x):

    # initialize position
    pos = 0

    # find log to the base 2
    # value of n.
    LOGN = int(math.log2(n))

    # if x less than first number.
    if (x <= presum[0]):
        return 0

    # starting from most significant bit.
    for i in range(LOGN, -1, -1) :

        # if value at this position less
        # than x then updateposition
        # Here (1<<i) is similar to 2^i.
        if (pos + (1 << i) < n and
            presum[pos + (1 << i)] < x) :
            pos += (1 << i)

    # +1 because 'pos' will have position
    # of largest value less than 'x'
    return pos + 1

# Driver code
if __name__ == "__main__":

    # given array
    arr = [ 2, 5, 7, 1, 6,
            9, 12, 4, 6 ]

    # value to find
    x = 8

    # size of array
    n = len(arr)

    # to store prefix sum
    presum = [0] * n

    # call for prefix sum
    MakePreSum(arr, presum, n)

    # function call
    print(BinaryLifting(presum, n, x))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find lower_bound of x in
// prefix sums array using binary lifting.
using System;

class GFG
{

    // function to make prefix sums array
    static void MakePreSum(int []arr,
                    int []presum, int n)
    {
        presum[0] = arr[0];
        for (int i = 1; i < n; i++)
            presum[i] = presum[i - 1] + arr[i];
    }

    // function to find lower_bound of x in
    // prefix sums array using binary lifting.
    static int BinaryLifting(int []presum,
                            int n, int x)
    {
        // initialize position
        int pos = 0;

        // find log to the base 2 value of n.
        int LOGN = (int)Math.Log(n);

        // if x less than first number.
        if (x <= presum[0])
            return 0;

        // starting from most significant bit.
        for (int i = LOGN; i >= 0; i--)
        {

            // if value at this position less
            // than x then updateposition
            // Here (1<<i) is similar to 2^i.
            if (pos + (1 << i) < n &&
                presum[pos + (1 << i)] < x)
            {
                pos += (1 << i);
            }
        }

        // +1 because 'pos' will have position
        // of largest value less than 'x'
        return pos + 1;
    }

    // Driver code
    public static void Main()
    {
        // given array
        int []arr = { 2, 5, 7, 1, 6, 9, 12, 4, 6 };

        // value to find
        int x = 8;

        // size of array
        int n = arr.Length;

        // to store prefix sum
        int []presum = new int[n];

        // call for prefix sum
        MakePreSum(arr, presum, n);

        // function call
        Console.WriteLine(BinaryLifting(presum, n, x));
    }
}

// This code has been contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find lower_bound of x in
// prefix sums array using binary lifting.

    // function to make prefix sums array
    function MakePreSum(arr,presum,n)
    {
        presum[0] = arr[0];
    for (let i = 1; i < n; i++)
        presum[i] = presum[i - 1] + arr[i];
    }

// function to find lower_bound of x in
// prefix sums array using binary lifting.
function BinaryLifting(presum, n,k)
{
    // initialize position
    let pos = 0;

    // find log to the base 2 value of n.
    let LOGN = Math.log(n);

    // if x less than first number.
    if (x <= presum[0])
        return 0;

    // starting from most significant bit.
    for (let i = LOGN; i >= 0; i--) {

        // if value at this position less
        // than x then updateposition
        // Here (1<<i) is similar to 2^i.
        if (pos + (1 << i) < n &&
            presum[pos + (1 << i)] < x) {
            pos += (1 << i);
        }
    }

    // +1 because 'pos' will have position
    // of largest value less than 'x'
    return pos + 1;
}

// Driver code

// given array
let arr=[2, 5, 7, 1, 6, 9, 12, 4, 6];
// value to find
let x = 8;

// size of array
let n = arr.length;

// to store prefix sum
let presum = new Array(n);
for(let i=0;i<n;i++)
{
    presum[i]=0;
}

// call for prefix sum
MakePreSum(arr, presum, n);

// function call
document.write(BinaryLifting(presum, n, x));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)