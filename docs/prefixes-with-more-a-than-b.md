# a 大于 b 的前缀

> 原文:[https://www.geeksforgeeks.org/prefixes-with-more-a-than-b/](https://www.geeksforgeeks.org/prefixes-with-more-a-than-b/)

给定一个字符串 **S** ，仅由字符**【a】**和**【b】**组成，以及一个整数 **N** 。将弦 S 相加 N 次，得到弦 **T** 。您的任务是计算前缀的数量，其中 a 的数量严格大于 b。n 次。
**举例:**

```
Input : aba 2
Output : 5
Explanation : 
The string T is "abaaba". It has five prefixes
which contain more a-s than b-s: "a", "aba", 
"abaa", "abaab" and "abaaba".

Input : baa 3
Output : 6
Explanation : The string T is "baabaabaa". The strings 
"baa", "baaba", "baabaa", "baabaab", "baabaaba" and 
"baabaabaa" are the six valid prefixes.
```

**天真的方法:**做这个程序的一个简单方法是生成整个字符串 T，然后运行一个循环来检查有效前缀，其中 A 的数量大于 b 的数量。如果 N 的值非常大，这种方法效率不高，但很耗时。
**高效进场:**
注意字符串是重复的。因此，我们不必检查整个字符串 T.
对字符串 S 进行操作，让，
**计数** =字符串 S 中的前缀数
**A** =字符串 S 中字符‘A’的出现频率
**B** =字符串 S 中字符‘B’的出现频率
**案例 1:如果有效前缀数为零，计数== 0**
。然后，即使我们生成整个字符串，有效前缀的数量仍然为零。
**CASE 2:count>0**
*这个案例有三个子案例:*
**a. A == B**
在这种情况下，S 之前的串联对 S 的传入/新串联没有影响，换句话说，当 A！= B，那么在每次将 S 加到 T 之后(A-B)的值会有一些变化，这会影响未来任何 S 的串联对计数的贡献。也就是说，既然 A == B，那么 T 中的 B 的个数在每次相加时不会和 A 的个数以同样的速度增加，这将影响下一次相加对最终答案的贡献。当 A == B 时，情况并非如此。因此，S 的每次相加都会对最终答案产生影响。S 有 N 个加法，我们已经通过前面的简单循环找到了计数。因此，对于这种情况，答案= count * n .
**B . A<B**
在这种情况下，因为 A < B，S 到 T 的每一个新的加法都会减少 A-B，换句话说，T 中的 B 的数量会比 A 的数量增加得更快，这将减少 S 的每一个未来加法对最终答案的贡献。我们看到，每次加法之后，下一次加法的贡献必须至少减少 1。因此，每个新字符串的计数将逐渐收敛到零。所以我们必须检查直到那发生。
例如，字符串 S 的 Say 计数经过 1000 次加法后收敛到零。如果 N = 99999，我们只需要检查到 1000，忽略其余的情况。如果 N = 5，我们要计算到 5 次加法。
**c. A > B**
很明显，S 到 T 的每次新加法都会增加 A-B，因此，T 中的 A 的个数会比 B 的个数增加得更快，这将增加 S 未来每次加法对最终答案的贡献。加法对我们的答案的最大可能贡献可以是|S|，即字符串 S 的长度。因此，在一些加法之后，每个字符串的计数将饱和到字符串的长度。在那之前我们必须检查。
例如:假设串 S 的计数在 X 相加后饱和到 S 的长度。所以，我们必须计算计数到 X，然后加上等于(N-X)* S 长度的余数(如果 N > X)
如果 N < X，那么我们必须计算到 N 次加法。
以下是上述办法的实施:

## C++

```
// CPP code to count the prefixes
// with more a than b
#include <bits/stdc++.h>

using namespace std;

// Function to count prefixes
int prefix(string k, int n)
{
    int a = 0, b = 0, count = 0;
    int i = 0;
    int len = k.size();

    // calculating for string S
    for (i = 0; i < len; i++) {
        if (k[i] == 'a')
            a++;

        if (k[i] == 'b')
            b++;

        if (a > b) {
            count++;
        }
    }

    // count==0 or when N==1
    if (count == 0 || n == 1) {
        cout << count << endl;
        return 0;
    }

    // when all characters are a or a-b==0
    if (count == len || a - b == 0) {
        cout << count * n << endl;
        return 0;
    }

    int n2 = n - 1, count2 = 0;

    // checking for saturation of
    // string after repetitive addition
    while (n2 != 0) {
        for (i = 0; i < len; i++) {
            if (k[i] == 'a')
                a++;

            if (k[i] == 'b')
                b++;

            if (a > b) {
                count2++;
            }
        }

        count += count2;
        n2--;

        if (count2 == 0)
            break;

        if (count2 == len) {
            count += (n2 * count2);
            break;
        }

        count2 = 0;
    }

    return count;
}

// Driver function
int main()
{
    string S = "aba";
    int N = 2;
    cout << prefix(S, N) << endl;

    S = "baa";
    N = 3;
    cout << prefix(S, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count the
// prefixes with more a than b
import java.io.*;

class GFG
{

// Function to
// count prefixes
static int prefix(String k, int n)
{
    int a = 0, b = 0,
               count = 0;
    int i = 0;
    int len = k.length();

    // calculating for string S
    for (i = 0; i < len; i++)
    {
        if (k.charAt(i) == 'a')
            a++;

        if (k.charAt(i) == 'b')
            b++;

        if (a > b)
        {
            count++;
        }
    }

    // count==0 or when N==1
    if (count == 0 || n == 1)
    {
        System.out.println(count);
        return 0;
    }

    // when all characters
    // are a or a-b==0
    if (count == len || a - b == 0)
    {
        System.out.println(count * n);
        return 0;
    }

    int n2 = n - 1, count2 = 0;

    // checking for saturation
    // of string after repetitive
    // addition
    while (n2 != 0)
    {
        for (i = 0; i < len; i++)
        {
            if (k.charAt(i) == 'a')
                a++;

            if (k.charAt(i) == 'b')
                b++;

            if (a > b)
            {
                count2++;
            }
        }

        count += count2;
        n2--;

        if (count2 == 0)
            break;

        if (count2 == len)
        {
            count += (n2 * count2);
            break;
        }

        count2 = 0;
    }

    return count;
}

// Driver Code
public static void main (String[] args)
{
    String S = "aba";
    int N = 2;
    System.out.println(prefix(S, N));

    S = "baa";
    N = 3;
    System.out.println(prefix(S, N)) ;
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 code to count the prefixes
# with more a than b

# Function to count prefixes
def prefix(k, n):

    a = 0
    b = 0
    count = 0
    i = 0
    Len = len(k)

    # calculating for string S
    for i in range(Len):
        if (k[i] == "a"):
            a += 1

        if (k[i] == "b"):
            b += 1

        if (a > b) :
            count += 1

    # count==0 or when N==1
    if (count == 0 or n == 1):
        print(count)
        return 0

    # when all characters are a or a-b==0
    if (count == Len or a - b == 0) :
        print(count * n)
        return 0

    n2 = n - 1
    count2 = 0

    # checking for saturation of
    # string after repetitive addition
    while (n2 != 0):
        for i in range(Len):
            if (k[i] == "a"):
                a += 1

            if (k[i] == "b"):
                b += 1

            if (a > b):
                count2 += 1

        count += count2
        n2 -= 1

        if (count2 == 0):
            break

        if (count2 == Len):
            count += (n2 * count2)
            break

        count2 = 0

    return count

# Driver Code
S = "aba"
N = 2
print(prefix(S, N))

S = "baa"
N = 3
print(prefix(S, N))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# code to count the
// prefixes with more
// a than b
using System;

class GFG
{

// Function to
// count prefixes
static int prefix(String k, int n)
{
    int a = 0, b = 0,
        count = 0;
    int i = 0;
    int len = k.Length;

    // calculating for string S
    for (i = 0; i < len; i++)
    {
        if (k[i] == 'a')
            a++;

        if (k[i] == 'b')
            b++;

        if (a > b)
        {
            count++;
        }
    }

    // count==0 or when N==1
    if (count == 0 || n == 1)
    {
        Console.WriteLine(count);
        return 0;
    }

    // when all characters
    // are a or a-b==0
    if (count == len ||
        a - b == 0)
    {
        Console.WriteLine(count * n);
        return 0;
    }

    int n2 = n - 1, count2 = 0;

    // checking for saturation
    // of string after repetitive
    // addition
    while (n2 != 0)
    {
        for (i = 0; i < len; i++)
        {
            if (k[i] == 'a')
                a++;

            if (k[i] == 'b')
                b++;

            if (a > b)
            {
                count2++;
            }
        }

        count += count2;
        n2--;

        if (count2 == 0)
            break;

        if (count2 == len)
        {
            count += (n2 * count2);
            break;
        }

        count2 = 0;
    }

    return count;
}

// Driver Code
public static void Main ()
{
    string S = "aba";
    int N = 2;
    Console.WriteLine(prefix(S, N));

    S = "baa";
    N = 3;
    Console.WriteLine(prefix(S, N)) ;
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to count the
// prefixes with more a than b

// Function to count prefixes
function prefix($k, $n)
{
    $a = 0; $b = 0; $count = 0;
    $i = 0;
    $len = strlen($k);

    // calculating for string S
    for ($i = 0; $i < $len; $i++)
    {
        if ($k[$i] == 'a')
            $a++;

        if ($k[$i] == 'b')
            $b++;

        if ($a > $b)
        {
            $count++;
        }
    }

    // count==0 or when N==1
    if ($count == 0 || $n == 1)
    {
        echo($count);
        return 0;
    }

    // when all characters
    // are a or a-b==0
    if ($count == $len || $a - $b == 0)
    {
        echo($count * $n);
        return 0;
    }

    $n2 = $n - 1; $count2 = 0;

    // checking for saturation
    // of string after repetitive
    // addition
    while ($n2 != 0)
    {
        for ($i = 0; $i < $len; $i++)
        {
            if ($k[$i] == 'a')
                $a++;

            if ($k[$i] == 'b')
                $b++;

            if ($a > $b)
            {
                $count2++;
            }
        }

        $count += $count2;
        $n2--;

        if ($count2 == 0)
            break;

        if ($count2 == $len)
        {
            $count += ($n2 * $count2);
            break;
        }

        $count2 = 0;
    }

    return $count;
}

// Driver Code
$S = "aba";
$N = 2;
echo(prefix($S,$N)."\n");

$S = "baa";
$N = 3;
echo(prefix($S, $N)."\n");

// This code is contributed
// by Mukul Singh.
```

## java 描述语言

```
<script>
// Javascript code to count the
// prefixes with more a than b

// Function to
// count prefixes
function prefix(k,n)
{
    let a = 0, b = 0,
               count = 0;
    let i = 0;
    let len = k.length;

    // calculating for string S
    for (i = 0; i < len; i++)
    {
        if (k[i] == 'a')
            a++;

        if (k[i] == 'b')
            b++;

        if (a > b)
        {
            count++;
        }
    }

    // count==0 or when N==1
    if (count == 0 || n == 1)
    {
        document.write(count+"<br>");
        return 0;
    }

    // when all characters
    // are a or a-b==0
    if (count == len || a - b == 0)
    {
        document.write((count * n)+"<br>");
        return 0;
    }

    let n2 = n - 1, count2 = 0;

    // checking for saturation
    // of string after repetitive
    // addition
    while (n2 != 0)
    {
        for (i = 0; i < len; i++)
        {
            if (k[i] == 'a')
                a++;

            if (k[i] == 'b')
                b++;

            if (a > b)
            {
                count2++;
            }
        }

        count += count2;
        n2--;

        if (count2 == 0)
            break;

        if (count2 == len)
        {
            count += (n2 * count2);
            break;
        }

        count2 = 0;
    }

    return count;
}

// Driver Code
let S = "aba";
let N = 2;
document.write(prefix(S, N)+"<br>");

S = "baa";
N = 3;
document.write(prefix(S, N)+"<br>") ;

// This code is contributed by patel2127
</script>
```

**Output:** 

```
5
6
```