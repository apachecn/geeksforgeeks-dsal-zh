# 检查一个数字是否有两个相邻的设定位

> 原文:[https://www . geesforgeks . org/check-number-two-邻接集位/](https://www.geeksforgeeks.org/check-number-two-adjacent-set-bits/)

给定一个数，你必须检查是否有一对相邻的设置位。
**例:**

```
Input : N = 67
Output : Yes
There is a pair of adjacent set bit
The binary representation is 100011

Input : N = 5
Output : No
```

一个简单的解决方案是遍历所有位。对于每个设置的位，检查下一个位是否也被设置。
一个有效的解决方案是将数字移位 1，然后按位“与”。如果按位“与”非零，则有两个相邻的设置位。否则不行。

## C++

```
// CPP program to check
// if there are two
// adjacent set bits.
#include <iostream>
using namespace std;

bool adjacentSet(int n)
{
    return (n & (n >> 1));
}

// Driver Code
int main()
{
    int n = 3;
    adjacentSet(n) ?
     cout << "Yes" :
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if there are two
// adjacent set bits.
class GFG
{

    static boolean adjacentSet(int n)
    {
        int x = (n & (n >> 1));

        if(x > 0)
            return true;
        else
            return false;
    }

    // Driver code
    public static void main(String args[])
    {

        int n = 3;

        if(adjacentSet(n))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python 3 program to check if there
# are two adjacent set bits.

def adjacentSet(n):
    return (n & (n >> 1))

# Driver Code
if __name__ == '__main__':
    n = 3
    if (adjacentSet(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to check
// if there are two
// adjacent set bits.
using System;

class GFG
{
    static bool adjacentSet(int n)
    {
        int x = (n & (n >> 1));

        if(x > 0)
            return true;
        else
            return false;
    }

    // Driver code
    public static void Main ()
    {
        int n = 3;

        if(adjacentSet(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if there are two
// adjacent set bits.

function adjacentSet($n)
{
    return ($n & ($n >> 1));
}

// Driver Code
$n = 3;
adjacentSet($n) ?
   print("Yes") :
     print("No");

// This code is contributed by Sam007.
?>
```

## java 描述语言

```
<script>

// Javascript program to check
// if there are two
// adjacent set bits.

function adjacentSet(n)
    {
        let x = (n & (n >> 1));

        if(x > 0)
            return true;
        else
            return false;
    }

// driver program

           let n = 3;

        if(adjacentSet(n))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**输出:**

```
Yes
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。