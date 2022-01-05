# 求给定积和差的 N 个整数

> 原文:[https://www . geesforgeks . org/find-n-整数-给定-差-积-和/](https://www.geeksforgeeks.org/find-n-integers-given-difference-product-sum/)

给定两个整数 N 和 D，找到一组 N 个整数，使得它们的乘积和之差等于 D。
示例:

```
Input : N = 2, D = 1
Output : 2 3
Explanation: 
product = 2*3 = 6,
Sum = 2 + 3 = 5.
Hence, 6 - 5 = 1(D).

Input : N = 3, D = 5.
Output : 1 2 8
Explanation :
Product = 1*2*8 = 16
Sum = 1+2+8 = 11.
Hence, 16-11 = 5(D).
```

一个棘手的解决方案是保留差 D，选择 N 个数字作为 N-2 '1 '，一个' 2 '和一个剩余的数字作为' N+D '。
和= (N-2)*(1) + 2 + (N+D) = 2*N + D.
积= 1*2*(N+D) = 2*N+2*D
差=(2 * N+2 * D)–(2 * N+D)= D .

## C++

```
// CPP code to generate numbers
// with difference between
// product and sum is D
#include <iostream>
using namespace std;

// Function to implement calculation
void findNumbers(int n, int d)
{
    for (int i = 0; i < n - 2; i++)
        cout << "1"  << " ";

    cout << "2" << " ";
    cout << n + d << endl;
}

// Driver code
int main()
{
    int N = 3, D = 5;
    findNumbers(N, D);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to generate numbers
// with difference between
// product and sum is D
import java.io.*;

class GFG {

    // Function to implement calculation
    static void findNumbers(int n, int d)
    {
        for (int i = 0; i < n - 2; i++)
            System.out.print("1" + " ");

        System.out.print("2" + " ");
        System.out.println(n + d);
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 3, D = 5;
        findNumbers(N, D);
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 code to generate numbers with
# difference between product and sum is D

# Function to implement calculation
def pattern(n, d) :

    for i in range(0, n - 2) :
        print("1", end=" ")

    print("2", end=" ")
    print(n + d)

# Driver code
N = 3
D = 5
pattern(N, D)

# This code is contributed by 'Akanshgupta'
```

## C#

```
// C# code to generate numbers
// with difference between
// product and sum is D
using System;

class GFG {

    // Function to implement calculation
    static void findNumbers(int n, int d)
    {
        for (int i = 0; i < n - 2; i++)
        Console.Write("1" + " ");

        Console.Write("2" + " ");
        Console.Write(n + d);
    }

    // Driver code
    public static void Main()
    {
        int N = 3, D = 5;
        findNumbers(N, D);
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to generate numbers
// with difference between
// product and sum is D

// Function to implement
// calculation
function findNumbers($n, $d)
{
    for ($i = 0; $i < $n - 2; $i++)
        echo "1" ," ";

    echo "2" , " ";
    echo $n + $d ,"\n";
}

    // Driver Code
    $N = 3;
    $D = 5;
    findNumbers($N, $D);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to generate numbers
// with difference between
// product and sum is D

// Function to implement calculation
    function findNumbers(n, d)
    {
        for (let i = 0; i < n - 2; i++)
            document.write("1" + " ");

        document.write("2" + " ");
       document.write(n + d);
    }

// Driver code

        let N = 3, D = 5;
        findNumbers(N, D);

</script>
```

**输出:**

```
 1 2 8
```