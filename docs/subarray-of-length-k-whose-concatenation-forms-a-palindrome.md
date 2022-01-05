# 长度为 K 的子阵列，其连接形成回文

> 原文:[https://www . geesforgeks . org/长度为 k 的子数组-what-concation-forms-a-回文/](https://www.geeksforgeeks.org/subarray-of-length-k-whose-concatenation-forms-a-palindrome/)

给定一个由**【0，9】**范围内的 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到一个长度为 **K** 的[子数组](https://www.geeksforgeeks.org/tag/subarray/)，从中我们可以生成一个数字[回文数](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。如果没有这样的子阵列，打印 **-1** 。

**注意:**数组中的元素在 0 到 10 的范围内。

**示例:**

> **输入:** arr[] = {1，5，3，2，3，5，4}，K = 5
> **输出:** 5，3，2，3，5
> **解释:**
> 子阵所有元素串联生成的数，即 **53235** ，是回文。
> 
> **输入:** arr[] = {2，3，5，1，3}，K = 4
> T3】输出: -1

**天真方法:**解决问题最简单的方法是[生成所有长度为 **K** 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，将子阵列中的所有元素串联起来，检查形成的数字是否为[回文数字](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(K)*

**有效方法:**使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)可以解决问题。按照以下步骤解决问题:

*   创建一个回文函数来检查给定的子数组(窗口滑动)是否是回文。
*   迭代数组，对每个子数组调用回文函数。
*   如果发现为真，则返回该子数组的起始索引，并打印从起始索引到下一个 k 索引的数组。
*   如果没有发现这样的子阵列是回文，打印-1。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is Palindrome or not
// here i is the starting index
// and j is the last index of the subarray
bool palindrome(vector<int> a, int i, int j)
{
     while(i<j)
     {
         // If the integer at i is not equal to j
         // then the subarray is not palindrome
         if(a[i] != a[j])
             return false;

         // Otherwise
         i++;
         j--;
     }

     // all a[i] is equal to a[j]
     // then the subarray is palindrome
     return true;
}

// Function to find a subarray whose
// concatenation forms a palindrome
// and return its starting index
int findSubArray(vector<int> arr, int k)
{
    int n= sizeof(arr)/sizeof(arr[0]);

    // Iterating over subarray of length k
    // and checking if that subarray is palindrome
    for(int i=0; i<=n-k; i++){
         if(palindrome(arr, i, i+k-1))
             return i;
    }

    // If no subarray is palindrome
    return -1;
}

// Driver Code
int main()
{
    vector<int> arr = { 2, 3, 5, 1, 3 };
    int k = 4;

    int ans = findSubArray(arr, k);

    if (ans == -1)

        cout << -1 << "\n";

    else {
        for (int i = ans; i < ans + k;
             i++)
            cout << arr[i] << " ";
        cout << "\n";
    }
    return 0;
}

// This code is contributed by Prafulla Shekhar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to check if a number
    // is Palindrome or not
    // here i is the starting index
    // and j is the last index of the subarray
    public static boolean palindrome(int[] a, int i, int j)
    {
         while(i<j)
         {
             // If the integer at i is not equal to j
             // then the subarray is not palindrome
             if(a[i] != a[j])
                 return false;

             // Otherwise
             i++;
             j--;
         }

         // all a[i] is equal to a[j]
         // then the subarray is palindrome
         return true;
     }

    // Function to find a subarray whose
    // concatenation forms a palindrome
    // and return its starting index
    static int findSubArray(int []arr, int k)
    {
        int n= arr.length;

        // Iterating over subarray of length k
        // and checking if that subarray is palindrome
        for(int i=0; i<=n-k; i++){
             if(palindrome(arr, i, i+k-1))
                 return i;
        }

        // If no subarray is palindrome
        return -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int []arr = { 2, 3, 5, 1, 3 };
        int k = 4;

        int ans = findSubArray(arr, k);

        if (ans == -1)
            System.out.print(-1 + "\n");

        else
        {
            for(int i = ans; i < ans + k; i++)
                System.out.print(arr[i] + " ");

            System.out.print("\n");
        }
    }
}

// This code is contributed by Prafulla Shekhar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a number
# is Palindrome or not here i is
# the starting index and j is the
# last index of the subarray
def palindrome(a, i, j):

    while(i < j):

        # If the integer at i is not equal to j
        # then the subarray is not palindrome
        if (a[i] != a[j]):
            return False

        # Otherwise
        i += 1
        j -= 1

    # all a[i] is equal to a[j]
    # then the subarray is palindrome
    return True

# Function to find a subarray whose
# concatenation forms a palindrome
# and return its starting index   
def findSubArray(arr, k):

    n = len(arr)

    # Iterating over subarray of length k
    # and checking if that subarray is palindrome  
    for i in range(n - k + 1):
        if (palindrome(arr, i, i + k - 1)):
            return i

    return -1

# Driver code   
arr = [ 2, 3, 5, 1, 3 ]
k = 4
ans = findSubArray(arr, k)

if (ans == -1):
    print(-1)
else:
    for i in range(ans,ans + k):
        print(arr[i], end = " ")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if a number
// is Palindrome or not here i is
// the starting index and j is the
// last index of the subarray
public static bool palindrome(int[] a, int i,
                              int j)
{
    while (i < j)
    {

        // If the integer at i is not equal to j
        // then the subarray is not palindrome
        if (a[i] != a[j])
            return false;

        // Otherwise
        i++;
        j--;
    }

    // All a[i] is equal to a[j]
    // then the subarray is palindrome
    return true;
}

// Function to find a subarray whose
// concatenation forms a palindrome
// and return its starting index
static int findSubArray(int[] arr, int k)
{
    int n = arr.Length;

    // Iterating over subarray of length k
    // and checking if that subarray is palindrome
    for(int i = 0; i <= n - k; i++)
    {
        if (palindrome(arr, i, i + k - 1))
            return i;
    }

    // If no subarray is palindrome
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 2, 3, 5, 1, 3 };
    int k = 4;
    int ans = findSubArray(arr, k);

    if (ans == -1)
        Console.Write(-1 + "\n");

    else
    {
        for(int i = ans; i < ans + k; i++)
            Console.Write(arr[i] + " ");

        Console.Write("\n");
    }
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

    // Function to check if a number
    // is Palindrome or not
    // here i is the starting index
    // and j is the last index of the subarray
    function palindrome(a, i, j)
    {
         while(i<j)
         {
             // If the integer at i is not equal to j
             // then the subarray is not palindrome
             if(a[i] != a[j])
                 return false;

             // Otherwise
             i++;
             j--;
         }

         // all a[i] is equal to a[j]
         // then the subarray is palindrome
         return true;
     }

    // Function to find a subarray whose
    // concatenation forms a palindrome
    // and return its starting index
    function findSubArray(arr, k)
    {
        let n= arr.length;

        // Iterating over subarray of length k
        // and checking if that subarray is palindrome
        for(let i=0; i<=n-k; i++){
             if(palindrome(arr, i, i+k-1))
                 return i;
        }

        // If no subarray is palindrome
        return -1;
    }

// Driver Code

         let arr = [ 2, 3, 5, 1, 3 ];
        let k = 4;

        let ans = findSubArray(arr, k);

        if (ans == -1)
            document.write(-1 + "\n");

        else
        {
            for(let i = ans; i < ans + k; i++)
                document.write(arr[i] + " ");

            document.write("<br/>");
        }

</script>
```

**Output**

```
-1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)