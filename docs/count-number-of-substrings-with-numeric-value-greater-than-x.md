# 统计数值大于 X 的子串数量

> 原文:[https://www . geesforgeks . org/count-number-of-substrings-with-numeric-value-behind-x/](https://www.geeksforgeeks.org/count-number-of-substrings-with-numeric-value-greater-than-x/)

给定一个字符串“S”(由数字组成)和一个整数“X”，任务是计算满足以下条件的“S”的所有子字符串:

*   子字符串不能以数字“0”开头。
*   它所代表的数字必须大于“X”。

**注意:**如果两种选择子串的方式在不同的索引处开始或结束，则它们是不同的。

**示例:**

```
Input: S = "471", X = 47
Output: 2
Only the sub-strings "471" and "71" 
satisfy the given conditions.

Input: S = "2222", X = 97
Output: 3
Valid strings are "222", "222" and "2222". 
```

**进场:**

*   迭代字符串“S”的每个数字，并选择大于“0”的数字。
*   现在，从上一步中选择的字符开始获取所有可能的子字符串，并将每个子字符串转换为整数。
*   将上一步中的整数与“X”进行比较。如果数字大于“X”，则递增计数变量。
*   最后，打印计数变量的值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts
// valid sub-strings
int count(string S, int X)
{
    int count = 0;
    const int N = S.length();
    for (int i = 0; i < N; ++i) {

        // Only take those numbers
        // that do not start with '0'.
        if (S[i] != '0') {
            for (int len = 1; (i + len) <= N; ++len) {

                // converting the sub-string
                // starting from index 'i'
                // and having length 'len' to int
                // and checking if it is greater
                // than X or not
                if (stoi(S.substr(i, len)) > X)
                    count++;
            }
        }
    }
    return count;
}

// Driver code
int main()
{

    string S = "2222";
    int X = 97;
    cout << count(S, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
// Function that counts
// valid sub-strings
static int count(String S, int X)
{
    int count = 0;
    int N = S.length();
    for (int i = 0; i < N; ++i)
    {

        // Only take those numbers
        // that do not start with '0'.
        if (S.charAt(i) != '0')
        {
            for (int len = 1;
                (i + len) <= N; ++len)
            {

                // converting the sub-string
                // starting from index 'i'
                // and having length 'len' to
                // int and checking if it is
                // greater than X or not
                int num = Integer.parseInt(S.substring(i, i + len));
                if (num > X)
                    count++;
            }
        }
    }
    return count;
}

// Driver code
public static void main(String []args)
{
    String S = "2222";
    int X = 97;
    System.out.println(count(S, X));
}
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach

# Function that counts
# valid sub-strings
def countSubStr(S, X):

    cnt = 0
    N = len(S)

    for i in range(0, N):

        # Only take those numbers
        # that do not start with '0'.
        if (S[i] != '0'):

            j = 1
            while((j + i) <= N):

                # converting the sub-string
                # starting from index 'i'
                # and having length 'len' to
                # int and checking if it is
                # greater than X or not
                num = int(S[i : i + j])

                if (num > X):
                    cnt = cnt + 1

                j = j + 1

    return cnt;

# Driver code
S = "2222";
X = 97;
print(countSubStr(S, X))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function that counts
// valid sub-strings
static int count(string S, int X)
{
    int count = 0;
    int N = S.Length;
    for (int i = 0; i < N; ++i)
    {

        // Only take those numbers
        // that do not start with '0'.
        if (S[i] != '0')
        {
            for (int len = 1;
                (i + len) <= N; ++len)
            {

                // converting the sub-string
                // starting from index 'i'
                // and having length 'len' to int
                // and checking if it is greater
                // than X or not
                int num = Int32.Parse(S.Substring(i, len));
                if (num > X)
                    count++;
            }
        }
    }
    return count;
}

// Driver code
public static void Main(String []args)
{
    string S = "2222";
    int X = 97;
    Console.WriteLine(count(S, X));
}
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that counts
// valid sub-strings
function countSubStr($S, $X)
{
    $cnt = 0;
    $N = strlen($S);

    for ($i = 0; $i < $N; ++$i)
    {

        // Only take those numbers
        // that do not start w$ith '0'.
        if ($S[$i] != '0')
        {
            for ($len = 1;
                ($i + $len) <= $N; ++$len)
            {

                // converting the sub-str$ing
                // starting from index 'i'
                // and having length 'len' to int
                // and checking if it is greater
                // than X or not
                $num = intval(substr($S, $i, $len));

                if ($num > $X)
                    $cnt++;
            }
        }
    }
    return $cnt;
}

// Driver code
$S = "2222";
$X = 97;
echo countSubStr($S, $X);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that counts
// valid sub-strings
function count(S, X)
{
    var count = 0;
    var N = S.length;
    for (var i = 0; i < N; ++i) {

        // Only take those numbers
        // that do not start with '0'.
        if (S[i] != '0') {
            for (var len = 1; (i + len) <= N; ++len) {

                // converting the sub-string
                // starting from index 'i'
                // and having length 'len' to int
                // and checking if it is greater
                // than X or not
                if (parseInt(S.substring(i, i+len)) > X)
                    count++;
            }
        }
    }
    return count;
}

// Driver code
var S = "2222";
var X = 97;
document.write( count(S, X));

</script>
```

**Output:** 

```
3
```