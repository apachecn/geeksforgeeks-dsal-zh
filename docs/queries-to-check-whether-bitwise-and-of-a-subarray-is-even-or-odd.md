# 查询以检查子阵列的位“与”是偶数还是奇数

> 原文:[https://www . geesforgeks . org/query-to-check-by-and-of-a-subarray 是偶数还是奇数/](https://www.geeksforgeeks.org/queries-to-check-whether-bitwise-and-of-a-subarray-is-even-or-odd/)

给定一个正整数数组**arr[]****N**，任务是回答 **Q** 的查询，其中每个查询由一个范围**【L，R】**组成，您必须检查给定索引范围内元素的按位“与”是偶数还是奇数。
**举例:**

> **输入:** arr[] = {1，1，2，3}，Q[][] = {{1，2}，{0，1}}
> **输出:**
> 偶数
> 奇数
> (1 & 2) = 0，为偶数。
> (1 & 1) = 1，奇数。
> **输入:** arr[] = {2，1，5，7，6，8，9}，Q[][] = {{0，2}，{1，2}，{2，3}，{3，6}}
> **输出:**
> 偶数
> 奇数
> 奇数
> 偶数

**进场:**

*   如果某个索引范围**【L，R】**中的所有元素都是奇数，则该索引范围内的按位“与”将是奇数，否则将是偶数。
*   所以，检查索引范围**【L，R】**内的所有元素是否都是奇数。
*   为了最佳地回答每个查询，创建一个数组并标记值为奇数的位置，然后取该数组的前缀和。
*   现在，索引范围**【L，R】**中奇数的计数可以计算为**pre[R]–pre[L–1]**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 1000005;
int even[MAXN], odd[MAXN];

// Function to precompute the count
// of even and odd numbers
void precompute(int arr[], int n)
{

    for (int i = 0; i < n; i++) {

        // If the current element is odd
        // then put 1 at odd[i]
        if (arr[i] % 2 == 1)
            odd[i] = 1;

        // If the current element is even
        // then put 1 at even[i]
        if (arr[i] % 2 == 0)
            even[i] = 1;
    }

    // Taking the prefix sums of these two arrays
    // so we can get the count of even and odd
    // numbers in a range [L, R] in O(1)
    for (int i = 1; i < n; i++) {
        even[i] = even[i] + even[i - 1];
        odd[i] = odd[i] + odd[i - 1];
    }
}

// Function that returns true if the bitwise
// AND of the subarray a[L...R] is odd
bool isOdd(int L, int R)
{

    // cnt will store the count of odd
    // numbers in the range [L, R]
    int cnt = odd[R];
    if (L > 0)
        cnt -= odd[L - 1];

    // Check if all the numbers in
    // the range are odd or not
    if (cnt == R - L + 1)
        return true;

    return false;
}

// Function to perform the queries
void performQueries(int a[], int n, int q[][2], int m)
{
    precompute(a, n);

    // Perform queries
    for (int i = 0; i < m; i++) {
        int L = q[i][0], R = q[i][1];
        if (isOdd(L, R))
            cout << "Odd\n";
        else
            cout << "Even\n";
    }
}

// Driver code
int main()
{
    int a[] = { 2, 1, 5, 7, 6, 8, 9 };
    int n = sizeof(a) / sizeof(a[0]);

    // Queries
    int q[][2] = { { 0, 2 }, { 1, 2 }, { 2, 3 }, { 3, 6 } };
    int m = sizeof(q) / sizeof(q[0]);

    performQueries(a, n, q, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static final int MAXN = 1000005;
    static int even[] = new int[MAXN];
    static int odd[] = new int[MAXN];

    // Function to precompute the count
    // of even and odd numbers
    static void precompute(int arr[], int n)
    {

        for (int i = 0; i < n; i++)
        {

            // If the current element is odd
            // then put 1 at odd[i]
            if (arr[i] % 2 == 1)
                odd[i] = 1;

            // If the current element is even
            // then put 1 at even[i]
            if (arr[i] % 2 == 0)
                even[i] = 1;
        }

        // Taking the prefix sums of these two arrays
        // so we can get the count of even and odd
        // numbers in a range [L, R] in O(1)
        for (int i = 1; i < n; i++)
        {
            even[i] = even[i] + even[i - 1];
            odd[i] = odd[i] + odd[i - 1];
        }
    }

    // Function that returns true if the bitwise
    // AND of the subarray a[L...R] is odd
    static boolean isOdd(int L, int R)
    {

        // cnt will store the count of odd
        // numbers in the range [L, R]
        int cnt = odd[R];
        if (L > 0)
            cnt -= odd[L - 1];

        // Check if all the numbers in
        // the range are odd or not
        if (cnt == R - L + 1)
            return true;

        return false;
    }

    // Function to perform the queries
    static void performQueries(int a[], int n,
                               int q[][], int m)
    {
        precompute(a, n);

        // Perform queries
        for (int i = 0; i < m; i++)
        {
            int L = q[i][0], R = q[i][1];
            if (isOdd(L, R))
                System.out.println("Odd");
            else
                System.out.println("Even");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int []a = { 2, 1, 5, 7, 6, 8, 9 };
        int n = a.length;

        // Queries
        int q[][] = { { 0, 2 }, { 1, 2 }, { 2, 3 }, { 3, 6 } };
        int m = q.length;

        performQueries(a, n, q, m);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python implementation of the approach
MAXN = 1000005;
even = [0] * MAXN;
odd = [0] * MAXN;

# Function to precompute the count
# of even and odd numbers
def precompute(arr, n):

    for i in range(n):

        # If the current element is odd
        # then put 1 at odd[i]
        if (arr[i] % 2 == 1):
            odd[i] = 1;

        # If the current element is even
        # then put 1 at even[i]
        if (arr[i] % 2 == 0):
            even[i] = 1;

    # Taking the prefix sums of these two arrays
    # so we can get the count of even and odd
    # numbers in a range [L, R] in O(1)
    for i in range(1, n):
        even[i] = even[i] + even[i - 1];
        odd[i] = odd[i] + odd[i - 1];

# Function that returns True if the bitwise
# AND of the subarray a[L...R] is odd
def isOdd(L, R):

    # cnt will store the count of odd
    # numbers in the range [L, R]
    cnt = odd[R];
    if (L > 0):
        cnt -= odd[L - 1];

    # Check if all the numbers in
    # the range are odd or not
    if (cnt == R - L + 1):
        return True;

    return False;

# Function to perform the queries
def performQueries(a, n, q, m):
    precompute(a, n);

    # Perform queries
    for i in range(m):
        L = q[i][0];
        R = q[i][1];
        if (isOdd(L, R)):
            print("Odd");
        else:
            print("Even");

# Driver code
if __name__ == '__main__':
    a = [ 2, 1, 5, 7, 6, 8, 9 ];
    n = len(a);

    # Queries
    q = [[ 0, 2 ],[ 1, 2 ],[ 2, 3 ],[ 3, 6 ]];
    m = len(q);

    performQueries(a, n, q, m);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static readonly int MAXN = 1000005;
    static int []even = new int[MAXN];
    static int []odd = new int[MAXN];

    // Function to precompute the count
    // of even and odd numbers
    static void precompute(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
        {

            // If the current element is odd
            // then put 1 at odd[i]
            if (arr[i] % 2 == 1)
                odd[i] = 1;

            // If the current element is even
            // then put 1 at even[i]
            if (arr[i] % 2 == 0)
                even[i] = 1;
        }

        // Taking the prefix sums of these two arrays
        // so we can get the count of even and odd
        // numbers in a range [L, R] in O(1)
        for (int i = 1; i < n; i++)
        {
            even[i] = even[i] + even[i - 1];
            odd[i] = odd[i] + odd[i - 1];
        }
    }

    // Function that returns true if the bitwise
    // AND of the subarray a[L...R] is odd
    static bool isOdd(int L, int R)
    {

        // cnt will store the count of odd
        // numbers in the range [L, R]
        int cnt = odd[R];
        if (L > 0)
            cnt -= odd[L - 1];

        // Check if all the numbers in
        // the range are odd or not
        if (cnt == R - L + 1)
            return true;

        return false;
    }

    // Function to perform the queries
    static void performQueries(int []a, int n,
                            int [,]q, int m)
    {
        precompute(a, n);

        // Perform queries
        for (int i = 0; i < m; i++)
        {
            int L = q[i, 0], R = q[i, 1];
            if (isOdd(L, R))
                Console.WriteLine("Odd");
            else
                Console.WriteLine("Even");
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        int []a = { 2, 1, 5, 7, 6, 8, 9 };
        int n = a.Length;

        // Queries
        int [,]q = { { 0, 2 }, { 1, 2 },
                  { 2, 3 }, { 3, 6 } };
        int m = q.GetLength(0);

        performQueries(a, n, q, m);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var MAXN = 1000005;
var even = Array(MAXN).fill(0);
var odd = Array(MAXN).fill(0);

// Function to precompute the count
// of even and odd numbers
function precompute(arr, n)
{

    for (var i = 0; i < n; i++) {

        // If the current element is odd
        // then put 1 at odd[i]
        if (arr[i] % 2 == 1)
            odd[i] = 1;

        // If the current element is even
        // then put 1 at even[i]
        if (arr[i] % 2 == 0)
            even[i] = 1;
    }

    // Taking the prefix sums of these two arrays
    // so we can get the count of even and odd
    // numbers in a range [L, R] in O(1)
    for (var i = 1; i < n; i++) {
        even[i] = even[i] + even[i - 1];
        odd[i] = odd[i] + odd[i - 1];
    }
}

// Function that returns true if the bitwise
// AND of the subarray a[L...R] is odd
function isOdd(L, R)
{

    // cnt will store the count of odd
    // numbers in the range [L, R]
    var cnt = odd[R];
    if (L > 0)
        cnt -= odd[L - 1];

    // Check if all the numbers in
    // the range are odd or not
    if (cnt == R - L + 1)
        return true;

    return false;
}

// Function to perform the queries
function performQueries(a, n, q, m)
{
    precompute(a, n);

    // Perform queries
    for (var i = 0; i < m; i++)
    {
        var L = q[i][0], R = q[i][1];
        if (isOdd(L, R))
            document.write( "Odd"+"<br>");
        else
            document.write("Even"+"<br>");
    }
}

// Driver code
var a = [2, 1, 5, 7, 6, 8, 9];
var n = a.length;

// Queries
var q = [ [ 0, 2 ], [ 1, 2 ], [ 2, 3 ], [ 3, 6 ] ];
var m = q.length;
performQueries(a, n, q, m);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
Even
Odd
Odd
Even
```

**时间复杂度:** O(Q)，其中 Q 为查询次数。