# 检查给定数字的二进制表示及其补码是否是字谜

> 原文:[https://www . geesforgeks . org/check-二进制-表示-给定-数字-补码-字谜/](https://www.geeksforgeeks.org/check-binary-representation-given-number-complement-anagram/)

给定一个正数，你需要检查它的补码和数字是否是字谜。
**例:**

```
Input : a = 4294967295
Output : Yes
Binary representation of 'a' and it's
complement are anagrams of each other

Input : a = 4
Output : No
```

**简单方法:**在这种方法中，允许计算数的补码。
1。使用简单的十进制到二进制表示技术找到数字及其补码的二进制表示。
2。对两种二进制表示进行排序，并进行比较，以检查它们是否是字谜。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A simple C++ program to check if binary
// representations of a number and it's
// complement are anagram.
#include <bits/stdc++.h>
#define ull unsigned long long int
using namespace std;

const int ULL_SIZE = 8*sizeof(ull);

bool isComplementAnagram(ull a)
{
    ull b = ~a; // Finding complement of a;

    // Find reverse binary representation of a.
    bool binary_a[ULL_SIZE] = { 0 };
    for (int i=0; a > 0; i++)
    {
        binary_a[i] = a % 2;
        a /= 2;
    }

    // Find reverse binary representation
    // of complement.
    bool binary_b[ULL_SIZE] = { 0 };
    for (int i=0; b > 0; i++)
    {
        binary_b[i] = b % 2;
        b /= 2;
    }

    // Sort binary representations and compare
    // after sorting.
    sort(binary_a, binary_a + ULL_SIZE);
    sort(binary_b, binary_b + ULL_SIZE);
    for (int i = 0; i < ULL_SIZE; i++)
        if (binary_a[i] != binary_b[i])
            return false;

    return true;
}

// Driver code
int main()
{
    ull a = 4294967295;
    cout << isComplementAnagram(a) << endl;
    return 0;
}
```

输出:

```
1
```

**有效方法:**只需计算给定数字的位表示中存在的 1 的数量。如果存在的 1 的个数是 32，那么它的补码在它的位表示中也将有 32 个 1，它们将是彼此的字谜。

## C++

```
// An efficient C++ program to check if binary
// representations of a number and it's complement are anagram.
#include <bits/stdc++.h>
#define ull unsigned long long int
using namespace std;

const int ULL_SIZE = 8*sizeof(ull);

// Returns true if binary representations of
// a and b are anagram.
bool bit_anagram_check(ull a)
{
    // _popcnt64(a) gives number of 1's present
    // in binary representation of a. If number
    // of 1s is half of total bits, return true.
    return (_popcnt64(a) == (ULL_SIZE >> 1));
}

int main()
{
    ull a = 4294967295;
    cout << bit_anagram_check(a) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to check if binary
// representations of a number and it's complement are anagram.
class GFG
{

static byte longSize = 8;
static int ULL_SIZE = 8*longSize;

// Returns true if binary representations of
// a and b are anagram.
static boolean bit_anagram_check(long a)
{
    // _popcnt64(a) gives number of 1's present
    // in binary representation of a. If number
    // of 1s is half of total bits, return true.
    return (Integer.bitCount((int)a) == (ULL_SIZE >> 1));
}

// Driver code
public static void main(String[] args)
{
long a = 4294967295L;
    System.out.println(bit_anagram_check(a));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# An efficient Python3 program to check
# if binary representations of a number
# and it's complement are anagram.
ULL_SIZE = 64

# Returns true if binary representations of
# a and b are anagram.
def bit_anagram_check(a):

    #_popcnt64(a) gives number of 1's present
    # in binary representation of a. If number
    # of 1s is half of total bits, return true.
    return (bin(a).count("1") == (ULL_SIZE >> 1))

# Driver Code
a = 4294967295
print(int(bit_anagram_check(a)))

# This code is contributed by Mohit Kumar
```

## C#

```
// An efficient C# program to check
// if binary representations of
// a number and it's complement
// are anagram.
using System;

class GFG
{

static byte longSize = 8;
static int ULL_SIZE = 8*longSize;

// Returns true if binary representations of
// a and b are anagram.
static bool bit_anagram_check(long a)
{
    // _popcnt64(a) gives number of 1's present
    // in binary representation of a. If number
    // of 1s is half of total bits, return true.
    return (BitCount((int)a) == (ULL_SIZE >> 1));
}

static int BitCount(int n)
{
    int count = 0;
    while (n != 0)
    {
        count++;
        n &= (n - 1);
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    long a = 4294967295L;
    Console.WriteLine(bit_anagram_check(a));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program to check
// if binary representations of
// a number and it's complement
// are anagram.

// Returns true if binary representations
// of a and b are anagram.
function bit_anagram_check($a)
{
    $longSize = 8;
    $ULL_SIZE = 8 * $longSize;

    // _popcnt64(a) gives number of 1's present
    // in binary representation of a. If number
    // of 1s is half of total bits, return true.
    return (BitCount($a) == ($ULL_SIZE >> 1));
}

function BitCount($n)
{
    $count = 0;
    while ($n != 0)
    {
        $count++;
        $n &= ($n - 1);
    }
    return $count;
}

// Driver code
$a = 4294967295;
echo(bit_anagram_check($a));

// This code contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// An efficient javascript
// program to check if binary
// representations of a number and
// it's complement are anagram.

var longSize = 8;
var ULL_SIZE = 8*longSize;

// Returns true if binary representations of
// a and b are anagram.
function bit_anagram_check(a)
{
    // _popcnt64(a) gives number of 1's present
    // in binary representation of a. If number
    // of 1s is half of total bits, return true.
    var ans =a.toString(2).split('0').join('').length
    == (ULL_SIZE >> 1)?1:0;
    return ans;
}

// Driver code
var a = 4294967295;
document.write(bit_anagram_check(a));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
1
```

**注:**
1。答案只取决于数字，在上面的方法中我们甚至没有发现需要获得数字的补码。
2。上面的代码使用了 GCC 特定的函数。如果我们希望为其他编译器编写代码，我们可以使用[计数整数中的设置位。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
本文由 [**阿迪蒂亚·古普塔**](https://www.linkedin.com/in/aditya-gupta-437504a7?trk=hp-identity-name) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。