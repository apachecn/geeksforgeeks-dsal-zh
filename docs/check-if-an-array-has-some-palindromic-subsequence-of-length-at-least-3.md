# 检查一个数组是否有长度至少为 3 的回文子序列

> 原文:[https://www . geesforgeks . org/check-如果一个数组至少有 3 个长度的回文子序列/](https://www.geeksforgeeks.org/check-if-an-array-has-some-palindromic-subsequence-of-length-at-least-3/)

给定的是整数数组 **Arr** 。任务是确定数组中是否有长度至少为 3 的子序列是回文。
**例:**

```
Input: Arr[] = [1, 2, 1] 
Output: YES
Explanation:
Here 1 2 1 is a palindrome.

Input: Arr[] = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5]
Output: NO
Explanation:
Here no subsequence of length at least 3
exists which is a palindrome.
```

**进场:**

*   其思想是只检查长度 3，因为如果长度大于 3 的回文子序列存在，那么总有长度为 3 的回文子序列。

*   为了找到长度为 3 的回文子序列，我们只需要找到一对相等的非相邻数。

以下是上述方法的实现:

## C++

```
// C++ code to check if
// palindromic subsequence of
// length atleast 3 exist or not
#include<bits/stdc++.h>
using namespace std;

string SubPalindrome(int n, int arr[])
{
    bool ok = false;
    for (int i = 0; i < n; i++)
    {
        for(int j = i + 2; j < n; j++)
        {
            if(arr[i] == arr[j])
                ok = true;
        }
    }
    if(ok)
        return "YES";
    else
        return "NO";
}

// Driver code
int main()
{

    // Input values to list
    int Arr[] = {1, 2, 2, 3, 2};

    // Calculating length of array
    int N = sizeof(Arr)/sizeof(Arr[0]);

    cout << SubPalindrome(N, Arr);
}

// This code is contributed by Bhupendra_Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if
// palindromic subsequence of
// length atleast 3 exist or not

import java.util.*;

class GFG{

static String SubPalindrome(int n, int arr[])
{
    boolean ok = false;
    for (int i = 0; i < n; i++)
    {
        for(int j = i + 2; j < n; j++)
        {
            if(arr[i] == arr[j])
                ok = true;
        }
    }
    if(ok)
        return "YES";
    else
        return "NO";
}

// Driver code
public static void main(String[] args)
{

    // Input values to list
    int Arr[] = {1, 2, 2, 3, 2};

    // Calculating length of array
    int N = Arr.length;

    System.out.print(SubPalindrome(N, Arr));
}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 code to check if
# palindromic subsequence of
# length atleast 3 exist or not
def SubPalindrome (n, arr):
    ok = False
    for i in range(n):
        for j in range(i + 2, n):
            if arr[i] == arr[j]:
                ok = True
    return('YES' if ok else 'NO')

# Driver code

# Input values to list
Arr = [1, 2, 2, 3, 2]

# Calculating length of the array
N = len(arr)

print (SubPalindrome(N, Arr))
```

## C#

```
// C# code to check if
// palindromic subsequence of
// length atleast 3 exist or not
using System;

public class GFG{

static string SubPalindrome(int n, int []arr)
{
    bool ok = false;
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 2; j < n; j++)
        {
            if(arr[i] == arr[j])
                ok = true;
        }
    }
    if(ok)
        return "YES";
    else
        return "NO";
}

// Driver code
static public void Main ()
{
    // Input values to list
    int []Arr = { 1, 2, 2, 3, 2 };

    // Calculating length of array
    int N = Arr.Length;
    Console.WriteLine(SubPalindrome(N, Arr));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript code to check if 
    // palindromic subsequence of
    // length atleast 3 exist or not

      function SubPalindrome(n, arr)
    {
        let ok = false;
        for (let i = 0; i < n; i++)
        {
            for(let j = i + 2; j < n; j++)
            { 
                if(arr[i] == arr[j])
                    ok = true;
            }
        }
        if(ok)
            return "YES";
        else
            return "NO";
    }

    // Input values to list
    let Arr = [1, 2, 2, 3, 2];

    // Calculating length of array 
    let N = Arr.length;

    document.write(SubPalindrome(N, Arr));

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N^2)