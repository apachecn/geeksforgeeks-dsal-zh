# 求整数的补码

> 原文:[https://www.geeksforgeeks.org/find-ones-complement-integer/](https://www.geeksforgeeks.org/find-ones-complement-integer/)

给定一个整数 n，求该整数的补数。
**例:**

```
Input  : n = 5
Output : 2

Input  : n = 255
Output : 0

Input  : n = 26
Output : 5
```

**基本方法:**

解决这个问题的天真方法是首先把给定的数字转换成它的二进制表示，然后把每一个 1 变成 0，0 变成 1。更改所有 0 和 1 后，将二进制表示转换为数字。

**实施上述方法:**

## C++

```
// CPP program to find 1's complement of n.
#include <bits/stdc++.h>
using namespace std;

unsigned int onesComplement(unsigned int n)
{
    vector<int> v;
    // convert to binary representation
    while (n != 0) {
        v.push_back(n % 2);
        n = n / 2;
    }
    reverse(v.begin(), v.end());
    // change 1's to 0 and 0's to 1
    for (int i = 0; i < v.size(); i++) {
        if (v[i] == 0)
            v[i] = 1;
        else
            v[i] = 0;
    }
    // convert back to number representation
    int two = 1;
    for (int i = v.size() - 1; i >= 0; i--) {
        n = n + v[i] * two;
        two = two * 2;
    }
    return n;
}

int main()
{
    unsigned int n = 22;
    cout << onesComplement(n);
    return 0;
}
```

**Output**

```
9
```

解决这个问题的有效方法如下:
1。求给定整数
2 中的位数。将给定整数与 2^number_of_bits-1
进行异或运算

## C++

```
// CPP program to find 1's complement of n.
#include<bits/stdc++.h>
using namespace std;

unsigned int onesComplement(unsigned int n)
{
   // Find number of bits in the given integer
   int number_of_bits = floor(log2(n))+1;

   // XOR the given integer with poe(2,
   // number_of_bits-1 and print the result
   return ((1 << number_of_bits) - 1) ^ n;
}

int main()
{
  unsigned int n = 22;
  cout << onesComplement(n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 1's complement of n.
class GFG {

    static int onesComplement(int n)
    {

        // Find number of bits in the
        // given integer
        int number_of_bits =
               (int)(Math.floor(Math.log(n) /
                             Math.log(2))) + 1;

        // XOR the given integer with poe(2,
        // number_of_bits-1 and print the result
        return ((1 << number_of_bits) - 1) ^ n;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 22;

        System.out.print(onesComplement(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# 1's complement of n.
import math

def onesComplement(n):

    # Find number of bits in
    # the given integer
    number_of_bits = (int)(math.floor(math.log(n) /
                                math.log(2))) + 1;

    # XOR the given integer with poe(2,
    # number_of_bits-1 and print the result
    return ((1 << number_of_bits) - 1) ^ n;

# Driver code
n = 22
print(onesComplement(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find 1's complement of n.
using System;

class GFG {

    static int onesComplement(int n)
    {

       // Find number of bits in the given integer
       int number_of_bits = (int)(Math.Floor(
                   Math.Log(n) / Math.Log(2))) + 1;

       // XOR the given integer with poe(2,
       // number_of_bits-1 and print the result
       return ((1 << number_of_bits) - 1) ^ n;
    }

    //Driver code
    public static void Main ()
    {

        int n = 22;

        Console.WriteLine(onesComplement(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find 1's
// complement of n.

function Log2($x)
{
    return (log10($x) / log10(2));
}

function onesComplement($n)
{

// Find number of bits in
// the given integer
$number_of_bits = floor(log2($n)) + 1;

// XOR the given integer with
// number_of_bits-1 and print the result
return ((1 << $number_of_bits) - 1) ^ $n;
}

// Driver Code
$n = 22;
echo onesComplement($n);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// 1's complement of n.

// Function to check whether a
// number is power of 2 or not
function onesComplement(n)
    {

        // Find number of bits in the
        // given integer
        let number_of_bits =
               (Math.floor(Math.log(n) /
                           Math.log(2))) + 1;

        // XOR the given integer with poe(2,
        // number_of_bits-1 and print the result
        return ((1 << number_of_bits) - 1) ^ n;
    }

// driver program

    let n = 22;

    document.write(onesComplement(n));

</script>
```

**Output**

```
9
```

https://youtu.be/bcA

-52W5vAk
本文由 [**阿米特 S K**](https://auth.geeksforgeeks.org/profile.php?user=Amit S K) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。