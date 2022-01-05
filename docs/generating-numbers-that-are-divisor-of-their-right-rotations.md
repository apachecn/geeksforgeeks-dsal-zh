# 生成右旋转除数

> 原文:[https://www . geesforgeks . org/generating-numbers-这些数字是它们右旋转的除数/](https://www.geeksforgeeks.org/generating-numbers-that-are-divisor-of-their-right-rotations/)

给定一个数 m，找出所有有 m 位数并且是其右旋转除数的数。数字 N 的右旋转是将 N 的数字向右旋转一个位置，并将最低有效数字环绕，使其成为最高有效数字的结果。例如，4356 的右旋转是 6435。

**示例:**

```
Input: 2
Output:
11
22
33
44
55
66
77
88
99

Input: 6
Output:
102564
111111
128205
142857
153846
179487
205128
222222
230769
333333
444444
555555
666666
777777
888888
999999

128205 satisfies the condition as 128205 * 4 = 512820.
```

**蛮力法** :
最简单的方法是遍历所有大于等于 10 <sup>m-1</sup> 小于 10 <sup>m</sup> 的数字，检查是否满足要求的条件。我们可以用常数时间来检查，所以整个过程的时间复杂度为 O(10 <sup>m</sup> ，只对 m 的小值可行
**以下是上述** **方法的实现:**

## C++

```
// C++ program to Generating numbers that
// are divisor of their right-rotations

#include <bits/stdc++.h>
using namespace std;

// Function to check if N is a
// divisor of its right-rotation

bool rightRotationDivisor(int N)
{
    int lastDigit = N % 10;
    int rightRotation = (lastDigit * pow(10 ,int(log10(N))))
                    + floor(N / 10);
    return (rightRotation % N == 0);
}

// Function to generate m-digit
// numbers which are divisor of
// their right-rotation
void generateNumbers(int m)
{
    for (int i=pow(10,(m - 1));i<pow(10 , m);i++)
        if (rightRotationDivisor(i))
            cout<<i<<endl;
 }

// Driver code
int main()
{
int m = 3;
generateNumbers(m);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Generating numbers that 
// are divisor of their right-rotations  

public class GFG {

    // Function to check if N is a 
    // divisor of its right-rotation
    static boolean rightRotationDivisor(int N)
    {
        int lastDigit = N % 10;
        int rightRotation = (int)(lastDigit * Math.pow(10 ,(int)(Math.log10(N))) 
                        + Math.floor(N / 10)); 
        return (rightRotation % N == 0);
    }

    // Function to generate m-digit 
    // numbers which are divisor of 
    // their right-rotation 
    static void generateNumbers(int m)
    {
        for (int i= (int)Math.pow(10,(m - 1)); i < Math.pow(10 , m);i++) 
            if (rightRotationDivisor(i))
                System.out.println(i);
     }

    // Driver code
    public static void main(String args[])
    {
        int m = 3;
        generateNumbers(m);

    }
    // This Code is contributed by ANKITRAI1
}

```

## 蟒蛇 3

```
# Python program to Generating numbers that are
# divisor of their right-rotations

from math import log10

# Function to check if N is a
# divisor of its right-rotation
def rightRotationDivisor(N):
    lastDigit = N % 10
    rightRotation = (lastDigit * 10 ** int(log10(N))
                    + N // 10)
    return rightRotation % N == 0

# Function to generate m-digit
# numbers which are divisor of
# their right-rotation
def generateNumbers(m):
    for i in range(10 ** (m - 1), 10 ** m):
        if rightRotationDivisor(i):
            print(i)

# Driver code
m = 3
generateNumbers(m)
```

## C#

```
// C# program to Generating numbers that
// are divisor of their right-rotations 

using System;
public class GFG{

    // Function to check if N is a
    // divisor of its right-rotation
    static bool rightRotationDivisor(int N)
    {
        int lastDigit = N % 10;
        int rightRotation = (int)(lastDigit * Math.Pow(10 ,(int)(Math.Log10(N)))
                        + Math.Floor((double)N/10));
        return (rightRotation % N == 0);
    }

    // Function to generate m-digit
    // numbers which are divisor of
    // their right-rotation
    static void generateNumbers(int m)
    {
        for (int i= (int)Math.Pow(10,(m - 1)); i < Math.Pow(10 , m);i++)
            if (rightRotationDivisor(i))
                Console.WriteLine(i);
    }

    // Driver code
    public static void Main()
    {
        int m = 3;
        generateNumbers(m);

    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Generating numbers that
// are divisor of their right-rotations

// Function to check if N is a
// divisor of its right-rotation
function rightRotationDivisor($N)
{
    $lastDigit = $N % 10;
    $rightRotation = ($lastDigit * pow(10 ,
                     (int)(log10($N)))) +
                           floor($N / 10);
    return ($rightRotation % $N == 0);
}

// Function to generate m-digit
// numbers which are divisor of
// their right-rotation
function generateNumbers($m)
{
    for ($i = pow(10, ($m - 1));
         $i < pow(10 , $m); $i++)
        if (rightRotationDivisor($i))
            echo $i . "\n";
}

// Driver code
$m = 3;
generateNumbers($m);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to Generating numbers that
// are divisor of their right-rotations 

    // Function to check if N is a
    // divisor of its right-rotation
    function rightRotationDivisor(N)
    {
        let lastDigit = N % 10;
        let rightRotation = (lastDigit * Math.pow(10 ,
                    Math.floor((Math.log10(N)))) + Math.floor(N / 10));
        return (rightRotation % N == 0);
    }

    // Function to generate m-digit
    // numbers which are divisor of
    // their right-rotation
    function generateNumbers(m)
    {
        for (let i= Math.floor(Math.pow(10,(m - 1))); i <
             Math.floor(Math.pow(10 , m));i++)
            if (rightRotationDivisor(i))
                document.write(i+"<br>");
    }

    // Driver code
    let m = 3;
    generateNumbers(m);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
111
222
333
444
555
666
777
888
999
```