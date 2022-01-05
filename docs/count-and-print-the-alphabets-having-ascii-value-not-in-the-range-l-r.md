# 计数并打印 ASCII 值不在[l，r]

范围内的字母

> 原文:[https://www . geesforgeks . org/count-and-print-the-alphabets-having-ascii-value-not-in-range-l-r/](https://www.geeksforgeeks.org/count-and-print-the-alphabets-having-ascii-value-not-in-the-range-l-r/)

给定一个字符串 **str** ，任务是计算具有 ASCII 值的字母数量，不在[l，r]范围内。
**例:**

```
Input: str = "geeksforgeeks", l = 102, r = 111
Output: Count = 7
Characters - e, s, r have ascii values not in the range [102, 111].

Input: str = "GeEkS", l = 80, r = 111
Output: Count = 2
```

**方法:**开始遍历字符串，检查当前字符的 ASCII 值是否小于等于 r 且大于等于 l。如果否，则增加计数并打印该元素。
以下是上述办法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of characters
// whose ascii value not in range [l, r]
int CountCharacters(string str, int l, int r)
{
    // Initializing the count to 0
    int cnt = 0;

    // using map to print a character only once
    unordered_map<char, int> m;
    int len = str.length();
    for (int i = 0; i < len; i++) {

        // Increment the count
        // if the value is less
        if (!(l <= str[i] and str[i] <= r)) {
            cnt++;
            if (m[str[i]] != 1) {
                cout << str[i] << " ";
            m[str[i]]++;
            }
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
            " not in the range [l, r] \nin the given string are: ";
    cout << "\nand their count is " << CountCharacters(str, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class Solution
{

// Function to count the number of characters
// whose ascii value not in range [l, r]
static int CountCharacters(String str, int l, int r)
{
    // Initializing the count to 0
    int cnt = 0;

    // using map to print a character only once
    Map<Character, Integer> m= new HashMap<Character, Integer>();
    int len = str.length();
    for (int i = 0; i < len; i++) {

        // Increment the count
        // if the value is less
        if (!(l <= str.charAt(i) && str.charAt(i) <= r)) {
            cnt++;
            if(m.get(str.charAt(i))!=null)
            if (m.get(str.charAt(i)) != 1) {
                System.out.print(str.charAt(i) + " ");
            m.put(str.charAt(i),m.get(str.charAt(i))==null?0:m.get(str.charAt(i))+1);
            }
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

    System.out.println( "Characters with ASCII values not in the range [l, r] \nin the given string are: ");
     System.out.println(  "\nand their count is " + CountCharacters(str, l, r));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to count the number of
# characters whose ascii value not
# in range [l, r]
def CountCharacters(str, l, r):

    # Initializing the count to 0
    cnt = 0

    # using map to pra character
    # only once
    m = {}
    length = len(str)
    for i in range(0, length):

        # Increment the count if the
        # value is less
        if (not(l <= ord(str[i]) and
                     ord(str[i]) <= r)):
            cnt += 1
            if ord(str[i]) not in m:
                m[ord(str[i])] = 0
                print(str[i], end = " ")
            m[ord(str[i])] += 1

    # return the count
    return cnt

# Driver Code
if __name__ == '__main__':

    str = "geeksforgeeks"
    str = str.strip()
    l = 102
    r = 111
    print("Characters with ASCII values", end = "")
    print(" not in the range [l, r]\n",
          "in the given string are: ", end = "")
    print("\nand their count is ",
            CountCharacters(str, l, r))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to count the number of characters
// whose ascii value not in range [l, r]
static int CountCharacters(string str, int l, int r)
{

    // Initializing the count to 0
    int cnt = 0;

    // using map to print a character only once
    Dictionary<char, int> m = new Dictionary<char, int>();
    int len = str.Length;
    for (int i = 0; i < len; i++)
    {

        // Increment the count
        // if the value is less
        if (!(l <= str[i] && str[i] <= r))
        {
            cnt++;
            if(!m.ContainsKey(str[i]))
            {
                m[str[i]] = 0;
                Console.Write(str[i] + " ");
            }
            m[str[i]]++;
        }
    }

    // return the count
    return cnt;
}

// Driver code
public static void Main(string []args)
{
    string str = "geeksforgeeks";
    int l = 102, r = 111;   
    Console.Write( "Characters with ASCII values" +
                  "not in the range [l, r] \nin" +
                  "the given string are: ");
     Console.WriteLine( "\nand their count is " +
                       CountCharacters(str, l, r));
}
}

// This code is contributed by rutvik_56
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count the number of characters
// whose ascii value not in range [l, r]
function CountCharacters($str, $l, $r)
{
    // Initializing the count to 0
    $cnt = 0;

    // using map to print a character
    // only once
    $m = array_fill(0, 256, NULL);
    $len = strlen($str);
    for ($i = 0; $i < $len; $i++)
    {

        // Increment the count
        // if the value is less
        if (!($l <= ord($str[$i]) and
                    ord($str[$i]) <= $r))
        {
            $cnt++;
            if (isset($m[ord($str[$i])]) != 1)
            {
                echo $str[$i] . " ";
                $m[ord($str[$i])]++;
            }
        }
    }
    // return the count
    return $cnt;
}

// Driver code
$str = "geeksforgeeks";
$l = 102;
$r = 111;
echo "Characters with ASCII values not in the " .
      "range [l, r] \nin the given string are: ";
echo "\nand their count is " .
       CountCharacters($str, $l, $r);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to count the number of characters
// whose ascii value not in range [l, r]
function CountCharacters(str,l,r)
{
    // Initializing the count to 0
    let cnt = 0;

    // using map to print a character only once
    let m= new Map();
    let len = str.length;
    for (let i = 0; i < len; i++) {

        // Increment the count
        // if the value is less
        if (!(l <= str[i].charCodeAt(0) &&
        str[i].charCodeAt(0) <= r)) {
            cnt++;
            if(!m.has(str[i]))
            {
                m.set(str[i],0);
                document.write(str[i] + " ");
            }   
            m.set(str[i],m.get(str[i]+1));
        }
    }
    // return the count
    return cnt;
}

// Driver code

let str = "geeksforgeeks";
let l = 102, r = 111;

document.write( "Characters with ASCII values " +
"not in the range [l, r] <br>in the given string are: ");

document.write(  "<br>and their count is " +
CountCharacters(str, l, r));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:**

```
Characters with ASCII values not in the range [l, r] 
in the given string are: e s r 
and their count is 7
```

**时间复杂度:** O(n)，其中 n 为字符串长度。