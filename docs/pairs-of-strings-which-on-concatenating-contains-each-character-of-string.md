# 成对的字符串，在连接时包含“字符串”的每个字符

> 原文:[https://www . geeksforgeeks . org/成对字符串串联包含每个字符串字符/](https://www.geeksforgeeks.org/pairs-of-strings-which-on-concatenating-contains-each-character-of-string/)

给定一组字符串 **arr[]** 。任务是找到无序的字符串对的计数 **(arr[i]，arr[j])** ，其在串联中包括字符串“string”的每个字符至少一次。

**示例:**

> **输入:**arr[]= {“s”，“ng”，“stri”}
> **输出:** 1
> (arr[1]，arr[2])是在串联
> 时唯一包含字符串“string”
> 的每个字符的对，即 arr[1]+arr[2]=“ngstri”
> 
> **输入:**arr[]= {“stri”、“ing”、“string”}
> **输出:** 3

**方式:**将给定字符串存储为位掩码，即字符串**“srin”**将存储为 **101110** 因为**【t】**和**【g】**缺失，所以它们对应的位为 **0** 。现在，创建一个大小为 **64** 的数组，这是获得的位掩码的最大可能值 **(0 (000000)到 63 (111111))** 。现在，问题简化为找到这些位掩码对的计数，这些位掩码将 **63(二进制 111111)**作为它们的或值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 64

// Function to return the bitmask for the string
int getBitmask(string s)
{
    int temp = 0;
    for (int j = 0; j < s.length(); j++) {
        if (s[j] == 's') {
            temp = temp | (1);
        }
        else if (s[j] == 't') {
            temp = temp | (2);
        }
        else if (s[j] == 'r') {
            temp = temp | (4);
        }
        else if (s[j] == 'i') {
            temp = temp | (8);
        }
        else if (s[j] == 'n') {
            temp = temp | (16);
        }
        else if (s[j] == 'g') {
            temp = temp | (32);
        }
    }

    return temp;
}

// Function to return the count of pairs
int countPairs(string arr[], int n)
{

    // bitMask[i] will store the count of strings
    // from the array whose bitmask is i
    int bitMask[MAX] = { 0 };
    for (int i = 0; i < n; i++)
        bitMask[getBitmask(arr[i])]++;

    // To store the count of pairs
    int cnt = 0;
    for (int i = 0; i < MAX; i++) {
        for (int j = i; j < MAX; j++) {

            // MAX - 1 = 63 i.e. 111111 in binary
            if ((i | j) == (MAX - 1)) {

                // arr[i] cannot make s pair with itself
                // i.e. (arr[i], arr[i])
                if (i == j)
                    cnt += ((bitMask[i] * bitMask[i] - 1) / 2);
                else
                    cnt += (bitMask[i] * bitMask[j]);
            }
        }
    }
    return cnt;
}

// Driver code
int main()
{
    string arr[] = { "strrr", "string", "gstrin" };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG
{

static int MAX = 64;

// Function to return the bitmask for the string
static int getBitmask(char[] s)
{
    int temp = 0;
    for (int j = 0; j < s.length; j++)
    {
        switch (s[j])
        {
            case 's':
                temp = temp | (1);
                break;
            case 't':
                temp = temp | (2);
                break;
            case 'r':
                temp = temp | (4);
                break;
            case 'i':
                temp = temp | (8);
                break;
            case 'n':
                temp = temp | (16);
                break;
            case 'g':
                temp = temp | (32);
                break;
            default:
                break;
        }
    }

    return temp;
}

// Function to return the count of pairs
static int countPairs(String arr[], int n)
{

    // bitMask[i] will store the count of strings
    // from the array whose bitmask is i
    int []bitMask = new int[MAX];
    for (int i = 0; i < n; i++)
        bitMask[getBitmask(arr[i].toCharArray())]++;

    // To store the count of pairs
    int cnt = 0;
    for (int i = 0; i < MAX; i++)
    {
        for (int j = i; j < MAX; j++)
        {

            // MAX - 1 = 63 i.e. 111111 in binary
            if ((i | j) == (MAX - 1))
            {

                // arr[i] cannot make s pair with itself
                // i.e. (arr[i], arr[i])
                if (i == j)
                    cnt += ((bitMask[i] * bitMask[i] - 1) / 2);
                else
                    cnt += (bitMask[i] * bitMask[j]);
            }
        }
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    String arr[] = { "strrr", "string", "gstrin" };
    int n = arr.length;
    System.out.println(countPairs(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 64

# Function to return the bitmask
# for the string
def getBitmask(s):

    temp = 0
    for j in range(len(s)):
        if (s[j] == 's'):
            temp = temp | 1
        elif (s[j] == 't'):
            temp = temp | 2
        elif (s[j] == 'r'):
            temp = temp | 4
        elif (s[j] == 'i'):
            temp = temp | 8
        elif (s[j] == 'n'):
            temp = temp | 16
        elif (s[j] == 'g'):
            temp = temp | 32

    return temp

# Function to return the count of pairs
def countPairs(arr, n):

    # bitMask[i] will store the count of strings
    # from the array whose bitmask is i
    bitMask = [0 for i in range(MAX)]

    for i in range(n):
        bitMask[getBitmask(arr[i])] += 1

    # To store the count of pairs
    cnt = 0
    for i in range(MAX):
        for j in range(i, MAX):

            # MAX - 1 = 63 i.e. 111111 in binary
            if ((i | j) == (MAX - 1)):

                # arr[i] cannot make s pair with itself
                # i.e. (arr[i], arr[i])
                if (i == j):
                    cnt += ((bitMask[i] *
                             bitMask[i] - 1) // 2)
                else:
                    cnt += (bitMask[i] * bitMask[j])

    return cnt

# Driver code
arr = ["strrr", "string", "gstrin"]
n = len(arr)
print(countPairs(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;

class GFG
{

static int MAX = 64;

// Function to return the bitmask for the string
static int getBitmask(char[] s)
{
    int temp = 0;
    for (int j = 0; j < s.Length; j++)
    {
        switch (s[j])
        {
            case 's':
                temp = temp | (1);
                break;
            case 't':
                temp = temp | (2);
                break;
            case 'r':
                temp = temp | (4);
                break;
            case 'i':
                temp = temp | (8);
                break;
            case 'n':
                temp = temp | (16);
                break;
            case 'g':
                temp = temp | (32);
                break;
            default:
                break;
        }
    }

    return temp;
}

// Function to return the count of pairs
static int countPairs(String []arr, int n)
{

    // bitMask[i] will store the count of strings
    // from the array whose bitmask is i
    int []bitMask = new int[MAX];
    for (int i = 0; i < n; i++)
        bitMask[getBitmask(arr[i].ToCharArray())]++;

    // To store the count of pairs
    int cnt = 0;
    for (int i = 0; i < MAX; i++)
    {
        for (int j = i; j < MAX; j++)
        {

            // MAX - 1 = 63 i.e. 111111 in binary
            if ((i | j) == (MAX - 1))
            {

                // arr[i] cannot make s pair with itself
                // i.e. (arr[i], arr[i])
                if (i == j)
                    cnt += ((bitMask[i] * bitMask[i] - 1) / 2);
                else
                    cnt += (bitMask[i] * bitMask[j]);
            }
        }
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    String []arr = { "strrr", "string", "gstrin" };
    int n = arr.Length;
    Console.WriteLine(countPairs(arr, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAX = 64;

// Function to return the bitmask for the string
function getBitmask($s)
{
    $temp = 0;
    for ($j = 0; $j < strlen($s); $j++)
    {
        if ($s[$j] == 's')
        {
            $temp = $temp | (1);
        }
        else if ($s[$j] == 't')
        {
            $temp = $temp | (2);
        }
        else if ($s[$j] == 'r')
        {
            $temp = $temp | (4);
        }
        else if ($s[$j] == 'i')
        {
            $temp = $temp | (8);
        }
        else if ($s[$j] == 'n')
        {
            $temp = $temp | (16);
        }
        else if ($s[$j] == 'g')
        {
            $temp = $temp | (32);
        }
    }

    return $temp;
}

// Function to return the count of pairs
function countPairs($arr, $n)
{

    // bitMask[i] will store the count of strings
    // from the array whose bitmask is i
    $bitMask = array_fill(0, $GLOBALS['MAX'], 0);

    for ($i = 0; $i < $n; $i++)
        $bitMask[getBitmask($arr[$i])]++;

    // To store the count of pairs
    $cnt = 0;
    for ($i = 0; $i < $GLOBALS['MAX']; $i++)
    {
        for ($j = $i; $j < $GLOBALS['MAX']; $j++)
        {

            // MAX - 1 = 63 i.e. 111111 in binary
            if (($i | $j) == ($GLOBALS['MAX'] - 1))
            {

                // arr[i] cannot make s pair with itself
                // i.e. (arr[i], arr[i])
                if ($i == $j)
                    $cnt += floor(($bitMask[$i] *
                                   $bitMask[$i] - 1) / 2);
                else
                    $cnt += ($bitMask[$i] * $bitMask[$j]);
            }
        }
    }
    return $cnt;
}

// Driver code
$arr = array( "strrr", "string", "gstrin" );
$n = count($arr);

echo countPairs($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the
      // above approach
      const MAX = 64;

      // Function to return the bitmask for the string
      function getBitmask(s) {
        var temp = 0;
        for (var j = 0; j < s.length; j++) {
          switch (s[j]) {
            case "s":
              temp = temp | 1;
              break;
            case "t":
              temp = temp | 2;
              break;
            case "r":
              temp = temp | 4;
              break;
            case "i":
              temp = temp | 8;
              break;
            case "n":
              temp = temp | 16;
              break;
            case "g":
              temp = temp | 32;
              break;
            default:
              break;
          }
        }

        return temp;
      }

      // Function to return the count of pairs
      function countPairs(arr, n) {
        // bitMask[i] will store the count of strings
        // from the array whose bitmask is i
        var bitMask = new Array(MAX).fill(0);
        for (var i = 0; i < n; i++)
            bitMask[getBitmask(arr[i].split(""))]++;

        // To store the count of pairs
        var cnt = 0;
        for (var i = 0; i < MAX; i++) {
          for (var j = i; j < MAX; j++) {
            // MAX - 1 = 63 i.e. 111111 in binary
            if ((i | j) === MAX - 1) {
              // arr[i] cannot make s pair with itself
              // i.e. (arr[i], arr[i])
              if (i === j)
                  cnt += parseInt((bitMask[i] * bitMask[i] - 1) / 2);
              else
                  cnt += bitMask[i] * bitMask[j];
            }
          }
        }
        return cnt;
      }

      // Driver code
      var arr = ["strrr", "string", "gstrin"];
      var n = arr.length;
      document.write(countPairs(arr, n));
</script>
```

**Output:** 

```
3
```

时间复杂度:O(n * |s| + MAX <sup>2</sup> )

辅助空间:0(最大)