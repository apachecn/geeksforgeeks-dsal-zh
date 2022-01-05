# 最接近的(或下一个)较小和较大的数字，具有相同的设置位数

> 原文:[https://www . geesforgeks . org/closer-next-small-great-numbers-number-set-bits/](https://www.geeksforgeeks.org/closest-next-smaller-greater-numbers-number-set-bits/)

给定一个正整数 n，打印下一个最小的数和前一个最大的数，这两个数在二进制表示中的位数相同。

**示例:**

```
Input : n = 5
Output : Closest Greater = 6
         Closest Smaller = 3
Note that 5, 6 and 3 have same number of 
set bits. 

Input : n = 11
Output : Closest Greater = 13
         Closest Smaller = 7 
```

**蛮力法**
一个简单的方法就是简单的蛮力:在 n 中数 1 的个数，然后递增(或递减)直到我们找到一个和 1 个数相同的数。
**【最佳方法】**
让我们从 getNext 的代码开始，然后进入 getPrev。
**获取下一个数字的位操作方法**
如果我们思考下一个数字应该是什么，我们可以观察到以下情况。给定数字 13948，二进制表示如下:

```
1   1   0   1   1  0  0  1  1  1  1  1  0  0
13  12  11  10  9  8  7  6  5  4  3  2  1  0
```

我们想让这个数字更大(但不要太大)。我们还需要保持相同数量的 1。
观察:给定一个数字 n 和两个比特位置 I 和 j，假设我们把比特 I 从 1 翻转到 0，比特 j 从 0 翻转到 1。如果我> j，那么 n 就会减少。如果我< j，那么 n 就会增加。

**我们知道如下:**

*   如果我们把 0 翻转到 1，我们必须把 1 翻转到 0。
*   当且仅当 0 到 1 位在 1 到 0 位的左边时，该数字(在两次翻转后)会更大。
*   我们想让这个数字更大，但不是不必要的更大。因此，我们需要翻转最右边的零，它的右边有一个。

换句话说，我们翻转最右边的非尾随零。也就是说，使用上面的例子，尾随零在第 0 和第 1 点。最右边的非尾随零在 7。让我们称这个位置为 p。

```
p ==> Position of rightmost non-trailing 0.
```

**第一步:翻转最右边的非尾随零**

```
1    1   0   1  1  0  1  1  1  1  1  1  0  0
13  12  11  10  9  8  7  6  5  4  3  2  1  0
```

通过这种改变，我们增加了 n 的 1 的数量。我们可以通过重新排列 p 位右边的所有位来缩小这个数量，使得 0 在左边，1 在右边。当我们这样做的时候，我们想用 0 替换 1 中的一个。
一个相对简单的方法是计算 p 右边有多少个 1，清除从 0 到 p 的所有位，然后将它们加回 c1-1 个 1。假设 c1 是 p 右边的 1 的数量，c0 是 p 右边的 0 的数量
让我们通过一个例子来了解一下。

```
c1 ==> Number of ones to the right of p
c0 ==> Number of zeros to the right of p.
p = c0 + c1
```

**第二步:清除 p 右边的位，从之前开始，c0 = 2。c1 = 5。p = 7。**

```
1    1   0   1  1  0  1  0  0  0  0  0  0  0
13  12  11  10  9  8  7  6  5  4  3  2  1  0
```

为了清除这些位，我们需要创建一个掩码，它是一个 1 序列，后跟 p 个 0。我们可以这样做:

```
// all zeros except for a 1 at position p.
a = 1 << p; 

// all zeros, followed by p ones.
b = a - 1;                       

// all ones, followed by p zeros.
mask = ~b;                       

// clears rightmost p bits.
n = n & mask;                

Or, more concisely, we do:
n &= ~((1 << p) - 1).
```

**第三步:加一个 C1–1 一。**

```
1   1   0   1   1  0  1  0  0  0  1  1  1  1
13  12  11  10  9  8  7  6  5  4  3  2  1  0
```

要在右侧插入 C1–1，我们需要执行以下操作:

```
// 0s with a 1 at position c1– 1
a = 1 << (c1 - 1);    

// 0s with 1s at positions 0 through c1-1
b = a - 1;                

// inserts 1s at positions 0 through c1-1
n = n | b;                

Or, more concisely:
n | = (1 << (c1 - 1)) - 1;  
```

我们现在已经得到了最小的数，在相同的数下大于 n。getNext 的代码实现如下。

## C++

```
// C++ implementation of  getNext with
// same number of bits 1's is below
#include <bits/stdc++.h>
using namespace std;

// Main Function to find next smallest
// number bigger than n
int getNext(int n)
{
    /* Compute c0 and c1 */
    int c = n;
    int c0 = 0;
    int c1 = 0;

    while (((c & 1) == 0) && (c != 0))
    {
        c0 ++;
        c >>= 1;
    }
    while ((c & 1)==1)
    {
        c1++;
        c >>= 1;
    }

    // If there is no bigger number with the
    // same no. of 1's
    if (c0 +c1 == 31 || c0 +c1== 0)
        return -1;

    // position of rightmost non-trailing zero
    int p = c0 + c1;

    // Flip rightmost non-trailing zero
    n |= (1 << p);

    // Clear all bits to the right of p
    n &= ~((1 << p) - 1);

    // Insert (c1-1) ones on the right.
    n |= (1 << (c1 - 1)) - 1;

    return n;
}

// Driver Code
int main()
{
    int n = 5;   // input 1
    cout << getNext(n) << endl;

    n = 8;     // input 2
    cout << getNext(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// getNext with same number
// of bits 1's is below
import java.io.*;

class GFG
{

    // Main Function to find next
    // smallest number bigger than n
    static int getNext(int n)
    {

        /* Compute c0 and c1 */
        int c = n;
        int c0 = 0;
        int c1 = 0;

        while (((c & 1) == 0) &&
                (c != 0))
        {
            c0++;
            c >>= 1;
        }
        while ((c & 1) == 1)
        {
            c1++;
            c >>= 1;
        }

        // If there is no bigger number
        // with the same no. of 1's
        if (c0 + c1 == 31 ||
            c0 + c1 == 0)
            return -1;

        // position of rightmost
        // non-trailing zero
        int p = c0 + c1;

        // Flip rightmost
        // non-trailing zero
        n |= (1 << p);

        // Clear all bits 
        // to the right of p
        n &= ~((1 << p) - 1);

        // Insert (c1-1) ones
        // on the right.
        n |= (1 << (c1 - 1)) - 1;

        return n;
    }

    // Driver Code
    public static void main (String[] args)
    {

        int n = 5; // input 1
        System.out.println(getNext(n));

        n = 8; // input 2
        System.out.println(getNext(n));
    }
}

// This code is contributed by aj_36
```

## 蟒蛇 3

```
# Python 3 implementation of getNext with
# same number of bits 1's is below

# Main Function to find next smallest
# number bigger than n
def getNext(n):

    # Compute c0 and c1
    c = n
    c0 = 0
    c1 = 0

    while (((c & 1) == 0) and (c != 0)):
        c0 += 1
        c >>= 1

    while ((c & 1) == 1):
        c1 += 1
        c >>= 1

    # If there is no bigger number with
    # the same no. of 1's
    if (c0 + c1 == 31 or c0 + c1== 0):
        return -1

    # position of rightmost non-trailing zero
    p = c0 + c1

    # Flip rightmost non-trailing zero
    n |= (1 << p)

    # Clear all bits to the right of p
    n &= ~((1 << p) - 1)

    # Insert (c1-1) ones on the right.
    n |= (1 << (c1 - 1)) - 1

    return n

# Driver Code
if __name__ == "__main__":

    n = 5 # input 1
    print(getNext(n))

    n = 8     # input 2
    print(getNext(n))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of getNext with
// same number of bits 1's is below
using System;

class GFG {

    // Main Function to find next
    // smallest number bigger than n
    static int getNext(int n)
    {

        /* Compute c0 and c1 */
        int c = n;
        int c0 = 0;
        int c1 = 0;

        while (((c & 1) == 0) && (c != 0))
        {
            c0++;
            c >>= 1;
        }
        while ((c & 1) == 1)
        {
            c1++;
            c >>= 1;
        }

        // If there is no bigger number
        // with the same no. of 1's
        if (c0 + c1 == 31 || c0 + c1== 0)
            return -1;

        // position of rightmost
        // non-trailing zero
        int p = c0 + c1;

        // Flip rightmost non-trailing
        // zero
        n |= (1 << p);

        // Clear all bits to the right
        // of p
        n &= ~((1 << p) - 1);

        // Insert (c1-1) ones on the
        // right.
        n |= (1 << (c1 - 1)) - 1;

        return n;
    }

    // Driver Code
    static void Main()
    {
        int n = 5; // input 1
        Console.WriteLine(getNext(n));

        n = 8; // input 2
        Console.Write(getNext(n));

    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of getNext with
// same number of bits 1's is below

// Function to find next smallest
// number bigger than n
function getNext($n)
{

    // Compute c0 and c1
    $c = $n;
    $c0 = 0;
    $c1 = 0;

    while ((($c & 1) == 0) &&
                   ($c != 0))
    {
        $c0 ++;
        $c >>= 1;
    }
    while (($c & 1) == 1)
    {
        $c1++;
        $c >>= 1;
    }

    // If there is no bigger
    // number with the
    // same no. of 1's
    if ($c0 + $c1 == 31 ||
        $c0 + $c1== 0)
        return -1;

    // position of rightmost
    // non-trailing zero
    $p = $c0 + $c1;

    // Flip rightmost non -
    // trailing zero
    $n |= (1 << $p);

    // Clear all bits to
    // the right of p
    $n &= ~((1 << $p) - 1);

    // Insert (c1-1) ones
    // on the right.
    $n |= (1 << ($c1 - 1)) - 1;

    return $n;
}

    // Driver Code
    // input 1
    $n = 5;
    echo getNext($n),"\n";

    // input 2
    $n = 8;
    echo getNext($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    function getNext(n)
    {
        /* Compute c0 and c1 */
        let c = n;
        let c0 = 0;
        let c1 = 0;

        while (((c & 1) == 0) &&
                (c != 0))
        {
            c0++;
            c >>= 1;
        }
        while ((c & 1) == 1)
        {
            c1++;
            c >>= 1;
        }

        // If there is no bigger number
        // with the same no. of 1's
        if (c0 + c1 == 31 ||
            c0 + c1 == 0)
            return -1;

        // position of rightmost
        // non-trailing zero
        let p = c0 + c1;

        // Flip rightmost
        // non-trailing zero
        n |= (1 << p);

        // Clear all bits 
        // to the right of p
        n &= ~((1 << p) - 1);

        // Insert (c1-1) ones
        // on the right.
        n |= (1 << (c1 - 1)) - 1;

        return n;
    }

    let  n = 5; // input 1
    document.write(getNext(n)+"<br>");

    n = 8; // input 2
    document.write(getNext(n));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
6
16
```

**获取先前编号的最佳位操作方法**
为了实现 getPrev，我们遵循非常相似的方法。

*   计算 c0 和 c1。注意 **c1** 是尾随 1 的数量， **c0** 是紧跟在尾随 1 左边的零块的大小。
*   将最右边的非尾随 1 翻转为零。这将在位置 p = c1 + c0。
*   清除 p 位右侧的所有位。
*   在 p 位置的右侧立即插入 c1 + 1。

请注意，步骤 2 将位 p 设置为零，步骤 3 将位 0 至 p-1 设置为零。我们可以合并这些步骤。
我们用一个例子来介绍一下。

```
c1 ==> number of trailing ones
c0 ==> size of the block of zeros immediately 
       to the left of the trailing ones.
p = c1 + c0
```

**第一步:初始数:p = 7。c1 = 2。c0 = 5。**

```
1   0   0   1   1  1  1  0  0  0  0  0  1  1
13  12  11  10  9  8  7  6  5  4  3  2  1  0
```

**步骤 2 & 3:清除位 0 至 p**

```
1   0   0   1   1  1  0  0  0  0  0  0  0  0
13  12  11  10  9  8  7  6  5  4  3  2  1  0
```

**我们可以这样做:**

```
// Sequence of 1s
int a = ~0;               

// Sequence of 1s followed by p + 1 zeros.
int b = a << (p + 1);     

// Clears bits 0 through p.
n & = b;                  
```

**第四步:在 p 位置右侧立即插入 c1 + 1 个**

```
1   0   0   1   1  1  0  1  1  1  0  0  0  0
13  12  11  10  9  8  7  6  5  4  3  2  1  0
```

请注意，由于 p =c1 + c0，因此(c1 + 1)个 1 后面将跟有(c0–1)个 0。
**我们可以这样做:**

```
// 0s with 1 at position (c1 + 1)
int a = 1 << (c1 + 1);    

// 0s followed by c1 + 1 ones       
int b = a - 1;                  

// c1 + 1 ones followed by c0 - 1 zeros.
int c = b << (c0 - 1);           
n |= c;
```

下面是实现这一点的代码。

## C++

```
// C++ Implementation of  getPrev in
// Same number of bits 1's is below
#include <bits/stdc++.h>
using namespace std;

// Main Function to find next Bigger number
// Smaller than n
int getPrev(int n)
{
    /* Compute c0 and c1  and store N*/
    int temp = n;
    int c0 = 0;
    int c1= 0;

    while ((temp & 1) == 1)
    {
        c1++;
        temp = temp >> 1;
    }

    if (temp == 0)
        return -1;

    while (((temp & 1) == 0) && (temp!= 0))
    {
        c0++;
        temp  = temp >> 1;
    }

    // position of rightmost non-trailing one.
    int p = c0 + c1;

    // clears from bit p onwards
    n = n & ((~0) << (p + 1));

    // Sequence of (c1+1) ones
    int mask = (1 << (c1 + 1)) - 1;

    n = n | mask << (c0 - 1);

    return n;
}

// Driver Code
int main()
{
    int n = 6;   // input 1
    cout << getPrev(n);

    n = 16;     // input 2
    cout << endl;
    cout << getPrev(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of 
// getPrev in Same number
// of bits 1's is below
import java.io.*;

class GFG
{

// Main Function to find
// next Bigger number
// Smaller than n
static int getPrev(int n)
{
    // Compute c0 and
    // c1 and store N
    int temp = n;
    int c0 = 0;
    int c1= 0;

    while((temp & 1) == 1)
    {
        c1++;
        temp = temp >> 1;
    }

    if(temp == 0)
        return -1;

    while(((temp & 1) == 0) &&
           (temp!= 0))
    {
        c0++;
        temp = temp >> 1;
    }

    // position of rightmost
    // non-trailing one.
    int p = c0 + c1;

    // clears from bit p onwards
    n = n & ((~0) << (p + 1));

    // Sequence of (c1+1) ones
    int mask = (1 << (c1 + 1)) - 1;

    n = n | mask << (c0 - 1);

    return n;
}

// Driver Code
public static void main(String[] args)
{
    int n = 6; // input 1
    System.out.println(getPrev(n));

    n = 16; // input 2
    System.out.println(getPrev(n));
}
}

// This code is contributed by aj_36
```

## 蟒蛇 3

```
# Python3 Implementation of  getPrev in
# Same number of bits 1's is below

# Main Function to find next Bigger number
# Smaller than n

def getPrev(n):

    # Compute c0 and c1  and store N
    temp = n
    c0 = 0
    c1 = 0

    while ((temp & 1) == 1):
        c1 = c1+1
        temp = temp >> 1

    if (temp == 0):
        return -1

    while (((temp & 1) == 0) and (temp != 0)):
        c0 = c0+1
        temp = temp >> 1

    # position of rightmost non-trailing one.
    p = c0 + c1

    # clears from bit p onwards
    n = n & ((~0) << (p + 1))

    # Sequence of (c1+1) ones
    mask = (1 << (c1 + 1)) - 1

    n = n | mask << (c0 - 1)

    return n

if __name__ == '__main__':
    n = 6   # input 1
    print(getPrev(n))

    n = 16     # input 2
    print(getPrev(n))

# This code is contributed by nirajgusain5
```

## C#

```
// C# Implementation of
// getPrev in Same number
// of bits 1's is below
using System;

class GFG
{

// Main Function to find
// next Bigger number
// Smaller than n
static int getPrev(int n)
{
    // Compute c0 and
    // c1 and store N
    int temp = n;
    int c0 = 0;
    int c1 = 0;

    while((temp & 1) == 1)
    {
        c1++;
        temp = temp >> 1;
    }

    if(temp == 0)
        return -1;

    while(((temp & 1) == 0) &&
           (temp != 0))
    {
        c0++;
        temp = temp >> 1;
    }

    // position of rightmost
    // non-trailing one.
    int p = c0 + c1;

    // clears from
    // bit p onwards
    n = n & ((~0) << (p + 1));

    // Sequence of
    // (c1+1) ones
    int mask = (1 << (c1 + 1)) - 1;

    n = n | mask << (c0 - 1);

    return n;
}

// Driver Code
static public void Main ()
{
    int n = 6; // input 1
    Console.WriteLine(getPrev(n));

    n = 16; // input 2
    Console.WriteLine(getPrev(n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Implementation of getPrev in
// Same number of bits 1's is below

// Main Function to find next Bigger
// number Smaller than n

function getPrev($n)
{
    // Compute c0 and
    // c1 and store N
    $temp = $n;
    $c0 = 0;
    $c1= 0;

    while (($temp & 1) == 1)
    {
        $c1++;
        $temp = $temp >> 1;
    }

    if ($temp == 0)
        return -1;

    while ((($temp & 1) == 0) &&
            ($temp!= 0))
    {
        $c0++;
        $temp = $temp >> 1;
    }

    // position of rightmost
    // non-trailing one.
    $p = $c0 + $c1;

    // clears from bit p onwards
    $n = $n & ((~0) << ($p + 1));

    // Sequence of (c1 + 1) ones
    $mask = (1 << ($c1 + 1)) - 1;

    $n = $n | $mask << ($c0 - 1);

    return $n;
}

// Driver Code

// input 1
$n = 6;
echo getPrev($n);

// input 2
$n = 16;    
echo " \n" ;
echo getPrev($n);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
// Javascript Implementation of
// getPrev in Same number
// of bits 1's is below

    // Main Function to find
// next Bigger number
// Smaller than n
    function getPrev(n)
    {
        // Compute c0 and
    // c1 and store N
    let temp = n;
    let c0 = 0;
    let c1= 0;

    while((temp & 1) == 1)
    {
        c1++;
        temp = temp >> 1;
    }

    if(temp == 0)
        return -1;

    while(((temp & 1) == 0) &&
           (temp!= 0))
    {
        c0++;
        temp = temp >> 1;
    }

    // position of rightmost
    // non-trailing one.
    let p = c0 + c1;

    // clears from bit p onwards
    n = n & ((~0) << (p + 1));

    // Sequence of (c1+1) ones
    let mask = (1 << (c1 + 1)) - 1;

    n = n | mask << (c0 - 1);

    return n;
    }

    // Driver Code
    let n = 6; // input 1
    document.write(getPrev(n)+"<br>");

    n = 16; // input 2
    document.write(getPrev(n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
5
8
```

**获取下一个数字的算术方法**
如果 c0 是尾随零的数量，c1 是紧接其后的一个块的大小，并且 p = c0 + c1，我们可以从前面形成我们的解，如下所示:

1.  将第 p 位设为 1。
2.  将 p 后面的所有位设置为 0。
3.  将位 0 至 C1–2 设置为 1。这将是 C1–1 的总位数。

执行步骤 1 和 2 的快速方法是将尾随零设置为 1(给我们 p 个尾随 1)，然后添加 1。加 1 会翻转所有尾随的 1，所以我们在 p 位得到 1，然后是 p 个 0。我们可以用算术方法来做这件事。
//将尾随 0 设置为 1，给我们 p 个尾随 1。
n+= 2<sup>c0</sup>–1；
//将第一个 p ls 翻转为 0，并将位 p 置 1。
n+= 1；
现在，为了以算术方式执行步骤 3，我们只需执行:
//将尾随的 C1–1 零设置为 1。
n+= 2<sup>C1–1</sup>–1；
此数学简化为:
next = n+(2<sup>c0</sup>–1)+1+(2<sup>C1–1</sup>–1)
= n+2<sup>c0</sup>+2<sup>C1–1</sup>–1

最好的部分是使用一点点操作，很容易编码。

## C++

```
// C++ Implementation of getNext with
// Same number of bits 1's is below
#include <bits/stdc++.h>
using namespace std;

// Main Function to find next smallest number
// bigger than n
int getNext(int n)
{
    /* Compute c0 and c1 */
    int c = n;
    int c0 = 0;
    int c1 = 0;

    while (((c & 1) == 0) && (c != 0))
    {
        c0 ++;
        c >>= 1;
    }
    while ((c & 1)==1)
    {
        c1++;
        c >>= 1;
    }

    // If there is no bigger number with the
    // same no. of 1's
    if (c0 +c1 == 31 || c0 +c1== 0)
        return -1;

    return n + (1 << c0) + (1 << (c1 - 1)) - 1;
}

// Driver Code
int main()
{
    int n = 5; // input 1
    cout << getNext(n);

    n = 8;     // input 2
    cout << endl;
    cout << getNext(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of getNext with
// Same number of bits 1's is below
import java.io.*;

class GFG
{

// Function to find next smallest
// number bigger than n
static int getNext(int n)
{
    /* Compute c0
    and c1 */
    int c = n;
    int c0 = 0;
    int c1 = 0;

    while (((c & 1) == 0) && (c != 0))
    {
        c0 ++;
        c >>= 1;
    }
    while ((c & 1) == 1)
    {
        c1++;
        c >>= 1;
    }

    // If there is no bigger number
    // with the same no. of 1's
    if (c0 + c1 == 31 || c0 + c1 == 0)
        return -1;

    return n + (1 << c0) +
               (1 << (c1 - 1)) - 1;
}

// Driver Code
public static void main (String[] args)
{
int n = 5; // input 1
System.out.println(getNext(n));

n = 8; // input 2
System.out.println(getNext(n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# python3 Implementation of getNext with
# Same number of bits 1's is below

# Main Function to find next smallest number
# bigger than n

def getNext(n):

    # Compute c0 and c1
    c = n
    c0 = 0
    c1 = 0

    while (((c & 1) == 0) and (c != 0)):
        c0 = c0+1
        c >>= 1

    while ((c & 1) == 1):
        c1 = c1+1
        c >>= 1

    # If there is no bigger number with the
    # same no. of 1's
    if (c0 + c1 == 31 or c0 + c1 == 0):
        return -1

    return n + (1 << c0) + (1 << (c1 - 1)) - 1

# Driver Code

if __name__ == '__main__':
    n = 5  # input 1
    print(getNext(n))
    n = 8     # input 2
    print(getNext(n))

# This code is contributed by nirajgusain5
```

## C#

```
// C# Implementation of getNext
// with Same number of bits
// 1's is below
using System;

class GFG
{

// Function to find next smallest
// number bigger than n
static int getNext(int n)
{
    /* Compute c0
    and c1 */
    int c = n;
    int c0 = 0;
    int c1 = 0;

    while (((c & 1) == 0) &&
            (c != 0))
    {
        c0 ++;
        c >>= 1;
    }
    while ((c & 1) == 1)
    {
        c1++;
        c >>= 1;
    }

    // If there is no bigger
    // number with the same
    // no. of 1's
    if (c0 + c1 == 31 ||
        c0 + c1 == 0)
        return -1;

    return n + (1 << c0) +
               (1 << (c1 - 1)) - 1;
}

// Driver Code
static public void Main ()
{
    int n = 5; // input 1
    Console.WriteLine(getNext(n));

    n = 8; // input 2
    Console.WriteLine(getNext(n));
    }
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Implementation of
// getNext with Same number
// of bits 1's is below

// Main Function to find
// next smallest number
// bigger than n
function getNext($n)
{
    /* Compute c0 and c1 */
    $c = $n;
    $c0 = 0;
    $c1 = 0;

    while ((($c & 1) == 0) &&
            ($c != 0))
    {
        $c0 ++;
        $c >>= 1;
    }
    while (($c & 1) == 1)
    {
        $c1++;
        $c >>= 1;
    }

    // If there is no bigger
    // number with the
    // same no. of 1's
    if ($c0 + $c1 == 31 ||
        $c0 + $c1 == 0)
        return -1;

    return $n + (1 << $c0) +
                (1 << ($c1 - 1)) - 1;
}

// Driver Code
$n = 5; // input 1
echo getNext($n);

$n = 8; // input 2
echo "\n";
echo getNext($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Implementation of getNext
    // with Same number of bits
    // 1's is below

    // Function to find next smallest
    // number bigger than n
    function getNext(n)
    {
        /* Compute c0
        and c1 */
        let c = n;
        let c0 = 0;
        let c1 = 0;

        while (((c & 1) == 0) &&
                (c != 0))
        {
            c0 ++;
            c >>= 1;
        }
        while ((c & 1) == 1)
        {
            c1++;
            c >>= 1;
        }

        // If there is no bigger
        // number with the same
        // no. of 1's
        if (c0 + c1 == 31 ||
            c0 + c1 == 0)
            return -1;

        return n + (1 << c0) +
                   (1 << (c1 - 1)) - 1;
    }

    let n = 5; // input 1
    document.write(getNext(n) + "</br>");

    n = 8; // input 2
    document.write(getNext(n));

</script>
```

**输出:**

```
6
16
```

**获取前一个数的算术方法**
如果 c1 是后一个数的个数，c0 是紧接其后的零块的大小，p =c0 + c1，我们可以把初始的 getPrev 解写成如下:

1.  将 pth 位设为 0
2.  将 p 后面的所有位设置为 1
3.  将位 0 至 c0–1 设为 0。

我们可以通过如下算法实现。为了清楚起见，我们假设 n = 10000011。这使得 c1 = 2，c0 = 5。

```
// Removes trailing 1s. n is now 10000000.
n -= 2c1 – 1;    

// Flips trailing 0s. n is now 01111111.
n -= 1;    

// Flips last (c0-1) 0s. n is now 01110000.
n -= 2c0 - 1 - 1;    

This reduces mathematically to:
next = n - (2c1 - 1) - 1 - ( 2c0-1 - 1) .
     = n - 2c1 - 2c0-1 + 1;
```

同样，这很容易实现。

## C++

```
// C++ Implementation of Arithmetic Approach to
// getPrev with Same number of bits 1's is below
#include <bits/stdc++.h>
using namespace std;

// Main Function to find next Bigger number
// Smaller than n
int getPrev(int n)
{
    /* Compute c0 and c1  and store N*/
    int temp = n;
    int c0 = 0;
    int c1 = 0;

    while ((temp & 1) == 1)
    {
        c1++;
        temp = temp >> 1;
    }

    if (temp == 0)
        return -1;

    while (((temp & 1) == 0) && (temp!= 0))
    {
        c0++;
        temp  = temp >> 1;
    }

    return n - (1 << c1) - (1 << (c0 - 1)) + 1;
}

// Driver Code
int main()
{
    int n = 6;   // input 1
    cout << getPrev(n);

    n = 16;     // input 2
    cout << endl;
    cout << getPrev(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of Arithmetic
// Approach to getPrev with Same
// number of bits 1's is below
import java.io.*;

class GFG
{

// Main Function to find next
// Bigger number Smaller than n
static int getPrev(int n)
{
    /* Compute c0 and
    c1 and store N*/
    int temp = n;
    int c0 = 0;
    int c1 = 0;

    while ((temp & 1) == 1)
    {
        c1++;
        temp = temp >> 1;
    }

    if (temp == 0)
        return -1;

    while (((temp & 1) == 0) &&
            (temp!= 0))
    {
        c0++;
        temp = temp >> 1;
    }

    return n - (1 << c1) -
               (1 << (c0 - 1)) + 1;
}

// Driver Code
public static void main (String[] args)
{

    int n = 6; // input 1
    System.out.println (getPrev(n));

    n = 16; // input 2
    System.out.println(getPrev(n));

}
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python3 Implementation of Arithmetic Approach to
# getPrev with Same number of bits 1's is below

# Main Function to find next Bigger
# number Smaller than n
def getPrev(n):

    # Compute c0 and c1 and store N
    temp = n
    c0 = 0
    c1 = 0

    while ((temp & 1) == 1):
        c1 += 1
        temp = temp >> 1
    if (temp == 0):
        return -1

    while (((temp & 1) == 0) and (temp != 0)):
        c0 += 1
        temp = temp >> 1

    return n - (1 << c1) - (1 << (c0 - 1)) + 1

# Driver Code
if __name__ == '__main__':
    n = 6 # input 1
    print(getPrev(n))

    n = 16     # input 2
    print(getPrev(n))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# Implementation of Arithmetic
// Approach to getPrev with Same
// number of bits 1's is below
using System;

class GFG
{

// Main Function to find next
// Bigger number Smaller than n
static int getPrev(int n)
{
    /* Compute c0 and
    c1 and store N*/
    int temp = n;
    int c0 = 0;
    int c1 = 0;

    while ((temp & 1) == 1)
    {
        c1++;
        temp = temp >> 1;
    }

    if (temp == 0)
        return -1;

    while (((temp & 1) == 0) &&
            (temp!= 0))
    {
        c0++;
        temp = temp >> 1;
    }

    return n - (1 << c1) -
               (1 << (c0 - 1)) + 1;
}

// Driver Code
static public void Main ()
{
    int n = 6; // input 1
    Console.WriteLine(getPrev(n));

    n = 16; // input 2
    Console.WriteLine(getPrev(n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count of
// steps until one of the
// two numbers become 0.

// Returns count of steps
// before one of the numbers
// become 0 after repeated
// subtractions.
function countSteps($x, $y)
{
    // If y divides x, then
    // simply return x/y.
    if ($x % $y == 0)
        return floor(((int)$x / $y));

    // Else recur. Note that this
    // function works even if x is
    // smaller than y because in that
    // case first recursive call
    // exchanges roles of x and y.
    return floor(((int)$x / $y) +
                   countSteps($y, $x % $y));
}

// Driver code
$x = 100;
$y = 19;
echo countSteps($x, $y);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript Implementation of Arithmetic
    // Approach to getPrev with Same
    // number of bits 1's is below

    // Main Function to find next
    // Bigger number Smaller than n
    function getPrev(n)
    {
        /* Compute c0 and
        c1 and store N*/
        let temp = n;
        let c0 = 0;
        let c1 = 0;

        while ((temp & 1) == 1)
        {
            c1++;
            temp = temp >> 1;
        }

        if (temp == 0)
            return -1;

        while (((temp & 1) == 0) &&
                (temp!= 0))
        {
            c0++;
            temp = temp >> 1;
        }

        return n - (1 << c1) -
                   (1 << (c0 - 1)) + 1;
    }

    let n = 6; // input 1
    document.write(getPrev(n) + "</br>");

    n = 16; // input 2
    document.write(getPrev(n));

</script>
```

**输出:**

```
5
8
```

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。