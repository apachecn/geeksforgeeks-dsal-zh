# 计算从 1 到 n 的异或

> 原文:[https://www.geeksforgeeks.org/calculate-xor-1-n/](https://www.geeksforgeeks.org/calculate-xor-1-n/)

给定一个数字 n，任务是找出从 1 到 n 的异或。
**例:**

```
Input : n = 6
Output : 7
// 1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 6  = 7

Input : n = 7
Output : 0
// 1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 6 ^ 7 = 0
```

**方法 1(天真方法):**
1-将结果初始化为 0。
1-遍历从 1 到 n 的所有数字。
2-对数字逐个进行异或运算，得到结果。
3-最后，返回结果。
**方法 2(有效方法):**
1-用 4 对 n 进行模运算，求 n 的余数。
2-如果 rem = 0，则异或等于 n。
3-如果 rem = 1，则异或等于 1。
4-如果 rem = 2，那么异或将为 n+1。
5-如果 rem = 3，则异或为 0。

## C++

```
// C++ program to find XOR of numbers
// from 1 to n.
#include<bits/stdc++.h>
using namespace std;

// Method to calculate xor
int computeXOR(int n)
{

  // If n is a multiple of 4
  if (n % 4 == 0)
    return n;

  // If n%4 gives remainder 1
  if (n % 4 == 1)
    return 1;

  // If n%4 gives remainder 2
  if (n % 4 == 2)
    return n + 1;

  // If n%4 gives remainder 3
  return 0;
}

// Driver method
int main()
{
  int n = 5;
  cout<<computeXOR(n);
}

// This code is contributed by rutvik_56.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of numbers
// from 1 to n.

class GFG
{
    // Method to calculate xor
    static int computeXOR(int n)
    {
        // If n is a multiple of 4
        if (n % 4 == 0)
            return n;

        // If n%4 gives remainder 1
        if (n % 4 == 1)
            return 1;

        // If n%4 gives remainder 2
        if (n % 4 == 2)
            return n + 1;

        // If n%4 gives remainder 3
        return 0;
    }

    // Driver method
    public static void main (String[] args)
    {
         int n = 5;
         System.out.println(computeXOR(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to find
# XOR of numbers from 1 to n.

# Function to calculate xor
def computeXOR(n) :

    # Modulus operator are expensive
    # on most of the computers. n & 3
    # will be equivalent to n % 4.

    # if n is multiple of 4
    if n % 4 == 0 :
        return n

    # If n % 4 gives remainder 1
    if n % 4 == 1 :
        return 1

    # If n%4 gives remainder 2
    if n % 4 == 2 :
        return n + 1

    # If n%4 gives remainder 3
    return 0

# Driver Code
if __name__ == "__main__" :

    n = 5

    # function calling
    print(computeXOR(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find XOR
// of numbers from 1 to n.
using System;

class GFG
{

    // Method to calculate xor
    static int computeXOR(int n)
    {
        // If n is a multiple of 4
        if (n % 4 == 0)
            return n;

        // If n%4 gives remainder 1
        if (n % 4 == 1)
            return 1;

        // If n%4 gives remainder 2
        if (n % 4 == 2)
            return n + 1;

        // If n%4 gives remainder 3
        return 0;
    }

    // Driver Code
    static public void Main ()
    {
        int n = 5;
        Console.WriteLine(computeXOR(n));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find XOR
// of numbers from 1 to n.

// Function to calculate xor
function computeXOR($n)
{
    // Modulus operator are expensive
    // on most of the computers. n & 3
    // will be equivalent to n % 4.

    switch($n & 3) // n % 4
    {
    // if n is multiple of 4
    case 0: return $n;

    // If n % 4 gives remainder 1
    case 1: return 1;

    // If n % 4 gives remainder 2
    case 2: return $n + 1; 

    // If n % 4 gives remainder 3
    case 3: return 0;
    }
}

// Driver code
$n = 5;
echo computeXOR($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to find XOR of numbers
// from 1 to n.

// Function to calculate xor
function computeXOR(n)
{
    // Modulus operator are expensive on most of the
    // computers. n & 3 will be equivalent to n % 4.

    // if n is multiple of 4
    if(n % 4 == 0)
        return n;   
    // If n % 4 gives remainder 1    
    if(n % 4 == 1)
        return 1;   
    // If n % 4 gives remainder 2   
    if(n % 4 == 2)
        return n + 1; 
    // If n % 4 gives remainder 3
    if(n % 4 == 3)
        return 0;    

}

// Driver code

    // your code goes here
    let n = 5;
    document.write(computeXOR(n));

// This code is constributed by Surbhi Tyagi.

</script>
```

**输出:**

```
1
```

时间复杂度:0(1)

辅助空间:0(1)

**这是如何工作的？**
当我们对数字进行异或运算时，我们在 4 的倍数之前得到 0 作为异或值。这在每 4 的倍数之前不断重复。

```
Number Binary-Repr  XOR-from-1-to-n
1         1           [0001]
2        10           [0011]
3        11           [0000]  <----- We get a 0
4       100           [0100]  <----- Equals to n
5       101           [0001]
6       110           [0111]
7       111           [0000]  <----- We get 0
8      1000           [1000]  <----- Equals to n
9      1001           [0001]
10     1010           [1011]
11     1011           [0000] <------ We get 0
12     1100           [1100] <------ Equals to n
```

本文由[萨希尔·查布拉](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。