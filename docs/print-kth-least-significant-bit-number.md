# 打印数字的第 K 个最低有效位

> 原文:[https://www . geesforgeks . org/print-kth-最低有效位数/](https://www.geeksforgeeks.org/print-kth-least-significant-bit-number/)

给出了一个数字 N。我们需要打印它的第 K 个[最低有效位](https://en.wikipedia.org/wiki/Least_significant_bit)。
**例:**

```
Input : num = 10, k = 4 
Output : 1
Explanation : Binary Representation 
of 10 is 1010\. 4th LSB is 1.

Input : num = 16, k = 3
Output : 0
Explanation : Binary Representation 
of 16 is 10000\. 3rd LSB is 0.
```

我们可以通过以下步骤轻松解决这个问题:

1.  向左移动数字“1”(K-1)次。
2.  这将产生一个除第 K 位之外的所有未设置位的数字。现在，我们将对给定的移位数进行逻辑与运算。
3.  除了第 K 位以外的所有位都将产生 0，第 K 位将取决于数字。这是因为，1 和 1 是 1。0 和 1 是 0。

## C++

```
// CPP code to print 'K'th LSB
#include <bits/stdc++.h>
using namespace std;

//Function returns 1 if set, 0 if not
bool LSB(int num, int K)
{
    return (num & (1 << (K-1)));
}

//Driver code
int main()
{
    int num = 10, K = 4;

    //Function call
    cout << LSB(num, K);

    return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// java code to print 'K'th LSB
import java .io.*;

class GFG {

    // Function returns 1 if set, 0 if not
    static boolean LSB(int num, int K)
    {
        boolean x = (num & (1 << (K-1))) != 0;
        return (x);
    }

    // Driver code
     public static void main(String[] args)
    {
        int num = 10, K = 4;

        //Function call
        if(LSB(num, K))
            System.out.println("1") ;

        else
            System.out.println("0");
    }
}

// This code is contributed by Anuj_67
```

## 计算机编程语言

```
# Python code to print 'K'th LSB

# Function returns 1 if set, 0 if not
def LSB(num, K):
    return bool(num & (1 << (K - 1) ))

# Driver code
num, k = 10, 4

res = LSB(num, k)
if res :
    print 1
else:
    print 0

#This code is contributed by Sachin Bisht
```

## C#

```
// C# code to print 'K'th LSB
using System;

class GFG {

    // Function returns 1 if set, 0 if not
    static bool LSB(int num, int K)
    {
        bool x = (num & (1 << (K-1))) != 0;
        return (x);
    }

    // Driver code
    static void Main()
    {
        int num = 10, K = 4;

        //Function call
        if(LSB(num, K))
            Console.Write("1") ;

        else
            Console.Write("0");
    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP code to print 'K'th LSB

// Function returns 1 if set, 0 if not
function LSB($num, $K)
{
    return ($num & (1 << ($K - 1)));
}

// Driver code
$num = 10;
$K = 4;

$r = LSB($num, $K);
if($r)
    echo '1';
else
    echo '0';

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
    // Javascript code to print 'K'th LSB

    // Function returns 1 if set, 0 if not
    function LSB(num, K)
    {
        let x = (num & (1 << (K-1))) != 0;
        return (x);
    }

    let num = 10, K = 4;

    //Function call
    if(LSB(num, K))
      document.write("1") ;

    else
      document.write("0");

</script>
```

**输出:**

```
1
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。