# 使数组所有元素的和与积非零的最小步骤

> 原文:[https://www . geeksforgeeks . org/求非零数组所有元素的和与积的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-make-sum-and-the-product-of-all-elements-of-array-non-zero/)

给定一个由 **N** 个整数组成的数组 **arr** ，任务是找出最小步长，在该最小步长内，数组中所有元素的和与积可以为非零。在一个步骤中，数组的任何元素都可以增加 1。
**例:**

> **输入:** N = 4，arr[] = {0，1，2，3}
> **输出:** 1
> **解释:**
> 由于数组所有元素的乘积为零
> 将数组元素 0 递增 1，这样数组和与乘积不等于零。
> **输入:** N = 4，arr[] = {-1，-1，0，0}
> **输出:** 3
> **解释:**
> 由于数组所有元素的乘积为零
> 将数组元素 2 和 3 加 1，这样数组和与乘积不等于零

**方法:**想法是将问题分成两部分，即–

1.  使数组乘积不等于零所需的最少步骤。
2.  使数组和不等于零所需的最小步骤。

对于不等于零的数组的所有元素的乘积，那么数组的每个元素都应该是非零的，并且要得到不等于零的数组和，如果数组和为零，则将任何元素递增 1。
**例如:**

```
N = 4, arr[] = {0, 1, 2, 3}

Iterate over the array to find,
If there is an element that is zero.
If yes, then increment it by 1 and also
increment the number of steps by 1.

Again, Iterate over the updated array,
To check if the array sum is zero. 
If the array sum of the updated array
is zero then increment any element by 1\. 
```

**算法:**

*   迭代数组以检查是否有零元素，然后将元素增加 1，并将步数增加 1
*   同样，迭代数组并找到数组的和，如果数组的和为零，那么将任意元素增加 1，并将步数增加 1。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum steps to make the array sum
// and the product not equal to zero
#include <bits/stdc++.h>
using namespace std;

int sum(int arr[], int n)
{
    int sum = 0;
    for(int i= 0; i < n; i++)
        sum += arr[i];
    return sum;
} 

// Function to to find the
// minimum steps to make the array sum
// and the product not equal to zero
int steps(int n, int a[])
{

    // Variable to store the minimum
    // number of steps required
    int count_steps = 0;

    // Loop to iterate over the array to
    // find if there is any element in
    // array which is zero
    for(int i = 0; i < n; i++)
    {
        if(a[i] == 0)
        {
            a[i] += 1;
            count_steps += 1;
        }
    }

    // Condition to check if the sum
    // of array elements is zero
    if( sum(a, n) != 0)
        return count_steps;
    else
        return count_steps + 1;
}

// Driver code
int main()
{
    int n = 4;
    int a[] = {-1, -1, 0, 0};
    int count = steps(n, a);
    cout<<(count);
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum steps to make the array sum
// and the product not equal to zero
class GFG
{

// Function to to find the
// minimum steps to make the array sum
// and the product not equal to zero
static int steps(int n, int []a)
{

    // Variable to store the minimum
    // number of steps required
    int count_steps = 0;

    // Loop to iterate over the array to
    // find if there is any element in
    // array which is zero
    for(int i = 0; i < n; i++)
    {
        if(a[i] == 0)
        {
            a[i] += 1;
            count_steps += 1;
        }
    }

    // Condition to check if the sum
    // of array elements is zero
    if( sum(a) != 0)
        return count_steps;
    else
        return count_steps + 1;
}

static int sum(int[] arr)
{
    int sum = 0;
    for(int i= 0; i < arr.length; i++)
        sum += arr[i];
    return sum;
}

// Driver code
public static void main(String []args) {
    int n = 4;
    int []a = {-1, -1, 0, 0};
    int count = steps(n, a);
    System.out.println(count);
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python implementation to find the
# minimum steps to make the array sum
# and the product not equal to zero

# Function to to find the
# minimum steps to make the array sum
# and the product not equal to zero
def steps(n, a):

    # Variable to store the minimum
    # number of steps required
    count_steps = 0

    # Loop to iterate over the array to
    # find if there is any element in
    # array which is zero
    for i in range(n):
        if a[i]== 0:
            a[i] += 1
            count_steps += 1

    # Condition to check if the sum
    # of array elements is zero
    if sum(a)!= 0:
        return count_steps
    else:
        return count_steps + 1

# Driver code
if __name__ == "__main__":
    n = 4
    a = [-1, -1, 0, 0]
    count  = steps(n, a)
    print(count)
```

## C#

```
// C# implementation to find the
// minimum steps to make the array sum
// and the product not equal to zero
using System;

class GFG
{

// Function to to find the
// minimum steps to make the array sum
// and the product not equal to zero
static int steps(int n, int []a)
{

    // Variable to store the minimum
    // number of steps required
    int count_steps = 0;

    // Loop to iterate over the array to
    // find if there is any element in
    // array which is zero
    for(int i = 0; i < n; i++)
    {
        if(a[i] == 0)
        {
            a[i] += 1;
            count_steps += 1;
        }
    }

    // Condition to check if the sum
    // of array elements is zero
    if( sum(a) != 0)
        return count_steps;
    else
        return count_steps + 1;
}

static int sum(int[] arr)
{
    int sum = 0;
    for(int i= 0; i < arr.Length; i++)
        sum += arr[i];
    return sum;
}

// Driver code
public static void Main(String []args) {
    int n = 4;
    int []a = {-1, -1, 0, 0};
    int count = steps(n, a);
    Console.WriteLine(count);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum steps to make the array sum
// and the product not equal to zero

// Function to to find the
// minimum steps to make the array sum
// and the product not equal to zero
function steps(n, a)
{

    // Variable to store the minimum
    // number of steps required
    let count_steps = 0;

    // Loop to iterate over the array to
    // find if there is any element in
    // array which is zero
    for(let i = 0; i < n; i++)
    {
        if(a[i] == 0)
        {
            a[i] += 1;
            count_steps += 1;
        }
    }

    // Condition to check if the sum
    // of array elements is zero
    if( sum(a) != 0)
        return count_steps;
    else
        return count_steps + 1;
}

function sum(arr)
{
    let sum = 0;
    for(let i= 0; i < arr.length; i++)
        sum += arr[i];
    return sum;
}

// Driver Code

    let n = 4;
    let a = [-1, -1, 0, 0];
    let count = steps(n, a);
    document.write(count);

</script>
```

**Output:** 

```
3
```

**业绩分析:**

*   **时间复杂度:**在给定的方法中，有两次迭代来计算使乘积非零所需的最小步数，还有一次迭代来计算数组的和。 **O(N)**
*   **空间复杂度:**在给定的方法中，没有使用额外的空间。 **O(1)**