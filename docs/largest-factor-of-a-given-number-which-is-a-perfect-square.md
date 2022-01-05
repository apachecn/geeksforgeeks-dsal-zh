# 给定数的最大因子，它是一个完美的正方形

> 原文:[https://www . geesforgeks . org/给定数字的最大因子是一个完美的正方形/](https://www.geeksforgeeks.org/largest-factor-of-a-given-number-which-is-a-perfect-square/)

给定一个数字![N      ](img/1dfc4130ed524ab15c69922e5ff8a4dd.png "Rendered by QuickLaTeX.com")。任务是找到那个数的最大因子，它是一个完美的正方形。
**例**:

```
Input : N = 420
Output : 4

Input : N = 100
Output : 100
```

一个**简单的解决方案**是从给定的数字开始，以递减的顺序遍历所有的数字，直到 1，如果这些数字中的任何一个是给定数字的因子，并且也是一个完美的正方形，打印那个数字。
**时间复杂度** : O(N)
**更好的解决方案:**更好的解决方案是使用给定数的[素因子分解](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。

*   首先找到那个数的所有质因数，直到 sqrt(num)。
*   取一个变量，*回答*，初始化为 1。它代表最大的平方数，也是这个数的一个因子。
*   现在，检查任何素数在给定数的素分解中出现偶数次，如果是，则将答案与该素因子相乘。
*   否则，如果出现奇数次，则将答案乘以质数(K–1)次，K 是质因数在质因数分解中的频率。

下面是上述方法的实现:

## C++

```
// C++ program to find the largest factor of
// a number which is also a perfect square

#include <cmath>
#include <iostream>
using namespace std;

// Function to find the largest factor
// of a given number which
// is a perfect square
int largestSquareFactor(int num)
{
    // Initialise the answer to 1
    int answer = 1;

    // Finding the prime factors till sqrt(num)
    for (int i = 2; i < sqrt(num); ++i) {
        // Frequency of the prime factor in the
        // factorisation initialised to 0
        int cnt = 0;
        int j = i;

        while (num % j == 0) {
            cnt++;
            j *= i;
        }

        // If the frequency is odd then multiply i
        // frequency-1 times to the answer
        if (cnt & 1) {
            cnt--;
            answer *= pow(i, cnt);
        }
        // Else if it is even, multiply
        // it frequency times
        else {
            answer *= pow(i, cnt);
        }
    }

    return answer;
}

// Driver Code
int main()
{
    int N = 420;

    cout << largestSquareFactor(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest factor of
// a number which is also a perfect square

class GFG
{

// Function to find the largest factor
// of a given number which
// is a perfect square
static int largestSquareFactor(int num)
{
    // Initialise the answer to 1
    int answer = 1;

    // Finding the prime factors till sqrt(num)
    for (int i = 2; i < Math.sqrt(num); ++i) {
        // Frequency of the prime factor in the
        // factorisation initialised to 0
        int cnt = 0;
        int j = i;

        while (num % j == 0) {
            cnt++;
            j *= i;
        }

        // If the frequency is odd then multiply i
        // frequency-1 times to the answer
        if ((cnt & 1)!=0) {
            cnt--;
            answer *= Math.pow(i, cnt);
        }
        // Else if it is even, multiply
        // it frequency times
        else {
            answer *= Math.pow(i, cnt);
        }
    }

    return answer;
}

// Driver Code
public static void  main(String args[])
{
    int N = 420;

    System.out.println(largestSquareFactor(N));

}
}
```

## 蟒蛇 3

```
# Python 3 program to find the largest
# factor of a number which is also a
# perfect square
import math

# Function to find the largest factor
# of a given number which is a
# perfect square
def largestSquareFactor( num):

    # Initialise the answer to 1
    answer = 1

    # Finding the prime factors till sqrt(num)
    for i in range(2, int(math.sqrt(num))) :

        # Frequency of the prime factor in the
        # factorisation initialised to 0
        cnt = 0
        j = i

        while (num % j == 0) :
            cnt += 1
            j *= i

        # If the frequency is odd then multiply i
        # frequency-1 times to the answer
        if (cnt & 1) :
            cnt -= 1
            answer *= pow(i, cnt)

        # Else if it is even, multiply
        # it frequency times
        else :
            answer *= pow(i, cnt)
    return answer

# Driver Code
if __name__ == "__main__":
    N = 420

    print(largestSquareFactor(N))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the largest factor of
// a number which is also a perfect square
using System;

class GFG
{

// Function to find the largest factor of
// a given number which is a perfect square
static double largestSquareFactor(double num)
{
    // Initialise the answer to 1
    double answer = 1;

    // Finding the prime factors
    // till sqrt(num)
    for (int i = 2; i < Math.Sqrt(num); ++i)
    {
        // Frequency of the prime factor in
        // the factorisation initialised to 0
        int cnt = 0;
        int j = i;

        while (num % j == 0)
        {
            cnt++;
            j *= i;
        }

        // If the frequency is odd then multiply i
        // frequency-1 times to the answer
        if ((cnt & 1) != 0)
        {
            cnt--;
            answer *= Math.Pow(i, cnt);
        }

        // Else if it is even, multiply
        // it frequency times
        else
        {
            answer *= Math.Pow(i, cnt);
        }
    }

    return answer;
}

// Driver Code
static public void Main ()
{
    int N = 420;
    Console.WriteLine(largestSquareFactor(N));
}
}

// This code is contributed by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the largest
// factor of a number which is also
// a perfect square

// Function to find the largest
// factor of a given number which
// is a perfect square
function largestSquareFactor($num)
{
    // Initialise the answer to 1
    $answer = 1;

    // Finding the prime factors
    // till sqrt(num)
    for ($i = 2; $i < sqrt($num); ++$i)
    {
        // Frequency of the prime factor
        // in the factorisation initialised to 0
        $cnt = 0;
        $j = $i;

        while ($num % $j == 0)
        {
            $cnt++;
            $j *= $i;
        }

        // If the frequency is odd then
        // multiply i frequency-1 times
        // to the answer
        if ($cnt & 1)
        {
            $cnt--;
            $answer *= pow($i, $cnt);
        }

        // Else if it is even, multiply
        // it frequency times
        else
        {
            $answer *= pow($i, $cnt);
        }
    }

    return $answer;
}

// Driver Code
$N = 420;
echo largestSquareFactor($N);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>
// Javascript program to find the largest factor of
// a number which is also a perfect square

// Function to find the largest factor
// of a given number which
// is a perfect square
function largestSquareFactor(num)
{

    // Initialise the answer to 1
    let answer = 1;

    // Finding the prime factors till sqrt(num)
    for (let i = 2; i < Math.sqrt(num); ++i)
    {

        // Frequency of the prime factor in the
        // factorisation initialised to 0
        let cnt = 0;
        let j = i;

        while (num % j == 0) {
            cnt++;
            j *= i;
        }

        // If the frequency is odd then multiply i
        // frequency-1 times to the answer
        if (cnt & 1)
        {
            cnt--;
            answer *= Math.pow(i, cnt);
        }

        // Else if it is even, multiply
        // it frequency times
        else {
            answer *= Math.pow(i, cnt);
        }
    }

    return answer;
}

// Driver Code
let N = 420;

document.write(largestSquareFactor(N));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
4
```

**时间复杂度** : O( sqrt(N))