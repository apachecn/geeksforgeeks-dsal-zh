# 一个数的所有子序列之和

> 原文:[https://www . geeksforgeeks . org/所有子序列的总和/a-number/](https://www.geeksforgeeks.org/sum-of-all-subsequences-of-a-number/)

给定一个数作为字符串 s，求 s 的所有可能子序列中存在的所有元素的和。
**示例:**

```
Input : s = "123" 
Output : 24 
Explanation : all possible sub-sequences are 
1, 2, 3, {1, 2}, {2, 3}, {1, 3}, {1, 2, 3} 
which add up to 24 

Input : s = "453" 
Output : 48 
```

**方法:**使用[幂集](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，我们可以找到所有的子序列，并在不同的函数中单独对所有的子序列求和。可能的子序列总数为 2 <sup>n</sup> -1。将所有子序列的总和与最终输出的总和相加。
以下是上述方法的实施。

## C++

```
// CPP program to find the sum of
// elements present in all subsequences
#include <bits/stdc++.h>
using namespace std;

// Returns numeric value of a subsequence of
// s. The subsequence to be picked is decided
// using bit pattern of num (We pick all those
// digits for which there is a set bit in num)
int findSubSequence(string s, int num)
{ 
    // Initialize the result
    int res = 0;

    // till n!=0
    int i = 0;
    while (num) {

        // if i-th bit is set
        // then add this number
        if (num & 1)
            res += s[i] - '0';
        i++;

        // right shift i
        num = num >> 1;
    }

    return res;
}

// function to find combined sum
// of all individual subsequence sum
int combinedSum(string s)
{
    // length of string
    int n = s.length();

    // stores the combined
    int c_sum = 0;

    // 2^n-1 subsequences
    int range = (1 << n) - 1;

    // loop for all subsequences
    for (int i = 0; i <= range; i++)
        c_sum += findSubSequence(s, i);

    // returns the combined sum
    return c_sum;
}

// driver code
int main()
{
    string s = "123";
    cout << combinedSum(s);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of elements
// present in all subsequences
import java.io.*;

class GFG {

    // Returns numeric value of a
    // subsequence of s. The subsequence
    // to be picked is decided using bit
    // pattern of num (We pick all those
    // digits for which there is a set
    // bit in num)
    static int findSubSequence(String s,
                                int num)
    {
        // Initialize the result
        int res = 0;

        // till n!=0
        int i = 0;
        while (num > 0) {

            // if i-th bit is set
            // then add this number
            if ((num & 1) == 1)
                res += s.charAt(i) - '0';
            i++;

            // right shift i
            num = num >> 1;
        }

        return res;
    }

    // function to find combined sum
    // of all individual subsequence
    // sum
    static int combinedSum(String s)
    {

        // length of String
        int n = s.length();

        // stores the combined
        int c_sum = 0;

        // 2^n-1 subsequences
        int range = (1 << n) - 1;

        // loop for all subsequences
        for (int i = 0; i <= range; i++)
            c_sum += findSubSequence(s, i);

        // returns the combined sum
        return c_sum;
    }

    // Driver function
    public static void main (String[] args) {

        String s = "123";
        System.out.println(combinedSum(s));
    }

}

// This code is contributed by Anuj_ 67
```

## 蟒蛇 3

```
# Python 3 program to find the sum of
# elements present in all subsequences

# Returns numeric value of a subsequence of
# s. The subsequence to be picked is decided
# using bit pattern of num (We pick all those
# digits for which there is a set bit in num)
def findSubSequence(s, num):

    # Initialize the result
    res = 0

    # till n!=0
    i = 0
    while (num) :

        # if i-th bit is set
        # then add this number
        if (num & 1):
            res += ord(s[i]) - ord('0')
        i+=1

        # right shift i
        num = num >> 1

    return res

# function to find combined sum
# of all individual subsequence sum
def combinedSum(s):

    # length of string
    n = len(s)

    # stores the combined
    c_sum = 0

    # 2^n-1 subsequences
    ran = (1 << n) - 1

    # loop for all subsequences
    for i in range( ran+1):
        c_sum += findSubSequence(s, i)

    # returns the combined sum
    return c_sum

# driver code
if __name__ == "__main__":

    s = "123"
    print(combinedSum(s))
```

## C#

```
// C# program to find the sum of elements
// present in all subsequences
using System;

class GFG {

    // Returns numeric value of a
    // subsequence of s. The subsequence
    // to be picked is decided using bit
    // pattern of num (We pick all those
    // digits for which there is a set
    // bit in num)
    static int findSubSequence(string s,
                                 int num)
    {
        // Initialize the result
        int res = 0;

        // till n!=0
        int i = 0;
        while (num > 0) {

            // if i-th bit is set
            // then add this number
            if ((num & 1) == 1)
                res += s[i] - '0';
            i++;

            // right shift i
            num = num >> 1;
        }

        return res;
    }

    // function to find combined sum
    // of all individual subsequence
    // sum
    static int combinedSum(string s)
    {

        // length of string
        int n = s.Length;

        // stores the combined
        int c_sum = 0;

        // 2^n-1 subsequences
        int range = (1 << n) - 1;

        // loop for all subsequences
        for (int i = 0; i <= range; i++)
            c_sum += findSubSequence(s, i);

        // returns the combined sum
        return c_sum;
    }

    // Driver function
    public static void Main()
    {
        string s = "123";
        Console.Write(combinedSum(s));
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of
// elements present in all subsequences

// Returns numeric value of a subsequence of
// s. The subsequence to be picked is decided
// using bit pattern of num (We pick all those
// digits for which there is a set bit in num)
function findSubSequence($s, $num)
{

    // Initialize the result
    $res = 0;

    // till n!=0
    $i = 0;
    while ($num) {

        // if i-th bit is set
        // then add this number
        if ($num & 1)
            $res += $s[$i] - '0';
        $i++;

        // right shintift i
        $num = $num >> 1;
    }

    return $res;
}

// function to find combined sum
// of all individual subsequence sum
function combinedSum(string $s)
{

    // length of string
    $n = strlen($s);

    // stores the combined
    $c_sum = 0;

    // 2^n-1 subsequences
    $range = (1 << $n) - 1;

    // loop for all subsequences
    for ($i = 0; $i <= $range; $i++)
        $c_sum += findSubSequence($s, $i);

    // returns the combined sum
    return $c_sum;
}

    // Driver Code
    $s = "123";
    echo combinedSum($s);

// This code is contributed by Anuj_67
?>
```

## java 描述语言

```
<script>
// Javascript program to find the sum of elements
// present in all subsequences

    // Returns numeric value of a
    // subsequence of s. The subsequence
    // to be picked is decided using bit
    // pattern of num (We pick all those
    // digits for which there is a set
    // bit in num)
    function findSubSequence(s,num)
    {
        // Initialize the result
        let res = 0;

        // till n!=0
        let i = 0;
        while (num > 0) {

            // if i-th bit is set
            // then add this number
            if ((num & 1) == 1)
                res += s[i].charCodeAt(0) - '0'.charCodeAt(0);
            i++;

            // right shift i
            num = num >> 1;
        }

        return res;
    }

    // function to find combined sum
    // of all individual subsequence
    // sum
    function combinedSum(s)
    {
        // length of String
        let n = s.length;

        // stores the combined
        let c_sum = 0;

        // 2^n-1 subsequences
        let range = (1 << n) - 1;

        // loop for all subsequences
        for (let i = 0; i <= range; i++)
            c_sum += findSubSequence(s, i);

        // returns the combined sum
        return c_sum;
    }

    // Driver function
    let s = "123";
    document.write(combinedSum(s));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
24 
```