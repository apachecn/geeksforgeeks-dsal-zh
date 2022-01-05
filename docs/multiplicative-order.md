# 乘法顺序

> 原文:[https://www.geeksforgeeks.org/multiplicative-order/](https://www.geeksforgeeks.org/multiplicative-order/)

在数论中，给定一个整数 a 和一个具有 gcd( A，N) = 1 的正整数 n，模 n 的乘法阶是具有 A^k(模 N ) = 1 的最小正整数 k。(0 < K < N)

**示例:**

```
Input : A = 4 , N = 7 
Output : 3
explanation :  GCD(4, 7) = 1  
               A^k( mod N ) = 1 ( smallest positive integer K )
               4^1 = 4(mod 7)  = 4
               4^2 = 16(mod 7) = 2
               4^3 = 64(mod 7)  = 1
               4^4 = 256(mod 7) = 4
               4^5 = 1024(mod 7)  = 2
               4^6 = 4096(mod 7)  = 1

smallest positive integer K = 3  

Input :  A = 3 , N = 1000 
Output : 100  (3^100 (mod 1000) == 1) 

Input : A = 4 , N = 11 
Output : 5 
```

如果我们仔细观察，我们会发现我们不需要每次都计算功率。我们可以通过将“A”乘以一个模块的前一个结果来获得下一个幂。

```
Explanation : 
A = 4 , N = 11  
initially result = 1 
with normal                with modular arithmetic (A * result)
4^1 = 4 (mod 11 ) = 4  ||  4 * 1 = 4 (mod 11 ) = 4 [ result = 4]
4^2 = 16(mod 11 ) = 5  ||  4 * 4 = 16(mod 11 ) = 5 [ result = 5]
4^3 = 64(mod 11 ) = 9  ||  4 * 5 = 20(mod 11 ) = 9 [ result = 9]
4^4 = 256(mod 11 )= 3  ||  4 * 9 = 36(mod 11 ) = 3 [ result = 3]
4^5 = 1024(mod 5 ) = 1 ||  4 * 3 = 12(mod 11 ) = 1 [ result = 1]

smallest positive integer  5 
```

运行一个从 1 到 N-1 的循环，在模 N 等于 1 的情况下返回 A 的最小+ve 次幂。

以下是上述想法的实现。

## C++

```
// C++ program to implement multiplicative order
#include<bits/stdc++.h>
using namespace std;

// function for GCD
int GCD ( int a , int b )
{
    if (b == 0 )
        return a;
    return GCD( b , a%b ) ;
}

// Function return smallest +ve integer that
// holds condition A^k(mod N ) = 1
int multiplicativeOrder(int A, int  N)
{
    if (GCD(A, N ) != 1)
        return -1;

    // result store power of A that rised to
    // the power N-1
    unsigned int result = 1;

    int K = 1 ;
    while (K < N)
    {
        // modular arithmetic
        result = (result * A) % N ;

        // return smallest +ve integer
        if (result  == 1)
            return K;

        // increment power
        K++;
    }

    return -1 ;
}

//driver program to test above function
int main()
{
    int A = 4 , N = 7;
    cout << multiplicativeOrder(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement multiplicative order
import java.io.*;

class GFG {

    // function for GCD
    static int GCD(int a, int b) {

        if (b == 0)
            return a;

        return GCD(b, a % b);
    }

    // Function return smallest +ve integer that
    // holds condition A^k(mod N ) = 1
    static int multiplicativeOrder(int A, int N) {

        if (GCD(A, N) != 1)
            return -1;

        // result store power of A that rised to
        // the power N-1
        int result = 1;

        int K = 1;

        while (K < N) {

            // modular arithmetic
            result = (result * A) % N;

            // return smallest +ve integer
            if (result == 1)
                return K;

            // increment power
            K++;
        }

        return -1;
    }

    // driver program to test above function
    public static void main(String args[]) {

        int A = 4, N = 7;

        System.out.println(multiplicativeOrder(A, N));
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to implement
# multiplicative order

# function for GCD
def GCD (a, b ) :
    if (b == 0 ) :
        return a
    return GCD( b, a % b )

# Function return smallest + ve
# integer that holds condition
# A ^ k(mod N ) = 1
def multiplicativeOrder(A, N) :
    if (GCD(A, N ) != 1) :
        return -1

    # result store power of A that rised
    # to the power N-1
    result = 1

    K = 1
    while (K < N) :

        # modular arithmetic
        result = (result * A) % N

        # return smallest + ve integer
        if (result == 1) :
            return K

        # increment power
        K = K + 1

    return -1

# Driver program
A = 4
N = 7
print(multiplicativeOrder(A, N))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to implement multiplicative order
using System;

class GFG {

    // function for GCD
    static int GCD(int a, int b)
    {

        if (b == 0)
            return a;

        return GCD(b, a % b);
    }

    // Function return smallest +ve integer
    // that holds condition A^k(mod N ) = 1
    static int multiplicativeOrder(int A, int N)
    {

        if (GCD(A, N) != 1)
            return -1;

        // result store power of A that
        // rised to the power N-1
        int result = 1;

        int K = 1;

        while (K < N)
        {

            // modular arithmetic
            result = (result * A) % N;

            // return smallest +ve integer
            if (result == 1)
                return K;

            // increment power
            K++;
        }

        return -1;
    }

    // Driver Code
    public static void Main()
    {

        int A = 4, N = 7;

        Console.Write(multiplicativeOrder(A, N));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// multiplicative order

// function for GCD
function GCD ( $a , $b )
{
    if ($b == 0 )
        return $a;
    return GCD( $b , $a % $b ) ;
}

// Function return smallest
// +ve integer that holds
// condition A^k(mod N ) = 1
function multiplicativeOrder($A, $N)
{
    if (GCD($A, $N ) != 1)
        return -1;

    // result store power of A
    // that rised to the power N-1
    $result = 1;

    $K = 1 ;
    while ($K < $N)
    {
        // modular arithmetic
        $result = ($result * $A) % $N ;

        // return smallest +ve integer
        if ($result == 1)
            return $K;

        // increment power
        $K++;
    }

    return -1 ;
}

// Driver Code
$A = 4; $N = 7;
echo(multiplicativeOrder($A, $N));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to implement
// multiplicative order

    // function for GCD
    function GCD(a, b) {

        if (b == 0)
            return a;

        return GCD(b, a % b);
    }

    // Function return smallest +ve integer that
    // holds condition A^k(mod N ) = 1
    function multiplicativeOrder(A, N) {

        if (GCD(A, N) != 1)
            return -1;

        // result store power of A that rised to
        // the power N-1
        let result = 1;

        let K = 1;

        while (K < N) {

            // modular arithmetic
            result = (result * A) % N;

            // return smallest +ve integer
            if (result == 1)
                return K;

            // increment power
            K++;
        }

        return -1;
    }

// Driver Code
    let A = 4, N = 7;

    document.write(multiplicativeOrder(A, N));

 // This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(N)

参考:[https://en.wikipedia.org/wiki/Multiplicative_order](https://en.wikipedia.org/wiki/Multiplicative_order)

本文由 [**尼尚·辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。