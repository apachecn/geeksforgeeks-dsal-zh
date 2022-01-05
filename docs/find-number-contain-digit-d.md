# 找出包含数字 d 的数字

> 原文:[https://www.geeksforgeeks.org/find-number-contain-digit-d/](https://www.geeksforgeeks.org/find-number-contain-digit-d/)

给定两个整数 n 和 d，任务是找出 0 到 n 之间包含特定数字 d 的数字

**示例:**

```
Input : n = 20
        d = 5
Output : 5 15

Input : n = 50
        d = 2
Output : 2 12 20 21 22 23 24 25 26 27 28 29 32 42 
```

**方法 1:**
从 0 到 n 做一个循环，逐一检查每个数字，如果数字包含数字 d，则打印出来，否则增加数字。继续这个过程，直到循环结束。

## C++

```
// C++ program to print the number which
// contain the digit d from 0 to n
#include <bits/stdc++.h>
using namespace std;

// Returns true if d is present as digit
// in number x.
bool isDigitPresent(int x, int d)
{
    // Breal loop if d is present as digit
    while (x > 0)
    {
        if (x % 10 == d)
            break;

        x = x / 10;
    }

    // If loop broke
    return (x > 0);
}

// function to display the values
void printNumbers(int n, int d)
{
    // Check all numbers one by one
    for (int i = 0; i <= n; i++)

        // checking for digit
        if (i == d || isDigitPresent(i, d))
            cout << i << " ";
}

// Driver code
int main()
{
    int n = 47, d = 7;
    printNumbers(n, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the number which
// contain the digit d from 0 to n

class GFG
{
    // Returns true if d is present as digit
    // in number x.
    static boolean isDigitPresent(int x, int d)
    {
        // Breal loop if d is present as digit
        while (x > 0)
        {
            if (x % 10 == d)
                break;

            x = x / 10;
        }

        // If loop broke
        return (x > 0);
    }

    // function to display the values
    static void printNumbers(int n, int d)
    {
        // Check all numbers one by one
        for (int i = 0; i <= n; i++)

            // checking for digit
            if (i == d || isDigitPresent(i, d))
                System.out.print(i + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 47, d = 7;
        printNumbers(n, d);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print the number which
# contain the digit d from 0 to n

# Returns true if d is present as digit
# in number x.
def isDigitPresent(x, d):

    # Breal loop if d is present as digit
    while (x > 0):

        if (x % 10 == d):
            break

        x = x / 10

    # If loop broke
    return (x > 0)

# function to display the values
def printNumbers(n, d):

    # Check all numbers one by one
    for i in range(0, n+1):

        # checking for digit
        if (i == d or isDigitPresent(i, d)):
            print(i,end=" ")

# Driver code
n = 47
d = 7
print("The number of values are")
printNumbers(n, d)
#This code is contributed by
#Smitha Dinesh Semwal
```

## C#

```
// C# program to print the number which
// contain the digit d from 0 to n
using System;

class GFG {

    // Returns true if d is present as digit
    // in number x.
    static bool isDigitPresent(int x, int d)
    {

        // Breal loop if d is present as digit
        while (x > 0)
        {
            if (x % 10 == d)
                break;

            x = x / 10;
        }

        // If loop broke
        return (x > 0);
    }

    // function to display the values
    static void printNumbers(int n, int d)
    {

        // Check all numbers one by one
        for (int i = 0; i <= n; i++)

            // checking for digit
            if (i == d || isDigitPresent(i, d))
                Console.Write(i + " ");
    }

    // Driver code
    public static void Main()
    {
        int n = 47, d = 7;

        printNumbers(n, d);
    }
}

// This code contribute by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the number which
// contain the digit d from 0 to n

// Returns true if d is present as digit
// in number x.
function isDigitPresent($x, $d)
{

    // Breal loop if d is
    // present as digit
    while ($x > 0)
    {
        if ($x % 10 == $d)
            break;

        $x = $x / 10;
    }

    // If loop broke
    return ($x > 0);
}

// function to display the values
function printNumbers($n, $d)
{

    // Check all numbers one by one
    for ($i = 0; $i <= $n; $i++)

        // checking for digit
        if ($i == $d || isDigitPresent($i, $d))
            echo $i , " ";
}

    // Driver Code
    $n = 47;
    $d = 7;
    printNumbers($n, $d);

// This code contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print the number which
// contain the digit d from 0 to n

// Returns true if d is present as digit
// in number x.
function isDigitPresent(x, d)
{

    // Breal loop if d is present as digit
    while (x > 0)
    {
        if (x % 10 == d)
            break;

        x = x / 10;
    }

    // If loop broke
    return (x > 0);
}

// Function to display the values
function printNumbers(n, d)
{

    // Check all numbers one by one
    for(let i = 0; i <= n; i++)

        // Checking for digit
        if (i == d || isDigitPresent(i, d))
            document.write(i + " ");
}

// Driver code
let n = 47, d = 7;

printNumbers(n, d);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
The number of values are
7 17 27 37 47
```

**方法 2:**
这种方法使用每个数字作为字符串，并检查数字是否存在。这种方法使用 String.indexOf()函数来检查字符串中是否存在该字符。
String.indexOf() > = 0 表示存在字符
，String.indexOf() = -1 表示不存在字符

## C++

```
// CPP program to print the number which
// contain the digit d from 0 to n
#include<bits/stdc++.h>
using namespace std;

// function to display the values
void printNumbers(int n, int d)
{

    // Converting d to character
    string st = "";
    st += to_string(d);
    char ch = st[0];

    string p = "";
    p += ch;

    // Loop to check each digit one by one.
    for (int i = 0; i <= n; i++)
    {

        // initialize the string
        st = "";
        st = st + to_string(i);
        int idx = st.find(p);

        // checking for digit
        if (i == d || idx!=-1)        
            cout << (i) << " ";
    }
}

// Driver code
int main()
{
    int n = 100, d = 5;
    printNumbers(n, d);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the number which
// contain the digit d from 0 to n

public class GFG {

    // function to display the values
    static void printNumbers(int n, int d)
    {

        // Converting d to character
        String st = "" + d;
        char ch = st.charAt(0);

        // Loop to check each digit one by one.
        for (int i = 0; i <= n; i++) {

            // initialize the string
            st = "";
            st = st + i;

            // checking for digit
            if (i == d || st.indexOf(ch) >= 0)               
                System.out.print(i + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 100, d = 5;
        printNumbers(n, d);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to print the number
# which contain the digit d from 0 to n

def index(st, ch):
    for i in range(len(st)):
        if(st[i] == ch):
            return i;
    return -1

# function to display the values
def printNumbers(n, d):

# Converting d to character
    st = "" + str(d)
    ch = st[0]

    # Loop to check each digit one by one.
    for i in range(0, n + 1, 1):

        # initialize the string
        st = ""
        st = st + str(i)

        # checking for digit
        if (i == d or index(st, ch) >= 0):
            print(i, end = " ")

# Driver code
if __name__ == '__main__':
    n = 100
    d = 5
    printNumbers(n, d)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to print the number which
// contain the digit d from 0 to n
using System;

class GFG
{

    // function to display the values
    static void printNumbers(int n, int d)
    {

        // Converting d to character
        String st = "" + d;
        char ch = st[0];

        // Loop to check each digit one by one.
        for (int i = 0; i < n; i++)
        {

            // initialize the string
            st = "";
            st = st + i;

            // checking for digit
            if (i == d || st.IndexOf(ch) >= 0)            
                Console.Write(i + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 100, d = 5;
        printNumbers(n, d);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to print the number which
// contain the digit d from 0 to n

// Function to display the values
function printNumbers(n, d)
{

    // Converting d to character
    let st = "" + d;
    let ch = st[0];

    // Loop to check each digit one by one.
    for(let i = 0; i < n; i++)
    {

        // Initialize the string
        st = "";
        st = st + i;

        // Checking for digit
        if (i == d || st.indexOf(ch) >= 0)           
            document.write(i + " ");
    }
}

// Driver code
let n = 100, d = 5;

printNumbers(n, d);

// This code is contributed by decode2207

</script>
```

**Output:** 

```
5 15 25 35 45 50 51 52 53 54 55 56 57 58 59 65 75 85 95
```