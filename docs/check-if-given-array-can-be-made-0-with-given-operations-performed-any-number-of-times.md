# 检查给定数组是否可以在给定操作执行任意次的情况下变为 0

> 原文:[https://www . geesforgeks . org/check-if-给定-array-can-make-0-with-给定-operations-executed-any-number-of-times/](https://www.geeksforgeeks.org/check-if-given-array-can-be-made-0-with-given-operations-performed-any-number-of-times/)

给定一个包含 **N** 个整数的数组 **arr[]** ，任务是通过以下操作来确定给定数组的所有元素是否都可以为 0:

*   将任何元素增加 2。
*   从数组的所有元素中减去数组的最小元素。
*   上述操作可以执行任意次数。

如果给定数组的所有元素都可以变成零，那么打印**是**否则打印**否**。
**例:**

> **输入:** arr[] = {1，1，3}
> **输出:**是
> **说明:**
> 第一轮:选择数组中的第一个元素，增加 2，即 arr[] = {3，1，3}。
> 然后将所有元素减少 1(这在当前数组中是最小值)，即 arr[] = {2，0，2}。
> 第二轮:选择数组中的第二个元素，增加 2，即 arr[] = {2，2，2}。
> 然后将所有元素减少 2(这是当前数组中的最小值)，即 arr[] = {0，0，0}。
> 因此，通过对数组的元素执行给定的操作，可以将给定数组的所有元素减少到 0。
> **输入:** arr[] = {2，1，4，2}
> **输出:**否
> **解释:**
> 我们不能通过执行给定的操作使数组的所有元素都为 0。

**进场:**借助[平价](https://www.geeksforgeeks.org/program-to-find-parity/)可以解决问题。

*   因为，通过在每次操作中将数组的元素增加 2，元素的[奇偶性](https://www.geeksforgeeks.org/program-to-find-parity/)不会改变，即**奇数保持奇数或偶数保持偶数**。
*   并且用数组中的最小元素减去数组中的每个元素后，偶数的**奇偶性变成奇数，奇数的奇偶性变成偶数**。
*   因此，要使数组的所有元素都为 0，所有元素的奇偶性必须相同，否则我们不能通过给定的运算使数组的所有元素都为 0。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to whether the array
// can be made zero or not
bool check(int arr[], int N)
{
    // Count for even elements
    int even = 0;

    // Count for odd elements
    int odd = 0;

    // Traverse the array to
    // count the even and odd
    for (int i = 0; i < N; i++) {

        // If arr[i] is odd
        if (arr[i] & 1) {
            odd++;
        }

        // If arr[i] is even
        else {
            even++;
        }
    }

    // Check if count of even
    // is zero or count of odd
    // is zero
    if (even == N || odd == N)
        cout << "Yes";
    else
        cout << "No";
}

// Driver's Code
int main()
{
    int arr[] = { 1, 1, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    check(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Function to whether the array
// can be made zero or not
static void check(int arr[], int N)
{
    // Count for even elements
    int even = 0;

    // Count for odd elements
    int odd = 0;

    // Traverse the array to
    // count the even and odd
    for (int i = 0; i < N; i++) {

        // If arr[i] is odd
        if (arr[i] % 2 == 1) {
            odd++;
        }

        // If arr[i] is even
        else {
            even++;
        }
    }

    // Check if count of even
    // is zero or count of odd
    // is zero
    if (even == N || odd == N)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver's Code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 3 };
    int N = arr.length;

    check(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to whether the array
# can be made zero or not
def check(arr, N):

    # Count for even elements
    even = 0;

    # Count for odd elements
    odd = 0;

    # Traverse the array to
    # count the even and odd
    for i in range(N):

        # If arr[i] is odd
        if (arr[i] % 2 == 1):
            odd += 1;

        # If arr[i] is even
        else:
            even += 1;

    # Check if count of even
    # is zero or count of odd
    # is zero
    if (even == N or odd == N):
        print("Yes");
    else:
        print("No");

# Driver's Code
if __name__ == '__main__':
    arr = [ 1, 1, 3];
    N = len(arr);

    check(arr, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to whether the array
// can be made zero or not
static void check(int []arr, int N)
{
    // Count for even elements
    int even = 0;

    // Count for odd elements
    int odd = 0;

    // Traverse the array to
    // count the even and odd
    for (int i = 0; i < N; i++) {

        // If arr[i] is odd
        if (arr[i] % 2 == 1) {
            odd++;
        }

        // If arr[i] is even
        else {
            even++;
        }
    }

    // Check if count of even
    // is zero or count of odd
    // is zero
    if (even == N || odd == N)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver's Code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 3 };
    int N = arr.Length;

    check(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to whether the array
// can be made zero or not
function check(arr, N)
{
    // Count for even elements
    let even = 0;

    // Count for odd elements
    let odd = 0;

    // Traverse the array to
    // count the even and odd
    for (let i = 0; i < N; i++) {

        // If arr[i] is odd
        if (arr[i] & 1) {
            odd++;
        }

        // If arr[i] is even
        else {
            even++;
        }
    }

    // Check if count of even
    // is zero or count of odd
    // is zero
    if (even == N || odd == N)
        document.write("Yes");
    else
        document.write("No");
}

// Driver's Code

let arr = [ 1, 1, 3 ];
let N = arr.length;

check(arr, N);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** **O(N)** ，其中 N 为给定数组的长度。

**辅助空间:** O(1)