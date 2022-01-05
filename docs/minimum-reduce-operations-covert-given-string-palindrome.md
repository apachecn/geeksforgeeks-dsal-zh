# 将给定字符串转换为回文的最小化运算

> 原文:[https://www . geesforgeks . org/minimum-reduce-operations-secret-给定字符串-回文/](https://www.geeksforgeeks.org/minimum-reduce-operations-covert-given-string-palindrome/)

给定一个字符串，找出将一个给定的字符串转换成回文所需的最小化操作数。在缩减操作中，我们可以将字符更改为一个更小的值。例如 b 可以覆盖到 a.
**例如:**

```
Input  :  abcd  
Output :  4
We need to reduce c once
and d three times.

Input  : ccc
Output : 0
```

想法很简单。我们从左开始遍历字符串，并将左半部分的字符与右半部分的相应字符进行比较。我们将字符之间的差异添加到结果中。

## C++

```
// CPP program to count minimum reduce
// operations to make a palindrome
#include <bits/stdc++.h>
using namespace std;

// Returns count of minimum character
// reduce operations to make palindrome.
int countReduce(string& str)
{
    int n = str.length();
    int res = 0;

    // Compare every character of first half
    // with the corresponding character of
    // second half and add difference to
    // result.
    for (int i = 0; i < n / 2; i++)
        res += abs(str[i] - str[n - i - 1]);

    return res;
}

// Driver code
int main()
{
    string str = "abcd";
    cout << countReduce(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum reduce
// operations to make a palindrome
import java.io.*;

class GFG
{
    // Returns count of minimum character
    // reduce operations to make palindrome.
    static int countReduce(String str)
    {
        int n = str.length();
        int res = 0;

        // Compare every character of first half
        // with the corresponding character of
        // second half and add difference to
        // result.
        for (int i = 0; i < n / 2; i++)
            res += Math.abs(str.charAt(i)
                   - str.charAt(n - i - 1));

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "abcd";
        System.out.println( countReduce(str));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# python3 program to count minimum reduce
# operations to make a palindrome

# Returns count of minimum character
# reduce operations to make palindrome.
def countReduce(str):

    n = len(str)
    res = 0

    # Compare every character of first half
    # with the corresponding character of
    # second half and add difference to
    # result.
    for i in range(0, int(n/2)):
        res += abs( int(ord(str[i])) -
               int(ord(str[n - i - 1])) )

    return res

# Driver code
str = "abcd"
print(countReduce(str))

# This code is contributed by Sam007
```

## C#

```
// C# program to count minimum reduce
// operations to make a palindrome
using System;

class GFG {

    // Returns count of minimum character
    // reduce operations to make palindrome.
    static int countReduce(string str)
    {
        int n = str.Length;
        int res = 0;

        // Compare every character of first
        // half with the corresponding
        // character of second half and
        // add difference to result.
        for (int i = 0; i < n / 2; i++)
            res += Math.Abs(str[i]
                    - str[n - i - 1]);

        return res;
    }

    // Driver code
    public static void Main ()
    {
        string str = "abcd";
        Console.WriteLine( countReduce(str));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count minimum
// reduce operations to make a
// palindrome

// Returns count of minimum
// character reduce operations
// to make palindrome.
function countReduce($str)
{
    $n = strlen($str);
    $res = 0;

    // Compare every character
    // of first half with the
    // corresponding character
    // of second half and add
    // difference to result.
    for ($i = 0; $i < $n / 2; $i++)
        $res += abs(ord($str[$i]) -
                    ord($str[($n - $i - 1)]));
    return $res;
}

// Driver code
$str = "abcd";
echo countReduce($str);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to count minimum reduce
    // operations to make a palindrome

    // Returns count of minimum character
    // reduce operations to make palindrome.
    function countReduce(str)
    {
        let n = str.length;
        let res = 0;

        // Compare every character of first
        // half with the corresponding
        // character of second half and
        // add difference to result.
        for (let i = 0; i < parseInt(n / 2, 10); i++)
            res += Math.abs(str[i].charCodeAt() - str[n - i - 1].charCodeAt());

        return res;
    }

      let str = "abcd";
      document.write(countReduce(str));

</script>
```

**输出:**

```
4
```

本文由 [**萨希尔·斯里瓦斯塔瓦**](https://auth.geeksforgeeks.org/profile.php?user=Sahil Srivastava) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。