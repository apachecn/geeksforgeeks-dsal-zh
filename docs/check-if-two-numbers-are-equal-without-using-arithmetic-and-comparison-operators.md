# 不使用算术和比较运算符检查两个数是否相等

> 原文:[https://www . geesforgeks . org/不使用算术和比较运算符检查两个数是否相等/](https://www.geeksforgeeks.org/check-if-two-numbers-are-equal-without-using-arithmetic-and-comparison-operators/)

以下不允许使用
1)算术和比较运算符
2)字符串函数

**方法一:**思路是用异或运算符。如果两个数相同，则两个数的异或为 0，否则为非零。

## C++

```
// C++ program to check if two numbers
// are equal without using arithmetic
// and comparison operators
#include <iostream>
using namespace std;

// Function to check if two
// numbers are equal using
// XOR operator
void areSame(int a, int b)
{
    if (a ^ b)
        cout << "Not Same";
    else
        cout << "Same";
}

// Driver Code
int main()
{

    // Calling function
    areSame(10, 20);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two numbers
// are equal without using arithmetic
// and comparison operators
class GFG {

    // Function to check if two
    // numbers are equal using
    // XOR operator
    static void areSame(int a, int b)
    {
        if ((a ^ b) != 0)
            System.out.print("Not Same");
        else
            System.out.print("Same");
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Calling function
        areSame(10, 20);
    }
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python3 program to check if two numbers
# are equal without using arithmetic
# and comparison operators

def areSame(a, b):

# Function to check if two
# numbers are equal using
# XOR operator
 if ((a ^ b) != 0):
    print("Not Same")
 else:
    print("Same")

# Driver Code

areSame(10, 20)

# This code is contributed by Smitha
```

## C#

```
// C# program to check if two numbers
// are equal without using arithmetic
// and comparison operators
using System;

class GFG {

    // Function to check if two
    // numbers are equal using
    // XOR operator
    static void areSame(int a, int b)
    {
        if ((a ^ b) != 0)
            Console.Write("Not Same");
        else
            Console.Write("Same");
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Calling function
        areSame(10, 20);
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// two numbers are equal
// without using arithmetic
// and comparison operators

// Function to check if two
// numbers are equal using
// XOR operator
function areSame($a, $b)
{
if ($a ^ $b)
echo "Not Same";
else
echo "Same";
}

// Driver Code

// Calling function
areSame(10, 20);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if two numbers
// are equal without using arithmetic and
// comparison operators  

// Function to check if two
// numbers are equal using
// XOR operator
function areSame(a, b)
{
    if ((a ^ b) != 0)
        document.write("Not Same");
    else
        document.write("Same");
}

// Driver Code
areSame(10, 20);

// This code is contributed by shikhasingrajput

</script>
```

**输出:**

```
Not Same
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**方法二:**这里的思路是用补码(~)和逐位的“&”运算符。

## C++

```
// C++ program to check if two numbers
// are equal without using arithmetic
// and comparison operators
#include <iostream>
using namespace std;

// Function to check if two
// numbers are equal using
// using ~ complement and & operator.
void areSame(int a, int b)
{
    if ((a & ~b) == 0 && (~a & b) == 0)
        cout << "Same";
    else
        cout << "Not Same";
}
// Driver Code
int main()
{

    // Calling function
    areSame(10, 20);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two numbers
// are equal without using arithmetic
// and comparison operators

class GFG {
    // Function to check if two
    // numbers are equal using
    // using ~ complement and & operator.
    static void areSame(int a, int b)
    {
        if ((a & ~b) == 0 && (~a & b) == 0)
            System.out.print("Same");
        else
            System.out.print("Not Same");
    }

    // Driver Code
    public static void main(String args[])
    {
        // Calling function
        areSame(10, 20);
    }
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 program to check if two numbers
# are equal without using arithmetic
# and comparison operators

# Function to check if two
# numbers are equal using
# using ~ complement and & operator.
def areSame(a, b):
    if ( (a & ~b) == 0 and (~a & b) == 0 ):
        print("Same")
    else:
        print("Not Same")    
# Calling function
areSame(10, 20)

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to check if two numbers
// are equal without using arithmetic
// and comparison operators
using System;

class GFG {
    // Function to check if two
    // numbers are equal using
    // using ~ complement and & operator.
    static void areSame(int a, int b)
    {
        if ((a & ~b) == 0 && (~a & b) == 0)
            Console.Write("Same");
        else
            Console.Write("Not Same");
    }

    // Driver Code
    public static void Main()
    {
        // Calling function
        areSame(10, 20);
    }
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if two numbers
// are equal without using arithmetic
// and comparison operators

// Function to check if two
// numbers are equal using
// using ~ complement and & operator.
function areSame($a, $b)
{
    if (($a & ~$b)==0 && (~$a & $b)==0)
        echo "Same";
    else
        echo "Not Same";
}

// Driver Code
// Calling function
areSame(1, 1);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to check if two numbers
// are equal without using arithmetic
// and comparison operators

// Function to check if two
// Numbers are equal using
// using ~ complement and & operator.
function areSame(a, b)
{
    if ((a & ~b) == 0 && (~a & b) == 0)
        document.write("Same");
    else
        document.write("Not Same");
}

// Driver Code

// Calling function
areSame(10, 20);

// This code is contributed by gauravrajput1

</script>
```

**输出:**

```
Not Same
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

来源:[https://www . geeksforgeeks . org/count-of-n-digits-numbers-其数字总和等于给定总和/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-sum-of-digits-equals-to-given-sum/)
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述主题的信息