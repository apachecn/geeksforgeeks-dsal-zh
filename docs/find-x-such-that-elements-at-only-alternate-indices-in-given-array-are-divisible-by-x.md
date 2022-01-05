# 找到 X，这样给定数组中只有交替索引处的元素才能被 X 整除

> 原文:[https://www . geeksforgeeks . org/find-x 这样给定数组中的元素只能被 x 整除/](https://www.geeksforgeeks.org/find-x-such-that-elements-at-only-alternate-indices-in-given-array-are-divisible-by-x/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到一个整数 **X** ，使得可被 **X** 整除的整数和不可被 **X** 整除的整数在数组中相互替换。如果没有这样的值，打印 **-1** 。

**示例:**

> **输入:** arr[] = {6，5，9，10，12，15}
> **输出:** 5
> **解释:**x = 5 除奇数索引处的所有元素(基于 0 的索引)
> 但不除偶数索引处的元素，因此答案是 5。
> 
> **输入:** {10，20，40，30}
> **输出:** -1

**方法:**该方法是基于 [GCD](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的，因为一组交替元素，无论是奇数索引还是偶数索引，都应该完全被一个整数整除，唯一能整除所有数字的数字就是这组元素的 GCD。一个集合的 GCD 不应该等于另一个集合的 GCD，那么只有那个 GCD 才是答案。按照以下步骤解决此问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，分别计算奇数索引 **(gcd1)** 处元素和偶数索引 **(gcd2)** 处元素的 GCD。
*   如果两个 gcd 不相等，则执行以下操作:
    *   检查**偶数索引**中是否有可被 **gcd1** 整除的整数。如果找到任何此类整数，则 **gcd1** 不是所需值。
    *   检查**奇数索引**中是否有可被 **gcd2** 整除的整数。如果找到任何此类整数，则 **gcd2** 不是所需值。
    *   如果以上两个条件中的任何一个为假，对应的 GCD 值就是答案。否则不存在这样的 X。
*   否则不可能有这样的 **X** 。

下面是上述方法的实现。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the gcd of the array
int gcdofarray(int arr[], int start, int N)
{
    int result = arr[start];
    for (int i = start + 2; i < N; i += 2)
        result = __gcd(arr[i], result);

    return result;
}

// Function to check if the whole set
// is not divisible by gcd
bool check(int arr[], int start, int gcd,
           int N)
{
    for (int i = start; i < N; i += 2) {

        // If any element is divisible
        // by gcd return 0
        if (arr[i] % gcd == 0) {
            return 0;
        }
    }
    return 1;
}

// Function to find the value x
void find_divisor(int arr[], int N)
{
    // Find gcds of values at odd indices
    // and at even indices separately
    int gcd1 = gcdofarray(arr, 1, N);
    int gcd2 = gcdofarray(arr, 0, N);

    // If both the gcds are not same
    if (gcd1 != gcd2) {
        if (check(arr, 0, gcd1, N) != 0) {
            int x = gcd1;
            cout << x << endl;
            return;
        }

        if (check(arr, 1, gcd2, N) != 0) {
            int x = gcd2;
            cout << x << endl;
            return;
        }
    }

    // If both the gcds are same print -1
    cout << -1 << endl;
}

// Driver Code
int main()
{

    // Initialize the array
    int arr[] = { 6, 5, 9, 10, 12, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Call the function
    find_divisor(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
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

// Function to find the gcd of the array
static int gcdofarray(int arr[], int start, int N)
{
    int result = arr[start];
    for(int i = start + 2; i < N; i += 2)
        result = __gcd(arr[i], result);

    return result;
}

// Function to check if the whole set
// is not divisible by gcd
static boolean check(int arr[], int start,
                     int gcd, int N)
{
    for(int i = start; i < N; i += 2)
    {

        // If any element is divisible
        // by gcd return 0
        if (arr[i] % gcd == 0)
        {
            return false;
        }
    }
    return true;
}

// Function to find the value x
static void find_divisor(int arr[], int N)
{

    // Find gcds of values at odd indices
    // and at even indices separately
    int gcd1 = gcdofarray(arr, 1, N);
    int gcd2 = gcdofarray(arr, 0, N);

    // If both the gcds are not same
    if (gcd1 != gcd2)
    {
        if (check(arr, 0, gcd1, N))
        {
            int x = gcd1;
            System.out.println(x);
            return;
        }

        if (check(arr, 1, gcd2, N))
        {
            int x = gcd2;
            System.out.println(x);
            return;
        }
    }

    // If both the gcds are same print -1
    System.out.print(-1);
}

// Driver Code
public static void main(String args[])
{

    // Initialize the array
    int arr[] = { 6, 5, 9, 10, 12, 15 };
    int N = arr.length;

    // Call the function
    find_divisor(arr, N);
}
}

// This code is contributed by sanjoy_62
```

**Output**

```
5
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)