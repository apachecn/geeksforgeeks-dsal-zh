# Brahmagupta Fibonacci 身份

> 哎哎哎::1230【https://www . geeksforgeeks . org/brahmagupta-Fibonacci-identity/

[婆罗门格普塔斐波那契恒等式](https://en.wikipedia.org/wiki/Brahmagupta%E2%80%93Fibonacci_identity)表示两个数的乘积，每个数都是 2 个平方的和，可以用 2 种不同的形式表示为 2 个平方的和。
**数学上，**

> 如果 a = p^2 + q^2，b = r^2 + s^2
> 那么 a * b 可以写成两种不同的形式:
> =(p^2+q^2)*(r^2+s^2)
> =(pr–QS)2+(PS+QR)2 ……( 1)
> =(pr+QS)2+(PS–QR)2 ………( 2)

一些**例子**是:

> a = 5(= 1^2+2^2)
> b = 25(= 3^2+4^2)
> a*b = 125
> a * b 表示为 2 个正方形之和:
> 2^2+11^2 = 125
> 5^2+10^2 = 125
> em>**解释:**t8】a = 5 和 b = 25 每个都可以表示为 2 个正方形之和，它们的积 a * b 为 125 可以表示为两个不同形式的 2 个正方形之和。这是根据
> 的梵天斐波那契恒等式，满足恒等式条件。
> a = 13(= 2^2+3^2)
> b = 41(= 4^2+5^2)
> a*b = 533
> 将 a * b 表示为 2 个正方形之和:
> 2^2+23^2 = 533
> 7^2+22^2 = 533
> a = 85(= 6 2+7 2)
> b = 41(= 4 2+5 2)
> a * b = 3485
> 将 a * b 表示为

下面是一个程序，用于验证给定的两个数字的梵天斐波那契恒等式，这两个数字是两个正方形的和。

## C++

```
// CPP code to verify
// Brahmagupta Fibonacci identity
#include <bits/stdc++.h>
using namespace std;

void find_sum_of_two_squares(int a,
                             int b)
{
    int ab = a*b;

    // represent the product
    // as sum of 2 squares
    for (int i = 0; i * i <= ab; i++)
    {
        for (int j = i; i * i +
                        j * j <= ab; j++)
        {

            // check identity criteria
            if (i * i + j * j == ab)
                cout << i << "^2 + " << j
                     << "^2 = " << ab << "\n";
        }
    }
}

// Driver code
int main()
{
    // 1^2 + 2^2
    int a = 1 * 1 + 2 * 2;

    // 3^2 + 4^2
    int b = 3 * 3 + 4 * 4;

    cout << "Representation of a * b as sum"
            " of 2 squares:\n";

    // express product of sum of 2 squares
    // as sum of (sum of 2 squares)
    find_sum_of_two_squares(a, b);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to verify Brahmagupta
// Fibonacci identity

class GFG
{
    static void find_sum_of_two_squares(int a,
                                        int b)
{
    int ab = a * b;

    // represent the product
    // as sum of 2 squares
    for (int i = 0; i * i <= ab; i++)
    {
        for (int j = i; i * i +
                        j * j <= ab; j++)
        {
            // check identity criteria
            if (i * i + j * j == ab)
                System.out.println(i + "^2 + " +
                                   j +"^2 = " + ab);
        }
    }
}

// Driver code
public static void main(String[] args)
{
    // 1^2 + 2^2
    int a = 1 * 1 + 2 * 2;

    // 3^2 + 4^2
    int b = 3 * 3 + 4 * 4;

    System.out.println("Representation of a * b " +
                        "as sum of 2 squares:");

    // express product of sum
    // of 2 squares as sum of
    // (sum of 2 squares)
    find_sum_of_two_squares(a, b);
}
}

// This code is contributed
// by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 code to verify
# Brahmagupta Fibonacci identity

def find_sum_of_two_squares(a, b):

    ab = a * b

    # represent the product
    # as sum of 2 squares
    i=0;
    while(i * i <= ab):
        j = i
        while(i * i + j * j <= ab):

            # check identity criteria
            if (i * i + j * j == ab):
                print(i,"^2 + ",j,"^2 = ",ab)
            j += 1
        i += 1

# Driver code
a = 1 * 1 + 2 * 2 # 1^2 + 2^2
b = 3 * 3 + 4 * 4 # 3^2 + 4^2

print("Representation of a * b as sum"
                     " of 2 squares:")

# express product of sum of 2 squares
# as sum of (sum of 2 squares)
find_sum_of_two_squares(a, b)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# code to verify Brahmagupta
// Fibonacci identity
using System;

class GFG
{
    static void find_sum_of_two_squares(int a,
                                        int b)
    {
    int ab = a * b;

    // represent the product
    // as sum of 2 squares
    for (int i = 0; i * i <= ab; i++)
    {
        for (int j = i; i * i +
                        j * j <= ab; j++)
        {
            // check identity criteria
            if (i * i + j * j == ab)
                Console.Write(i + "^2 + " + j +
                          "^2 = " + ab + "\n");
        }
    }
}

// Driver code
public static void Main()
{
    // 1^2 + 2^2
    int a = 1 * 1 + 2 * 2;

    // 3^2 + 4^2
    int b = 3 * 3 + 4 * 4;

    Console.Write("Representation of a * b " +
                   "as sum of 2 squares:\n");

    // express product of sum of
    // 2 squares as sum of (sum of
    // 2 squares)
    find_sum_of_two_squares(a, b);
}
}

// This code is contributed
// by Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to verify
// Brahmagupta Fibonacci identity

function find_sum_of_two_squares($a, $b)
{
    $ab = $a * $b;

    // represent the product
    // as sum of 2 squares
    for ($i = 0; $i * $i <= $ab; $i++)
    {
        for ($j = $i; $i * $i +
                      $j * $j <= $ab; $j++)
        {

            // check identity criteria
            if ($i * $i + $j * $j == $ab)
                echo $i ,"^2 + ", $j ,
                     "^2 = " , $ab ,"\n";
        }
    }
}

// Driver code
// 1^2 + 2^2
$a = 1 * 1 + 2 * 2;

// 3^2 + 4^2
$b = 3 * 3 + 4 * 4;

echo "Representation of a * b ".
     "as sum of 2 squares:\n";

// express product of sum of
// 2 squares as sum of (sum
// of 2 squares)
find_sum_of_two_squares($a, $b);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to verify Brahmagupta
// Fibonacci identity

    function find_sum_of_two_squares(a, b)
{
     let ab = a * b;

    // represent the product
    // as sum of 2 squares
    for (let i = 0; i * i <= ab; i++)
    {
        for (let j = i; i * i +
                        j * j <= ab; j++)
        {
            // check identity criteria
            if (i * i + j * j == ab)
                document.write(i + "^2 + " +
                                   j +"^2 = " + ab + "<br/>");
        }
    }
}

// Driver code

     // 1^2 + 2^2
    let a = 1 * 1 + 2 * 2;

    // 3^2 + 4^2
    let b = 3 * 3 + 4 * 4;

     document.write("Representation of a * b " +
                        "as sum of 2 squares:" + "<br/>");

    // express product of sum
    // of 2 squares as sum of
    // (sum of 2 squares)
    find_sum_of_two_squares(a, b);

    // This code is contributed by code_hunt.
</script>
```

**Output :** 

```
Representation of a * b as sum of 2 squares:
2^2 + 11^2 = 125
5^2 + 10^2 = 125
```