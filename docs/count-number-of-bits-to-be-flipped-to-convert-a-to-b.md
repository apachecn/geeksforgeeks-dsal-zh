# 计算将 A 转换为 B 需要翻转的位数

> 原文:[https://www . geesforgeks . org/count-要翻转的位数-转换为 a-b/](https://www.geeksforgeeks.org/count-number-of-bits-to-be-flipped-to-convert-a-to-b/)

给定两个数字“a”和“b”。编写一个程序，计算将“a”转换为“b”所需翻转的位数。
**例:**

```
Input : a = 10, b = 20
Output : 4
Binary representation of a is 00001010
Binary representation of b is 00010100
We need to flip highlighted four bits in a
to make it b.

Input : a = 7, b = 10
Output : 3
Binary representation of a is 00000111
Binary representation of b is 00001010
We need to flip highlighted three bits in a
to make it b.
```

```
  1\. Calculate XOR of A and B.      
        a_xor_b = A ^ B
  2\. Count the set bits in the above 
     calculated XOR result.
        countSetBits(a_xor_b)
```

两个数异或将仅在 A 与 b 不同的地方设置位

## C++

```
// Count number of bits to be flipped
// to convert A into B
#include <iostream>
using namespace std;

// Function that count set bits
int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        count++;
        n &= (n-1);
    }
    return count;
}

// Function that return count of
// flipped number
int FlippedCount(int a, int b)
{
    // Return count of set bits in
    // a XOR b
    return countSetBits(a^b);
}

// Driver code
int main()
{
    int a = 10;
    int b = 20;
    cout << FlippedCount(a, b)<<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Count number of bits to be flipped
// to convert A into B
import java.util.*;

class Count {

    // Function that count set bits
    public static int countSetBits(int n)
    {
        int count = 0;
        while (n != 0) {
            count++;
            n &=(n-1);
        }
        return count;
    }

    // Function that return count of
    // flipped number
    public static int FlippedCount(int a, int b)
    {
        // Return count of set bits in
        // a XOR b
        return countSetBits(a ^ b);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 10;
        int b = 20;
        System.out.print(FlippedCount(a, b));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Count number of bits to be flipped
# to convert A into B

# Function that count set bits
def countSetBits( n ):
    count = 0
    while n:
        count += 1
        n &= (n-1)
    return count

# Function that return count of
# flipped number
def FlippedCount(a , b):

    # Return count of set bits in
    # a XOR b
    return countSetBits(a^b)

# Driver code
a = 10
b = 20
print(FlippedCount(a, b))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// Count number of bits to be
// flipped to convert A into B
using System;

class Count {

    // Function that count set bits
    public static int countSetBits(int n)
    {
        int count = 0;
        while (n != 0) {
            count++;
            n &= (n-1);
        }
        return count;
    }

    // Function that return
    // count of flipped number
    public static int FlippedCount(int a, int b)
    {
    // Return count of set
    // bits in a XOR b
        return countSetBits(a ^ b);
    }

    // Driver code
    public static void Main()
    {
        int a = 10;
        int b = 20;
        Console.WriteLine(FlippedCount(a, b));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Count number of bits to be
// flipped to convert A into B

// Function that count set bits
function countSetBits($n)
{
    $count = 0;
    while($n)
    {
        $count += 1;
        $n &= (n-1);
    }
    return $count;
}

// Function that return
// count of flipped number
function FlippedCount($a, $b)
{
    // Return count of set
    // bits in a XOR b
    return countSetBits($a ^ $b);
}

// Driver code
$a = 10;
$b = 20;
echo FlippedCount($a, $b);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Count number of bits to be flipped
// to convert A into Bclass Count {

    // Function that count set bits
    function countSetBits(n) {
        var count = 0;
        while (n != 0) {
            count++;
            n &= (n - 1);
        }
        return count;
    }

    // Function that return count of
    // flipped number
    function FlippedCount(a , b) {
        // Return count of set bits in
        // a XOR b
        return countSetBits(a ^ b);
    }

    // Driver code
        var a = 10;
        var b = 20;
        document.write(FlippedCount(a, b));

// This code is contributed by shikhasingrajput
</script>
```

**Output**

```
4
```

#### 另一种方法:

## C++

```
// C++ program
#include <iostream>
using namespace std;

int countFlips(int a, int b)
{

  // initially flips is equal to 0
  int flips = 0;

  // & each bits of a && b with 1
  // and store them if t1 and t2
  // if t1 != t2 then we will flip that bit

  while(a > 0 || b > 0){

    int t1 = (a&1);
    int t2 = (b&1);

    if(t1!=t2){
      flips++;
    }
    // right shifting a and b
    a>>=1;
    b>>=1;
  }

  return flips;
}

int main () {
  int a = 10;
  int b = 20;
  cout <<countFlips(a, b);
}

// this code is contributed by shivanisinghss2110
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

// CONTRIBUTED BY PRAVEEN VISHWAKARMA

import java.io.*;

class GFG {

      public static int countFlips(int a, int b){
          // initially flips is equal to 0
        int flips = 0;

          // & each bits of a && b with 1
          // and store them if t1 and t2
        // if t1 != t2 then we will flip that bit

          while(a>0 || b>0){

            int t1 = (a&1);
              int t2 = (b&1);

              if(t1!=t2){
                flips++;
            }
              // right shifting a and b
              a>>>=1;
              b>>>=1;
        }

      return flips;
    }

    public static void main (String[] args) {
        int a = 10;
          int b = 20;
          System.out.println(countFlips(a, b));
    }

}
```

## 蟒蛇 3

```
def countFlips(a, b):

    # initially flips is equal to 0
    flips = 0

    # & each bits of a && b with 1
    # and store them if t1 and t2
    # if t1 != t2 then we will flip that bit
    while(a > 0 or b > 0):
        t1 = (a & 1)
        t2 = (b & 1)
        if(t1 != t2):
            flips += 1

        # right shifting a and b
        a>>=1
        b>>=1

    return flips

a = 10
b = 20
print(countFlips(a, b))

# This code is contributed by shivanisinghss2110
```

## C#

```
/*package whatever //do not write package name here */
using System;

class GFG {

      public static int countFlips(int a, int b)
      {

          // initially flips is equal to 0
        int flips = 0;

          // & each bits of a && b with 1
          // and store them if t1 and t2
        // if t1 != t2 then we will flip that bit       
          while(a > 0 || b > 0){

            int t1 = (a&1);
              int t2 = (b&1);

              if(t1 != t2){
                flips++;
            }
              // right shifting a and b
              a>>=1;
              b>>=1;
        }

      return flips;
    }

  // Driver code
    public static void Main (String[] args) {
        int a = 10;
          int b = 20;
          Console.Write(countFlips(a, b));
    }

}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
/*package whatever //do not write package name here */

function countFlips(a, b){
          // initially flips is equal to 0
        var flips = 0;

          // & each bits of a && b with 1
          // and store them if t1 and t2
        // if t1 != t2 then we will flip that bit

          while(a>0 || b>0){

            var t1 = (a&1);
              var t2 = (b&1);

              if(t1!=t2){
                flips++;
            }
              // right shifting a and b
              a>>>=1;
              b>>>=1;
        }

      return flips;
    }

          var a = 10;
          var b = 20;
          document.write(countFlips(a, b));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
4
```

感谢 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 提供以上实现。

要获得设置的比特数，请查看此帖子:[用整数计算设置的比特数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或将文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。