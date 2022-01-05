# 凯斯号

> 原文:[https://www.geeksforgeeks.org/keith-number/](https://www.geeksforgeeks.org/keith-number/)

如果一个 n 位数字 x 出现在用其数字生成的特殊序列(定义如下)中，则称其为 Keith 数。特殊序列的前 n 个项是 x 的数字，其他项被递归计算为前 n 个项的和。
任务是找出给定的数字是不是基思数。
**例:**

```
Input : x = 197
Output : Yes
197 has 3 digits, so n = 3
The number is Keith because it appears in the special
sequence that has first three terms as 1, 9, 7 and 
remaining terms evaluated using sum of previous 3 terms.
1, 9, 7, 17, 33, 57, 107, 197, .....

Input : x = 12
Output : No
The number is not Keith because it doesn't appear in
the special sequence generated using its digits.
1, 2, 3, 5, 8, 13, 21, .....

Input : x = 14
Output : Yes
14 is a Keith number since it appears in the sequence,
1, 4, 5, 9, 14, ...
```

**算法:**

1.  将给定数字“x”的“n”位存储在数组“terms”中。
2.  循环用于生成序列的下一项并添加前一个“n”项。
3.  继续将步骤 2 中的 next_terms 存储在数组“terms”中。
4.  如果下一项等于 x，那么 x 就是 Keith 数。如果下一项变得大于 x，那么 x 不是基思数。

## C++

```
// C++ program to check if a number is Keith or not

#include<bits/stdc++.h>
using namespace std;

// Returns true if x is Keith, else false.
bool isKeith(int x)
{
    // Store all digits of x in a vector "terms"
    // Also find number of digits and store in "n".
    vector <int> terms;
    int temp = x, n = 0; // n is number of digits in x
    while (temp > 0)
    {
        terms.push_back(temp%10);
        temp = temp/10;
        n++;
    }

    // To get digits in right order (from MSB to
    // LSB)
    reverse(terms.begin(), terms.end());

    // Keep finding next trms of a sequence generated
    // using digits of x until we either reach x or a
    // number greate than x
    int next_term = 0, i = n;
    while (next_term < x)
    {
        next_term = 0;

        // Next term is sum of previous n terms
        for (int j=1; j<=n; j++)
            next_term += terms[i-j];

        terms.push_back(next_term);
        i++;
    }

    /* When the control comes out of the while loop,
       either the next_term is equal to the number
       or greater than it.
       If next_term is equal to x, then x is a
       Keith number, else not */
    return (next_term == x);
}

// Driver program
int main()
{
   isKeith(14)? cout << "Yes\n" : cout << "No\n";
   isKeith(12)? cout << "Yes\n" : cout << "No\n";
   isKeith(197)? cout << "Yes\n" : cout << "No\n";
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is Keith or not
import java.io.*;
import java.util.*;

class GFG{
// Returns true if x is Keith, else false.
static boolean isKeith(int x)
{
    // Store all digits of x in a vector "terms"
    // Also find number of digits and store in "n".
    ArrayList<Integer> terms=new ArrayList<Integer>();
    int temp = x, n = 0; // n is number of digits in x
    while (temp > 0)
    {
        terms.add(temp%10);
        temp = temp/10;
        n++;
    }

    // To get digits in right order (from MSB to
    // LSB)
    Collections.reverse(terms);

    // Keep finding next trms of a sequence generated
    // using digits of x until we either reach x or a
    // number greate than x
    int next_term = 0, i = n;
    while (next_term < x)
    {
        next_term = 0;

        // Next term is sum of previous n terms
        for (int j=1; j<=n; j++)
            next_term += terms.get(i-j);

        terms.add(next_term);
        i++;
    }

    /* When the control comes out of the while loop,
    either the next_term is equal to the number
    or greater than it.
    If next_term is equal to x, then x is a
    Keith number, else not */
    return (next_term == x);
}

// Driver program
public static void main(String[] args)
{
if (isKeith(14))
System.out.println("Yes");
else
System.out.println("No");
if(isKeith(12))
System.out.println("Yes");
else
System.out.println("No");
if(isKeith(197))
System.out.println("Yes");
else
System.out.println("No");

}
}
// this code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to check if a number
# is Keith or not

# Returns true if x is Keith,
# else false.
def isKeith(x):

    # Store all digits of x in a vector "terms"
    # Also find number of digits and store in "n".
    terms = [];
    temp = x;
    n = 0; # n is number of digits in x
    while (temp > 0):
        terms.append(temp % 10);
        temp = int(temp / 10);
        n+=1;

    # To get digits in right order
    # (from MSB to LSB)
    terms.reverse();

    # Keep finding next trms of a sequence
    # generated using digits of x until we
    # either reach x or a number greate than x
    next_term = 0;
    i = n;
    while (next_term < x):
        next_term = 0;

        # Next term is sum of previous n terms
        for j in range(1,n+1):
            next_term += terms[i - j];

        terms.append(next_term);
        i+=1;

    # When the control comes out of the
    # while loop, either the next_term is
    # equal to the number or greater than it.
    # If next_term is equal to x, then x is a
    # Keith number, else not
    return (next_term == x);

# Driver Code
print("Yes") if (isKeith(14)) else print("No");
print("Yes") if (isKeith(12)) else print("No");
print("Yes") if (isKeith(197)) else print("No");

# This code is contributed by mits
```

## C#

```
// C# program to check if a number is Keith or not
using System;
using System.Collections;

class GFG{
// Returns true if x is Keith, else false.
static bool isKeith(int x)
{
    // Store all digits of x in a vector "terms"
    // Also find number of digits and store in "n".
    ArrayList terms = new ArrayList();
    int temp = x, n = 0; // n is number of digits in x
    while (temp > 0)
    {
        terms.Add(temp%10);
        temp = temp/10;
        n++;
    }

    // To get digits in right order (from MSB to
    // LSB)
    terms.Reverse();

    // Keep finding next trms of a sequence generated
    // using digits of x until we either reach x or a
    // number greate than x
    int next_term = 0, i = n;
    while (next_term < x)
    {
        next_term = 0;

        // Next term is sum of previous n terms
        for (int j=1; j<=n; j++)
            next_term += (int)terms[i-j];

        terms.Add(next_term);
        i++;
    }

    /* When the control comes out of the while loop,
    either the next_term is equal to the number
    or greater than it.
    If next_term is equal to x, then x is a
    Keith number, else not */
    return (next_term == x);
}

// Driver program
public static void Main()
{
if (isKeith(14))
Console.WriteLine("Yes");
else
Console.WriteLine("No");
if(isKeith(12))
Console.WriteLine("Yes");
else
Console.WriteLine("No");
if(isKeith(197))
Console.WriteLine("Yes");
else
Console.WriteLine("No");

}
}
// this code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is Keith or not

// Returns true if x is Keith,
// else false.
function isKeith($x)
{
    // Store all digits of x in a vector "terms"
    // Also find number of digits and store in "n".
    $terms = array();
    $temp = $x;
    $n = 0; // n is number of digits in x
    while ($temp > 0)
    {
        array_push($terms, $temp % 10);
        $temp = (int)($temp / 10);
        $n++;
    }

    // To get digits in right order
    // (from MSB to LSB)
    $terms=array_reverse($terms);

    // Keep finding next trms of a sequence
    // generated using digits of x until we
    // either reach x or a number greate than x
    $next_term = 0;
    $i = $n;
    while ($next_term < $x)
    {
        $next_term = 0;

        // Next term is sum of previous n terms
        for ($j = 1; $j <= $n; $j++)
            $next_term += $terms[$i - $j];

        array_push($terms, $next_term);
        $i++;
    }

    /* When the control comes out of the
    while loop, either the next_term is
    equal to the number or greater than it.
    If next_term is equal to x, then x is a
    Keith number, else not */
    return ($next_term == $x);
}

// Driver Code
isKeith(14) ? print("Yes\n") : print("No\n");
isKeith(12) ? print("Yes\n") : print("No\n");
isKeith(197) ? print("Yes\n") : print("No\n");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number
// is Keith or not

// Returns true if x is Keith,
// else false.
function isKeith(x)
{
    // Store all digits of x in a vector "terms"
    // Also find number of digits and store in "n".
    let terms = [];
    let temp = x;
    let n = 0; // n is number of digits in x
    while (temp > 0)
    {
        terms.push(temp % 10);
        temp = parseInt(temp / 10);
        n++;
    }

    // To get digits in right order
    // (from MSB to LSB)
    terms= terms.reverse();

    // Keep finding next trms of a sequence
    // generated using digits of x until we
    // either reach x or a number greate than x
    let next_term = 0;
    let i = n;
    while (next_term < x)
    {
        next_term = 0;

        // Next term is sum of previous n terms
        for (let j = 1; j <= n; j++)
            next_term += terms[i - j];

        terms.push(next_term);
        i++;
    }

    /* When the control comes out of the
    while loop, either the next_term is
    equal to the number or greater than it.
    If next_term is equal to x, then x is a
    Keith number, else not */
    return (next_term == x);
}

// Driver Code
isKeith(14) ? document.write("Yes<br>") :
document.write("No<br>");
isKeith(12) ? document.write("Yes<br>") :
document.write("No<br>");
isKeith(197) ? document.write("Yes<br>") :
document.write("No<br>");

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Yes
No
Yes
```

本文由 [**Pratik Agarwal**](https://www.facebook.com/Pratik.Agarwal01) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。