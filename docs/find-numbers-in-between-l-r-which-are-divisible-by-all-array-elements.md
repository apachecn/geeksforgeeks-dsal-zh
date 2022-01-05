# 找出在【L，R】之间可以被所有数组元素整除的数字

> 原文:[https://www . geesforgeks . org/find-numbers-in-l-r-哪些可被所有数组元素整除/](https://www.geeksforgeeks.org/find-numbers-in-between-l-r-which-are-divisible-by-all-array-elements/)

给定一个数组 **arr[]** ，该数组包含 **N** 正整数和两个变量 **L** 和 **R** ，表示从 **L** 到 **R** 的整数范围(含)。任务是打印 **L** 到 **R** 之间所有可以被所有数组元素整除的数字。如果不存在这样的值，打印-1。

> **输入:** arr[] = {3，5，12}，L = 90，R = 280
> **输出:** 120 180 240
> **说明:**120 180 240 是可被所有 arr[]元素整除的数。
> 
> **输入:** arr[] = {4，7，13，16}，L = 200，R = 600
> **输出:** -1

**天真方法:**在这种方法中，对于范围内的每个元素**【L，R】**检查它是否可以被数组的所有元素整除。

***时间复杂度:*** O((R-L)*N)
***辅助空间:*** O(1)

**有效方法:**给定的问题可以用基本数学来解决。任何可被数组所有元素整除的元素都是所有数组元素的 LCM 的倍数。求范围[L，R]内 LCM 的倍数，存储在数组中。最后打印存储在数组中的数字。

***时间复杂度:*** O(N)
***辅助空间:***O(R–L)

**空间优化方法:**以下步骤可用于解决问题:

1.  计算给定 arr[]的所有元素的 [LCM](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)
2.  现在，检查 **LCM** 是否存在这些情况:
    1.  如果 **(LCM < L 和 LCM*2 > R)** ，则打印-1。
    2.  如果 **(LCM > R)** ，则打印-1。
3.  现在，取最近的 **L** (在 **L** 到 **R** 之间)的值，这个值可以被 **LCM** 整除，比如说 **i** 。
4.  现在开始打印 **i** ，每次打印后按 **LCM** 递增，直到大于 **R** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return Kth smallest
// prime number if it exists
void solve(int* arr, int N, int L, int R)
{
    // For storing the LCM
    int LCM = arr[0];

    // Loop to iterate the array
    for (int i = 1; i < N; i++) {
        // Taking LCM of numbers
        LCM = (LCM * arr[i]) /
            (__gcd(LCM, arr[i]));
    }

    // Checking if no elements is divisible
    // by all elements of given array of given
    // range, print -1
    if ((LCM < L && LCM * 2 > R) || LCM > R) {
        cout << "-1";
        return;
    }

    // Taking nearest value of L which is
    // divisible by whole array
    int k = (L / LCM) * LCM;

    // If k is less than L, make it in the
    // range between L to R
    if (k < L)
        k = k + LCM;

    // Loop to iterate the from L to R
    // and printing the numbers which
    // are divisible by all array elements
    for (int i = k; i <= R; i = i + LCM) {
        cout << i << ' ';
    }
}

// Driver Code
int main()
{
    int L = 90;
    int R = 280;
    int arr[] = { 3, 5, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);
    solve(arr, N, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Recursive function to return gcd of a and b
static int __gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Function to return Kth smallest
// prime number if it exists
static void solve(int[] arr, int N, int L, int R)
{

    // For storing the LCM
    int LCM = arr[0];

    // Loop to iterate the array
    for(int i = 1; i < N; i++)
    {

        // Taking LCM of numbers
        LCM = (LCM * arr[i]) /
        (__gcd(LCM, arr[i]));
    }

    // Checking if no elements is divisible
    // by all elements of given array of given
    // range, print -1
    if ((LCM < L && LCM * 2 > R) || LCM > R)
    {
        System.out.println("-1");
        return;
    }

    // Taking nearest value of L which is
    // divisible by whole array
    int k = (L / LCM) * LCM;

    // If k is less than L, make it in the
    // range between L to R
    if (k < L)
        k = k + LCM;

    // Loop to iterate the from L to R
    // and printing the numbers which
    // are divisible by all array elements
    for(int i = k; i <= R; i = i + LCM)
    {
        System.out.print(i + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int L = 90;
    int R = 280;
    int arr[] = { 3, 5, 12 };
    int N = arr.length;

    solve(arr, N, L, R);
}
}

// This code is contributed by sanjoy_62
```

**Output**

```
120 180 240 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)