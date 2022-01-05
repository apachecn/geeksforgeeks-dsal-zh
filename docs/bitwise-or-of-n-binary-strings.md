# N 个二进制字符串的按位“或”

> 原文:[https://www . geeksforgeeks . org/n 位二进制字符串或/](https://www.geeksforgeeks.org/bitwise-or-of-n-binary-strings/)

给定二进制字符串的数组 **arr[]** ，任务是计算所有这些字符串的按位“或”并打印结果字符串。
**例:**

> **输入:**arr[]= {“100”、“1001”、“0011”}
> **输出** 1111
> 0100 **或** 1001 **或** 0011 = 1111
> **输入:**arr[]= {“10”、“11”、“1000001”}
> **输出:**10001

**方法:**我们可以这样做，首先找到最大大小的字符串。我们需要这样做，因为我们必须在长度小于最大长度的字符串前面加上 0。然后对每一位进行或运算。
例如，如果字符串是“100”、“001”和“1111”。这里最大大小是 4，所以我们必须在第一个和第二个字符串上加 1 个零，使它们的长度为 4，然后对数字的每个位执行“或”运算，得到“0100”或“0001”或“1111”=“1111”。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the bitwise OR of
// all the binary strings
string strBitwiseOR(string* arr, int n)
{
    string res;

    int max_size = INT_MIN;

    // Get max size and reverse each string
    // Since we have to perform OR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for (int i = 0; i < n; i++) {
        max_size = max(max_size, (int)arr[i].size());
        reverse(arr[i].begin(), arr[i].end());
    }

    for (int i = 0; i < n; i++) {

        // Add 0s to the end of strings
        // if needed
        string s;
        for (int j = 0; j < max_size - arr[i].size(); j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform OR operation on each bit
    for (int i = 0; i < max_size; i++) {
        int curr_bit = 0;
        for (int j = 0; j < n; j++)
            curr_bit = curr_bit | (arr[j][i] - '0');

        res += (curr_bit + '0');
    }

    // Reverse the resultant string
    // to get the final string
    reverse(res.begin(), res.end());

    // Return the final string
    return res;
}

// Driver code
int main()
{
    string arr[] = { "10", "11", "1000001" };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << strBitwiseOR(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to return the bitwise OR of
// all the binary strings
static String strBitwiseOR(String[] arr, int n)
{
    String res="";

    int max_size = Integer.MIN_VALUE;

    // Get max size and reverse each string
    // Since we have to perform OR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for (int i = 0; i < n; i++)
    {
        max_size = Math.max(max_size, (int)arr[i].length());
        arr[i] = reverse(arr[i]);
    }

    for (int i = 0; i < n; i++)
    {

        // Add 0s to the end of strings
        // if needed
        String s="";
        for (int j = 0; j < max_size - arr[i].length(); j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform OR operation on each bit
    for (int i = 0; i < max_size; i++)
    {
        int curr_bit = 0;
        for (int j = 0; j < n; j++)
            curr_bit = curr_bit | (arr[j].charAt(i) - '0');

        res += (char)(curr_bit + '0');
    }

    // Reverse the resultant string
    // to get the final string
    res = reverse(res);

    // Return the final string
    return res;
}

static String reverse(String input)
{
    char[] temparray = input.toCharArray();
    int left, right = 0;
    right = temparray.length - 1;

    for (left = 0; left < right; left++, right--)
    {
        // Swap values of left and right
        char temp = temparray[left];
        temparray[left] = temparray[right];
        temparray[right] = temp;
    }
    return String.valueOf(temparray);
}

// Driver code
public static void main(String[] args)
{
    String arr[] = { "10", "11", "1000001" };
    int n = arr.length;
    System.out.println(strBitwiseOR(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the bitwise OR of
# all the binary strings
def strBitwiseOR(arr, n):
    res=""
    max_size = -(2**32)

    # Get max size and reverse each string
    # Since we have to perform OR operation
    # on bits from right to left
    # Reversing the string will make it easier
    # to perform operation from left to right
    for i in range(n):
        max_size = max(max_size, len(arr[i]))
        arr[i] = arr[i][::-1]

    for i in range(n):

        # Add 0s to the end of strings
        # if needed
        s = ""
        for j in range(max_size - len(arr[i])):
            s += '0'

        arr[i] = arr[i] + s

    # Perform OR operation on each bit
    for i in range(max_size):
        curr_bit = 0
        for j in range(n):
            curr_bit = curr_bit | ord(arr[j][i])

        res += chr(curr_bit)

    # Reverse the resultant string
    # to get the final string
    res=res[::-1]

    # Return the final string
    return res

# Driver code
arr = ["10", "11", "1000001"]
n = len(arr)
print(strBitwiseOR(arr, n))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the bitwise OR of
// all the binary strings
static String strBitwiseOR(String[] arr, int n)
{
    String res="";

    int max_size = int.MinValue;

    // Get max size and reverse each string
    // Since we have to perform OR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for (int i = 0; i < n; i++)
    {
        max_size = Math.Max(max_size, (int)arr[i].Length);
        arr[i] = reverse(arr[i]);
    }

    for (int i = 0; i < n; i++)
    {

        // Add 0s to the end of strings
        // if needed
        String s="";
        for (int j = 0; j < max_size - arr[i].Length; j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform OR operation on each bit
    for (int i = 0; i < max_size; i++)
    {
        int curr_bit = 0;
        for (int j = 0; j < n; j++)
            curr_bit = curr_bit | (arr[j][i] - '0');

        res += (char)(curr_bit + '0');
    }

    // Reverse the resultant string
    // to get the final string
    res = reverse(res);

    // Return the final string
    return res;
}

static String reverse(String input)
{
    char[] temparray = input.ToCharArray();
    int left, right = 0;
    right = temparray.Length - 1;

    for (left = 0; left < right; left++, right--)
    {
        // Swap values of left and right
        char temp = temparray[left];
        temparray[left] = temparray[right];
        temparray[right] = temp;
    }
    return String.Join("",temparray);
}

// Driver code
public static void Main(String[] args)
{
    String []arr = { "10", "11", "1000001" };
    int n = arr.Length;
    Console.WriteLine(strBitwiseOR(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the bitwise OR of
// all the binary strings
function strBitwiseOR(arr, n)
{
    var res = "";

    var max_size = -1000000000;

    // Get max size and reverse each string
    // Since we have to perform OR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for (var i = 0; i < n; i++) {
        max_size = Math.max(max_size, arr[i].length);
        arr[i] = arr[i].split('').reverse().join('');
    }

    for (var i = 0; i < n; i++) {

        // Add 0s to the end of strings
        // if needed
        var s = "";
        for (var j = 0; j < max_size - arr[i].length; j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform OR operation on each bit
    for (var i = 0; i < max_size; i++) {
        var curr_bit = 0;
        for (var j = 0; j < n; j++)
            curr_bit = curr_bit | (arr[j][i].charCodeAt(0) -
            '0'.charCodeAt(0));

        res += String.fromCharCode(curr_bit + '0'.charCodeAt(0));
    }

    // Reverse the resultant string
    // to get the final string
    res = res.split('').reverse().join('');

    // Return the final string
    return res;
}

// Driver code

var arr = ["10", "11", "1000001"];
var n = arr.length;
document.write( strBitwiseOR(arr, n));

</script>
```

**Output:** 

```
1000011
```