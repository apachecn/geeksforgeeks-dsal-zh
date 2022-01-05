# 乔利跳线序列

> 原文:[https://www.geeksforgeeks.org/jolly-jumper-sequence/](https://www.geeksforgeeks.org/jolly-jumper-sequence/)

n 个数字的序列(n < 3000) is called **Jolly Jumper** 如果连续元素之间的差值的绝对值取从 1 到 n-1 的所有可能值。这个定义意味着单个整数的任何序列都是一个快乐的跳跃者。

**示例:**

```
Input: 1 4 2 3
Output: True
This sequence 1 4 2 3 is Jolly Jumper because
the absolute differences are 3, 2, and 1.

Input: 1 4 2 -1 6  
Output: False
The absolute differences are 3, 2, 3, 7\. 
This does not contain  all the  values from 1 
through n-1\. So, this sequence is not Jolly.

Input: 11 7 4 2 1 6
Output: True
```

其思想是维护一个布尔数组来存储连续元素的绝对差集。
a)如果两个元素的绝对差大于 n-1 或 0，则返回 false。
b)如果一个绝对差重复，那么从 1 到 n-1 的所有绝对差都不能存在([鸽子洞原理](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/))，返回 false。

以下是基于上述思想的实现。

## C++

```
// Program for Jolly Jumper Sequence
#include<bits/stdc++.h>
using namespace std;

// Function to check whether given sequence is
// Jolly Jumper or not
bool isJolly(int a[], int n)
{
    // Boolean vector to diffSet set of differences.
    // The vector is initialized as false.
    vector<bool> diffSet(n, false);

    // Traverse all array elements
    for (int i=0; i < n-1 ; i++)
    {
        // Find absolute difference between current two
        int d = abs(a[i]-a[i+1]);

        // If difference is out of range or repeated,
        // return false.
        if (d == 0 || d > n-1 || diffSet[d] == true)
            return false;

        // Set presence of d in set.
        diffSet[d] = true;
    }

    return true;
}

// Driver Code
int main()
{
    int a[] = {11, 7, 4, 2, 1, 6};
    int n = sizeof(a)/ sizeof(a[0]);
    isJolly(a, n)? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program for Jolly Jumper Sequence
import java.util.*;

class GFG
{

// Function to check whether given sequence
// is Jolly Jumper or not
static boolean isJolly(int a[], int n)
{
    // Boolean vector to diffSet set of differences.
    // The vector is initialized as false.
    boolean []diffSet = new boolean[n];

    // Traverse all array elements
    for (int i = 0; i < n - 1 ; i++)
    {
        // Find absolute difference
        // between current two
        int d = Math.abs(a[i] - a[i + 1]);

        // If difference is out of range or repeated,
        // return false.
        if (d == 0 || d > n - 1 ||
            diffSet[d] == true)
            return false;

        // Set presence of d in set.
        diffSet[d] = true;
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = {11, 7, 4, 2, 1, 6};
    int n = a.length;
    if(isJolly(a, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program for Jolly Jumper
# Sequence

# Function to check whether given
# sequence is Jolly Jumper or not
def isJolly(a, n):

    # Boolean vector to diffSet set
    # of differences. The vector is
    # initialized as false.
    diffSet = [False] * n

    # Traverse all array elements
    for i in range(0, n-1):

        # Find absolute difference between
        # current two
        d = abs(a[i]-a[i + 1])

        # If difference is out of range or
        # repeated, return false.
        if (d == 0 or d > n-1 or diffSet[d] == True):
            return False

        # Set presence of d in set.
        diffSet[d] = True

    return True

# Driver Code
a = [11, 7, 4, 2, 1, 6]
n = len(a)

print("Yes") if isJolly(a, n) else print("No")

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// Program for Jolly Jumper Sequence
using System;

class GFG
{

// Function to check whether given sequence
// is Jolly Jumper or not
static Boolean isJolly(int []a, int n)
{
    // Boolean vector to diffSet set of differences.
    // The vector is initialized as false.
    Boolean []diffSet = new Boolean[n];

    // Traverse all array elements
    for (int i = 0; i < n - 1 ; i++)
    {
        // Find absolute difference
        // between current two
        int d = Math.Abs(a[i] - a[i + 1]);

        // If difference is out of range or repeated,
        // return false.
        if (d == 0 || d > n - 1 ||
            diffSet[d] == true)
            return false;

        // Set presence of d in set.
        diffSet[d] = true;
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = {11, 7, 4, 2, 1, 6};
    int n = a.Length;
    if(isJolly(a, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program for Jolly Jumper Sequence

// Function to check whether given sequence is
// Jolly Jumper or not
function isJolly(a, n)
{

    // Boolean vector to diffSet set of
    // differences. The vector is
    // initialized as false.
    let diffSet = new Array(n).fill(false);

    // Traverse all array elements
    for(let i = 0; i < n - 1; i++)
    {

        // Find absolute difference between
        // current two
        let d = Math.abs(a[i] - a[i + 1]);

        // If difference is out of range or repeated,
        // return false.
        if (d == 0 || d > n - 1 ||
            diffSet[d] == true)
            return false;

        // Set presence of d in set.
        diffSet[d] = true;
    }
    return true;
}

// Driver Code
let a = [ 11, 7, 4, 2, 1, 6 ];
let n = a.length;

isJolly(a, n) ? document.write("Yes") :
                document.write("No");

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)
**参考文献:**
[http://users . CSC . calpoly . edu/~ JD albey/301/Labs/jollyjumpers . html](http://users.csc.calpoly.edu/~jdalbey/301/Labs/JollyJumpers.html)

本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。