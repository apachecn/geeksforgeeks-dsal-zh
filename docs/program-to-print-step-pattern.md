# 程序打印步进模式

> 原文:[https://www . geesforgeks . org/program-to-print-step-pattern/](https://www.geeksforgeeks.org/program-to-print-step-pattern/)

程序必须接受一个字符串 **S** 和一个整数 **N** 作为输入。程序必须打印所需的图案，如下所示:
**示例:**

> **输入:** string = "abcdefghijk "，n = 3
> **输出:**
> a
> * b
> * * c
> * d
> e
> * f
> * * g
> * h
> I
> * j
> * * k
> **说明:**
> 此处 N 为 3。字符串模式的最高可能高度必须是 3。从 1 的高度开始。递增，直到达到数值 n(=3)。一旦达到高度，开始递减。重复该过程，直到打印出字符串中的所有字符。
> **输入:** string = "GeeksForGeeks "，n = 4
> **输出:**
> g
> * e
> * * e
> * * * k
> * * s
> * f
> o
> * r
> * * g
> * * * e
> * * e
> * k
> s

**接近**T2】

1.  设置一个标志来表示是增加还是减少

2.  设置一个变量 x 来表示要打印的*s 的数量，并将其初始化为 0

3.  遍历字符串中的所有字符

4.  对于每个字符打印 x *s

5.  如果设置了标志，则增加

6.  否则减量

7.  如果 x 值等于 n-1，则将标志设置为假

8.  如果 x 值等于 0，则将标志设置为真

**执行:**

## C++

```
// C++ program to print Step Pattern
#include <iostream>

using namespace std;

// function to print the steps
void steps(string str, int n)
{
    // declare a flag
    bool flag;
    int x = 0;

    // traverse through all the characters in the string
    for (int i = 0; i < str.length(); i++) {

        // if the x value is 0.. then
        // we must increment till n ...
        // set flag to true
        if (x == 0)
            flag = true;

        // if the x value is n-1 then
        // we must decrement till 0 ...
        // set flag as false
        if (x == n - 1)
            flag = false;

        // print x *s
        for (int j = 0; j < x; j++)
            cout << "*";

        cout << str[i] << "\n";

        // checking whether to
        // increment or decrement x
        if (flag == true)
            x++;
        else
            x--;
    }
}

int main()
{

    // Get the String and the number n
    int n = 4;
    string str = "GeeksForGeeks";

    cout << "String: " << str << endl;
    cout << "Max Length of Steps: "
         << n << endl;

    // calling the function
    steps(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print Step Pattern
import java.util.*;

class solution
{

// function to print the steps
static void steps(String str, int n)
{
    // declare a flag
    boolean flag = false;
    int x = 0;

    // traverse through all the characters in the string
    for (int i = 0; i < str.length(); i++) {

        // if the x value is 0.. then
        // we must increment till n ...
        // set flag to true
        if (x == 0)
            flag = true;

        // if the x value is n-1 then
        // we must decrement till 0 ...
        // set flag as false
        if (x == n - 1)
            flag = false;

        // print x *s
        for (int j = 0; j < x; j++)
            System.out.print("*");

        System.out.print(str.charAt(i)+"\n");

        // checking whether to
        // increment or decrement x
        if (flag == true)
            x++;
        else
            x--;
    }
}

public static void main(String args[])
{

    // Get the String and the number n
    int n = 4;
    String str = "GeeksForGeeks";

    System.out.println("String: "+str);
    System.out.println("Max Length of Steps: "+n);

    // calling the function
    steps(str, n);

}
}

// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 program to print Step Pattern
import math as mt

# function to print the steps
def steps(string, n):

    # declare a flag
    flag = False
    x = 0

    # traverse through all the characters
    # in the string
    for i in range(len(string)):

        # if the x value is 0.. then
        # we must increment till n ...
        # set flag to true
        if (x == 0):
            flag = True

        # if the x value is n-1 then
        # we must decrement till 0 ...
        # set flag as false
        if (x == n - 1):
            flag = False

        # print x *s
        for j in range(x):
            print("*", end = "")

        print(string[i])

        # checking whether to
        # increment or decrement x
        if (flag == True):
            x += 1
        else:
            x -= 1

# Driver code

# Get the String and the number n
n = 4
string = "GeeksForGeeks"

print("String: ", string)
print("Max Length of Steps: ", n)

# calling the function
steps(string, n)

# This code is contributed
# by Mohit kumar 29
```

## C#

```
using System;

// C# Program to print Step Pattern

public class solution
{

// function to print the steps
public static void steps(string str, int n)
{
    // declare a flag
    bool flag = false;
    int x = 0;

    // traverse through all the characters in the string
    for (int i = 0; i < str.Length; i++)
    {

        // if the x value is 0.. then
        // we must increment till n ...
        // set flag to true
        if (x == 0)
        {
            flag = true;
        }

        // if the x value is n-1 then
        // we must decrement till 0 ...
        // set flag as false
        if (x == n - 1)
        {
            flag = false;
        }

        // print x *s
        for (int j = 0; j < x; j++)
        {
            Console.Write("*");
        }

        Console.Write(str[i] + "\n");

        // checking whether to
        // increment or decrement x
        if (flag == true)
        {
            x++;
        }
        else
        {
            x--;
        }
    }
}

// Driver code
public static void Main(string[] args)
{

    // Get the String and the number n
    int n = 4;
    string str = "GeeksForGeeks";

    Console.WriteLine("String: " + str);
    Console.WriteLine("Max Length of Steps: " + n);

    // calling the function
    steps(str, n);

}
}

  // This code is contributed by shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print Step Pattern

// function to print the steps
function steps($str, $n)
{
    $x = 0;

    // traverse through all the characters
    // in the string
    for ($i = 0; $i < strlen($str); $i++)
    {

        // if the x value is 0.. then
        // we must increment till n ...
        // set flag to true
        if ($x == 0)
            $flag = true;

        // if the x value is n-1 then
        // we must decrement till 0 ...
        // set flag as false
        if ($x == $n - 1)
            $flag = false;

        // print x *s
        for ($j = 0; $j < $x; $j++)
            echo "*";

        echo $str[$i], "\n";

        // checking whether to
        // increment or decrement x
        if ($flag == true)
            $x++;
        else
            $x--;
    }
}

// Driver Code

// Get the String and the number n
$n = 4;
$str = "GeeksForGeeks";

echo "String: ", $str, "\n";
echo "Max Length of Steps: ", $n, "\n";

// calling the function
steps($str, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
      // JavaScript program to print Step Pattern

      // function to print the steps
      function steps(str, n) {
        // declare a flag
        var flag;
        var x = 0;

        // traverse through all the characters in the string
        for (var i = 0; i < str.length; i++) {
          // if the x value is 0.. then
          // we must increment till n ...
          // set flag to true
          if (x == 0) flag = true;

          // if the x value is n-1 then
          // we must decrement till 0 ...
          // set flag as false
          if (x == n - 1) flag = false;

          // print x *s
          for (var j = 0; j < x; j++) document.write("*");

          document.write(str[i] + "<br>");

          // checking whether to
          // increment or decrement x
          if (flag == true) x++;
          else x--;
        }
      }

      // Get the String and the number n
      var n = 4;
      var str = "GeeksForGeeks";
      document.write("String: " + str + "<br>");
      document.write("Max Length of Steps: " + n + "<br>");
      // calling the function
      steps(str, n);
    </script>
```

**Output:** 

```
String: GeeksForGeeks
Max Length of Steps: 4
G
*e
**e
***k
**s
*F
o
*r
**G
***e
**e
*k
s
```