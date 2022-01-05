# 检查除数是偶数还是奇数

> 原文:[https://www . geeksforgeeks . org/check-如果除数总数是偶数还是奇数/](https://www.geeksforgeeks.org/check-if-total-number-of-divisors-are-even-or-odd/)

给定一个数“n”，求它的除数总数是偶数还是奇数。
**例:**

```
Input  : n = 10      
Output : Even

Input:  n = 100
Output: Odd

Input:  n = 125
Output: Even
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problem-page.php?pid=520)

一种天真的方法是[找到所有的除数](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)，然后看看除数的总数是偶数还是奇数。
这种解决方案的时间复杂度为 0(sqrt(n))

## C++

```
// Naive Solution to find
// if count of divisors
// is even or odd
#include <bits/stdc++.h>
using namespace std;

// Function to count
// the divisors
void countDivisors(int n)
{
    // Initialize count
    // of divisors
    int count = 0;

    // Note that this
    // loop runs till
    // square root
    for (int i = 1; i <= sqrt(n) + 1; i++)
    {
        if (n % i == 0)

            // If divisors are
            // equal increment
            // count by one
            // Otherwise increment
            // count by 2
            count += (n / i == i) ? 1 : 2;
    }

    if (count % 2 == 0)
        cout << "Even" << endl;
    else
        cout << "Odd" << endl;
}

// Driver Code
int main()
{
    cout << "The count of divisor: ";
    countDivisors(10);
    return 0;
}

// This code is Contributed by SHUBHAMSINGH10
```

## C

```
// Naive Solution to find
// if count of divisors
// is even or odd

#include <math.h>
#include <stdio.h>

// Function to count
// the divisors
void countDivisors(int n)
{
    // Initialize count
    // of divisors
    int count = 0;

    // Note that this
    // loop runs till
    // square root
    for (int i = 1; i <= sqrt(n) + 1; i++)
    {
        if (n % i == 0)

            // If divisors are
            // equal increment
            // count by one
            // Otherwise increment
            // count by 2
            count += (n / i == i) ? 1 : 2;
    }

    if (count % 2 == 0)
        printf("Even\n");

    else
        printf("Odd\n");
}

// Driver Code
int main()
{
    printf("The count of divisor: ");
    countDivisors(10);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Naive Solution to find if count
// of divisors is even or odd

import java.io.*;
import java.math.*;

class GFG
{

    // Function to count
    // the divisors
    static void countDivisors(int n)
    {
        // Initialize count
        // of divisors
        int count = 0;

        // Note that this
        // loop runs till
        // square root
        for (int i = 1; i <= Math.sqrt(n) + 1; i++)
        {
            if (n % i == 0)

                // If divisors are
                // equal increment
                // count by one
                // Otherwise increment
                // count by 2
                count += (n / i == i) ? 1 : 2;
        }

        if (count % 2 == 0)
            System.out.println("Even");

        else
            System.out.println("Odd");
    }

    // Driver Code
    public static void main(String args[])
    {
        System.out.print("The count of divisor: ");
        countDivisors(10);
    }
}
// This code is contributed by Nikita Tiwari
```

## 计算机编程语言

```
# Naive Solution to find if count 
# of divisors is even or odd
import math

# Function to count
# the divisors
def countDivisors(n) :

    # Initialize count
    # of divisors
    count = 0

    # Note that this loop
    # runs till square
    # root
    for i in range(1, (int)(math.sqrt(n)) + 2) :
        if (n % i == 0) :

            # If divisors are
            # equal, increment
            # count by one
            # Otherwise increment
            # count by 2
            if( n // i == i) :
                count = count + 1
            else :
                count = count + 2

    if (count % 2 == 0) :
        print("Even")
    else :
        print("Odd")

# Driver Code
print("The count of divisor: ")
countDivisors(10)

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# program using Naive
// Solution to find if
// count of divisors
// is even or odd
using System;

class GFG {

    // Function to count
    // the divisors
    static void countDivisors(int n)
    {
        // Initialize count
        // of divisors
        int count = 0;

        // Note that this
        // loop runs till
        // square root
        for (int i = 1; i <= Math.Sqrt(n)
                                 + 1;
             i++) {
            if (n % i == 0)

                // If divisors are
                // equal increment
                // count by one
                // Otherwise increment
                // count by 2
                count += (n / i == i) ? 1 : 2;
        }

        if (count % 2 == 0)
            Console.Write("Even");

        else
            Console.Write("Odd");
    }

    // Driver code
    public static void Main()
    {
        Console.Write("The count of divisor: ");
        countDivisors(10);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Naive Solution to
// find if count of
// divisors is even
// or odd

// Function to count
// the divisors
function countDivisors($n)
{

    // Initialize count
    // of divisors
    $count = 0;

    // Note that this
    // loop runs till
    // square root
    for ($i = 1; $i <= sqrt($n) + 1; $i++)
    {
        if ($n % $i == 0)

            // If divisors are
            // equal increment
            // count by one
            // Otherwise increment
            // count by 2
            $count += ($n / $i == $i)? 1 : 2;
    }

    if ($count % 2 == 0)
        echo "Even\n";

    else
        echo "Odd\n";
}

    // Driver Code
    echo "The count of divisor: ";
    countDivisors(10);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Naive Solution to find
// if count of divisors
// is even or odd

// Function to count
// the divisors
function countDivisors(n)
{
    // Initialize count
    // of divisors
    let count = 0;

    // Note that this
    // loop runs till
    // square root
    for (let i = 1; i <= Math.sqrt(n) + 1; i++)
    {
        if (n % i == 0)

            // If divisors are
            // equal increment
            // count by one
            // Otherwise increment
            // count by 2
            count += (Math.floor(n / i) == i) ? 1 : 2;
    }

    if (count % 2 == 0)
        document.write("Even" + "<br>");
    else
        document.write("Odd" + "<br>");
}

// Driver Code
    document.write("The count of divisor: ");
    countDivisors(10);

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
The count of divisor: Even 
```

**有效解:**
我们可以观察到除数只有在完美平方的情况下才是奇数。因此，最好的解决办法是检查给定的数字是否是完美的正方形。如果它是一个完美的正方形，那么除数将是奇数，否则它将是偶数。
以下是上述思路的实现:

## C++

```
// C++ program for
// Efficient Solution to find
// if count of divisors is
// even or odd
#include <bits/stdc++.h>
using namespace std;

// Function to find if count
// of divisors is even or
// odd
void countDivisors(int n)
{
    int root_n = sqrt(n);

    // If n is a perfect square,
    // then it has odd divisors
    if (root_n * root_n == n)
        printf("Odd\n");
    else
        printf("Even\n");
}

// Driver Code
int main()
{
    cout << "The count of divisors"
         << " of 10 is: ";

    countDivisors(14);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Efficient
// Solution to find if count of
// divisors is even or odd
import java.io.*;
import java.math.*;

class GFG
{

    // Function to find if count
    // of divisors is even or
    // odd
    static void countDivisors(int n)
    {
        int root_n = (int)(Math.sqrt(n));

        // If n is a perfect square,
        // then, it has odd divisors
        if (root_n * root_n == n)
            System.out.println("Odd");

        else
            System.out.println("Even");
    }

    // Driver code
    public static void main(String args[])
        throws IOException
    {
        System.out.print("The count of" +
                    "divisors of 10 is: ");

        countDivisors(10);
    }
}

// This code is contributed by Nikita Tiwari
```

## 计算机编程语言

```
# Python program for
# Efficient Solution to find
# find if count of divisors
# is even or odd
import math

def NumOfDivisor(n):
    if n < 1:
        return
    root_n = int(math.sqrt(n))

    # If n is a perfect square,
    # then it has odd divisors
    if root_n**2 == n:
        print('Odd')
    else:
        print('Even')

# Driver code    
if __name__ == '__main__':
    print("The count of divisor is:")
    NumOfDivisor(14)

# This code is contributed by Yt R   
```

## C#

```
// C# program for efficient
// solution to find of
// count of divisors is
// even or odd
using System;

class GFG {

    // Function to find if
    // count of divisors
    // is even or odd
    static void countDivisors(int n)
    {
        int root_n = (int)(Math.Sqrt(n));

        // If n is a perfect square,
        // then, it has odd divisors
        if (root_n * root_n == n)
            Console.WriteLine("Odd");

        else
            Console.WriteLine("Even");
    }

    // Driver code
    public static void Main()
    {
        Console.Write("The count of divisors : ");

        countDivisors(10);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program for Efficient
// Solution to find if count of
// divisors is even or odd

// Function to find if count
// of divisors is even or
// odd

function countDivisors($n)
{
    $root_n = sqrt($n);

    // If n is a perfect square,
    // then it has odd divisors
    if ($root_n * $root_n == $n)
        echo "Odd\n";
    else
        echo "Even\n";
}

// Driver Code
echo "The count of divisors of 10 is: ";

countDivisors(10);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for
// Efficient Solution to find
// if count of divisors
// is even or odd

// Function to count
// the divisors
function countDivisors(n)
{
    // Store square root of n
    let root_n = Math.sqrt(n);

    // If n is a perfect square,
    // then it has odd divisors
    if (root_n * root_n == n)
        document.write("Odd" + "<br>");
    else
        document.write("Even" + "<br>");     
}

// Driver Code
    document.write("The count of divisor: ");
    countDivisors(10);

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
The count of divisor: Even
```

本文由[阿舒托什·库马尔](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。