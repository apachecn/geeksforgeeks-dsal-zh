# 奇数二进制串的旋转

> 原文:[https://www . geeksforgeeks . org/带奇数的二进制字符串的旋转数/](https://www.geeksforgeeks.org/rotations-of-a-binary-string-with-odd-value/)

给定一个二进制字符串。我们可以在不改变字符串中位的相对顺序的情况下进行字符串的循环旋转。
例如，字符串“011001”所有可能的圆周旋转为:

```
101100
010110
001011
100101
110010
```

我们被要求通过做圆周旋转来告诉二进制串的**不同的**奇数十进制等价可能的总数。
**例:**

```
Input : 011001 
Output : 3
Explanation:
All odd possible binary representations are:
["011001", "001011", "100101"]

Input : 11011
Output : 4
Explanation:
All odd possible binary representations are:
["11011", "01111", "10111", "11101"]
```

**概念:**
可以观察到，二进制串只有最后一位为 1 时才是奇数，因为最后一位的值是 2^0.因此，既然我们在做圆周旋转。

## C++

```
// CPP program to find count of rotations
// with odd value.
#include <bits/stdc++.h>
using namespace std;

// function to calculate total odd decimal
// equivalent
int oddEquivalent(string s, int n)
{
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (s[i] == '1')
            count++;
    }
    return count;
}

// Driver code
int main()
{
    string s = "1011011";
    int n = s.length();
    cout << oddEquivalent(s, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of rotations
// with odd value.

class solution
{
static int oddEquivalent(String s, int n)
{

int count = 0;
// function to calculate total odd decimal
// equivalent
for (int i = 0; i < n; i++)
    {
        if(s.charAt(i) == '1')
            count++;
    }
    return count;
}

// Driver code
public static void main(String ar[])
{

String s = "1011011";
int n = s.length();
System.out.println(oddEquivalent(s, n));

}
}
//This code is contributed
//By Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find count
# of rotations with odd value

#function to calculate total odd equivalent
def oddEquivalent(s, n):
    count=0
    for i in range(0,n):
        if (s[i] == '1'):
            count = count + 1
    return count

#Driver code
if __name__=='__main__':
    s = "1011011"
    n = len(s)
    print(oddEquivalent(s, n))

# this code is contributed by Shashank_Sharma
```

## C#

```
// C# program to find count of
// rotations with odd value.
using System;

class GFG
{
static int oddEquivalent(String s, int n)
{
    int count = 0;

    // function to calculate total
    // odd decimal equivalent
    for (int i = 0; i < n; i++)
        {
            if(s[i] == '1')
                count++;
        }
    return count;
}

// Driver code
public static void Main()
{
    String s = "1011011";
    int n = s.Length;
    Console.WriteLine(oddEquivalent(s, n));
}
}

// This code is contributed
// by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count
// of rotations with odd value.

// function to calculate total
// odd decimal equivalent
function oddEquivalent($s, $n)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($s[$i] == '1')
            $count++;
    }
    return $count;
}

// Driver code
$s = "1011011";
$n = strlen($s);
echo(oddEquivalent($s, $n));

// This code is contributed
// by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript program to find count of rotations
// with odd value.

// function to calculate total odd decimal
// equivalent
function oddEquivalent(s, n)
{
    var count = 0;
    for (var i = 0; i < n; i++) {
        if (s[i] == '1')
            count++;
    }
    return count;
}

// Driver code
var s = "1011011";
var n = s.length;
document.write( oddEquivalent(s, n));

</script>   
```

**Output:** 

```
5
```