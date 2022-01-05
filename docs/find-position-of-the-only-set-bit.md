# 找到唯一设定位的位置

> 原文:[https://www . geeksforgeeks . org/find-唯一设置位的位置/](https://www.geeksforgeeks.org/find-position-of-the-only-set-bit/)

给定一个二进制表示中只有一个“1”和所有其他“0”的数字 N，找到唯一设置位的位置。如果有 0 个或 1 个以上的设置位，答案应该是-1。在数字的二进制表示中，设置位“1”的位置应从 1 开始计数。

来源:[微软访谈| 18](https://www.geeksforgeeks.org/microsoft-interview-178/)

**示例:-**

```
Input:
N = 2
Output:
2
Explanation:
2 is represented as "10" in Binary.
As we see there's only one set bit
and it's in Position 2 and thus the
Output 2.

```

这是另一个例子

```
Input:
N = 5
Output:
-1
Explanation:
5 is represented as "101" in Binary.
As we see there's two set bits
and thus the Output -1.
```

其思想是从最右边的位开始，逐个检查每一位的值。下面是详细的算法。
**(1)**如果数是二的幂，那么只有它的二进制表示只包含一个‘1’。这就是为什么要检查给定的数字是否是 2 的幂。如果给定的数字不是 2 的幂，则打印错误信息并退出。
**2)** 初始化两个变量；i = 1(用于循环)和 pos = 1(用于查找设置位的位置)
**3)** 在循环内部，对 I 和数字“N”进行按位“与”。如果该操作的值为真，则设置“pos”位，因此中断循环并返回位置。否则，将“位置”增加 1，将左移位 I 增加 1，并重复该过程。

## C++

```
// C++ program to find position of only set bit in a given number
#include <bits/stdc++.h>
using namespace std;

// A utility function to check whether n is a power of 2 or not.
// See http://goo.gl/17Arj
int isPowerOfTwo(unsigned n)
{
    return n && (!(n & (n - 1)));
}

// Returns position of the only set bit in 'n'
int findPosition(unsigned n)
{
    if (!isPowerOfTwo(n))
        return -1;

    unsigned i = 1, pos = 1;

    // Iterate through bits of n till we find a set bit
    // i&n will be non-zero only when 'i' and 'n' have a set bit
    // at same position
    while (!(i & n)) {
        // Unset current bit and set the next bit in 'i'
        i = i << 1;

        // increment position
        ++pos;
    }

    return pos;
}

// Driver program to test above function
int main(void)
{
    int n = 16;
    int pos = findPosition(n);
    (pos == -1) ? cout << "n = " << n << ", Invalid number" << endl : cout << "n = " << n << ", Position " << pos << endl;

    n = 12;
    pos = findPosition(n);
    (pos == -1) ? cout << "n = " << n << ", Invalid number" << endl : cout << "n = " << n << ", Position " << pos << endl;

    n = 128;
    pos = findPosition(n);
    (pos == -1) ? cout << "n = " << n << ", Invalid number" << endl : cout << "n = " << n << ", Position " << pos << endl;

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to find position of only set bit in a given number
#include <stdio.h>

// A utility function to check whether n is a power of 2 or not.
// See http://goo.gl/17Arj
int isPowerOfTwo(unsigned n)
{
    return n && (!(n & (n - 1)));
}

// Returns position of the only set bit in 'n'
int findPosition(unsigned n)
{
    if (!isPowerOfTwo(n))
        return -1;

    unsigned i = 1, pos = 1;

    // Iterate through bits of n till we find a set bit
    // i&n will be non-zero only when 'i' and 'n' have a set bit
    // at same position
    while (!(i & n)) {
        // Unset current bit and set the next bit in 'i'
        i = i << 1;

        // increment position
        ++pos;
    }

    return pos;
}

// Driver program to test above function
int main(void)
{
    int n = 16;
    int pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    n = 12;
    pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    n = 128;
    pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find position of only set bit in a given number
class GFG {

    // A utility function to check whether n is a power of 2 or not.
    // See http://goo.gl/17Arj
    static boolean isPowerOfTwo(int n)
    {
        return (n > 0 && ((n & (n - 1)) == 0)) ? true : false;
    }

    // Returns position of the only set bit in 'n'
    static int findPosition(int n)
    {
        if (!isPowerOfTwo(n))
            return -1;

        int i = 1, pos = 1;

        // Iterate through bits of n till we find a set bit
        // i&n will be non-zero only when 'i' and 'n' have a set bit
        // at same position
        while ((i & n) == 0) {
            // Unset current bit and set the next bit in 'i'
            i = i << 1;

            // increment position
            ++pos;
        }

        return pos;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 16;
        int pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number");
        else
            System.out.println("n = " + n + ", Position " + pos);

        n = 12;
        pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number");
        else
            System.out.println("n = " + n + ", Position " + pos);

        n = 128;
        pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number");
        else
            System.out.println("n = " + n + ", Position " + pos);
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find position of
# only set bit in a given number

# A utility function to check
# whether n is power of 2 or
# not.
def isPowerOfTwo(n):
    return (True if(n > 0 and
                   ((n & (n - 1)) > 0))
                 else False);

# Returns position of the
# only set bit in 'n'
def findPosition(n):
    if (isPowerOfTwo(n) == True):
        return -1;

    i = 1;
    pos = 1;

    # Iterate through bits of n
    # till we find a set bit i&n
    # will be non-zero only when
    # 'i' and 'n' have a set bit
    # at same position
    while ((i & n) == 0):

        # Unset current bit and
        # set the next bit in 'i'
        i = i << 1;

        # increment position
        pos += 1;

    return pos;

# Driver Code
n = 16;
pos = findPosition(n);
if (pos == -1):
    print("n =", n, ", Invalid number");
else:
    print("n =", n, ", Position ", pos);

n = 12;
pos = findPosition(n);
if (pos == -1):
    print("n =", n, ", Invalid number");
else:
    print("n =", n, ", Position ", pos);

n = 128;
pos = findPosition(n);
if (pos == -1):
    print("n =", n, ", Invalid number");
else:
    print("n =", n, ", Position ", pos);

# This code is contributed by mits
```

## C#

```
// C# program to find position of only set bit in a given number
using System;

class GFG {

    // A utility function to check whether n is a power of 2 or not.
    // See http://goo.gl/17Arj
    static bool isPowerOfTwo(int n)
    {
        return (n > 0 && ((n & (n - 1)) == 0)) ? true : false;
    }

    // Returns position of the only set bit in 'n'
    static int findPosition(int n)
    {
        if (!isPowerOfTwo(n))
            return -1;

        int i = 1, pos = 1;

        // Iterate through bits of n till we find a set bit
        // i&n will be non-zero only when 'i' and 'n' have a set bit
        // at same position
        while ((i & n) == 0) {
            // Unset current bit and set the next bit in 'i'
            i = i << 1;

            // increment position
            ++pos;
        }

        return pos;
    }

    // Driver code
    static void Main()
    {
        int n = 16;
        int pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);

        n = 12;
        pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);

        n = 128;
        pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find position of
// only set bit in a given number

// A utility function to check
// whether n is power of 2 or
// not. See http://goo.gl/17Arj
function isPowerOfTwo($n)
{
    return $n && (!($n & ($n - 1)));

}

// Returns position of the
// only set bit in 'n'
function findPosition($n)
{
    if (!isPowerOfTwo($n))
        return -1;

    $i = 1;
    $pos = 1;

    // Iterate through bits of n
    // till we find a set bit i&n
    // will be non-zero only when
    // 'i' and 'n' have a set bit
    // at same position
    while (!($i & $n))
    {
        // Unset current bit and
        // set the next bit in 'i'
        $i = $i << 1;

        // increment position
        ++$pos;
    }

    return $pos;
}

// Driver Code
$n = 16;
$pos = findPosition($n);
if (($pos == -1) == true)
        echo "n =", $n, ", ",
             " Invalid number", "\n";
else
        echo "n = ", $n, ", ",
             " Position ", $pos, "\n";

$n = 12;
$pos = findPosition($n);
if(($pos == -1) == true)    
        echo "n = ", $n, ", ",
             " Invalid number", "\n";
else
        echo "n =", $n, ", ",
             " Position ", $pos, "\n";
$n = 128;
$pos = findPosition($n);
if(($pos == -1) == true)    
        echo "n =", $n, ", ",
             " Invalid number", "\n";
else
        echo "n = ", $n, ", ",
             " Position ", $pos, "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find position of
// only set bit in a given number

// A utility function to check
// whether n is power of 2 or
// not.
function isPowerOfTwo(n){

    return (n > 0 && ((n & (n - 1)) == 0)) ? true : false;
}

// Returns position of the
// only set bit in 'n'
function findPosition(n){
    if (isPowerOfTwo(n) == false)
        return -1;

    var i = 1;
    var pos = 1;

    // Iterate through bits of n
    // till we find a set bit i&n
    // will be non-zero only when
    // 'i' and 'n' have a set bit
    // at same position
    while ((i & n) == 0){

        // Unset current bit and
        // set the next bit in 'i'
        i = i << 1;

        // increment position
        pos += 1;
    }
    return pos;
}

// Driver Code
var n = 16;
var pos = findPosition(n);
if (pos == -1)
    document.write("n =" + n + ", Invalid number");
else
    document.write("n =" + n + ", Position " + pos);
    document.write("<br>");

n = 12;
pos = findPosition(n);
if (pos == -1)
    document.write("n =" + n + ", Invalid number");
else
    document.write("n =" + n + ", Position ", pos);
    document.write("<br>");

n = 128;
pos = findPosition(n);
if (pos == -1)
    document.write("n =" + n + ", Invalid number");
else
    document.write("n =" + n + ", Position " + pos);

// This code is contributed by AnkThon

</script>
```

**输出:**

```
n = 16, Position 5
n = 12, Invalid number
n = 128, Position 8
```

下面是**针对这个问题的另一种方法**。其思想是将给定数字“n”的设置位一个接一个地右移，直到“n”变成 0。数一下我们移动了多少次，使 n 为零。最终计数是置位位的位置。

## C++

```
// C++ program to find position of only set bit in a given number
#include <bits/stdc++.h>
using namespace std;

// A utility function to check whether n is power of 2 or not
int isPowerOfTwo(unsigned n)
{
    return n && (!(n & (n - 1)));
}

// Returns position of the only set bit in 'n'
int findPosition(unsigned n)
{
    if (!isPowerOfTwo(n))
        return -1;

    unsigned count = 0;

    // One by one move the only set bit to right till it reaches end
    while (n)
    {
        n = n >> 1;

        // increment count of shifts
        ++count;
    }

    return count;
}

// Driver code
int main(void)
{
    int n = 0;
    int pos = findPosition(n);
    (pos == -1) ? cout<<"n = "<<n<<", Invalid number\n" :
                    cout<<"n = "<<n<<", Position "<< pos<<endl;

    n = 12;
    pos = findPosition(n);
    (pos == -1) ? cout<<"n = "<<n<<", Invalid number\n" :
               cout<<"n = "<<n<<", Position "<< pos<<endl;

    n = 128;
    pos = findPosition(n);
    (pos == -1) ? cout<<"n = "<<n<<", Invalid number\n" :
                cout<<"n = "<<n<<", Position "<< pos<<endl;

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to find position of only set bit in a given number
#include <stdio.h>

// A utility function to check whether n is power of 2 or not
int isPowerOfTwo(unsigned n)
{
    return n && (!(n & (n - 1)));
}

// Returns position of the only set bit in 'n'
int findPosition(unsigned n)
{
    if (!isPowerOfTwo(n))
        return -1;

    unsigned count = 0;

    // One by one move the only set bit to right till it reaches end
    while (n) {
        n = n >> 1;

        // increment count of shifts
        ++count;
    }

    return count;
}

// Driver program to test above function
int main(void)
{
    int n = 0;
    int pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    n = 12;
    pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    n = 128;
    pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find position of only
// set bit in a given number

class GFG {

    // A utility function to check whether
    // n is power of 2 or not
    static boolean isPowerOfTwo(int n)
    {
        return n > 0 && ((n & (n - 1)) == 0);
    }

    // Returns position of the only set bit in 'n'
    static int findPosition(int n)
    {
        if (!isPowerOfTwo(n))
            return -1;

        int count = 0;

        // One by one move the only set bit
        // to right till it reaches end
        while (n > 0) {
            n = n >> 1;

            // increment count of shifts
            ++count;
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 0;
        int pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number");
        else
            System.out.println("n = " + n + ", Position " + pos);

        n = 12;
        pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number");
        else
            System.out.println("n = " + n + ", Position " + pos);

        n = 128;
        pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number");
        else
            System.out.println("n = " + n + ", Position " + pos);
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to find position
# of only set bit in a given number

# A utility function to check whether
# n is power of 2 or not
def isPowerOfTwo(n) :

    return (n and ( not (n & (n-1))))

# Returns position of the only set bit in 'n'
def findPosition(n) :

    if not isPowerOfTwo(n) :
        return -1

    count = 0

    # One by one move the only set bit to
    # right till it reaches end
    while (n) :

        n = n >> 1

        # increment count of shifts
        count += 1

    return count

# Driver program to test above function
if __name__ == "__main__" :
    n = 0
    pos = findPosition(n)

    if pos == -1 :
        print("n =", n, "Invalid number")
    else :
        print("n =", n, "Position", pos)

    n = 12
    pos = findPosition(n)

    if pos == -1 :
        print("n =", n, "Invalid number")
    else :
        print("n =", n, "Position", pos)

    n = 128
    pos = findPosition(n)

    if pos == -1 :
        print("n =", n, "Invalid number")
    else :
        print("n =", n, "Position", pos)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find position of only
// set bit in a given number
using System;

class GFG {

    // A utility function to check whether
    // n is power of 2 or not
    static bool isPowerOfTwo(int n)
    {
        return n > 0 && ((n & (n - 1)) == 0);
    }

    // Returns position of the only set bit in 'n'
    static int findPosition(int n)
    {
        if (!isPowerOfTwo(n))
            return -1;

        int count = 0;

        // One by one move the only set bit
        // to right till it reaches end
        while (n > 0) {
            n = n >> 1;

            // increment count of shifts
            ++count;
        }

        return count;
    }

    // Driver code
    static void Main()
    {
        int n = 0;
        int pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);

        n = 12;
        pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);

        n = 128;
        pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find position of
// only set bit in a given number

// A utility function to check
// whether n is power of 2 or not
function isPowerOfTwo($n)
{
    return $n && (! ($n & ($n - 1)));
}

// Returns position of the
// only set bit in 'n'
function findPosition($n)
{
    if (!isPowerOfTwo($n))
        return -1;

    $count = 0;

    // One by one move the only set
    // bit to right till it reaches end
    while ($n)
    {
        $n = $n >> 1;

        // increment count of shifts
        ++$count;
    }

    return $count;
}

// Driver Code
$n = 0;
$pos = findPosition($n);
if(($pos == -1) == true)
    echo "n = ", $n, ", ",
         " Invalid number", "\n";
else
    echo "n = ", $n, ", ",
         " Position ", $pos, "\n";

$n = 12;
$pos = findPosition($n);
if (($pos == -1) == true)
        echo "n = ", $n, ", ",
             " Invalid number", "\n";
else
        echo "n = ", $n,
             " Position ", $pos, "\n";

$n = 128;
$pos = findPosition($n);
    if(($pos == -1) == true)
        echo "n = ", $n, ", ",
             " Invalid number", "\n";
else
        echo "n = ", $n, ", ",
             " Position ", $pos, "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find position
// of only set bit in a given number

// A utility function to check whether
// n is power of 2 or not
function isPowerOfTwo(n) {

    return (n && ( !(n & (n-1))))
}

// Returns position of the only set bit in 'n'
function findPosition(n) {

    if (!isPowerOfTwo(n))
        return -1

    var count = 0

    // One by one move the only set bit to
    // right till it reaches end
    while (n) {

        n = n >> 1

        // increment count of shifts
        count += 1
    }

    return count

}

// Driver program to test above function
var n = 0
var pos = findPosition(n)

if (pos == -1)
    document.write("n = ", n, ", Invalid number ")
else
    document.write("n =", n, ", Position ", pos)

document.write("<br>")

n = 12
pos = findPosition(n)

if (pos == -1)
    document.write("n = ", n, ", Invalid number")
else
    document.write("n = ", n, ", Position ", pos)

document.write("<br>")

n = 128
pos = findPosition(n)

if (pos == -1)
    document.write("n = ", n, ", Invalid number")
else
    document.write("n = ", n, ", Position ", pos)

document.write("<br>")

// This code is contributed by AnkThon

</script>
```

**输出:**

```
n = 0, Invalid number
n = 12, Invalid number
n = 128, Position 8
```

**我们也可以用原木底座 2 找位置**。感谢[阿伦库马](https://www.facebook.com/arunkumar.somalinga)提出这个解决方案。

## C++

```
#include <bits/stdc++.h>
using namespace std;

unsigned int Log2n(unsigned int n)
{
    return (n > 1) ? 1 + Log2n(n / 2) : 0;
}

int isPowerOfTwo(unsigned n)
{
    return n && (!(n & (n - 1)));
}

int findPosition(unsigned n)
{
    if (!isPowerOfTwo(n))
        return -1;
    return Log2n(n) + 1;
}

// Driver code
int main(void)
{
    int n = 0;
    int pos = findPosition(n);
    (pos == -1) ? cout<<"n = "<<n<<", Invalid number\n" :
            cout<<"n = "<<n<<", Position "<<pos<<" \n";

    n = 12;
    pos = findPosition(n);
    (pos == -1) ? cout<<"n = "<<n<<", Invalid number\n" :
            cout<<"n = "<<n<<", Position "<<pos<<" \n";

    n = 128;
    pos = findPosition(n);
    (pos == -1) ? cout<<"n = "<<n<<", Invalid number\n" :
            cout<<"n = "<<n<<", Position "<<pos<<" \n";

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>

unsigned int Log2n(unsigned int n)
{
    return (n > 1) ? 1 + Log2n(n / 2) : 0;
}

int isPowerOfTwo(unsigned n)
{
    return n && (!(n & (n - 1)));
}

int findPosition(unsigned n)
{
    if (!isPowerOfTwo(n))
        return -1;
    return Log2n(n) + 1;
}

// Driver program to test above function
int main(void)
{
    int n = 0;
    int pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    n = 12;
    pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    n = 128;
    pos = findPosition(n);
    (pos == -1) ? printf("n = %d, Invalid number\n", n) : printf("n = %d, Position %d \n", n, pos);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find position
// of only set bit in a given number

class GFG {
    static int Log2n(int n)
    {
        return (n > 1) ? 1 + Log2n(n / 2) : 0;
    }

    static boolean isPowerOfTwo(int n)
    {
        return n > 0 && ((n & (n - 1)) == 0);
    }

    static int findPosition(int n)
    {
        if (!isPowerOfTwo(n))
            return -1;
        return Log2n(n) + 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 0;
        int pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number ");
        else
            System.out.println("n = " + n + ", Position " + pos);

        n = 12;
        pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number ");
        else
            System.out.println("n = " + n + ", Position " + pos);

        n = 128;
        pos = findPosition(n);
        if (pos == -1)
            System.out.println("n = " + n + ", Invalid number ");
        else
            System.out.println("n = " + n + ", Position " + pos);
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python program to find position
# of only set bit in a given number

def Log2n(n):
    if (n > 1):
        return (1 + Log2n(n / 2))
    else:
        return 0

# A utility function to check
# whether n is power of 2 or not   
def isPowerOfTwo(n):
    return n and (not (n & (n-1)) )

def findPosition(n):
    if (not isPowerOfTwo(n)):
        return -1
    return Log2n(n) + 1

# Driver program to test above function

n = 0
pos = findPosition(n)
if(pos == -1):
    print("n =", n, ", Invalid number")
else:
    print("n = ", n, ", Position ", pos)

n = 12
pos = findPosition(n)
if(pos == -1):
    print("n =", n, ", Invalid number")
else:
    print("n = ", n, ", Position ", pos)
n = 128
pos = findPosition(n)
if(pos == -1):
    print("n = ", n, ", Invalid number")
else:
    print("n = ", n, ", Position ", pos)

# This code is contributed
# by Sumit Sudhakar
```

## C#

```
// C# program to find position
// of only set bit in a given number

using System;

class GFG {
    static int Log2n(int n)
    {
        return (n > 1) ? 1 + Log2n(n / 2) : 0;
    }

    static bool isPowerOfTwo(int n)
    {
        return n > 0 && ((n & (n - 1)) == 0);
    }

    static int findPosition(int n)
    {
        if (!isPowerOfTwo(n))
            return -1;
        return Log2n(n) + 1;
    }

    // Driver program to test above function
    static void Main()
    {
        int n = 0;
        int pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number ");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);

        n = 12;
        pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number ");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);

        n = 128;
        pos = findPosition(n);
        if (pos == -1)
            Console.WriteLine("n = " + n + ", Invalid number ");
        else
            Console.WriteLine("n = " + n + ", Position " + pos);
    }
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find position
// of only set bit in a given number
function Log2n($n)
{
return ($n > 1) ? 1 +
  Log2n($n / 2) : 0;
}

function isPowerOfTwo($n)
{
    return $n && (! ($n &
                    ($n - 1)));
}

function findPosition($n)
{
    if (!isPowerOfTwo($n))
        return -1;
    return Log2n($n) + 1;
}

// Driver Code
$n = 0;
$pos = findPosition($n);
if(($pos == -1) == true)
        echo "n =", $n, ", ",
             " Invalid number", "\n";
else
        echo "n = ", $n, ", ",
             " Position n", $pos, "\n";

$n = 12;
$pos = findPosition($n);
if(($pos == -1) == true)
            echo "n = ", $n, ", ",
                 " Invalid number", "\n";
        else
            echo "n =", $n, ", ",
                 " Position", $pos, "\n";

// Driver Code
$n = 128;
$pos = findPosition($n);
if(($pos == -1) == true)
        echo "n = ", $n, ", ",
             " Invalid number", "\n";
else
        echo "n = ", $n, ", ",
             " Position ", $pos, "\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to find position
// of only set bit in a given number

function Log2n(n){
    if (n > 1)
        return (1 + Log2n(n / 2))
    else
        return 0
}

// A utility function to check
// whether n is power of 2 or not   
function isPowerOfTwo(n){
    return n && ( ! (n & (n-1)) )
}

function findPosition(n){
    if (isPowerOfTwo(n) == false)
        return -1
    return Log2n(n) + 1
 }

// Driver program to test above function

var n = 0
var pos = findPosition(n)
if(pos == -1)
    document.write("n = ", n, ", Invalid number")
else
    document.write("n = ", n, ", Position ", pos)

document.write("<br>")

n = 12
pos = findPosition(n)
if(pos == -1)
    document.write("n = ", n, ", Invalid number")
else
    document.write("n = ", n, ", Position ", pos)

document.write("<br>")
n = 128
pos = findPosition(n)
if(pos == -1)
    document.write("n = ", n, ", Invalid number")
else
    document.write("n = ", n, ", Position ", pos)

// This code is contributed AnkThon

</script>
```

**输出:**

```
n = 0, Invalid number
n = 12, Invalid number
n = 128, Position 8
```

本文由**纳伦德拉·康拉尔卡尔**整理。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。