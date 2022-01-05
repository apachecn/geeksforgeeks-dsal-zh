# 添加 n 个二进制字符串

> 原文:[https://www.geeksforgeeks.org/add-n-binary-strings/](https://www.geeksforgeeks.org/add-n-binary-strings/)

给定 n 个二进制字符串，返回它们的和(也是二进制字符串)。

**示例:**

```
Input:  arr[] = ["11", "1"]
Output: "100"

Input : arr[] = ["1", "10", "11"]
Output : "110" 
```

**算法**

1.  将“result”初始化为空字符串。
2.  从 i = 0 到 n-1 遍历输入。
3.  对于每个 I，在“结果”中添加 arr[i]。如何添加“结果”和 arr[i]？从两个字符串的最后一个字符开始，逐一计算数字总和。如果总和大于 1，则存储下一个数字的进位。将这个总和作为“结果”。
4.  遍历整个输入后的“结果”值就是最终答案。

## C++

```
// C++ program to add n binary strings
#include <bits/stdc++.h>
using namespace std;

// This function adds two binary strings and return
// result as a third string
string addBinaryUtil(string a, string b)
{
    string result = ""; // Initialize result
    int s = 0; // Initialize digit sum

    // Traverse both strings starting from last
    // characters
    int i = a.size() - 1, j = b.size() - 1;
    while (i >= 0 || j >= 0 || s == 1) {

        // Compute sum of last digits and carry
        s += ((i >= 0) ? a[i] - '0' : 0);
        s += ((j >= 0) ? b[j] - '0' : 0);

        // If current digit sum is 1 or 3,
        // add 1 to result
        result = char(s % 2 + '0') + result;

        // Compute carry
        s /= 2;

        // Move to next digits
        i--;
        j--;
    }
    return result;
}

// function to add n binary strings
string addBinary(string arr[], int n)
{
    string result = "";
    for (int i = 0; i < n; i++)
        result = addBinaryUtil(result, arr[i]);
    return result;
}

// Driver program
int main()
{
    string arr[] = { "1", "10", "11" };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << addBinary(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to add n binary strings
class GFG
{

    // This function adds two binary
    // strings and return result as
    // a third string
    static String addBinaryUtil(String a, String b)
    {
        String result = ""; // Initialize result
        int s = 0; // Initialize digit sum

        // Traverse both strings starting
        // from last characters
        int i = a.length() - 1, j = b.length() - 1;
        while (i >= 0 || j >= 0 || s == 1)
        {

            // Compute sum of last digits and carry
            s += ((i >= 0) ? a.charAt(i) - '0' : 0);
            s += ((j >= 0) ? b.charAt(j) - '0' : 0);

            // If current digit sum is 1 or 3,
            // add 1 to result
            result = s % 2 + result;

            // Compute carry
            s /= 2;

            // Move to next digits
            i--;
            j--;
        }
        return result;
    }

    // function to add n binary strings
    static String addBinary(String arr[], int n)
    {
        String result = "";
        for (int i = 0; i < n; i++)
        {
            result = addBinaryUtil(result, arr[i]);
        }
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String arr[] = {"1", "10", "11"};
        int n = arr.length;
        System.out.println(addBinary(arr, n));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 program to add n binary strings

# This function adds two binary strings and
# return result as a third string
def addBinaryUtil(a, b):

    result = ""; # Initialize result
    s = 0;       # Initialize digit sum

    # Traverse both strings
    # starting from last characters
    i = len(a) - 1;
    j = len(b) - 1;
    while (i >= 0 or j >= 0 or s == 1):

        # Compute sum of last digits and carry
        s += (ord(a[i]) - ord('0')) if(i >= 0) else 0;
        s += (ord(b[j]) - ord('0')) if(j >= 0) else 0;

        # If current digit sum is 1 or 3,
        # add 1 to result
        result = chr(s % 2 + ord('0')) + result;

        # Compute carry
        s //= 2;

        # Move to next digits
        i -= 1;
        j -= 1;

    return result;

# function to add n binary strings
def addBinary(arr, n):
    result = "";
    for i in range(n):
        result = addBinaryUtil(result, arr[i]);
    return result;

# Driver code
arr = ["1", "10", "11"];
n = len(arr);
print(addBinary(arr, n));

# This code is contributed by mits
```

## C#

```
// C# program to add n binary strings
using System;

class GFG
{

    // This function adds two binary
    // strings and return result as
    // a third string
    static String addBinaryUtil(String a,
                                String b)
    {
        // Initialize result
        String result = "";

        // Initialize digit sum
        int s = 0;

        // Traverse both strings starting
        // from last characters
        int i = a.Length - 1, j = b.Length - 1;
        while (i >= 0 || j >= 0 || s == 1)
        {

            // Compute sum of last digits and carry
            s += ((i >= 0) ? a[i] - '0' : 0);
            s += ((j >= 0) ? b[j] - '0' : 0);

            // If current digit sum is 1 or 3,
            // add 1 to result
            result = s % 2 + result;

            // Compute carry
            s /= 2;

            // Move to next digits
            i--;
            j--;
        }
        return result;
    }

    // function to add n binary strings
    static String addBinary(String []arr, int n)
    {
        String result = "";
        for (int i = 0; i < n; i++)
        {
            result = addBinaryUtil(result, arr[i]);
        }
        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String []arr = {"1", "10", "11"};
        int n = arr.Length;
        Console.WriteLine(addBinary(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to add n binary strings

// This function adds two binary strings and return
// result as a third string
function addBinaryUtil($a, $b)
{
    $result = ""; // Initialize result
    $s = 0; // Initialize digit sum

    // Traverse both strings starting from last
    // characters
    $i = strlen($a) - 1;
    $j = strlen($b) - 1;
    while ($i >= 0 || $j >= 0 || $s == 1)
    {

        // Compute sum of last digits and carry
        $s += (($i >= 0) ? ord($a[$i]) - ord('0') : 0);
        $s += (($j >= 0) ? ord($b[$j]) - ord('0') : 0);

        // If current digit sum is 1 or 3,
        // add 1 to result
        $result = chr($s % 2 + ord('0')).$result;

        // Compute carry
        $s =(int)($s/2);

        // Move to next digits
        $i--;
        $j--;
    }
    return $result;
}

// function to add n binary strings
function addBinary($arr, $n)
{
    $result = "";
    for ($i = 0; $i < $n; $i++)
        $result = addBinaryUtil($result, $arr[$i]);
    return $result;
}

// Driver code
    $arr = array( "1", "10", "11" );
    $n = count($arr);
    echo addBinary($arr, $n)."\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to add n binary strings

// This function adds two binary strings and return
// result as a third string
function addBinaryUtil(a, b)
{
    var result = ""; // Initialize result
    var s = 0; // Initialize digit sum

    // Traverse both strings starting from last
    // characters
    var i = a.length - 1, j = b.length - 1;
    while (i >= 0 || j >= 0 || s == 1) {

        // Compute sum of last digits and carry
        s += ((i >= 0) ? a.charCodeAt(i) - '0'.charCodeAt(0) : 0);
        s += ((j >= 0) ? b.charCodeAt(j) - '0'.charCodeAt(0) : 0);

        // If current digit sum is 1 or 3,
        // add 1 to result
        result = String.fromCharCode((s % 2 ==1 ?1:0) +
                                     '0'.charCodeAt(0)) + result;

        // Compute carry
        s = parseInt(s/2);

        // Move to next digits
        i--;
        j--;
    }
    return result;
}

// function to add n binary strings
function addBinary(arr, n)
{
    var result = "";
    for (var i = 0; i < n; i++)
        result = addBinaryUtil(result, arr[i]);
    return result;
}

// Driver program
var arr = ["1", "10", "11"];
var n = arr.length;
document.write( addBinary(arr, n));

</script>
```

**Output:** 

```
110
```