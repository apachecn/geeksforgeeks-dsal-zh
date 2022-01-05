# 互换琴弦的第一和第二部分

> 原文:[https://www . geesforgeks . org/interchanging-first-second-half-stings/](https://www.geeksforgeeks.org/interchanging-first-second-halves-stings/)

给定两根弦![a    ](img/e601e610cd0f8488d8b71390172c9e86.png "Rendered by QuickLaTeX.com")和![b    ](img/56c19e62ea115719245402c109e4c477.png "Rendered by QuickLaTeX.com")。通过将一根弦的前半部分和后半部分分别与另一根弦的前半部分和后半部分交换来创建两根新弦。

**示例:**

```
Input : fighter
        warrior
Output :warhter
        figrior

Input :remuneration
       day
Output :dration
        remuneay
```

在第一个例子中，**战斗机**由两部分组成**图**和**图**。同样的，**战士**也是由两部分组成**战**和**瑞奥**。互换两根弦的第一部分，创建两根新弦**和**以及**和**。类似地，在第二个示例中，**报酬的第一部分**即 **remune** 与**日的第一部分**交换，以创建 **dration** 和 **remuneay** 。

## C++

```
// CPP code to create two new strings
// by swapping first and second halves
#include<bits/stdc++.h>
using namespace std;

// Function to concatenate two
// different halves of given strings
void swapTwoHalves(string a , string b)
{
    int la = a.length();
    int lb = b.length();

    // Creating new strings by
    // exchanging the first half
    // of a and b. Please refer below for
    // details of substr.
    // https://www.geeksforgeeks.org/stdsubstr-in-ccpp/
    string c = a.substr(0, la/2) +
               b.substr(lb/2, lb);
    string d = b.substr(0, lb/2) +
               a.substr(la/2, la);

    cout << c << endl << d << endl;
}

// Driver function
int main()
{
    string a = "remuneration";
    string b = "day";
    swapTwoHalves(a, b);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to create two new strings
// by swapping first and second halves
import java.io.*;
class ns
{

    // Function to concatenate two
    // different halves of given strings
    public static void swapTwoHalves(String a,
                                     String b)
    {
        int la = a.length();
        int lb = b.length();

        // Creating new strings by
        // exchanging the first half
        // of a and b. Please refer below
        // for details of substring.
        // https://www.geeksforgeeks.org/java-lang-string-substring-java/
        String c = a.substring(0,la/2) +
                   b.substring(lb/2,lb);
        String d = b.substring(0,lb/2) +
                  a.substring(la/2,la);

        System.out.println(c + "\n" + d);
    }
    public static void main (String args[])
    {
        // Given strings
        String a = "remuneration";
        String b = "day";

        // Calling function
        swapTwoHalves(a, b);
    }
}
```

## 蟒蛇 3

```
# Python 3 code to create two new strings
# by swapping first and second halves

# Function to concatenate two
# different halves of given strings
def swapTwoHalves( a ,b) :
    la = len(a)
    lb = len(b)

    # Creating new strings by
    # exchanging the first half
    # of a and b. Please refer below for
    # details of substr.
    # https://www.geeksforgeeks.org/stdsubstr-in-ccpp/
    c = a[0:la//2] + b[lb//2: lb]
    d = b[0: lb//2] + a[la//2: la]

    print( c, "\n" , d )

# Driver function
a = "remuneration"
b = "day"
swapTwoHalves(a, b)

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# code to create two
// new strings by swapping
// first and second halves
using System;

class GFG
{
    // Function to concatenate
    // two different halves
    // of given strings
    static void swapTwoHalves(string a ,
                              string b)
    {
        int la = a.Length;
        int lb = b.Length;

        // Creating new strings
        // by exchanging the
        // first half of a and b.
        string c = a.Substring(0, la / 2) +
                   b.Substring(lb / 2,
                               lb / 2 + 1);
        string d = b.Substring(0, lb / 2) +
                   a.Substring(la / 2,
                               la / 2);

        Console.Write (c + "\n" +
                       d + "\n");
    }    

    // Driver Code
    static void Main()
    {
        string a = "remuneration";
        string b = "day";
        swapTwoHalves(a, b);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to create two
// new strings by swapping
// first and second halves

// Function to concatenate 
// two different halves of
// given strings
function swapTwoHalves($a , $b)
{
    $la = strlen($a);
    $lb = strlen($b);

    // Creating new strings
    // by exchanging the first
    // half of a and b.
    $c = substr($a, 0, intval($la / 2)) .
         substr($b, intval($lb / 2), $lb);
    $d = substr($b, 0, intval($lb / 2)) .
         substr($a, intval($la / 2), $la);

    echo ($c . "\n" .
          $d . "\n");
}

// Driver Code
$a = "remuneration";
$b = "day";

swapTwoHalves($a, $b);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript code to create two new strings
// by swapping first and second halves
// Function to concatenate two
// different halves of given strings
function swapTwoHalves(a, b)
    {
        var la = a.length;
        var lb = b.length;

        // Creating new strings by
        // exchanging the first half
        // of a and b. Please refer below
        // for details of substring.
        // https://www.geeksforgeeks.org/java-lang-string-substring-java/
        var c = a.substring(0,la/2) +
                   b.substring(lb/2,lb);
        var d = b.substring(0,lb/2) +
                  a.substring(la/2,la);

        document.write(c +"<br>" + "\n" + d);
    }

        // Given strings
        var a = "remuneration";
        var b = "day";

        // Calling function
        swapTwoHalves(a, b);

// This code is contributed by shivanisinghss2110
</script>
```

**输出:**

```
remuneay
dration 
```