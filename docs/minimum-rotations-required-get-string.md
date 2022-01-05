# 获得相同字符串所需的最小旋转次数

> 原文:[https://www . geesforgeks . org/minimum-rotations-required-get-string/](https://www.geeksforgeeks.org/minimum-rotations-required-get-string/)

给定一个字符串，我们需要找到获得相同字符串所需的最小旋转次数。
**例:**

```
Input : s = "geeks"
Output : 5

Input : s = "aaaa"
Output : 1
```

这个想法是基于下面的帖子。
[检查字符串是否相互旋转的程序](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)
**第一步:**初始化结果= 0(这里的结果是旋转计数)
**第二步:**取一个临时字符串等于与自身连接的原始字符串。
**步骤 3 :** 现在从第二个字符(或索引 1)开始，取与原始字符串大小相同的临时字符串的子字符串。
**第四步:**增加计数。
**第五步:**检查子串是否变得与原串相等。如果是，那么打破循环。否则转到步骤 2，从下一个索引开始重复。

## C++

```
// C++ program to determine minimum number
// of rotations required to yield same
// string.
#include <iostream>
using namespace std;

// Returns count of rotations to get the
// same string back.
int findRotations(string str)
{
    // tmp is the concatenated string.
    string tmp = str + str;
    int n = str.length();

    for (int i = 1; i <= n; i++) {

        // substring from i index of original
        // string size.
        string substring = tmp.substr(i, str.size());

        // if substring matches with original string
        // then we will come out of the loop.
        if (str == substring)
            return i;
    }
    return n;
}

// Driver code
int main()
{
    string str = "abc";
    cout << findRotations(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine minimum number
// of rotations required to yield same
// string.

import java.util.*;

class GFG
{
    // Returns count of rotations to get the
    // same string back.
    static int findRotations(String str)
    {
        // tmp is the concatenated string.
        String tmp = str + str;
        int n = str.length();

        for (int i = 1; i <= n; i++)
        {

            // substring from i index of original
            // string size.

            String substring = tmp.substring(
                      i, i+str.length());

            // if substring matches with original string
            // then we will come out of the loop.
            if (str.equals(substring))
                return i;
        }
        return n;
    }

    // Driver Method
    public static void main(String[] args)
    {
            String str = "aaaa";
        System.out.println(findRotations(str));
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python 3 program to determine minimum
# number of rotations required to yield
# same string.

# Returns count of rotations to get the
# same string back.
def findRotations(str):

    # tmp is the concatenated string.
    tmp = str + str
    n = len(str)

    for i in range(1, n + 1):

        # substring from i index of
        # original string size.
        substring = tmp[i: i+n]

        # if substring matches with
        # original string then we will
        # come out of the loop.
        if (str == substring):
            return i
    return n

# Driver code
if __name__ == '__main__':

    str = "abc"
    print(findRotations(str))

# This code is contributed
# by 29AjayKumar.
```

## C#

```
// C# program to determine minimum number
// of rotations required to yield same
// string.
using System;

class GFG {

    // Returns count of rotations to get
    // the same string back.
    static int findRotations(String str)
    {

        // tmp is the concatenated string.
        String tmp = str + str;
        int n = str.Length;

        for (int i = 1; i <= n; i++)
        {

            // substring from i index of
            // original string size.

            String substring =
                 tmp.Substring(i, str.Length);

            // if substring matches with
            // original string then we will
            // come out of the loop.
            if (str == substring)
                return i;
        }

        return n;
    }

    // Driver Method
    public static void Main()
    {
        String str = "abc";

        Console.Write(findRotations(str));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to determine minimum
// number of rotations required to
// yield same string.

// Returns count of rotations
// to get the same string back.
function findRotations($str)
{
    // tmp is the concatenated string.
    $tmp = ($str + $str);
    $n = strlen($str);

    for ( $i = 1; $i <= $n; $i++)
    {

        // substring from i index
        // of original string size.
        $substring = $tmp.substr($i,
                          strlen($str));

        // if substring matches with
        // original string then we will
        // come out of the loop.
        if ($str == $substring)
            return $i;
    }
    return $n;
}

// Driver code
$str = "abc";
echo findRotations($str), "\n";

// This code is contributed
// by Sachin
?>
```

## java 描述语言

```
<script>
// javascript program to determine minimum number
// of rotations required to yield same
// string.

    // Returns count of rotations to get the
    // same string back.
    function findRotations( str) {
        // tmp is the concatenated string.
        var tmp = str + str;
        var n = str.length;

        for (var i = 1; i <= n; i++) {

            // substring from i index of original
            // string size.

            var substring = tmp.substring(i ,str.length);

            // if substring matches with original string
            // then we will come out of the loop.
            if (str===(substring))
                return i;
        }
        return n;
    }

    // Driver Method

        var str = "abc";
        document.write(findRotations(str));

// This code contributed by gauravrajput1
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n <sup>2</sup>

**空间复杂度:** O(2n) ~ O(n)

我们可以在不使用任何临时变量作为额外空间的情况下解决这个问题。我们将遍历原始字符串，并在每个位置对其进行分割，连接右子字符串和左子字符串，并检查它是否等于原始字符串

## C++

```
// C++ program to determine minimum number
// of rotations required to yield same
// string.
#include <iostream>
using namespace std;

// Returns count of rotations to get the
// same string back.
int findRotations(string str)
{
    int ans = 0; //to store the answer
      int n = str.length(); //length of the string

      //All the length where we can partition
      for(int i=1;i<str.length()-1;i++)
    {
          //right part + left part = rotated string
          // we are checking weather the rotated string is equal to
        //original string
          if(str.substr(i,n-i) + str.substr(0,i)  == str)
        {
             ans = i;
              break;
        }
    }
      if(ans == 0)
      return n;
      return ans;
}

// Driver code
int main()
{
    string str = "abc";
    cout << findRotations(str) << endl;
    return 0;
}
```

**Output**

```
3

```

**时间复杂度:** O(n <sup>2</sup>

**空间复杂度:** O(1)

**Python 中的替代实现:**

## 蟒蛇 3

```
# Python 3 program to determine minimum
# number of rotations required to yield
# same string.

# input
string = 'aaaa'
check = ''

for r in range(1, len(string)+1):
  # checking the input after each rotation
  check = string[r:] + string[:r]

  # following if statement checks if input is
  # equals to check , if yes it will print r and
  # break out of the loop
  if check == string:
    print(r)
    break

# This code is contributed
# by nagasowmyanarayanan.
```

**输出:**

```
1
```

本文由 **Jatin Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。