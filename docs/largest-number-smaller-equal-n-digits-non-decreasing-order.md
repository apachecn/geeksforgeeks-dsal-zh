# 小于或等于 n 的最大数字和非递减顺序的数字

> 原文:[https://www . geesforgeks . org/最大-数字-较小-相等-n 位数-非递减-顺序/](https://www.geeksforgeeks.org/largest-number-smaller-equal-n-digits-non-decreasing-order/)

给定一个数字 n，找出小于或等于 n 的最大数字和非递减顺序的数字。

**示例:**

```
Input  : n = 200
Output : 199
If the given number is 200, the largest 
number which is smaller or equal to it 
having digits in non decreasing order is
199.

Input  : n = 139
Output : 139
```

**方法 1(蛮力)**
从 n 开始，对于每个数字，检查其位数是否为非递减顺序。如果是，那么返回。否则检查下一个数字，直到我们找到结果。

## C++

```
/* C++ program for brute force approach to find
   largest number having digits in non-decreasing
   order. */
#include<bits/stdc++.h>
using namespace std;

// Returns the required number
long long nondecdigits(long long n)
{
    /* loop to recursively check the numbers less
       than or equal to given number*/
    long long int x = 0;
    for (x=n; x>=1; x--)
    {
        int no = x;
        int prev_dig = 11;

        // Keep traversing digits from
        // right to left. For every digit
        // check if it is smaller than prev_dig
        bool flag = true;
        while (no != 0)
        {
            if (prev_dig < no%10)
            {
               flag = false;
               break;
            }
            prev_dig = no % 10;
            no /= 10;
        }

        // We found the required number
        if (flag == true)
           break;
    }

    return x;
}

// Driver program
int main()
{
    long long n = 200;
    cout << nondecdigits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for brute force
// approach to find largest number
// having digits in non-decreasing
// order.
import java.io.*;

class GFG
{

// Returns the required number
static int nondecdigits(int n)
{
    // loop to recursively check
    // the numbers less than or
    // equal to given number
    int x = 0;
    for (x = n; x >= 1; x--)
    {
        int no = x;
        int prev_dig = 11;

        // Keep traversing digits
        // from right to left. For
        // every digit check if it
        // is smaller than prev_dig
        boolean flag = true;
        while (no != 0)
        {
            if (prev_dig < no % 10)
            {
                flag = false;
                break;
            }
            prev_dig = no % 10;
            no /= 10;
        }

        // We found the
        // required number
        if (flag == true)
        break;
    }

    return x;
}

// Driver Code
public static void main (String[] args)
{
    int n = 200;
    System.out.println (nondecdigits(n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python 3 program for brute force approach
# to find largest number having digits in
# non-decreasing order.

# Returns the required number
def nondecdigits( n):

    ''' loop to recursively check the numbers
    less than or equal to given number'''
    x = 0
    for x in range(n, 0, -1):
        no = x
        prev_dig = 11

        # Keep traversing digits from
        # right to left. For every digit
        # check if it is smaller than prev_dig
        flag = True
        while (no != 0):
            if (prev_dig < no % 10):
                flag = False
                break

            prev_dig = no % 10
            no //= 10

        # We found the required number
        if (flag == True):
            break
    return x

# Driver Code
if __name__=="__main__":

    n = 200
    print(nondecdigits(n))

# This code is contributed by ita_c
```

## C#

```
// C# program for brute
// force approach to find
// largest number having
// digits in non-decreasing
// order.
using System;

class GFG
{
// Returns the required number
static int nondecdigits(int n)
{
    // loop to recursively
    // check the numbers less
    // than or equal to given
    // number
    int x = 0;
    for (x = n; x >= 1; x--)
    {
        int no = x;
        int prev_dig = 11;

        // Keep traversing digits
        // from right to left. For
        // every digit check if it
        // is smaller than prev_dig
        bool flag = true;
        while (no != 0)
        {
            if (prev_dig < no % 10)
            {
                flag = false;
                break;
            }
            prev_dig = no % 10;
            no /= 10;
        }

        // We found the
        // required number
        if (flag == true)
        break;
    }

    return x;
}

// Driver Code
static public void Main ()
{
    int n = 200;
    Console.WriteLine(nondecdigits(n));
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for brute
// force approach to find
// largest number having
// digits in non-decreasing
// order.

// Returns the required number
function nondecdigits($n)
{

    /* loop to recursively
       check the numbers less
       than or equal to
       given number*/
    $x = 0;
    for ($x = $n; $x >= 1; $x--)
    {
        $no = $x;
        $prev_dig = 11;

        // Keep traversing
        // digits from
        // right to left.
        // For every digit
        // check if it is
        // smaller than prev_dig
        $flag = true;
        while ($no != 0)
        {
            if ($prev_dig < $no%10)
            {
                $flag = false;
                break;
            }
            $prev_dig = $no % 10;
            $no /= 10;
        }

        // We found the
        // required number
        if ($flag == true)
        break;
    }

    return $x;
}

    // Driver Code
    $n = 200;
    echo nondecdigits($n);

// This code is contributed by ajt
?>
```

## java 描述语言

```
<script>

// Javascript program for brute force 
// approach to find largest number
// having digits in non-decreasing
// order.    

// Returns the required number
function nondecdigits(n)
{

    // Loop to recursively check
    // the numbers less than or
    // equal to given number
    let x = 0;
    for(x = n; x >= 1; x--)
    {
        let no = x;
        let prev_dig = 11;

        // Keep traversing digits
        // from right to left. For
        // every digit check if it
        // is smaller than prev_dig
        let flag = true;
        while (no != 0)
        {
            if (prev_dig < no % 10)
            {
                flag = false;
                  break;
            }
            prev_dig = no % 10;
            no = Math.floor(no / 10);
        }

        // We found the
        // required number
        if (flag == true)
          break;
    }
    return x;
}

// Driver code
let n = 200;

document.write(nondecdigits(n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
199
```

**有效方法**
上面讨论的方法效率不高，因为只会给出 10^5 之前的数字的结果，但是如果数字非常大，以至于它包含 10^5 数字。

所以，我们将讨论这种大数的另一种方法。
**第一步:**将数字的位数存储在数组或向量中。
**第二步:**从给定数字的最右边到最左边开始遍历数组。
**第三步:**如果一个数字大于其右边的数字，记下该数字在该数组中的索引，并将该数字减 1。
**第 4 步:**继续更新该索引，直到如第 3 步中所讨论的那样完全遍历该数组。
**第 4 步:**将该索引右侧的所有数字设置为 9。
**第五步:**打印数组，因为这是需要的数字。

假设数字是 200，数字是 2，0，0。最左边的数字大于右边的数字的索引是索引 1(在 1-index 之后)，所以索引 1 的数字是 2–1 = 1，它右边的所有数字都是 9。所以最后的数组是 1，9，9。所需的号码是 199。

## C++

```
/* C++ program for efficient approach to find
   largest number having digits in non-decreasing
   order. */
#include<bits/stdc++.h>
using namespace std;

// Prints the largest number smaller than s and
// digits in non-decreasing order.
void nondecdigits(string s)
{
    long long m = s.size();

    /* array to store digits of number */
    long long a[m];

    /* conversion of characters of string int number */
    for (long long i=0; i<m; i++)
        a[i] = s[i] - '0';

    /* variable holds the value of index after which
       all digits are set 9 */
    long long level = m-1;
    for (long long i=m-1; i>0; i--)
    {
        /* Checking the condition if the digit is
           less than its left digit */
        if (a[i] < a[i-1])
        {
            a[i-1]--;
            level=i-1;
        }
    }

    /* If first digit is 0 no need to print it */
    if (a[0] != 0)
    {
        for (long long i=0; i<=level; i++)
            cout << a[i];
        for (long long i=level+1; i<m; i++)
            cout << "9";
    }
    else
    {
        for (long long i=1; i<level; i++)
            cout << a[i];
        for (long long i=level+1; i<m; i++)
            cout << "9";
    }
}

// Driver function
int main()
{
    string n = "200";
    nondecdigits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program for efficient approach to find
largest number having digits in non-decreasing
order. */
import java.util.*;

class GFG
{

// Prints the largest number smaller than s and
// digits in non-decreasing order.
static void nondecdigits(String s)
{
    int m = s.length();

    /* array to store digits of number */
    int[] a = new int[m + 1];

    /* conversion of characters of string int number */
    for (int i = 0; i < m; i++)
        a[i] = (int)s.charAt(i) - (int)'0';

    /* variable holds the value of index after which
    all digits are set 9 */
    int level = m - 1;
    for (int i = m - 1; i > 0; i--)
    {
        /* Checking the condition if the digit is
        less than its left digit */
        if (a[i] < a[i - 1])
        {
            a[i - 1]--;
            level = i - 1;
        }
    }

    /* If first digit is 0 no need to print it */
    if (a[0] != 0)
    {
        for (int i = 0; i <= level; i++)
            System.out.print(a[i]);
        for (int i = level + 1; i < m; i++)
            System.out.print("9");
    }
    else
    {
        for (int i = 1; i < level; i++)
            System.out.print(a[i]);
        for (int i = level + 1; i < m; i++)
            System.out.print("9");
    }
}

// Driver code
public static void main(String[] args)
{
    String n = "200";
    nondecdigits(n);
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program for efficient approach to
# find largest number having digits in
# non-decreasing order.

# Prints the largest number smaller than s
# and digits in non-decreasing order.
def nondecdigits(s):
    m = len(s);

    # array to store digits of number
    a = [0] * m;

    # conversion of characters of string
    # int number
    for i in range(m):
        a[i] = ord(s[i]) - ord('0');

    # variable holds the value of index
    # after which all digits are set 9
    level = m - 1;
    for i in range(m - 1, 0, -1):

        # Checking the condition if the digit
        # is less than its left digit
        if (a[i] < a[i - 1]):
            a[i - 1] -= 1;
            level = i - 1;

    # If first digit is 0 no need to print it */
    if (a[0] != 0):
        for i in range(level + 1):
            print(a[i], end = "");
        for i in range(level + 1, m):
            print("9", end = "");
    else:
        for i in range(1, level):
            print(a[i], end = "");
        for i in range(level + 1, m):
            print("9", end = "");

# Driver Code
n = "200";
nondecdigits(n);

# This code is contributed by mits
```

## C#

```
/* C# program for efficient approach to find
largest number having digits in non-decreasing
order. */
using System;

class GFG
{

// Prints the largest number smaller than s and
// digits in non-decreasing order.
static void nondecdigits(string s)
{
    int m = s.Length;

    /* array to store digits of number */
    int[] a = new int[m + 1];

    /* conversion of characters of string int number */
    for (int i = 0; i < m; i++)
        a[i] = (int)s[i] - (int)'0';

    /* variable holds the value of index after which
    all digits are set 9 */
    int level = m - 1;
    for (int i = m - 1; i > 0; i--)
    {
        /* Checking the condition if the digit is
        less than its left digit */
        if (a[i] < a[i - 1])
        {
            a[i - 1]--;
            level = i - 1;
        }
    }

    /* If first digit is 0 no need to print it */
    if (a[0] != 0)
    {
        for (int i = 0; i <= level; i++)
            Console.Write(a[i]);
        for (int i = level + 1; i < m; i++)
            Console.Write("9");
    }
    else
    {
        for (int i = 1; i < level; i++)
            Console.Write(a[i]);
        for (int i = level + 1; i < m; i++)
            Console.Write("9");
    }
}

// Driver code
static void Main()
{
    string n = "200";
    nondecdigits(n);
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* PHP program for efficient
approach to find largest number
having digits in non-decreasing
order. */

// Prints the largest number
// smaller than s and digits
// in non-decreasing order.
function nondecdigits($s)
{
    $m = strlen($s);

    /* array to store
    digits of number */
    $a[$m] = 0;

    /* conversion of characters
    of string int number */
    for ($i = 0; $i < $m; $i++)
        $a[$i] = $s[$i] - '0';

    /* variable holds the
    value of index after
    which all digits are set 9 */
    $level = $m - 1;
    for ($i = $m - 1; $i > 0; $i--)
    {
        /* Checking the condition
        if the digit is less than
        its left digit */
        if ($a[$i] < $a[$i - 1])
        {
            $a[$i - 1]--;
            $level = $i - 1;
        }
    }

    /* If first digit is 0
    no need to print it */
    if ($a[0] != 0)
    {
        for ($i = 0;
             $i <= $level; $i++)
            echo $a[$i];
        for ($i = $level + 1;
             $i < $m; $i++)
            echo "9";
    }
    else
    {
        for ($i = 1; $i < $level; $i++)
            echo $a[$i];
        for ($i = $level + 1;
             $i < $m; $i++)
                echo "9";
    }
}

// Driver Code
$n = "200";
nondecdigits($n);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program for efficient approach
// to find largest number having digits in
// non-decreasing order.

// Prints the largest number smaller than
// s and digits in non-decreasing order.
function nondecdigits(s)
{
    var m = s.length;

    // Array to store digits of number
    var a = Array.from({length: m + 1}, (_, i) => 0);

    // Conversion of characters of string var number
    for(i = 0; i < m; i++)
        a[i] = s.charAt(i).charCodeAt(0) -
                       '0'.charCodeAt(0);

    // Variable holds the value of index
    // after which all digits are set 9
    var level = m - 1;
    for(i = m - 1; i > 0; i--)
    {

        // Checking the condition if the digit is
        // less than its left digit
        if (a[i] < a[i - 1])
        {
            a[i - 1]--;
            level = i - 1;
        }
    }

    // If first digit is 0 no need to print it
    if (a[0] != 0)
    {
        for(i = 0; i <= level; i++)
            document.write(a[i]);
        for(i = level + 1; i < m; i++)
            document.write("9");
    }
    else
    {
        for(i = 1; i < level; i++)
            document.write(a[i]);
        for(i = level + 1; i < m; i++)
            document.write("9");
    }
}

// Driver code
var n = "200";
nondecdigits(n);

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
199
```

**时间复杂度**时间复杂度为 O(d)，其中 d 为数字中的位数。

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。