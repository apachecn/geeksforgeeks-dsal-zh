# 以‘X’格式打印奇数长度的字符串

> 原文:[https://www . geesforgeks . org/print-x 格式奇数长度字符串/](https://www.geeksforgeeks.org/print-string-of-odd-length-in-x-format/)

给定奇数长度的字符串，以 X 格式打印该字符串。
**例:**

```
Input: 12345
Output:
1       5
  2   4
    3
  2   4
1       5 

Input: geeksforgeeks
Output:
g                         s
  e                     k
    e                 e
      k             e
        s         g
          f      r
             o
          f     r
        s         g
      k             e
    e                 e
  e                      k
g                          s 
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
想法是在单个循环中使用两个变量，第一个变量‘I’从左到右，第二个变量‘j’从右到左。十字(或 X)的上半部分在它们相遇之前被打印出来。中心字符在它们相遇时被打印，下分字符在它们交叉后被打印。在上部，str[i]打印在 str[j]之前，在下部，str[j]打印在 str[i]之前。
以下是以上思路的实现。

## C

```
// C++ program to print Cross pattern
#include<iostream>
using namespace std;

// Function to print given string in cross pattern
// Length of string must be odd
void printPattern(string str)
{
    int len = str.length();

    // i goes from 0 to len and j goes from len-1 to 0
    for (int i=0,j=len-1; i<=len,j>=0; i++,j--)
    {
        // To print the upper part. This loop runs
        // till middle point of string (i and j become
        // same
        if (i<j)
        {
            // Print i spaces
            for (int x=0; x<i; x++)
                cout << " ";

            // Print i'th character
            cout << str[i];

            // Print j-i-1 spaces
            for (int x=0; x<j-i-1; x++)
                cout << " ";

            // Print j'th character
            cout << str[j] << endl;
        }

        // To print center point
        if (i==j)
        {
            // Print i spaces
            for (int x=0; x<i; x++)
                cout << " ";

            // Print middle character
            cout << str[i] << endl;
        }

        // To print lower part
        else if (i>j)
        {
            // Print j spaces
            for (int x = j-1; x>=0; x--)
                cout << " ";

            // Print j'th character
            cout << str[j];

            // Print i-j-1 spaces
            for (int x=0; x<i-j-1; x++)
                cout << " ";

            // Print i'h character
            cout << str[i] << endl;
        }
    }
}

// Driver program
int main()
{
    printPattern("geeksforgeeks");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// print cross pattern
class GFG
{

// Function to print given
// string in cross pattern
static void pattern(String str,
                    int len)
{

    // i and j are the indexes
    // of characters to be
    // displayed in the ith
    // iteration i = 0 initially
    // and go upto length of string
    // j = length of string initially
    // in each iteration of i,
    // we increment i and decrement j,
    // we print character only
    // of k==i or k==j
    for (int i = 0; i < len; i++)
    {
        int j = len - 1 - i;
        for (int k = 0; k < len; k++)
        {
            if (k == i || k == j)
                System.out.print(str.charAt(k));
            else
                System.out.print(" ");
        }
        System.out.println("");
    }
}

// Driver code
public static void main (String[] args)
{
    String str = "geeksforgeeks";
    int len = str.length();
    pattern(str, len);

}
}

// This code is contributed
// by Smitha
```

## 蟒蛇 3

```
# Python 3 program to
# print cross pattern

# Function to print given
# string in cross pattern
def pattern(str, len):

    # i and j are the indexes
    # of characters to be
    # displayed in the ith
    # iteration i = 0 initially
    # and go upto length of string
    # j = length of string initially
    # in each iteration of i, we
    # increment i and decrement j,
    # we print character only of
    # k==i or k==j
    for i in range(0, len):

        j = len -1 - i
        for k in range(0, len):

            if (k == i or k == j):
                print(str[k],
                      end = "")
            else:
                print(end = " ")

        print(" ")

# Driver code
str = "geeksforgeeks"
len = len(str)
pattern(str, len)

# This code is contributed
# by Smitha
```

## C#

```
// C# program to print
// cross pattern
using System;

class GFG
{

// Function to print given
// string in cross pattern
static void pattern(String str,
                    int len)
{

    // i and j are the indexes
    // of characters to be
    // displayed in the ith
    // iteration i = 0 initially
    // and go upto length of string
    // j = length of string initially
    // in each iteration of i, we
    // increment i and decrement j,
    // we print character only of
    // k==i or k==j
    for (int i = 0; i < len; i++)
    {
        int j = len - 1 - i;
        for (int k = 0; k < len; k++)
        {
            if (k == i || k == j)
                Console.Write(str[k]);
            else
                Console.Write(" ");
        }
        Console.Write("\n");
    }
}

// Driver code
public static void Main ()
{
    String str = "geeksforgeeks";
    int len = str.Length;
    pattern(str, len);
}
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// Cross pattern

// Function to print given
// string in cross pattern,
// Length of string must be odd
function printPattern($str)
{
    $len = strlen($str);

    // i goes from 0 to len and
    // j goes from len-1 to 0
    for ($i = 0, $j = $len - 1;
         $i <= $len, $j >= 0;
         $i++, $j--)
    {
        // To print the upper part.
        // This loop runs till middle point
        // of string i and j become same
        if ($i < $j)
        {
            // Print i spaces
            for ($x = 0; $x < $i; $x++)
                echo " ";

            // Print i'th character
            echo $str[$i];

            // Print j-i-1 spaces
            for ( $x = 0; $x < $j - $i - 1;
                                      $x++)
                echo " ";

            // Print j'th character
            echo $str[$j]."\n";
        }

        // To print center point
        if ($i == $j)
        {
            // Print i spaces
            for ($x = 0; $x < $i; $x++)
                echo " ";

            // Print middle character
            echo $str[$i]."\n";
        }

        // To print lower part
        else if ($i > $j)
        {
            // Print j spaces
            for ($x = $j - 1; $x >= 0;
                                 $x--)
                echo " ";

            // Print j'th character
            echo $str[$j];

            // Print i-j-1 spaces
            for ( $x = 0; $x < $i - $j - 1;
                                      $x++)
                echo " ";

            // Print i'h character
            echo $str[$i]."\n";
        }
    }
}

// Driver code
printPattern("geeksforgeeks");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to
// print cross pattern // Function to print given
// string in cross pattern
function pattern(str,len)
{

    // i and j are the indexes
    // of characters to be
    // displayed in the ith
    // iteration i = 0 initially
    // and go upto length of string
    // j = length of string initially
    // in each iteration of i,
    // we increment i and decrement j,
    // we print character only
    // of k==i or k==j
    for (i = 0; i < len; i++)
    {
        var j = len - 1 - i;
        for (k = 0; k < len; k++)
        {
            if (k == i || k == j)
                document.write(str.charAt(k));
            else
                document.write(" ");
        }
        document.write("<br>");
    }
}

// Driver code
str = "geeksforgeeks";
var len = str.length;
pattern(str, len);

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
g           s
 e         k
  e       e
   k     e
    s   g
     f r
      o
     f r
    s   g
   k     e
  e       e
 e         k
g           s
```

**备选方案:**

## C++

```
// CPP program to print cross pattern
#include<bits/stdc++.h>
using namespace std;

// Function to print given string in
// cross pattern
void pattern(string str, int len){

    // i and j are the indexes of characters
    // to be displayed in the ith iteration
    // i = 0 initially and go upto length of
    // string
    // j = length of string initially
    // in each iteration of i, we increment
    // i and decrement j, we print character
    // only of k==i or k==j
    for (int i = 0; i < len; i++)
    {
        int j = len -1 - i;
        for (int k = 0; k < len; k++)
        {
            if (k == i || k == j)
                cout << str[k];
            else
                cout << " ";
        }
        cout << endl;      
    }
}

// driver code
int main ()
{
    string str = "geeksforgeeks";
    int len = str.size();
    pattern(str, len);

    return 0;
}
// This code is contributed by Satinder Kaur
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print cross pattern

class GFG
{

// Function to print given 
// string in cross pattern
static void pattern(String str, int len)
{

    // i and j are the indexes of
    // characters  to be displayed
    // in the ith iteration i = 0
    // initially and go upto length
    // of string j = length of string 
    // initially in each iteration
    // of i, we increment i and decrement
    // j, we print character only
    // of k==i or k==j
    for (int i = 0; i < len; i++)
    {
        int j = len -1 - i;
        for (int k = 0; k < len; k++)
        {
            if (k == i || k == j)
                System.out.print(str.charAt(k));

            else
                System.out.print(" ");
        }
        System.out.println("");    
    }
}

// driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int len = str.length();
    pattern(str, len);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to print cross pattern

# Function to print given string in
# cross pattern
def pattern(st, length):

    # i and j are the indexes of characters
    # to be displayed in the ith iteration
    # i = 0 initially and go upto length of
    # string
    # j = length of string initially
    # in each iteration of i, we increment
    # i and decrement j, we print character
    # only of k==i or k==j
    for i in range(length):
        j = length -1 - i
        for k in range(length):
            if (k == i or k == j):
                print(st[k],end="")
            else:
                print(" ",end="")
        print()

# driver code
if __name__ == "__main__":

    st = "geeksforgeeks"
    length = len(st)
    pattern(st, length)
```

## C#

```
// C# program to print cross pattern
using System;

class GFG
{

// Function to print given
// string in cross pattern
static void pattern(String str, int len)
{

    // i and j are the indexes of
    // characters to be displayed
    // in the ith iteration i = 0
    // initially and go upto length
    // of string j = length of string
    // initially in each iteration
    // of i, we increment i and decrement
    // j, we print character only
    // of k==i or k==j
    for (int i = 0; i < len; i++)
    {
        int j = len -1 - i;
        for (int k = 0; k < len; k++)
        {
            if (k == i || k == j)
                Console.Write(str[k]);

            else
                Console.Write(" ");
        }
        Console.WriteLine("");    
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int len = str.Length;
    pattern(str, len);
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// cross pattern

// Function to print given
// string in cross pattern
function pattern($str, $len)
{

    // i and j are the indexes of
    // characters  to be displayed
    // in the ith iteration i = 0
    // initially and go upto length of
    // string
    // j = length of string initially
    // in each iteration of i, we
    // increment i and decrement j, we
    // print character only of k==i or k==j
    for ($i = 0; $i < $len; $i++)
    {
        $j = $len -1 - $i;
        for ($k = 0; $k < $len; $k++)
        {
            if ($k == $i || $k == $j)
                echo $str[$k];
            else
                echo " ";
        }
        echo "\n";
    }
}

// Driver code
$str = "geeksforgeeks";
$len = strlen($str);
pattern($str, $len);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print cross pattern

// Function to print given 
// string in cross pattern
function pattern(str , len)
{

    // i and j are the indexes of
    // characters  to be displayed
    // in the ith iteration i = 0
    // initially and go upto length
    // of string j = length of string 
    // initially in each iteration
    // of i, we increment i and decrement
    // j, we print character only
    // of k==i or k==j
    for (var i = 0; i < len; i++)
    {
        var j = len -1 - i;
        for (var k = 0; k < len; k++)
        {
            if (k == i || k == j)
                document.write(str.charAt(k));

            else
                document.write(" ");
        }
        document.write('<br>');    
    }
}

// driver code
var str = "geeksforgeeks";
var len = str.length;
pattern(str, len);

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
g           s
 e         k
  e       e
   k     e
    s   g
     f r
      o
     f r
    s   g
   k     e
  e       e
 e         k
g           s
```

**解决方案 3** :这个问题也可以通过观察字符是沿着左右对角线打印的，只要我们把图案封装在一个矩阵内就可以解决。现在，如果字符串的长度是 *len* ，那么该模式可以包含在有序的方形矩阵 *len* 中。

*   左对角线上的元素可以通过条件 **( i==j )** 来访问，其中 I 和 j 分别是行号和列号。
*   右对角线上的元素可以通过条件 **(i+j == len-1)** 访问。

因此，运行顺序为 *len* 的嵌套循环，用各自的字符填充满足上述两个条件的位置，并用空格填充其余位置。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print the given pattern

#include<bits/stdc++.h>
using namespace std;

// Function to print the given
// string in respective pattern
void printPattern(string str, int len)
{  
    for(int i = 0; i < len; i++)
    {
        for(int j = 0; j < len; j++)
        {  
            // Print characters at corresponding
            // places satisfying the two conditions
            if((i == j) || (i + j == len-1))
                cout<<str[j];
            // Print blank space at rest of places
            else
                cout<<" ";
        }

        cout<<endl;
    }
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";

    int len = str.size();

    printPattern(str, len);

    return 0;
}

// This code and Approach is contributed by
// Aravind Kimonn
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the given pattern
import java.io.*;
class GFG
{

  // Function to print the given
  // string in respective pattern
  static void printPattern(String str, int len)
  {
    for(int i = 0; i < len; i++)
    {
      for(int j = 0; j < len; j++)
      {  

        // Print characters at corresponding
        // places satisfying the two conditions
        if((i == j) || (i + j == len - 1))
          System.out.print(str.charAt(j));

        // Print blank space at rest of places
        else
          System.out.print(" ");
      }

      System.out.println();
    }
  }

  // Driver code
  public static void main (String[] args)
  {   
    String str = "geeksforgeeks";
    int len = str.length();
    printPattern(str, len);
  }
}

// This code is contributed by rag2127.
```

## 蟒蛇 3

```
# Python3 program to print the given pattern

# Function to print the given
# string in respective pattern
def printPattern (Str, Len) :
    for i in range(Len) :
        for j in range(Len) :

            # Print characters at corresponding
            # places satisfying the two conditions
            if ((i == j) or (i + j == Len - 1)) :
                print(Str[j], end = "")

            # Print blank space at rest of places
            else :
                print(" ", end = "")
        print()

Str = "geeksforgeeks"
Len = len(Str)
printPattern(Str, Len)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to print the given pattern
using System;
public class GFG
{

  // Function to print the given
  // string in respective pattern
  static void printPattern(string str, int len)
  {
    for(int i = 0; i < len; i++)
    {
      for(int j = 0; j < len; j++)
      {  

        // Print characters at corresponding
        // places satisfying the two conditions
        if((i == j) || (i + j == len - 1))
          Console.Write(str[j]);

        // Print blank space at rest of places
        else
          Console.Write(" ");
      }
      Console.WriteLine();
    }
  }

  // Driver code  
  static public void Main ()
  {
    String str = "geeksforgeeks";
    int len = str.Length;
    printPattern(str, len);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// javascript program to print the given pattern
 // Function to print the given
  // string in respective pattern
  function printPattern(str , len)
  {
    for(var i = 0; i < len; i++)
    {
      for(var j = 0; j < len; j++)
      {  

        // Print characters at corresponding
        // places satisfying the two conditions
        if((i == j) || (i + j == len - 1))
          document.write(str.charAt(j));

        // Print blank space at rest of places
        else
          document.write(" ");
      }

      document.write('<br>');
    }
  }

  // Driver code
  var str = "geeksforgeeks";
  var len = str.length;
  printPattern(str, len);

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
g           s
 e         k
  e       e
   k     e
    s   g
     f r
      o
     f r
    s   g
   k     e
  e       e
 e         k
g           s
```

https://youtu . be/7 gyjmrezos

本文由 [**Dinesh T.P.D**](https://www.facebook.com/Dinesh.TP) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息