# 检查一个阵列是否是另一个阵列的子阵列

> 原文:[https://www . geesforgeks . org/check-一个数组是否是另一个数组的子数组/](https://www.geeksforgeeks.org/check-whether-an-array-is-subarray-of-another-array/)

给定由![n ](img/872c13b29b9001d12460c34eb30ae8d0.png "Rendered by QuickLaTeX.com")和![m ](img/3ed7f2d3ccee4076e24a827154017a2e.png "Rendered by QuickLaTeX.com")整数组成的两个数组 A[]和 B[]。任务是检查阵列 B[]是否是阵列 A[]的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。
**例** :

> **输入** : A[] = {2，3，0，5，1，1，2}，B[] = {3，0，5，1}
> **输出**:是
> **输入** : A[] = {1，2，3，4，5}，B[] = {2，5，6}
> **输出**:否

**来源** : [签证面试经验](https://www.geeksforgeeks.org/visa-interview-experience/)
**简单方法**:简单方法是运行两个嵌套循环，生成数组 A[]的所有子数组，再用一个循环检查 A[]的任何子数组是否等于数组 B[]。
**高效方法**:一种高效的方法是使用两个指针同时遍历两个数组。保持数组 B[]的指针不动，如果 A[]的任何元素与 B[]的第一个元素匹配，则增加两个数组的指针，否则将 A 的指针设置为前一个起点的下一个元素，并将 B 的指针重置为 0。如果 B 的所有元素都匹配，则打印是，否则打印否
以下是上述方法的实现:

## C++

```
// C++ program to check if an array is
// subarray of another array

#include <bits/stdc++.h>
using namespace std;

// Function to check if an array is
// subarray of another array
bool isSubArray(int A[], int B[], int n, int m)
{
    // Two pointers to traverse the arrays
    int i = 0, j = 0;

    // Traverse both arrays simultaneously
    while (i < n && j < m) {

        // If element matches
        // increment both pointers
        if (A[i] == B[j]) {

            i++;
            j++;

            // If array B is completely
            // traversed
            if (j == m)
                return true;
        }
        // If not,
        // increment i and reset j
        else {
            i = i - j + 1;
            j = 0;
        }
    }

    return false;
}

// Driver Code
int main()
{
    int A[] = { 2, 3, 0, 5, 1, 1, 2 };
    int n = sizeof(A) / sizeof(int);
    int B[] = { 3, 0, 5, 1 };
    int m = sizeof(B) / sizeof(int);

    if (isSubArray(A, B, n, m))
        cout << "YES\n";
    else
        cout << "NO\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if an array is
// subarray of another array
class gfg
{

    // Function to check if an array is
    // subarray of another array
    static boolean isSubArray(int A[], int B[],
                                   int n, int m)
    {
        // Two pointers to traverse the arrays
        int i = 0, j = 0;

        // Traverse both arrays simultaneously
        while (i < n && j < m)
        {

            // If element matches
            // increment both pointers
            if (A[i] == B[j])
            {

                i++;
                j++;

                // If array B is completely
                // traversed
                if (j == m)
                    return true;
            }

            // If not,
            // increment i and reset j
            else
            {
                i = i - j + 1;
                j = 0;
            }
        }
        return false;
    }

    // Driver Code
    public static void main(String arr[])
    {
        int A[] = { 2, 3, 0, 5, 1, 1, 2 };
        int n = A.length;
        int B[] = { 3, 0, 5, 1 };
        int m = B.length;

        if (isSubArray(A, B, n, m))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by gp6
```

## 蟒蛇 3

```
# Python3 program to check if an array is
# subarray of another array

# Function to check if an array is
# subarray of another array
def isSubArray(A, B, n, m):

    # Two pointers to traverse the arrays
    i = 0; j = 0;

    # Traverse both arrays simultaneously
    while (i < n and j < m):

        # If element matches
        # increment both pointers
        if (A[i] == B[j]):

            i += 1;
            j += 1;

            # If array B is completely
            # traversed
            if (j == m):
                return True;

        # If not,
        # increment i and reset j
        else:
            i = i - j + 1;
            j = 0;

    return False;

# Driver Code
if __name__ == '__main__':
    A = [ 2, 3, 0, 5, 1, 1, 2 ];
    n = len(A);
    B = [ 3, 0, 5, 1 ];
    m = len(B);

    if (isSubArray(A, B, n, m)):
        print("YES");
    else:
        print("NO");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to check if an array is
// subarray of another array
using System;

public class GFG
{

    // Function to check if an array is
    // subarray of another array
    static bool isSubArray(int []A, int []B,
                                   int n, int m)
    {
        // Two pointers to traverse the arrays
        int i = 0, j = 0;

        // Traverse both arrays simultaneously
        while (i < n && j < m)
        {

            // If element matches
            // increment both pointers
            if (A[i] == B[j])
            {

                i++;
                j++;

                // If array B is completely
                // traversed
                if (j == m)
                    return true;
            }

            // If not,
            // increment i and reset j
            else
            {
                i = i - j + 1;
                j = 0;
            }
        }
        return false;
    }

    // Driver Code
    public static void Main(String []arr)
    {
        int []A = { 2, 3, 0, 5, 1, 1, 2 };
        int n = A.Length;
        int []B = { 3, 0, 5, 1 };
        int m = B.Length;

        if (isSubArray(A, B, n, m))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to check if an array is
// subarray of another array

// Function to check if an array is
// subarray of another array
function isSubArray(A, B, n,m)
{
    // Two pointers to traverse the arrays
    var i = 0, j = 0;

    // Traverse both arrays simultaneously
    while (i < n && j < m) {

        // If element matches
        // increment both pointers
        if (A[i] == B[j]) {

            i++;
            j++;

            // If array B is completely
            // traversed
            if (j == m)
                return true;
        }
        // If not,
        // increment i and reset j
        else {
            i = i - j + 1;
            j = 0;
        }
    }

    return false;
}

var A = [ 2, 3, 0, 5, 1, 1, 2 ];
var n = A.length;
var B = [ 3, 0, 5, 1 ];
var m =B.length;
if (isSubArray(A, B, n, m))
        document.write( "YES<br>");
    else
        document.write( "NO<br>");

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
YES
```