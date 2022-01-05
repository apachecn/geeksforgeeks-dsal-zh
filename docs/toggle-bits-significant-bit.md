# 在最高有效位后切换所有位

> 原文:[https://www.geeksforgeeks.org/toggle-bits-significant-bit/](https://www.geeksforgeeks.org/toggle-bits-significant-bit/)

给定一个数字，在包括最高有效位的最高有效位之后切换它的所有位。

**示例:**

```
Input : 10 
Output : 5
Binary representation of 10 is 1010
After toggling we get 0101

Input : 5
Output : 2
```

我们可以通过对 1 进行异或操作来切换一个位(注意，1 ^ 0 = 1，1 ^ 1 = 0)。想法是取一个只有一个位设置的数字 **temp** 。一个接一个地向左移动**温度**的唯一设置位，并与 n 进行异或运算，直到它越过 n 的最高有效位

## C++

```
// CPP program to toggle set  bits starting
// from MSB
#include<bits/stdc++.h>
using namespace std;

void toggle(int &n)
{
    // temporary variable to
    // use XOR with one of a n
    int temp = 1;

    // Run loop until the only
    // set bit in temp crosses
    // MST of n.
    while (temp <= n)
    {
        // Toggle bit of n
        // corresponding to
        // current set bit in
        // temp.
        n = n ^ temp;

        // Move set bit to next
        // higher position.
        temp = temp << 1;
    }
}

// Driver code
int main()
{
    int n = 10;
    toggle(n);
    cout << n;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to toggle set
// bits starting from MSB

class GFG {

static int toggle(int n) {

    // temporary variable to
    // use XOR with one of a n
    int temp = 1;

    // Run loop until the only
    // set bit in temp crosses
    // MST of n.
    while (temp <= n) {

    // Toggle bit of n
    // corresponding to
    // current set bit in
    // temp.
    n = n ^ temp;

    // Move set bit to next
    // higher position.
    temp = temp << 1;
    }
    return n;
}

// Driver code
public static void main(String arg[])
{
    int n = 10;
    n = toggle(n);
    System.out.print(n);
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to toggle
# set  bits starting
# from MSB

def toggle(n):

    # temporary variable to
    # use XOR with one of a n
    temp = 1

    #Run loop until the only
    #set bit in temp crosses
    #MST of n.
    while (temp <= n):

        # Toggle bit of n
        # corresponding to
        # current set bit in
        # temp.
        n = n ^ temp

        # Move set bit to next
        # higher position.
        temp = temp << 1

    return n

# Driver code

n = 10
n=toggle(n)
print(n)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to toggle set
// bits starting from MSB
using System;

class GFG {

// Function to toggle bits
// starting from MSB   
static int toggle(int n) {

    // temporary variable to
    // use XOR with one of a n
    int temp = 1;

    // Run loop until the only
    // set bit in temp crosses
    // MST of n.
    while (temp <= n) {

    // Toggle bit of n
    // corresponding to
    // current set bit in
    // temp.
    n = n ^ temp;

    // Move set bit to next
    // higher position.
    temp = temp << 1;
    }
    return n;
}

// Driver code
public static void Main()
{
    int n = 10;
    n = toggle(n);
    Console.Write(n);
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to toggle set
// bits starting from MSB

function toggle( &$n)
{
    // temporary variable to
    // use XOR with one of a n
    $temp = 1;

    // Run loop until the only
    // set bit in temp crosses
    // MST of n.
    while ($temp <= $n)
    {
        // Toggle bit of n
        // corresponding to
        // current set bit in
        // temp.
        $n = $n ^ $temp;

        // Move set bit to next
        // higher position.
        $temp = $temp << 1;
    }
}

// Driver code
$n = 10;
toggle($n);
echo $n;

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to toggle set
// bits starting from MSB
function toggle(n)
{

    // Temporary variable to
    // use XOR with one of a n
    let temp = 1;

    // Run loop until the only
    // set bit in temp crosses
    // MST of n.
    while (temp <= n)
    {

        // Toggle bit of n
        // corresponding to
        // current set bit in
        // temp.
        n = n ^ temp;

        // Move set bit to next
        // higher position.
        temp = temp << 1;
    }
    return n;
}

// Driver code
let n = 10;
n = toggle(n);

document.write(n);

// This code is contributed by subham348

</script>
```

**输出:**

```
5
```

假设数字以 32 位存储，上述解决方案可以优化为在 O(1)时间内工作。

## C++

```
// CPP program to toggle set  bits starting
// from MSB
#include<bits/stdc++.h>
using namespace std;

// Returns a number which has all set bits
// starting from MSB of n
int setAllBitsAfterMSB(int n)
{   
    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    n |= n>>1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    n |= n>>2;  

    n |= n>>4; 
    n |= n>>8;
    n |= n>>16;
    return n;
}

void toggle(int &n)
{
    n = n ^ setAllBitsAfterMSB(n);
}

// Driver code
int main()
{
    int n = 10;
    toggle(n);
    cout << n;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to toggle set bits
// starting from MSB

class GFG {

// Returns a number which has all
// set bits starting from MSB of n
static int setAllBitsAfterMSB(int n) {

    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 2;

    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;
    return n;
}
static int toggle(int n)
{
    n = n ^ setAllBitsAfterMSB(n);
    return n;
}

// Driver code
public static void main(String arg[])
{
    int n = 10;
    n = toggle(n);
    System.out.print(n);
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to toggle set  bits starting
# from MSB

# Returns a number which has all set bits
# starting from MSB of n
def setAllBitsAfterMSB(n):

    # This makes sure two bits
    # (From MSB and including MSB)
    # are set
    n |= n>>1

    # This makes sure 4 bits
    # (From MSB and including MSB)
    # are set
    n |= n>>2  

    n |= n>>4 
    n |= n>>8
    n |= n>>16
    return n

def toggle(n):

    n = n ^ setAllBitsAfterMSB(n)
    return n

#Driver code

n = 10
n=toggle(n)
print(n)
# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to toggle set bits
// starting from MSB
using System;

class GFG {

    // Returns a number which has all
    // set bits starting from MSB of n
    static int setAllBitsAfterMSB(int n)
    {

        // This makes sure two bits
        // (From MSB and including MSB)
        // are set
        n |= n >> 1;

        // This makes sure 4 bits
        // (From MSB and including MSB)
        // are set
        n |= n >> 2;

        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;
        return n;
    }

    static int toggle(int n)
    {
        n = n ^ setAllBitsAfterMSB(n);
        return n;
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        n = toggle(n);
        Console.WriteLine(n);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to toggle set
// bits starting from MSB

// Returns a number which
// has all set bits starting
// from MSB of n
function setAllBitsAfterMSB($n)
{
    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    $n |= $n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    $n |= $n >> 2;

    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;
    return $n;
}
function toggle(&$n)
{
    $n = $n ^ setAllBitsAfterMSB($n);
}

// Driver Code
$n = 10;
toggle($n);
echo $n;

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to toggle set  bits starting
// from MSB

// Returns a number which has all set bits
// starting from MSB of n
function setAllBitsAfterMSB(n)
{   
    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    n |= n>>1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    n |= n>>2;  

    n |= n>>4; 
    n |= n>>8;
    n |= n>>16;
    return n;
}

function toggle(n)
{
    n = n ^ setAllBitsAfterMSB(n);
    return n;
}

// Driver code
    let n = 10;
    document.write(toggle(n));

</script>
```

**输出:**

```
5
```

感谢**德万舒·阿加瓦尔**提出这个方法。

本文由**德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。