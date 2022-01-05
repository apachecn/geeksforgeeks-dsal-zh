# 检查单次翻转是否可以使所有位相同

> 原文:[https://www . geeksforgeeks . org/check-如果所有位都可以通过单次翻转进行相同的制作/](https://www.geeksforgeeks.org/check-if-all-bits-can-be-made-same-by-single-flip/)

给定一个二进制字符串，通过恰好翻转一位来查找是否有可能使它的所有数字相等(全部为 0 或全部为 1)。

```
Input: 101
Output: Yes
Explanation: In 101, the 0 can be flipped
             to make it all 1

Input: 11
Output: No
Explanation: No matter whichever digit you 
  flip, you will not get the desired string.

Input: 1
Output: Yes
Explanation: We can flip 1, to make all 0's
```

**方法 1(计算 0 和 1)**
如果一个字符串的所有数字都可以通过恰好翻转一次而变得相同，这意味着除了必须翻转的这个数字之外，该字符串的所有数字都彼此相等，并且该数字必须不同于该字符串的所有其他数字。这个数字的值可以是零，也可以是一。因此，这个字符串要么正好有一个数字等于零，所有其他数字等于一，要么正好有一个数字等于一，所有其他数字等于零。
因此，我们只需要检查字符串是否正好有一个等于零/一的数字，如果有，答案是肯定的；否则答案是否定的。

以下是上述想法的实现。

## C++

```
// C++ program to check if a single bit can
// be flipped tp make all ones
#include <bits/stdc++.h>
using namespace std;

// This function returns true if we can
// bits same in given binary string str.
bool canMakeAllSame(string str)
{
    int zeros = 0, ones = 0;

    // Traverse through given string and
    // count numbers of 0's and 1's
    for (char ch : str)
        (ch == '0') ? ++zeros : ++ones;

    // Return true if any of the two counts
    // is 1
    return (zeros == 1 || ones == 1);
}

// Driver code
int main()
{
    canMakeAllSame("101") ? printf("Yes\n") : printf("No\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a single bit can
// be flipped to make all ones
public class GFG {

    // This function returns true if we can
    // bits same in given binary string str.
    static boolean canMakeAllSame(String str)
    {
        int zeros = 0, ones = 0;

        // Traverse through given string and
        // count numbers of 0's and 1's
        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            if (ch == '0')
                ++zeros;
            else
                ++ones;
        }

        // Return true if any of the two counts
        // is 1
        return (zeros == 1 || ones == 1);
    }

    // Driver code
    public static void main(String args[])
    {
        System.out.println(canMakeAllSame("101") ? "Yes" : "No");
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# python program to check if a single
# bit can be flipped tp make all ones

# This function returns true if we can
# bits same in given binary string str.
def canMakeAllSame(str):
    zeros = 0
    ones = 0

    # Traverse through given string and
    # count numbers of 0's and 1's
    for i in range(0, len(str)):
        ch = str[i];
        if (ch == '0'):
            zeros = zeros + 1
        else:
            ones = ones + 1

    # Return true if any of the two
    # counts is 1
    return (zeros == 1 or ones == 1);

# Driver code
if(canMakeAllSame("101")):
    print("Yes\n")
else:
    print("No\n")

# This code is contributed by Sam007.
```

## C#

```
// C# program to check if a single bit can
// be flipped to make all ones
using System;

class GFG {

    // This function returns true if we can
    // bits same in given binary string str.
    static bool canMakeAllSame(string str)
    {
        int zeros = 0, ones = 0;

        // Traverse through given string and
        // count numbers of 0's and 1's
        for (int i = 0; i < str.Length; i++) {
            char ch = str[i];
            if (ch == '0')
                ++zeros;
            else
                ++ones;
        }

        // Return true if any of the two counts
        // is 1
        return (zeros == 1 || ones == 1);
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(canMakeAllSame("101") ? "Yes" : "No");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to check if a single bit can
// be flipped tp make all ones

// This function returns true if we can
// bits same in given binary string str.
function canMakeAllSame($str)
{
    $zeros = 0;
    $ones = 0;

    // Traverse through given string and
    // count numbers of 0's and 1's

    for($i=0;$i<strlen($str);$i++)
    {
        $ch = $str[$i];
        if ($ch == '0')
            ++$zeros ;
        else
            ++$ones;
    }
    // Return true if any of the two counts
    // is 1
    return ($zeros == 1 || $ones == 1);
}

// Driver code

    if (canMakeAllSame("101") )
       echo "Yes\n" ;
    else echo "No\n";
    return 0;
?>
```

## java 描述语言

```
<script>
// Javascript program to check if a single bit can
// be flipped to make all ones

    // This function returns true if we can
    // bits same in given binary string str.
    function canMakeAllSame(str)
    {
        let zeros = 0, ones = 0;

        // Traverse through given string and
        // count numbers of 0's and 1's
        for (let i = 0; i < str.length; i++) {
            let ch = str[i];
            if (ch == '0')
                ++zeros;
            else
                ++ones;
        }

        // Return true if any of the two counts
        // is 1
        return (zeros == 1 || ones == 1);
    }

    // Driver code
    document.write(canMakeAllSame("101") ? "Yes" : "No");

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)其中 n 是字符串的长度。

**方法 2(计算 0 和 1)**
想法是计算所有位的和。如果和是 n-1 或 1，则输出为真，否则为假。这个解决方案不需要循环比较。

以下是上述想法的实现。

## C++

```
// Check if all bits can be made same by single flip
// Idea is to add the integer value all the elements
// in the given string.
// If the sum is 1 it indicates that there is
// only single '1' in the string.
// If the sum is 0 it indicates that there is only
// single '0' in the string.
// It takes O(n) time.

#include <bits/stdc++.h>
using namespace std;

bool isOneFlip(string str)
{
    int sum = 0;
    int n = str.length();

    // Traverse through given string and
    // count the total sum of numbers
    for (int i = 0; i < n; i++)
        sum += str[i] - '0';

    // Return true if any of the two counts
    // is 1
    return (sum == n - 1 || sum == 1);
}

// Main function
int main()
{
    isOneFlip("101111111111") ? printf("Yes\n") : printf("No\n");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*Check if all bits can be made same by single
flip. Idea is to add the integer value all the
elements in the given string.
If the sum is 1 it indicates that there is
   only single '1' in the string.
If the sum is 0 it indicates that there is only
   single '0' in the string.
It takes O(n) time.*/
public class GFG {

    static boolean isOneFlip(String str)
    {
        int sum = 0;
        int n = str.length();

        // Traverse through given string and
        // count the total sum of numbers
        for (int i = 0; i < n; i++)
            sum += str.charAt(i) - '0';

        // Return true if any of the two counts
        // is 1
        return (sum == n - 1 || sum == 1);
    }

    // Main function
    public static void main(String args[])
    {
        System.out.println(isOneFlip("101111111111") ? "Yes" : "No");
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Check if all bits can be made same
# by single flip Idea is to add the
# integer value all the elements in
# the given string. If the sum is 1
# it indicates that there is only
# single '1' in the string. If the
# sum is 0 it indicates that there
# is only single '0' in the string.
# It takes O(n) time.

def isOneFlip(str):

    sum = 0
    n = len(str)

    # Traverse through given string
    # and count the total sum of
    # numbers
    for i in range( 0, n ):
        sum += int(str[i]) - int('0')

    # Return true if any of the two
    # counts is 1
    return (sum == n - 1 or sum == 1)

# Main function
(print("Yes") if isOneFlip("101111111111")
                        else print("No"))

# This code is contributed by Smitha
```

## C#

```
/*Check if all bits can be made same by single
  flip. Idea is to add the integer value all the
  elements in the given string.
  If the sum is 1 it indicates that there is
  only single '1' in the string.
  If the sum is 0 it indicates that there is only
  single '0' in the string.
  It takes O(n) time.*/
using System;

class GFG {

    static bool isOneFlip(string str)
    {
        int sum = 0;
        int n = str.Length;

        // Traverse through given string and
        // count the total sum of numbers
        for (int i = 0; i < n; i++)
            sum += str[i] - '0';

        // Return true if any of the two counts
        // is 1
        return (sum == n - 1 || sum == 1);
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(isOneFlip("101111111111") ? "Yes" : "No");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Check if all bits can be made same by
// single flip Idea is to add the integer
// value all the elements in the given
// string. If the sum is 1 it indicates
// that there is only single '1' in the
// string. If the sum is 0 it indicates
// that there is only single '0' in the
// string. It takes O(n) time.

function isOneFlip($str)
{
    $sum = 0;
    $n = strlen($str);

    // Traverse through given string and
    // count the total sum of numbers
    for ( $i = 0; $i < $n; $i++)
        $sum += $str[$i] - '0';

    // Return true if any of the two counts
    // is 1
    return ($sum == $n - 1 || $sum == 1);
}

// Main function
    if(isOneFlip("101111111111") )
        echo "Yes\n";
    else
        echo "No\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

/*Check if all bits can be made same by single
flip. Idea is to add the integer value all the
elements in the given string.
If the sum is 1 it indicates that there is
   only single '1' in the string.
If the sum is 0 it indicates that there is only
   single '0' in the string.
It takes O(n) time.*/
function isOneFlip(str)
{
    let sum = 0;
    let n = str.length;

    // Traverse through given string and
    // count the total sum of numbers
    for(let i = 0; i < n; i++)
        sum += str[i] - '0';

    // Return true if any of the two counts
    // is 1
    return (sum == n - 1 || sum == 1);
}

// Driver code
document.write(isOneFlip("101111111111") ?
               "Yes" : "No");

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(N)
**辅助空间:** O(1)
感谢**苏拉布·加弗黑尔**提出这个解决方案

本文由 **Subrata Ghosh** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。