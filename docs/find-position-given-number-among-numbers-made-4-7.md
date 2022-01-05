# 在由 4 和 7 组成的数字中找到给定数字的位置

> 原文:[https://www . geesforgeks . org/find-position-给定-number-in-made-4-7/](https://www.geeksforgeeks.org/find-position-given-number-among-numbers-made-4-7/)

考虑一系列仅由数字 4 和 7 组成的数字。数列的前几个数字是 4，7，44，47，74，77，444，..等等。给定一个仅由 4，7 位数字构成的数，我们需要找到这个数在这个数列中的位置。
示例:

```
Input : 7
Output : pos = 2 

Input : 444
Output : pos = 7
```

与以下文章相反:
[求数列中只允许有 2 位(4 和 7)的第 n 个元素|集合 2 (log(n)方法)](https://www.geeksforgeeks.org/find-n-th-element-series-2-digits-4-7-allowed-set-2-logn-method/)

```
                      ""
               /              \
             1(4)            2(7)
          /        \       /      \ 
        3(44)    4(47)   5(74)    6(77)
       / \       / \      / \      / \
```

这个想法是基于这样一个事实，即所有偶数位置的数字都有 7 作为最后一个数字，所有奇数位置的数字都有 4 作为最后一个数字。
如果数字是 4，那么它是树的左节点，那么它对应于(pos*2)+1。否则右子节点(7)对应于(位置*2)+2。

## C++

```
// C++ program to find position of a number
// in a series of numbers with 4 and 7 as the
// only digits.
#include <iostream>
#include <algorithm>
using namespace std;

int findpos(string n)
{
    int i = 0, pos = 0;
    while (n[i] != '\0') {

        // check all digit position
        switch (n[i])
        {

        // if number is left then pos*2+1
        case '4':
            pos = pos * 2 + 1;
            break;

        // if number is right then pos*2+2
        case '7':
            pos = pos * 2 + 2;
            break;
        }
        i++;
    }
    return pos;
}

// Driver code
int main()
{
    // given a number which is constructed
    // by 4 and 7 digit only
    string n = "774";
    cout << findpos(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find position of a number
// in a series of numbers with 4 and 7 as the
// only digits.
import java.util.*;

class GFG {

    static int findpos(String n)
    {

        int k = 0, pos = 0, i = 0;
        while (k != n.length()) {

            // check all digit position
            switch (n.charAt(i)) {

            // if number is left then pos*2+1
            case '4':
                pos = pos * 2 + 1;
                break;

            // if number is right then pos*2+2
            case '7':
                pos = pos * 2 + 2;
                break;
            }

            i++;
            k++;
        }

        return pos;
    }

    // Driver code
    public static void main(String[] args)
    {

        // given a number which is constructed
        // by 4 and 7 digit only
        String n = "774";

        System.out.println(findpos(n));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# python program to find position
# of a number in a series of
# numbers with 4 and 7 as the
# only digits.
def findpos(n):
    i = 0
    j = len(n)
    pos = 0
    while (i<j):

        # check all digit position
        # if number is left then
        # pos*2+1
        if(n[i] == '4'):
            pos = pos * 2 + 1

        # if number is right then
        # pos*2+2
        if(n[i] == '7'):
            pos = pos * 2 + 2

        i= i+1

    return pos

# Driver code
# given a number which is constructed
# by 4 and 7 digit only
n = "774"
print(findpos(n))

# This code is contributed by Sam007
```

## C#

```
// C# program to find position of
// a number in a series of numbers
// with 4 and 7 as the only digits.
using System;

class GFG
{
    static int findpos(String n)
    {

        int k = 0, pos = 0, i = 0;
        while (k != n.Length) {

            // check all digit position
            switch (n[i]) {

            // if number is left then pos*2+1
            case '4':
                pos = pos * 2 + 1;
                break;

            // if number is right then pos*2+2
            case '7':
                pos = pos * 2 + 2;
                break;
            }

            i++;
            k++;
        }

        return pos;
    }

    // Driver code
    static void Main()
    {

        // given a number which is constructed
        // by 4 and 7 digit only
        String n = "774";

        Console.Write(findpos(n));
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find position of a number
// in a series of numbers with 4 and 7 as the
// only digits.

function findpos($n)
{
    $i = 0;
    $pos = 0;
    while($i < strlen($n)) {

        // check all digit position
        switch ($n[$i])
        {

        // if number is left then pos*2+1
        case '4':
            $pos = $pos * 2 + 1;
            break;

        // if number is right then pos*2+2
        case '7':
            $pos = $pos * 2 + 2;
            break;
        }
        $i++;
    }
    return $pos;
}

    // Driver code
    // given a number which
    // is constructed by 4
    // and 7 digit only
    $n = "774";
    echo findpos($n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to find position of a number
// in a series of numbers with 4 and 7 as the
// only digits.

function findpos(n)
{
    let i = 0;
    let pos = 0;
    while(i < n.length) {

        // check all digit position
        switch (n[i])
        {

        // if number is left then pos*2+1
        case '4':
            pos = pos * 2 + 1;
            break;

        // if number is right then pos*2+2
        case '7':
            pos = pos * 2 + 2;
            break;
        }
        i++;
    }
    return pos;
}

    // Driver code
    // given a number which
    // is constructed by 4
    // and 7 digit only
    let n = "774";
    document.write(findpos(n));

// This code is contributed by _saurabh_jaiswal
</script>
```

输出:

```
13
```

本文由**德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。