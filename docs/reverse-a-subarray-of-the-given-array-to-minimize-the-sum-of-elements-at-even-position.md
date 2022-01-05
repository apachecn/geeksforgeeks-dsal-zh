# 反转给定阵列的子阵列，以最小化偶数位置的元素总和

> 原文:[https://www . geeksforgeeks . org/反转给定数组的子数组以最小化偶数位置的元素总和/](https://www.geeksforgeeks.org/reverse-a-subarray-of-the-given-array-to-minimize-the-sum-of-elements-at-even-position/)

给定正整数的数组 arr[]。任务是反转一个子阵列，使偶数位置的元素之和最小，并打印最小和。

***注意:**只执行一次移动。斯巴莱可能不会逆转。*

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 7
> **解释:**
> 偶数位置的元素之和最初= arr[0]+arr[2]+arr[4]= 1+3+5 = 9
> 从位置[1，4]反转子阵列时，阵列变为:{1，5，4，3，2}
> 现在偶数位置的元素之和= arr[0]+arr
> 
> **输入:** arr[] = {0，1，4，3}
> **输出:** 1
> **解释:**
> 偶数位置的元素之和最初= arr[0] + arr[2] = 0 + 4 = 4
> 从位置[1，2]反转子阵列时，数组变为:{0，4，1，3}
> 现在偶数位置的元素之和= arr[0] + arr[2] = 0 + 1 = 1，即

**天真法:**思路是应用蛮力法，[生成所有的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，检查偶数位置的元素之和。打印所有总和中的最小值。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**高效方法:**思路是观察数组 arr[]的以下要点:

*   反转**奇数长度**的子阵列不会改变总和，因为偶数索引处的所有元素将再次来到偶数索引处。
*   反转一个**偶数长度**子阵列将使索引位置的所有元素进入偶数索引，偶数索引的元素进入奇数索引。
*   只有当奇数索引元素放在偶数索引元素时，元素的总和才会改变。假设索引 1 处的元素可以转到索引 0 或索引 2。
*   当从一个**偶数指数反转到另一个偶数指数**时，例如从指数 2 到 4，它将覆盖第一种情况，或者如果从**奇数指数反转到偶数指数**例如从指数 1 到 4，它将覆盖第二种情况。

以下是基于上述观察的方法步骤:

*   因此，我们的想法是只找到偶数索引元素的和，并初始化两个数组，比如说 *v1* 和 *v2* ，这样如果第一个索引元素变为 0，v1 将记录变化，而如果第一个索引元素变为 2，v2 将记录变化。
*   获取这两个值的最小值，并检查它是否小于 0。如果是，则将其添加到答案中，最后返回答案。

下面是上述方法的实现:

## C++

```
// C++ implementation to reverse a subarray
// of the given array to minimize the
// sum of elements at even position

#include <bits/stdc++.h>
#define N 5
using namespace std;

// Function that will give
// the max negative value
int after_rev(vector<int> v)
{
    int mini = 0, count = 0;

    for (int i = 0; i < v.size(); i++) {
        count += v[i];

        // Check for count
        // greater than 0
        // as we require only
        // negative solution
        if (count > 0)
            count = 0;

        if (mini > count)
            mini = count;
    }

    return mini;
}

// Function to print the minimum sum
void print(int arr[N])
{
    int sum = 0;

    // Taking sum of only
    // even index elements
    for (int i = 0; i < N; i += 2)
        sum += arr[i];

    // Initialize two vectors v1, v2
    vector<int> v1, v2;

    // v1 will keep account for change
    // if 1th index element goes to 0
    for (int i = 0; i + 1 < N; i += 2)
        v1.push_back(arr[i + 1] - arr[i]);

    // v2 will keep account for change
    // if 1th index element goes to 2
    for (int i = 1; i + 1 < N; i += 2)
        v2.push_back(arr[i] - arr[i + 1]);

    // Get the max negative value
    int change = min(after_rev(v1),
                     after_rev(v2));
    if (change < 0)
        sum += change;

    cout << sum << endl;
}

// Driver code
int main()
{

    int arr[N] = { 0, 1, 4, 3 };
    print(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to reverse a subarray
// of the given array to minimize the
// sum of elements at even position
import java.util.*;

class GFG{

static final int N = 5;

// Function that will give
// the max negative value
static int after_rev(Vector<Integer> v)
{
    int mini = 0, count = 0;

    for(int i = 0; i < v.size(); i++)
    {
        count += v.get(i);

        // Check for count greater
        // than 0 as we require only
        // negative solution
        if (count > 0)
            count = 0;

        if (mini > count)
            mini = count;
    }
    return mini;
}

// Function to print the minimum sum
static void print(int arr[])
{
    int sum = 0;

    // Taking sum of only
    // even index elements
    for(int i = 0; i < N; i += 2)
        sum += arr[i];

    // Initialize two vectors v1, v2
    Vector<Integer> v1, v2;
    v1 = new Vector<Integer>();
    v2 = new Vector<Integer>();

    // v1 will keep account for change
    // if 1th index element goes to 0
    for(int i = 0; i + 1 < N; i += 2)
        v1.add(arr[i + 1] - arr[i]);

    // v2 will keep account for change
    // if 1th index element goes to 2
    for(int i = 1; i + 1 < N; i += 2)
        v2.add(arr[i] - arr[i + 1]);

    // Get the max negative value
    int change = Math.min(after_rev(v1),
                          after_rev(v2));
    if (change < 0)
        sum += change;

    System.out.print(sum + "\n");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 4, 3, 0 };
    print(arr);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to reverse
# a subarray of the given array to
# minimize the sum of elements at
# even position

# Function that will give
# the max negative value
def after_rev(v):

    mini = 0
    count = 0

    for i in range(len(v)):
        count += v[i]

        # Check for count greater
        # than 0 as we require only
        # negative solution
        if(count > 0):
            count = 0

        if(mini > count):
            mini = count

    return mini

# Function to print the
# minimum sum
def print_f(arr):

    sum = 0

    # Taking sum of only
    # even index elements
    for i in range(0, len(arr), 2):
        sum += arr[i]

    # Initialize two vectors v1, v2
    v1, v2 = [], []

    # v1 will keep account for change
    # if 1th index element goes to 0
    i = 1
    while i + 1 < len(arr):
        v1.append(arr[i + 1] - arr[i])
        i += 2

    # v2 will keep account for change
    # if 1th index element goes to 2
    i = 1
    while i + 1 < len(arr):
        v2.append(arr[i] - arr[i + 1])
        i += 2

    # Get the max negative value
    change = min(after_rev(v1),
                 after_rev(v2))

    if(change < 0):
        sum += change

    print(sum)

# Driver code
if __name__ == '__main__':

    arr = [ 0, 1, 4, 3 ]

    print_f(arr)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation to reverse a subarray
// of the given array to minimize the
// sum of elements at even position
using System;
using System.Collections.Generic;
class GFG{

static readonly int N = 5;

// Function that will give
// the max negative value
static int after_rev(List<int> v)
{
    int mini = 0, count = 0;

    for(int i = 0; i < v.Count; i++)
    {
        count += v[i];

        // Check for count greater
        // than 0 as we require only
        // negative solution
        if (count > 0)
            count = 0;

        if (mini > count)
            mini = count;
    }
    return mini;
}

// Function to print the minimum sum
static void print(int []arr)
{
    int sum = 0;

    // Taking sum of only
    // even index elements
    for(int i = 0; i < N; i += 2)
        sum += arr[i];

    // Initialize two vectors v1, v2
    List<int> v1, v2;
    v1 = new List<int>();
    v2 = new List<int>();

    // v1 will keep account for change
    // if 1th index element goes to 0
    for(int i = 0; i + 1 < N; i += 2)
        v1.Add(arr[i + 1] - arr[i]);

    // v2 will keep account for change
    // if 1th index element goes to 2
    for(int i = 1; i + 1 < N; i += 2)
        v2.Add(arr[i] - arr[i + 1]);

    // Get the max negative value
    int change = Math.Min(after_rev(v1),
                          after_rev(v2));
    if (change < 0)
        sum += change;

    Console.Write(sum + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 4, 3, 0 };
    print(arr);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to reverse a subarray
// of the given array to minimize the
// sum of elements at even position

var N = 3;

// Function that will give
// the max negative value
function after_rev(v)
{
    var mini = 0, count = 0;

    for (var i = 0; i < v.length; i++) {
        count += v[i];

        // Check for count
        // greater than 0
        // as we require only
        // negative solution
        if (count > 0)
            count = 0;

        if (mini > count)
            mini = count;
    }

    return mini;
}

// Function to print the minimum sum
function print(arr)
{
    var sum = 0;

    // Taking sum of only
    // even index elements
    for (var i = 0; i < N; i += 2)
        sum += arr[i];

    // Initialize two vectors v1, v2
    var v1 = [], v2 = [];

    // v1 will keep account for change
    // if 1th index element goes to 0
    for (var i = 0; i + 1 < N; i += 2)
        v1.push(arr[i + 1] - arr[i]);

    // v2 will keep account for change
    // if 1th index element goes to 2
    for (var i = 1; i + 1 < N; i += 2)
        v2.push(arr[i] - arr[i + 1]);

    // Get the max negative value
    var change = Math.min(after_rev(v1),
                     after_rev(v2));
    if (change < 0)
        sum += change;

    document.write( sum );
}

// Driver code
var arr = [0, 1, 4, 3];
print(arr);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*