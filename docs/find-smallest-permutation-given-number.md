# 求给定数的最小排列

> 原文:[https://www . geesforgeks . org/find-最小排列-给定数字/](https://www.geeksforgeeks.org/find-smallest-permutation-given-number/)

给定一个长整数，返回该数的最小(幅度)整数排列。
**例** :

```
Input : 5468001
Output : 1004568

Input : 5341
Output : 1345
```

**问题来源:** [GE 数字面试体验|第 6 集](https://www.geeksforgeeks.org/ge-digital-interview-experience-set-6/)
我们已经在下方帖子里讨论了解决方案。
[通过重新排列给定数字](https://www.geeksforgeeks.org/smallest-number-rearranging-digits-given-number/)
的数字来最小化数字在这篇文章中，讨论了一种不同的方法。
**处理方法:**由于数字很长，将数字存储为字符串，对字符串进行排序，如果没有前导零，则返回该字符串，如果有前导零，则用字符串的第一个非零元素交换字符串的第一个元素，并返回该字符串。
以下是上述方法的实施:

## C++

```
// CPP program to find smallest
// permutation of given number
#include <bits/stdc++.h>
using namespace std;

// return the smallest number permutation
string findSmallestPermutation(string s)
{
    int len = s.length();

    // sort the string
    sort(s.begin(), s.end());

    // check for leading zero in string
    // if there are any leading zeroes,
    // swap the first zero with first non-zero number
    int i = 0;
    while (s[i] == '0')
        i++;

    swap(s[0], s[i]);
    return s;
}

// driver program
int main()
{
    // take number input in string
    string s = "5468001";
    string res = findSmallestPermutation(s);
    cout << res << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest
// permutation of given number
import java.util.Arrays;

public class GFG {

    // return the smallest number permutation
    static char[] findSmallestPermutation(String s1)
    {
        // sort the string
        char s[] = s1.toCharArray();
        Arrays.sort(s);

        // check for leading zero in string
        // if there are any leading zeroes,
        // swap the first zero with first non-zero
        // number
        int i = 0;
        while (s[i] == '0')
            i++;

        char temp = s[0];
        s[0] = s[i];
        s[i] = temp;
        return s;
    }

    // driver program
    public static void main(String args[])
    {
        // take number input in string
        String s = "5468001";
        char res[] = findSmallestPermutation(s);
        System.out.println(res);
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to find smallest
# permutation of given number

# Sort function
def sort_string(a):
    return ''.join(sorted(a))

# return the smallest number permutation
def findSmallestPermutation(s):

    # sort the string
    s = sort_string(s)

    # check for leading zero in string
    # if there are any leading zeroes,
    # swap the first zero with first non-zero number
    i = 0
    while (s[i] == '0'):
        i += 1
    a = list(s)
    temp = a[0]
    a[0] = a[i]
    a[i] = temp
    s = "".join(a)
    return s

# driver program

# take number input in string
s = "5468001"
res = findSmallestPermutation(s)
print res

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find smallest
// permutation of given number
using System;

public class GFG {

    // return the smallest number permutation
    static char[] findSmallestPermutation(string s1)
    {

        // sort the string
        char []s = s1.ToCharArray();;
        Array.Sort(s);

        // check for leading zero in string
        // if there are any leading zeroes,
        // swap the first zero with first non-zero
        // number
        int i = 0;
        while (s[i] == '0')
            i++;

        char temp = s[0];
        s[0] = s[i];
        s[i] = temp;
        return s;
    }

    // driver program
    public static void Main()
    {

        // take number input in string
        string s = "5468001";

        char []res = findSmallestPermutation(s);
        Console.WriteLine(res);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest
// permutation of given number

// return the smallest
// number permutation
function findSmallestPermutation($s)
{
    $len = strlen($s);
    $s = str_split($s);

    // sort the string
    sort($s);

    // check for leading zero
    // in string if there are
    // any leading zeroes,
    // swap the first zero with
    // first non-zero number
    $i = 0;
    while ($s[$i] == '0')
        $i++;

    $tmp = $s[0];
    $s[0] = $s[$i];
    $s[$i] = $tmp;
    $s=implode("", $s);
    return $s;
}

// Driver Code

// take number
// input in string
$s = "5468001";
$res = findSmallestPermutation($s);
echo $res;

// This code is contributed
// by mits.
?>
```

## java 描述语言

```
// Javascript program to find smallest
// permutation of given number

// return the smallest
// number permutation
function findSmallestPermutation(s)
{
    let len = s.length;
    s = s.split("");

    // sort the string
    s = s.sort();

    // check for leading zero
    // in string if there are
    // any leading zeroes,
    // swap the first zero with
    // first non-zero number
    let i = 0;
    while (s[i] == '0')
        i++;

    let tmp = s[0];
    s[0] = s[i];
    s[i] = tmp;
    s=  s.join("");
    return s;
}

// Driver Code

// take number
// input in string
let s = "5468001";
let res = findSmallestPermutation(s);
document.write(res);

// This code is contributed
// by _saurabh_jaiswal
```

**输出:**

```
1004568
```

**优化:**
由于字符集有限(' 0 '到' 9 ')，我们可以编写自己的排序方法，在线性时间内工作(通过统计所有字符的频率)
本文由 [**曼德普·辛格**](https://github.com/msdeep14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。