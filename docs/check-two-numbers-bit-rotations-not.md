# 检查两个数是否为彼此的位旋转

> 原文:[https://www . geesforgeks . org/check-两位数-位旋转-not/](https://www.geeksforgeeks.org/check-two-numbers-bit-rotations-not/)

给定两个正整数 x 和 y，检查一个整数是否是通过旋转另一个整数的位获得的。

```
Input constraint: 0 < x, y < 2^32 
```

**位旋转:**旋转(或循环移位)是一种类似移位的操作，只是一端脱落的位放回另一端。
关于钻头旋转的更多信息可在此处
**中找到示例 1 :**

```
Input : a = 8, b = 1
Output : yes

Explanation :
Representation of a = 8 : 0000 0000 0000 0000 0000 0000 0000 1000
Representation of b = 1 : 0000 0000 0000 0000 0000 0000 0000 0001
If we rotate a by 3 units right we get b, hence answer is yes
```

**例 2 :**

```
Input : a = 122, b = 2147483678
Output : yes

Explanation :
Representation of a = 122        : 0000 0000 0000 0000 0000 0000 0111 1010
Representation of b = 2147483678 : 1000 0000 0000 0000 0000 0000 0001 1110
If we rotate a by 2 units right we get b, hence answer is yes
```

由于 x 或 y 可以表示的总位数是 32，因为 x，y > 0 和 x，y < 2^32. 
所以我们需要找到 x 的所有 32 个可能的旋转，并与 y 进行比较，直到 x 和 y 不相等。
为此，我们使用一个 64 位的临时变量 x64，它是 x 到 x ie 连接的结果..
x64 的前 32 位与 x 的位相同，后 32 位也与 x64 的位相同。
然后我们继续在右侧将 x64 移位 1，并将 x64 最右边的 32 位与 y 进行比较。
这样，我们将能够获得由于旋转而产生的所有可能的位组合。
以上算法实现如下。

## C++

```
// C++ program to check if two numbers are bit rotations
// of each other.
#include <iostream>
using namespace std;

// function to check if  two numbers are equal
// after bit rotation
bool isRotation(unsigned int x, unsigned int y)
{
    // x64 has concatenation of x with itself.
    unsigned long long int x64 = x | ((unsigned long long int)x << 32);

    while (x64 >= y)
    {
        // comparing only last 32 bits
        if (unsigned(x64) == y)
            return true;

        // right shift by 1 unit
        x64 >>= 1;
    }
    return false;
}

// driver code to test above function
int main()
{
    unsigned int x = 122;
    unsigned int y = 2147483678;

    if (isRotation(x, y))
        cout << "yes" << endl;
    else
        cout << "no" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two numbers are bit rotations
// of each other.
class GFG {

// function to check if two numbers are equal
// after bit rotation
    static boolean isRotation(long x, long y) {
        // x64 has concatenation of x with itself.
        long x64 = x | (x << 32);

        while (x64 >= y) {
            // comparing only last 32 bits
            if (x64 == y) {
                return true;
            }

            // right shift by 1 unit
            x64 >>= 1;
        }
        return false;
    }

// driver code to test above function
    public static void main(String[] args) {
        long x = 122;
        long y = 2147483678L;

        if (isRotation(x, y) == false) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if two
# numbers are bit rotations of each other.

# function to check if two numbers
# are equal after bit rotation
def isRotation(x, y) :

    # x64 has concatenation of x
    # with itself.
    x64 = x | (x << 32)

    while (x64 >= y) :

        # comparing only last 32 bits
        if ((x64) == y) :
            return True

        # right shift by 1 unit
        x64 >>= 1

    return False

# Driver Code
if __name__ == "__main__" :

    x = 122
    y = 2147483678

    if (isRotation(x, y) == False) :
        print("yes")
    else :
        print("no")

# This code is contributed by Ryuga
```

## C#

```
// C# program to check if two numbers
// are bit rotations of each other.
using System;

class GFG
{

// function to check if two numbers
// are equal after bit rotation
static bool isRotation(long x, long y)
{
    // x64 has concatenation of
    // x with itself.
    long x64 = x | (x << 32);

    while (x64 >= y)
    {
        // comparing only last 32 bits
        if (x64 == y)
        {
            return true;
        }

        // right shift by 1 unit
        x64 >>= 1;
    }
    return false;
}

// Driver Code
public static void Main()
{
    long x = 122;
    long y = 2147483678L;

    if (isRotation(x, y) == false)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if two
// numbers are bit rotations of
// each other.

// function to check if two
// numbers are equal after
// bit rotation
function isRotation($x, $y)
{
    // x64 has concatenation
    // of x with itself.
    $x64 = $x | ($x << 32);

    while ($x64 >= $y)
    {
        // comparing only last 32 bits
        if (($x64) == $y)
            return 1;

        // right shift by 1 unit
        $x64 >>= 1;
    }
    return -1;
}

// Driver Code
$x = 122;
$y = 2147483678;

if (isRotation($x, $y))
    echo "yes" ,"\n";
else
    echo "no" ,"\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// javascript program to check if two numbers are bit rotations
// of each other.

// function to check if two numbers are equal
// after bit rotation
function isRotation(x, y)
{

    // x64 has concatenation of x with itself.
    var x64 = x | (x << 32);
    while (x64 >= y)
    {

        // comparing only last 32 bits
        if (x64 == y) {
            return true;
        }

        // right shift by 1 unit
        x64 >>= 1;
    }
    return false;
}

// driver code to test above function
var x = 122;
var y = 2147483678;

if (isRotation(x, y) == false) {
    document.write("Yes");
} else {
    document.write("No");
}

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
yes
```

本文由 [**普拉蒂克·查哈尔**](https://pratik-chhajer.github.io/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。