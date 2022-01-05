# 求数字根为 X 的第 n 个正数

> 原文:[https://www . geesforgeks . org/find-n-正数-number-what-digital-root-is-x/](https://www.geeksforgeeks.org/find-nth-positive-number-whose-digital-root-is-x/)

给定一个数字 X ( 1 <= X <= 9) and a positive number N, find the Nth positive number whose **数字根**是 X.
**数字根**:正数的数字根是通过对一个数字的数字进行迭代求和得到的。在每次迭代中，数字被其位数的总和所取代，当数字减少到一位数时，迭代停止。这个一位数被称为数字根。例如，65 的数字根是 2，因为 6 + 5 = 11，1 + 1 = 2。

**示例:**

> **输入** : X = 3，N = 100
> **输出** : 894
> 数字根为 X 的第 N 个数字是 894
> 
> **输入** : X = 7，N = 43
> 输出 : 385

**简易法**:简易法就是从 1 开始计算每个数字的*数字根*，每当我们遇到一个*数字根*等于 X 的数字，我们就把计数器加 1。当我们的计数器等于 n 时，我们将停止搜索

下面是上述方法的实现:

## C++

```
// C++ program to find the N-th number whose
// digital root is X

#include <bits/stdc++.h>
using namespace std;

// Function to find the digital root of
// a number
int findDigitalRoot(int num)
{
    int sum = INT_MAX, tempNum = num;

    while (sum >= 10) {
        sum = 0;

        while (tempNum > 0) {
            sum += tempNum % 10;
            tempNum /= 10;
        }

        tempNum = sum;
    }

    return sum;
}

// Function to find the Nth number with
// digital root as X
void findAnswer(int X, int N)
{
    // Counter variable to keep the
    // count of valid numbers
    int counter = 0;

    for (int i = 1; counter < N; ++i) {

        // Find digital root
        int digitalRoot = findDigitalRoot(i);

        // Check if is required answer or not
        if (digitalRoot == X) {
            ++counter;
        }

        // Print the answer if you have found it
        // and breakout of the loop
        if (counter == N) {
            cout << i;

            break;
        }
    }
}

// Driver Code
int main()
{
    int X = 1, N = 3;

    findAnswer(X, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th number whose
// digital root is X
class GFG
{

// Function to find the digital root of
// a number
static int findDigitalRoot(int num)
{
    int sum = Integer.MAX_VALUE, tempNum = num;

    while (sum >= 10)
    {
        sum = 0;

        while (tempNum > 0)
        {
            sum += tempNum % 10;
            tempNum /= 10;
        }

        tempNum = sum;
    }

    return sum;
}

// Function to find the Nth number with
// digital root as X
static void findAnswer(int X, int N)
{
    // Counter variable to keep the
    // count of valid numbers
    int counter = 0;

    for (int i = 1; counter < N; ++i)
    {

        // Find digital root
        int digitalRoot = findDigitalRoot(i);

        // Check if is required answer or not
        if (digitalRoot == X)
        {
            ++counter;
        }

        // Print the answer if you have found it
        // and breakout of the loop
        if (counter == N)
        {
            System.out.print( i);

            break;
        }
    }
}

// Driver Code
public static void main(String args[])
{
    int X = 1, N = 3;

    findAnswer(X, N);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the N-th number whose
# digital root is X
import sys

# Function to find the digital root of
# a number
def findDigitalRoot(num):
    sum = sys.maxsize;
    tempNum = num;

    while (sum >= 10):
        sum = 0;

        while (tempNum > 0):
            sum += tempNum % 10;
            tempNum //= 10;

        tempNum = sum;

    return sum;

# Function to find the Nth number with
# digital root as X
def findAnswer(X, N):

    # Counter variable to keep the
    # count of valid numbers
    counter = 0;
    i = 0;
    while (counter < N):
        i += 1;

        # Find digital root
        digitalRoot = findDigitalRoot(i);

        # Check if is required answer or not
        if (digitalRoot == X):
            counter += 1;

        # Print the answer if you have found it
        # and breakout of the loop
        if (counter == N):
            print(i);
            break;

# Driver Code
if __name__ == '__main__':
    X = 1;
    N = 3;

    findAnswer(X, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find the N-th number whose
// digital root is X
using System;

class GFG
{

// Function to find the digital root of
// a number
static int findDigitalRoot(int num)
{
    int sum = int.MaxValue, tempNum = num;

    while (sum >= 10)
    {
        sum = 0;

        while (tempNum > 0)
        {
            sum += tempNum % 10;
            tempNum /= 10;
        }

        tempNum = sum;
    }

    return sum;
}

// Function to find the Nth number with
// digital root as X
static void findAnswer(int X, int N)
{
    // Counter variable to keep the
    // count of valid numbers
    int counter = 0;

    for (int i = 1; counter < N; ++i)
    {

        // Find digital root
        int digitalRoot = findDigitalRoot(i);

        // Check if is required answer or not
        if (digitalRoot == X)
        {
            ++counter;
        }

        // Print the answer if you have found it
        // and breakout of the loop
        if (counter == N)
        {
            Console.Write( i);

            break;
        }
    }
}

// Driver Code
public static void Main(String []args)
{
    int X = 1, N = 3;

    findAnswer(X, N);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the N-th number
// whose digital root is X

// Function to find the digital root
// of a number
function findDigitalRoot($num)
{
    $sum = PHP_INT_MAX;
    $tempNum = $num;

    while ($sum >= 10)
    {
        $sum = 0;

        while ($tempNum > 0)
        {
            $sum += $tempNum % 10;
            $tempNum /= 10;
        }

        $tempNum = $sum;
    }

    return $sum;
}

// Function to find the Nth number 
// with digital root as X
function findAnswer($X, $N)
{

    // Counter variable to keep the
    // count of valid numbers
    $counter = 0;

    for ($i = 1; $counter < $N; ++$i)
    {

        // Find digital root
        $digitalRoot = findDigitalRoot($i);

        // Check if is required answer or not
        if ($digitalRoot == $X)
        {
            ++$counter;
        }

        // Print the answer if you have found
        // it and breakout of the loop
        if ($counter == $N)
        {
            echo( $i);

            break;
        }
    }
}

// Driver Code
$X = 1; $N = 3;

findAnswer($X, $N);

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// JavaScript program to find the N-th number whose
// digital root is X    

// Function to find the digital root of
// a number
    function findDigitalRoot(num) {
        var sum = Number.MAX_VALUE, tempNum = num;

        while (sum >= 10) {
            sum = 0;

            while (tempNum > 0) {
                sum += tempNum % 10;
                tempNum = parseInt(tempNum/10);
            }

            tempNum = sum;
        }

        return sum;
    }

    // Function to find the Nth number with
    // digital root as X
    function findAnswer(X , N) {
        // Counter variable to keep the
        // count of valid numbers
        var counter = 0;

        for (var i = 1; counter < N; ++i) {

            // Find digital root
            var digitalRoot = findDigitalRoot(i);

            // Check if is required answer or not
            if (digitalRoot == X) {
                counter+=1;
            }

            // Print the answer if you have found it
            // and breakout of the loop
            if (counter == N) {
                document.write(i);

                break;
            }
        }
    }

    // Driver Code

        var X = 1, N = 3;

        findAnswer(X, N);

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
19
```

**高效方法:**我们可以直接使用公式找到数字 K 的*数字根*:

```
digitalRoot(k) = (k - 1)mod 9 +1
```

由此我们可以找到*数字*根为 K 的第 N 个数为，

```
Nth number = (N - 1)*9 + K
```

下面是上述方法的实现:

## C++

```
// C++ program to find the N-th number with
// digital root as X

#include <bits/stdc++.h>
using namespace std;

// Function to find the N-th number with
// digital root as X
int findAnswer(int X, int N)
{
    return (N - 1) * 9 + X;
}

// Driver Code
int main()
{
    int X = 7, N = 43;

    cout << findAnswer(X, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th number with
// digital root as X

class GfG
{

    // Function to find the N-th number with
    // digital root as X
    static int findAnswer(int X, int N)
    {
        return (N - 1) * 9 + X;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int X = 7, N = 43;
        System.out.println(findAnswer(X, N));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the N-th 
# number with digital root as X

# Function to find the N-th number
# with digital root as X
def findAnswer(X, N):

    return (N - 1) * 9 + X;

# Driver Code
X = 7;
N = 43;
print(findAnswer(X, N));

# This code is contributed by mits
```

## C#

```
// C# program to find the N-th number
// with digital root as X
using System;

class GFG
{

// Function to find the N-th
// number with digital root as X
static int findAnswer(int X, int N)
{
    return (N - 1) * 9 + X;
}

// Driver Code
public static void Main()
{
    int X = 7, N = 43;
    Console.WriteLine(findAnswer(X, N));
}
}

// This code contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the N-th number
// with digital root as X

// Function to find the N-th number
// with digital root as X
function findAnswer($X, $N)
{
    return ($N - 1) * 9 + $X;
}

// Driver Code
$X = 7; $N = 43;
echo(findAnswer($X, $N));

// This code contributed
// by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript program to find the N-th number
// with digital root as X

// Function to find the N-th number
// with digital root as X
function findAnswer(X, N)
{
    return (N - 1) * 9 + X;
}

// Driver Code
let X = 7;
let N = 43;

document.write(findAnswer(X, N));

// This code is contributed by mohan1240760

</script>
```

**Output:** 

```
385
```