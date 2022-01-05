# 计数并打印 ASCII 值在[l，r]

范围内的字母

> 原文:[https://www . geesforgeks . org/count-and-print-the-alphabets-having-ascii-value-in-l-r/](https://www.geeksforgeeks.org/count-and-print-the-alphabets-having-ascii-value-in-the-range-l-r/)

给定一个字符串 **str** ，任务是计算 ascii 在[l，r]范围内的字母数量。
**例:**

```
Input: str = "geeksforgeeks"
        l = 102, r = 111
Output: Count = 6, Characters = g, f, k, o
Characters - g, f, k, o have ascii values in the range [102, 111].

Input: str = "GeEkS"
        l = 80, r = 111
Output: Count = 3, Characters = e, k, S 
```

**方法:**开始遍历字符串，检查当前字符的 ASCII 值是否小于等于 r 且大于等于 l。如果是，则增加计数并打印该元素。
以下是上述办法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// characters whose ascii value is in range [l, r]
int CountCharacters(string str, int l, int r)
{
    // Initializing the count to 0
    int cnt = 0;

    int len = str.length();
    for (int i = 0; i < len; i++) {

        // Increment the count
        // if the value is less
        if (l <= str[i] and str[i] <= r) {
            cnt++;
            cout << str[i] << " ";
        }
    }

    // return the count
    return cnt;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int l = 102, r = 111;

    cout << "Characters with ASCII values"
            " in the range [l, r] are \n";
    cout << "\nand their count is " << CountCharacters(str, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.lang.*;

class GFG
{
// Function to count the number
// of characters whose ascii
// value is in range [l, r]
static int CountCharacters(String str,
                        int l, int r)
{
    // Initializing the count to 0
    int cnt = 0;

    int len = str.length();
    for (int i = 0; i < len; i++)
    {

        // Increment the count
        // if the value is less
        if (l <= str.charAt(i) && str.charAt(i) <= r)
        {
            cnt++;
            System.out.print(str.charAt(i) + " ");
        }
    }

    // return the count
    return cnt;
}

// Driver code
public static void main(String args[])
{
    String str = "geeksforgeeks";
    int l = 102, r = 111;

    System.out.print("Characters with ASCII values" +
                " in the range [l, r] are \n");
    System.out.print("\nand their count is " +
                CountCharacters(str, l, r));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count the number of characters
# whose ascii value is in range [l, r]
def CountCharacters(str1, l, r):

    # Initializing the count to 0
    cnt = 0;

    len1 = len(str1)
    for i in str1:

        # Increment the count
        # if the value is less
        if (l <= ord(i) and ord(i) <= r):
            cnt = cnt + 1
            print(i, end = " ")

    # return the count
    return cnt

# Driver code
if __name__=='__main__':

    str1 = "geeksforgeeks"
    l = 102
    r = 111

    print("Characters with ASCII values " +
                "in the range [l, r] are")
    print("\nand their count is ",
            CountCharacters(str1, l, r))

# This code is contributed by
# Kirti_Mangal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// Function to count the number
// of characters whose ascii
// value is in range [l, r]
static int CountCharacters(string str,
                           int l, int r)
{
    // Initializing the count to 0
    int cnt = 0;

    int len = str.Length;
    for (int i = 0; i < len; i++)
    {

        // Increment the count
        // if the value is less
        if (l <= str[i] && str[i] <= r)
        {
            cnt++;
            Console.Write(str[i] + " ");
        }
    }

    // return the count
    return cnt;
}

// Driver code
public static void Main()
{
    string str = "geeksforgeeks";
    int l = 102, r = 111;

    Console.Write("Characters with ASCII values" +
                   " in the range [l, r] are \n");
    Console.Write("\nand their count is " +
                  CountCharacters(str, l, r));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count the number of
// characters whose ascii value is
// in range [l, r]
function CountCharacters($str, $l, $r)
{
    // Initializing the count to 0
    $cnt = 0;

    $len = strlen($str);
    for ($i = 0; $i < $len; $i++)
    {

        // Increment the count
        // if the value is less
        if ($l <= ord($str[$i]) &&
                  ord($str[$i]) <= $r)
        {
            $cnt++;
            echo $str[$i] ." ";
        }
    }

    // return the count
    return $cnt;
}

// Driver code
$str = "geeksforgeeks";
$l = 102;
$r = 111;

echo "Characters with ASCII values" .
       " in the range [l, r] are \n";
echo "\nand their count is " .
       CountCharacters($str, $l, $r);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // Function to count the number
// of characters whose ascii
// value is in range [l, r]
    function CountCharacters(str,l,r)
    {
        // Initializing the count to 0
    let cnt = 0;

    let len = str.length;
    for (let i = 0; i < len; i++)
    {

        // Increment the count
        // if the value is less
        if (l <= str[i].charCodeAt(0) && str[i].charCodeAt(0) <= r)
        {
            cnt++;
            document.write(str[i] + " ");
        }
    }

    // return the count
    return cnt;
    }

    // Driver code
    let str = "geeksforgeeks";
    let l = 102, r = 111;
    document.write("Characters with ASCII values" +
                " in the range [l, r] are <br>");

    document.write("<br>and their count is " +
                CountCharacters(str, l, r));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Characters with ASCII values in the range [l, r] are 
g k f o g k 
and their count is 6
```

**时间复杂度**–O(N)