# 在只允许 2 位数(4 和 7)的数列中寻找第 n 个元素|集合 2 (log(n)方法)

> 原文:[https://www . geesforgeks . org/find-n-th-element-series-2-digits-4-7-allowed-set-2-logn-method/](https://www.geeksforgeeks.org/find-n-th-element-series-2-digits-4-7-allowed-set-2-logn-method/)

考虑一系列仅由数字 4 和 7 组成的数字。数列中的前几个数字是 4，7，44，47，74，77，444，..等等。给定一个数 n，我们需要找到数列中的第 n 个数。
**例:**

```
Input : n = 2
Output : 7

Input : n = 3
Output : 44

Input  : n = 5
Output : 74

Input  : n = 6
Output : 77
```

我们已经在下面的帖子中讨论了一个 O(n)解决方案。
[在只允许 2 位数(4 和 7)的数列中找到第 n 个元素](https://www.geeksforgeeks.org/find-n-th-element-series-2-digits-4-7-allowed/)
在这篇文章中，讨论了一个基于下面数字模式的 O(log n)解。数字可见

```
                 ""
              /      \
            4         7
          /   \     /   \ 
        44    47   74    77
       / \   / \   / \  / \
```

想法是从头到尾填写所需的数字。我们知道可以观察到，如果 n 是奇数，最后一位是 4，如果 n 是偶数，最后一位是 7。填充最后一个数字后，我们移动到树中的父节点。如果 n 是奇数，那么父节点对应于(n-1/2。否则父节点对应于(n-2)/2。

## C++

```
// C++ program to find n-th number containing
// only 4 and 7.
#include<bits/stdc++.h>
using namespace std;

string findNthNo(int n)
{
    string res = "";
    while (n >= 1)
    {
        // If n is odd, append 4 and
        // move to parent
        if (n & 1)
        {
            res = res + "4";
            n = (n-1)/2;       
        }

        // If n is even, append 7 and
        // move to parent
        else
        {
            res = res + "7";
            n = (n-2)/2;     
        }
    }

   // Reverse res and return.
   reverse(res.begin(), res.end());
   return res;
}

// Driver code
int main()
{
    int n = 13;
    cout << findNthNo(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find n-th number
// containing only 4 and 7.
public class GFG {

    static String findNthNo(int n)
    {
        String res = "";
        while (n >= 1)
        {

            // If n is odd, append
            // 4 and move to parent
            if ((n & 1) == 1)
            {
                res = res + "4";
                n = (n - 1) / 2;    
            }

            // If n is even, append
            // 7 and move to parent
            else
            {
                res = res + "7";
                n = (n - 2) / 2;    
            }
        }

        // Reverse res and return.
        StringBuilder sb =
            new StringBuilder(res);
        sb.reverse();
        return new String(sb);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 13;

        System.out.print( findNthNo(n) );
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to find
# n-th number containing
# only 4 and 7.
def reverse(s):
    if len(s) == 0:
        return s
    else:
        return reverse(s[1:]) + s[0]

def findNthNo(n):
    res = "";
    while (n >= 1):

        # If n is odd, append
        # 4 and move to parent
        if (n & 1):
            res = res + "4";
            n = (int)((n - 1) / 2);

            # If n is even, append7
            # and move to parent
        else:
            res = res + "7";
            n = (int)((n - 2) / 2);

    # Reverse res
    # and return.
    return reverse(res);

# Driver code
n = 13;
print(findNthNo(n));

# This code is contributed
# by mits
```

## C#

```
// C# program to find n-th number
// containing only 4 and 7.
using System;
class GFG {

static string findNthNo(int n)
{
    string res = "";
    while (n >= 1)
    {

        // If n is odd, append 4 and
        // move to parent
        if ((n & 1) == 1)
        {
            res = res + "4";
            n = (n - 1) / 2;    
        }

        // If n is even, append 7 and
        // move to parent
        else
        {
            res = res + "7";
            n = (n - 2) / 2;    
        }
    }

    // Reverse res and return.
    char[] arr = res.ToCharArray();
    Array.Reverse(arr);
    return new string(arr);

}

// Driver Code
public static void Main()
{
        int n = 13;
        Console.Write( findNthNo(n) );
}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// n-th number containing
// only 4 and 7.

function findNthNo($n)
{
    $res = "";
    while ($n >= 1)
    {
        // If n is odd, append
        // 4 and move to parent
        if ($n & 1)
        {
            $res = $res . "4";
            $n = (int)(($n - 1) / 2);
        }

        // If n is even, append
        // 7 and move to parent
        else
        {
            $res = $res . "7";
            $n = (int)(($n - 2) / 2);
        }
    }

// Reverse res
// and return.
return strrev($res);
}

// Driver code
$n = 13;
echo findNthNo($n);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// javascript program to find n-th number
// containing only 4 and 7.

function findNthNo(n)
{
res = "";
while (n >= 1)
{

// If n is odd, append
// 4 and move to parent
if ((n & 1) == 1)
{
res = res + "4";
n = (n - 1) / 2;    
}

// If n is even, append
// 7 and move to parent
else
{
res = res + "7";
n = parseInt((n - 2) / 2);    
}
}

// Reverse res and return.
return res.split("").reverse().join("");
}

// Driver code
var n = 13;

document.write( findNthNo(n) );

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
774
```

在这段代码中，总复杂度为 0(对数 n)。因为 while 循环运行 log (n)次。
本文由**德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。