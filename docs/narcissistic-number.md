# 自恋号

> 原文:[https://www.geeksforgeeks.org/narcissistic-number/](https://www.geeksforgeeks.org/narcissistic-number/)

给定 N，检查是否是自恋数。
**注:**自恋数是一个数字，它是它自己的数字的总和，每个数字都是数字的幂

**示例:**

> **输入:** 153
> **输出:**是
> T6】解释: 1^3+5^3+3^3=153
> 
> **输入:** 1634
> **输出:**是
> T6】解释: 1^4+6^4+3^4+4^4=1634

**方法**是先统计数字的个数，然后提取每一个数字，然后用幂函数得到那个数字的幂，最后相加，和原来的数比较，看是不是自恋数。

以下是上述想法的实现。

## C++

```
// CPP program for checking of
// Narcissistic number
#include <bits/stdc++.h>
using namespace std;

// function to count digits
int countDigit(int n)
{
    if (n == 0)
        return 0;

    return 1 + countDigit(n / 10);
}

// Returns true if n is Narcissistic number
bool check(int n)
{
    // count the number of digits
    int l = countDigit(n);
    int dup = n;
    int sum = 0;

    // calculates the sum of digits
    // raised to power
    while (dup)
    {
        sum += pow(dup % 10, l);
        dup /= 10;
    }

    return (n == sum);
}

// Driver code
int main()
{
    int n = 1634;
    if (check(n))
        cout << "yes";
    else
        cout << "no";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for checking
// of Narcissistic number
import java.io.*;
import static java.lang.Math.*;
class narcissistic
{

// function to count digits
int countDigit(int n)
{
    if (n == 0)
        return 0;

    return 1 + countDigit(n / 10);
}

// Returns true if n is Narcissistic number
boolean check(int n)
{
    // count the number of digits
    int l = countDigit(n);
    int dup = n;
    int sum = 0;

    // calculates the sum of
    //digits raised to power
    while(dup > 0)
    {
        sum += pow(dup % 10, l);
        dup /= 10;
    }

    return (n == sum);
}

// Driver code
public static void main(String args[])
 {
    narcissistic obj = new narcissistic();
    int n = 1634;
    if (obj.check(n))
        System.out.println("yes");
    else
        System.out.println("no");
  }
}

//This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python 3 program for checking of
# Narcissistic number

# function to count digits
def countDigit(n) :
    if (n == 0) :
        return 0

    return (1 + countDigit(n // 10))

# Returns true if n is Narcissistic number
def check(n) :

    # Count the number of digits
    l = countDigit(n)
    dup = n; sm = 0

    # Calculates the sum of digits
    # raised to power
    while (dup) :
        sm = sm + pow(dup % 10, l)
        dup = dup // 10

    return (n == sm)

# Driver code
n = 1634
if (check(n)) :
    print( "yes")
else :
    print( "no")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program for checking
// of Narcissistic number
using System;

class narcissistic
{

    // function to count digits
    int countDigit(int n)
    {
        if (n == 0)
            return 0;

        return 1 + countDigit(n / 10);
    }

    // Returns true if n is Narcissistic number
    bool check(int n)
    {
        // count the number of digits
        int l = countDigit(n);
        int dup = n;
        int sum = 0;

        // calculates the sum of
        //digits raised to power
        while(dup > 0)
        {
            sum += (int)Math.Pow(dup % 10, l);
            dup /= 10;
        }

        return (n == sum);
    }

    // Driver code
    public static void Main()
    {
        narcissistic obj = new narcissistic();
        int n = 1634;
        if (obj.check(n))
            Console.WriteLine("yes");
        else
            Console.WriteLine("no");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for checking of
// Narcissistic number

// Function to count digits
function countDigit($n)
{
    if ($n == 0)
        return 0;

    return (1 + countDigit($n / 10));
}

// Returns true if n is
// Narcissistic number
function check( $n)
{
    // count the number of digits
    $l = countDigit($n);
    $dup = $n;
    $sum = 0;

    // calculates the sum of digits
    // raised to power
    while ($dup)
    {
        $sum += pow($dup % 10, $l);
        $dup = (int)$dup / 10;
    }

    return ($n == $sum);
}

// Driver Code
$n = 1634;
if (check(!$n))
    echo "yes";
else
    echo "no";

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program for checking of
// Narcissistic number

// Function to count digits
function countDigit(n)
{
    if (n == 0)
        return 0;

    return (1 + countDigit(n / 10));
}

// Returns true if n is
// Narcissistic number
function check( n)
{
    // count the number of digits
    let l = countDigit(n);
    let dup = n;
    let sum = 0;

    // calculates the sum of digits
    // raised to power
    while (dup)
    {
        sum += Math.pow(dup % 10, l);
        dup = parseINT(dup / 10);
    }

    return (n == sum);
}

// Driver Code
let n = 1634;
if (check(!n))
    document.write("yes");
else
    document.write("no");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output**

```
yes
```

**方法 2:使用字符串的简化方法**

我们必须将输入作为一个字符串，并通过字符串长度遍历每个字符的字符串计算能力。**注意:**这里字符串的长度给出了该数字的位数

下面是上述方法的实现

## C++14

```
// CPP program for checking of
// Narcissistic number
#include <bits/stdc++.h>
#include <string.h>
using namespace std;

string getResult(string st)
{
    int sum = 0;
    int length = st.length();

    // Traversing through the string
    for (int i = 0; i < length; i++)
    {
        // Since ascii value of numbers
        // starts from 48 so we subtract it from sum
        sum = sum + pow(st[i] - '0', length);
    }

    // Converting string to integer
    int number = stoi(st);

    // Comparing number and sum
    if (number == sum)
        return "yes";
    else
        return "no";
}

// Driver Code
int main()
{
    string st = "153";
    cout << getResult(st);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for checking of
// Narcissistic number
class GFG
{

static String getResult(String st)
{
    int sum = 0;
    int length = st.length();

    // Traversing through the string
    for (int i = 0; i < length; i++)
    {

        // Since ascii value of numbers
        // starts from 48 so we subtract it from sum
        sum = sum + (int)Math.pow(st.charAt(i) - '0', length);
    }

    // Converting string to integer
    int number = Integer.parseInt(st);

    // Comparing number and sum
    if (number == sum)
        return "yes";
    else
        return "no";
}

// Driver Code
public static void main(String []args)
{
    String st = "153";
    System.out.print(getResult(st));
}
}

// This code is contributed by rutvik_56.
```

## 蟒蛇 3

```
# Python program for checking of
# Narcissistic number

def getResult(st):
    sum = 0
    length = len(st)

    # Traversing through the string
    for i in st:

        # Converting character to int
        sum = sum + int(i) ** length

    # Converting string to integer
    number = int(st)

    # Comparing number and sum
    if (number == sum):
        return "true"
    else:
        return "false"

# Driver Code
# taking input as string
st = "153"
print(getResult(st))
```

## C#

```
// C# program for checking of
// Narcissistic number
using System;
class GFG
{

static string getResult(string st)
{
    int sum = 0;
    int length = st.Length;

    // Traversing through the string
    for (int i = 0; i < length; i++)
    {

        // Since ascii value of numbers
        // starts from 48 so we subtract it from sum
        sum = sum + (int)Math.Pow(st[i] - '0', length);
    }

    // Converting string to integer
    int number = int.Parse(st);

    // Comparing number and sum
    if (number == sum)
        return "yes";
    else
        return "no";
}

// Driver Code
public static void Main(string []args)
{
    string st = "153";
    Console.Write(getResult(st));
}
}

// This code is contributed by pratham76.
```

## java 描述语言

```
<script>
    // Javascript program for checking of
    // Narcissistic number

    function getResult(st)
    {
        let sum = 0;
        let length = st.length;

        // Traversing through the string
        for (let i = 0; i < length; i++)
        {

            // Since ascii value of numbers
            // starts from 48 so we subtract it from sum
            sum = sum + Math.pow(st[i] - '0', length);
        }

        // Converting string to integer
        let number = parseInt(st, 10);

        // Comparing number and sum
        if (number == sum)
            return "yes";
        else
            return "no";
    }

    let st = "153";
    document.write(getResult(st));

</script>
```

**Output**

```
yes
```

**参考文献:**[http://mathmandmultimedia . com/2012/01/16/自恋-数字/](http://mathandmultimedia.com/2012/01/16/narcissistic-numbers/)