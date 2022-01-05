# 使用异或和查表计算一个数的奇偶性

> 原文:[https://www . geesforgeks . org/compute-parity-number-use-xor-table-look/](https://www.geeksforgeeks.org/compute-parity-number-using-xor-table-look/)

一个数的奇偶性是指它是包含奇数位还是偶数位。如果该数包含奇数个 1 位，则该数具有“奇数奇偶校验”，如果该数包含偶数个 1 位，则该数具有“偶数奇偶校验”。

```
1 --> parity of the set is odd
0 --> parity of the set is even
```

**示例:**

```
Input : 254
Output : Odd Parity
Explanation : Binary of 254 is 11111110\. 
There are 7 ones. Thus, parity is odd.

Input : 1742346774
Output : Even

```

**方法一:(天真的做法)**
这个方法我们已经讨论过了[这里](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-parity-of-an-unsigned-integer/)。

**方法二:(高效)**
先决条件:[查表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)[X-OR 魔法](https://www.geeksforgeeks.org/tag/xor/)

如果我们把一个数 S 分成两部分 S <sub>1</sub> 和 S <sub>2</sub> 这样**S = S<sub>1</sub>S<sub>2</sub>T9】。如果我们知道 S <sub>1</sub> 和 S <sub>2</sub> 的奇偶性，我们可以用以下事实计算 S 的奇偶性:**

1.  如果 S <sub>1</sub> 和 S <sub>2</sub> 具有相同的奇偶校验，即它们都具有偶数比特或奇数比特，它们的并集 S 将具有偶数比特。
2.  因此 S 的奇偶性是 S <sub>1</sub> 和 S <sub>2</sub> 奇偶性的异或

这个想法是创建一个查找表来存储所有 8 位数字的奇偶校验。然后通过将整数分成 8 个比特数并利用上述事实来计算它的奇偶性。

**步骤:**

```
1\. Create a look-up table for 8-bit numbers ( 0 to 255 )
   Parity of 0 is 0.
   Parity of 1 is 1.
   .
   .
   .
   Parity of 255 is 0.
2\. Break the number into 8-bit chunks
   while performing XOR operations.
3\. Check for the result in the table for
    the 8-bit number.

```

由于 32 位或 64 位数字包含恒定的字节数，上述步骤需要 0(1)时间。

**示例:**

```
1\. Take 32-bit number : 1742346774

2\. Calculate Binary of the number : 
   01100111110110100001101000010110

3\. Split the 32-bit binary representation into 
  16-bit chunks :
0110011111011010 | 0001101000010110 

4\. Compute X-OR :
  0110011111011010
^ 0001101000010110
___________________
= 0111110111001100

5\. Split the 16-bit binary representation 
   into 8-bit chunks : 01111101 | 11001100

6\. Again, Compute X-OR :
  01111101
^ 11001100
___________________
= 10110001
10110001 is 177 in decimal. Check
 for its parity in look-up table :
Even number of 1 = Even parity.

Thus, Parity of 1742346774 is even.

```

下面是**对 32 位和 64 位**数字都有效的实现。

## C++

```
// CPP program to illustrate Compute the parity of a
// number using XOR
#include <bits/stdc++.h>

// Generating the look-up table while pre-processing
#define P2(n) n, n ^ 1, n ^ 1, n
#define P4(n) P2(n), P2(n ^ 1), P2(n ^ 1), P2(n)
#define P6(n) P4(n), P4(n ^ 1), P4(n ^ 1), P4(n)
#define LOOK_UP P6(0), P6(1), P6(1), P6(0)

// LOOK_UP is the macro expansion to generate the table
unsigned int table[256] = { LOOK_UP };

// Function to find the parity
int Parity(int num)
{
    // Number is considered to be of 32 bits
    int max = 16;

    // Dividing the number into 8-bit
    // chunks while performing X-OR
    while (max >= 8) {
        num = num ^ (num >> max);
        max = max / 2;
    }

    // Masking the number with 0xff (11111111)
    // to produce valid 8-bit result
    return table[num & 0xff];
}

// Driver code
int main()
{
    unsigned int num = 1742346774;

    // Result is 1 for odd parity, 0 for even parity
    bool result = Parity(num);

    // Printing the desired result
    result ? std::cout << "Odd Parity" :
             std::cout << "Even Parity";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to illustrate Compute the 
# parity of a number using XOR 

# Generating the look-up table while 
# pre-processing 
def P2(n, table):
    table.extend([n, n ^ 1, n ^ 1, n])
def P4(n, table):
    return (P2(n, table), P2(n ^ 1, table), 
            P2(n ^ 1, table), P2(n, table))
def P6(n, table):
    return (P4(n, table), P4(n ^ 1, table),
            P4(n ^ 1, table), P4(n, table)) 
def LOOK_UP(table):
    return (P6(0, table), P6(1, table),
            P6(1, table), P6(0, table)) 

# LOOK_UP is the macro expansion to
# generate the table 
table = [0] * 256
LOOK_UP(table)

# Function to find the parity 
def Parity(num) :

    # Number is considered to be
    # of 32 bits 
    max = 16

    # Dividing the number o 8-bit 
    # chunks while performing X-OR 
    while (max >= 8): 
        num = num ^ (num >> max) 
        max = max // 2

    # Masking the number with 0xff (11111111) 
    # to produce valid 8-bit result 
    return table[num & 0xff] 

# Driver code 
if __name__ =="__main__":
    num = 1742346774

    # Result is 1 for odd parity, 
    # 0 for even parity 
    result = Parity(num)
    print("Odd Parity") if result else print("Even Parity")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to illustrate
// Compute the parity of a
// number using XOR

/* Generating the look-up 
table while pre-processing
#define P2(n) n, n ^ 1, n ^ 1, n
#define P4(n) P2(n), P2(n ^ 1), 
              P2(n ^ 1), P2(n)
#define P6(n) P4(n), P4(n ^ 1), 
              P4(n ^ 1), P4(n)
#define LOOK_UP P6(0), P6(1), 
                P6(1), P6(0)

LOOK_UP is the macro expansion
to generate the table
$table = array(LOOK_UP );
*/

// Function to find
// the parity
function Parity($num)
{
    global $table;

    // Number is considered 
    // to be of 32 bits
    $max = 16;

    // Dividing the number 
    // into 8-bit chunks 
    // while performing X-OR
    while ($max >= 8) 
    {
        $num = $num ^ ($num >> $max);
        $max = (int)$max / 2;
    }

    // Masking the number with 
    // 0xff (11111111) to produce
    // valid 8-bit result
    return $table[$num & 0xff];
}

// Driver code
$num = 1742346774;

// Result is 1 for odd 
// parity, 0 for even parity
$result = Parity($num);

// Printing the desired result
if($result == true)
        echo "Odd Parity" ;
    else
        echo"Even Parity";

// This code is contributed by ajit
?>
```

**Output:**

```
Even Parity

```

**时间复杂度:** O(1)。请注意，32 位或 64 位数字具有固定的字节数(32 位为 4，64 位为 8)。

本文由 **[罗希特·塔普利亚尔](https://www.linkedin.com/in/rohit-thapliyal-515b5913a/)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。