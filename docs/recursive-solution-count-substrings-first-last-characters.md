# 计算第一个和最后一个字符相同的子串的递归解

> 原文:[https://www . geesforgeks . org/recursive-solution-count-substrings-first-last-characters/](https://www.geeksforgeeks.org/recursive-solution-count-substrings-first-last-characters/)

给我们一个字符串，我们需要找到以相同字符开始和结束的所有连续子字符串的计数。

示例:

```
Input  : S = "abcab"
Output : 7
There are 15 substrings of "abcab"
a, ab, abc, abca, abcab, b, bc, bca
bcab, c, ca, cab, a, ab, b
Out of the above substrings, there 
are 7 substrings : a, abca, b, bcab, 
c, a and b.

Input  : S = "aba"
Output : 4
The substrings are a, b, a and aba
```

我们在下面的帖子中讨论了不同的解决方案。
[统计前后字符相同的子串](https://www.geeksforgeeks.org/count-substrings-with-same-first-and-last-characters/)
本文讨论了一个简单的递归解决方案。

## C++

```
// c++ program to count substrings with same
// first and last characters
#include <iostream>
#include <string>
using namespace std;

/* Function to count substrings with same first and
  last characters*/
int countSubstrs(string str, int i, int j, int n)
{
    // base cases
    if (n == 1)
        return 1;
    if (n <= 0)
        return 0;

    int res =  countSubstrs(str, i + 1, j, n - 1) + 
               countSubstrs(str, i, j - 1, n - 1) -
               countSubstrs(str, i + 1, j - 1, n - 2);           

    if (str[i] == str[j])
        res++;

    return res;
}

// driver code
int main()
{
    string str = "abcab";
    int n = str.length();
    cout << countSubstrs(str, 0, n - 1, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count substrings
// with same first and last characters

class GFG
{
    // Function to count substrings
    // with same first and
    // last characters
    static int countSubstrs(String str, int i,
                                         int j, int n)
    {
        // base cases
        if (n == 1)
            return 1;
        if (n <= 0)
            return 0;

        int res = countSubstrs(str, i + 1, j, n - 1) +
                countSubstrs(str, i, j - 1, n - 1) -
                countSubstrs(str, i + 1, j - 1, n - 2);        

        if (str.charAt(i) == str.charAt(j))
            res++;

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "abcab";
        int n = str.length();
        System.out.print(countSubstrs(str, 0, n - 1, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to count substrings with same
# first and last characters

# Function to count substrings with same first and
# last characters
def countSubstrs(str, i, j, n):

    # base cases
    if (n == 1):
        return 1
    if (n <= 0):
        return 0

    res = (countSubstrs(str, i + 1, j, n - 1)
        + countSubstrs(str, i, j - 1, n - 1)
        - countSubstrs(str, i + 1, j - 1, n - 2))    

    if (str[i] == str[j]):
        res += 1

    return res

# driver code
str = "abcab"
n = len(str)
print(countSubstrs(str, 0, n - 1, n))

# This code is contributed by Smitha
```

## C#

```
// C# program to count substrings
// with same first and last characters
using System;

class GFG {

    // Function to count substrings
    // with same first and
    // last characters
    static int countSubstrs(string str, int i,
                                 int j, int n)
    {

        // base cases
        if (n == 1)
            return 1;
        if (n <= 0)
            return 0;

        int res = countSubstrs(str, i + 1, j, n - 1)
                + countSubstrs(str, i, j - 1, n - 1)
            - countSubstrs(str, i + 1, j - 1, n - 2);    

        if (str[i] == str[j])
            res++;

        return res;
    }

    // Driver code
    public static void Main ()
    {
        string str = "abcab";
        int n = str.Length;

        Console.WriteLine(
                countSubstrs(str, 0, n - 1, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// substrings with same
// first and last characters

//Function to count substrings
// with same first and
// last characters
function countSubstrs($str, $i,
                      $j, $n)
{

    // base cases
    if ($n == 1)
        return 1;
    if ($n <= 0)
        return 0;

    $res = countSubstrs($str, $i + 1, $j, $n - 1) +
           countSubstrs($str, $i, $j - 1, $n - 1) -
           countSubstrs($str, $i + 1, $j - 1, $n - 2);    

    if ($str[$i] == $str[$j])
        $res++;

    return $res;
}

// Driver Code
$str = "abcab";
$n = strlen($str);
echo(countSubstrs($str, 0, $n - 1, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to count substrings
// with same first and last characters

// Function to count substrings
// with same first and
// last characters
function countSubstrs(str, i, j, n)
{

    // Base cases
    if (n == 1)
        return 1;
    if (n <= 0)
        return 0;

    let res = countSubstrs(str, i + 1, j, n - 1) +
              countSubstrs(str, i, j - 1, n - 1) -
          countSubstrs(str, i + 1, j - 1, n - 2);    

    if (str[i] == str[j])
        res++;

    return res;
}

// Driver code
let str = "abcab";
let n = str.length;

document.write(countSubstrs(str, 0, n - 1, n));

// This code is contributed by rameshtravel07

</script>
```

**Output**

```
7
```