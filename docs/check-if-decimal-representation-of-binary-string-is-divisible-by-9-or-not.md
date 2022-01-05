# 检查二进制字符串的十进制表示是否能被 9 整除

> 原文:[https://www . geesforgeks . org/检查二进制字符串的十进制表示是否可被 9 整除/](https://www.geeksforgeeks.org/check-if-decimal-representation-of-binary-string-is-divisible-by-9-or-not/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是检查二进制字符串的[十进制表示是](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)[被 **9** 整除还是没有](https://www.geeksforgeeks.org/divisibility-9-using-bitwise-operators/) t 整除。

**示例:**

> **输入:** S = 1010001
> **输出:**是
> **说明:**二进制字符串 S 的十进制表示为 81，可被 9 整除。因此，所需的输出是“是”。
> 
> **输入:** S = 1010011
> **输出:**否
> **说明:**二进制字符串 S 的十进制表示为 83，不能被 9 整除。因此，需要的输出是 No。

**天真法**:解决这个问题最简单的方法就是[把二进制数转换成十进制数](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)，检查[十进制数是否能被 9](https://www.geeksforgeeks.org/check-large-number-divisible-9-not/) 整除。如果发现为真，则打印“真”。否则，打印“假”。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**如果二进制字符串的长度大于 **64** ，则二进制字符串的[十进制表示将导致溢出。因此，为了减少溢出问题，想法是](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)[将二进制字符串转换为八进制表示](https://www.geeksforgeeks.org/convert-binary-number-octal/)，并检查二进制字符串的八进制表示是否可被 **9** 整除。按照以下步骤解决问题:

*   将[二进制字符串转换为八进制表示](https://www.geeksforgeeks.org/convert-binary-number-octal/)。
*   初始化一个变量，比如说 **Oct_9** 来存储 **9** 的八进制表示。
*   求数字的和，比如在二进制字符串的八进制表示中出现在偶数位置的 **evenSum** 。
*   求二进制字符串八进制表示中奇数位置出现的数字之和，比如 **oddSum** 。
*   检查**ABS(odd sum–even sum)% Oct _ 9 = = 0**是否存在。如果发现是真的，那么打印**是**。
*   否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to convert the binary string
// into octal representation
string ConvertequivalentBase8(string S)
{
    // Stores binary representation of
    // the decimal value [0 - 7]
    map<string, char> mp;

    // Stores the decimal values
    // of binary strings [0 - 7]
    mp["000"] = '0';
    mp["001"] = '1';
    mp["010"] = '2';
    mp["011"] = '3';
    mp["100"] = '4';
    mp["101"] = '5';
    mp["110"] = '6';
    mp["111"] = '7';

    // Stores length of S
    int N = S.length();

    if (N % 3 == 2) {

        // Update S
        S = "0" + S;
    }
    else if (N % 3 == 1) {

        // Update S
        S = "00" + S;
    }

    // Update N
    N = S.length();

    // Stores octal representation
    // of the binary string
    string oct;

    // Traverse the binary string
    for (int i = 0; i < N; i += 3) {

        // Stores 3 consecutive characters
        // of the binary string
        string temp = S.substr(i, 3);

        // Append octal representation
        // of temp
        oct.push_back(mp[temp]);
    }

    return oct;
}

// Function to check if binary string
// is divisible by 9 or not
string binString_div_9(string S, int N)
{
    // Stores octal representation
    // of S
    string oct;

    oct = ConvertequivalentBase8(S);

    // Stores sum of elements present
    // at odd positions of oct
    int oddSum = 0;

    // Stores sum of elements present
    // at odd positions of oct
    int evenSum = 0;

    // Stores length of oct
    int M = oct.length();

    // Traverse the string oct
    for (int i = 0; i < M; i += 2) {
        // Update oddSum
        oddSum += int(oct[i] - '0');
    }

    // Traverse the string oct
    for (int i = 1; i < M; i += 2) {
        // Update evenSum
        evenSum += int(oct[i] - '0');
    }

    // Stores cotal representation
    // of 9
    int Oct_9 = 11;

    // If absolute value of (oddSum
    // - evenSum) is divisible by Oct_9
    if (abs(oddSum - evenSum) % Oct_9
        == 0) {
        return "Yes";
    }
    return "No";
}

// Driver Code
int main()
{
    string S = "1010001";
    int N = S.length();
    cout << binString_div_9(S, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to convert the binary string
// into octal representation   
static String ConvertequivalentBase8(String S)
{

    // Stores binary representation of
    // the decimal value [0 - 7]
    HashMap<String,
            Character> mp = new HashMap<String,
                                        Character>();

    // Stores the decimal values
    // of binary Strings [0 - 7]
    mp.put("000", '0');
    mp.put("001", '1');
    mp.put("010", '2');
    mp.put("011", '3');
    mp.put("100", '4');
    mp.put("101", '5');
    mp.put("110", '6');
    mp.put("111", '7');

    // Stores length of S
    int N = S.length();

    if (N % 3 == 2)
    {

        // Update S
        S = "0" + S;
    }
    else if (N % 3 == 1)
    {

        // Update S
        S = "00" + S;
    }

    // Update N
    N = S.length();

    // Stores octal representation
    // of the binary String
    String oct = "";

    // Traverse the binary String
    for(int i = 0; i < N; i += 3)
    {

        // Stores 3 consecutive characters
        // of the binary String
        String temp = S.substring(i, i + 3);

        // Append octal representation
        // of temp
        oct += mp.get(temp);
    }
    return oct;
}

// Function to check if binary String
// is divisible by 9 or not
static String binString_div_9(String S, int N)
{

    // Stores octal representation
    // of S
    String oct = "";

    oct = ConvertequivalentBase8(S);

    // Stores sum of elements present
    // at odd positions of oct
    int oddSum = 0;

    // Stores sum of elements present
    // at odd positions of oct
    int evenSum = 0;

    // Stores length of oct
    int M = oct.length();

    // Traverse the String oct
    for(int i = 0; i < M; i += 2)

        // Update oddSum
        oddSum += (oct.charAt(i) - '0');

    // Traverse the String oct
    for(int i = 1; i < M; i += 2)
    {

        // Update evenSum
        evenSum += (oct.charAt(i) - '0');
    }

    // Stores octal representation
    // of 9
    int Oct_9 = 11;

    // If absolute value of (oddSum
    // - evenSum) is divisible by Oct_9
    if (Math.abs(oddSum - evenSum) % Oct_9 == 0)
    {
        return "Yes";
    }
    return "No";
}

// Driver Code
public static void main(String[] args)
{
    String S = "1010001";
    int N = S.length();

    System.out.println(binString_div_9(S, N));
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to convert the binary
# string into octal representation
def ConvertequivalentBase8(S):

    # Stores binary representation of
    # the decimal value [0 - 7]
    mp = {}

    # Stores the decimal values
    # of binary strings [0 - 7]
    mp["000"] = '0'
    mp["001"] = '1'
    mp["010"] = '2'
    mp["011"] = '3'
    mp["100"] = '4'
    mp["101"] = '5'
    mp["110"] = '6'
    mp["111"] = '7'

    # Stores length of S
    N = len(S)

    if (N % 3 == 2):

        # Update S
        S = "0" + S

    elif (N % 3 == 1):

        # Update S
        S = "00" + S

    # Update N
    N = len(S)

    # Stores octal representation
    # of the binary string
    octal = ""

    # Traverse the binary string
    for i in range(0, N, 3):

        # Stores 3 consecutive characters
        # of the binary string
        temp = S[i: i + 3]

        # Append octal representation
        # of temp
        if temp in mp:
           octal += (mp[temp])

    return octal

# Function to check if binary string
# is divisible by 9 or not
def binString_div_9(S, N):

    # Stores octal representation
    # of S
    octal = ConvertequivalentBase8(S)

    # Stores sum of elements present
    # at odd positions of oct
    oddSum = 0

    # Stores sum of elements present
    # at odd positions of oct
    evenSum = 0

    # Stores length of oct
    M = len(octal)

    # Traverse the string oct
    for i in range(0, M, 2):

        # Update oddSum
        oddSum += ord(octal[i]) - ord('0')

    # Traverse the string oct
    for i in range(1, M, 2):

        # Update evenSum
        evenSum += ord(octal[i]) - ord('0')

    # Stores cotal representation
    # of 9
    Oct_9 = 11

    # If absolute value of (oddSum
    # - evenSum) is divisible by Oct_9
    if (abs(oddSum - evenSum) % Oct_9 == 0):
        return "Yes"

    return "No"

# Driver Code
if __name__ == "__main__":

    S = "1010001"
    N = len(S)

    print(binString_div_9(S, N))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to convert the binary string
// into octal representation   
static String ConvertequivalentBase8(String S)
{

    // Stores binary representation of
    // the decimal value [0 - 7]
    Dictionary<String,
               char> mp = new Dictionary<String,
                                         char>();

    // Stores the decimal values
    // of binary Strings [0 - 7]
    mp.Add("000", '0');
    mp.Add("001", '1');
    mp.Add("010", '2');
    mp.Add("011", '3');
    mp.Add("100", '4');
    mp.Add("101", '5');
    mp.Add("110", '6');
    mp.Add("111", '7');

    // Stores length of S
    int N = S.Length;

    if (N % 3 == 2)
    {

        // Update S
        S = "0" + S;
    }
    else if (N % 3 == 1)
    {

        // Update S
        S = "00" + S;
    }

    // Update N
    N = S.Length;

    // Stores octal representation
    // of the binary String
    String oct = "";

    // Traverse the binary String
    for(int i = 0; i < N; i += 3)
    {

        // Stores 3 consecutive characters
        // of the binary String
        String temp = S.Substring(0, N);

        // Append octal representation
        // of temp
        if (mp.ContainsKey(temp))
            oct += mp[temp];
    }
    return oct;
}

// Function to check if binary String
// is divisible by 9 or not
static String binString_div_9(String S, int N)
{

    // Stores octal representation
    // of S
    String oct = "";

    oct = ConvertequivalentBase8(S);

    // Stores sum of elements present
    // at odd positions of oct
    int oddSum = 0;

    // Stores sum of elements present
    // at odd positions of oct
    int evenSum = 0;

    // Stores length of oct
    int M = oct.Length;

    // Traverse the String oct
    for(int i = 0; i < M; i += 2)

        // Update oddSum
        oddSum += (oct[i] - '0');

    // Traverse the String oct
    for(int i = 1; i < M; i += 2)
    {

        // Update evenSum
        evenSum += (oct[i] - '0');
    }

    // Stores octal representation
    // of 9
    int Oct_9 = 11;

    // If absolute value of (oddSum
    // - evenSum) is divisible by Oct_9
    if (Math.Abs(oddSum - evenSum) % Oct_9 == 0)
    {
        return "Yes";
    }
    return "No";
}

// Driver Code
public static void Main(String[] args)
{
    String S = "1010001";
    int N = S.Length;

    Console.WriteLine(binString_div_9(S, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to convert the binary string
// into octal representation  
function ConvertequivalentBase8(S)
{

    // Stores binary representation of
    // the decimal value [0 - 7]
    let mp = new Map();

    // Stores the decimal values
    // of binary Strings [0 - 7]
    mp.set("000", '0');
    mp.set("001", '1');
    mp.set("010", '2');
    mp.set("011", '3');
    mp.set("100", '4');
    mp.set("101", '5');
    mp.set("110", '6');
    mp.set("111", '7');

    // Stores length of S
    let N = S.length;

    if (N % 3 == 2)
    {

        // Update S
        S = "0" + S;
    }
    else if (N % 3 == 1)
    {

        // Update S
        S = "00" + S;
    }

    // Update N
    N = S.length;

    // Stores octal representation
    // of the binary String
    let oct = "";

    // Traverse the binary String
    for(let i = 0; i < N; i += 3)
    {

        // Stores 3 consecutive characters
        // of the binary String
        let temp = S.substring(i, i + 3);

        // Append octal representation
        // of temp
        oct += mp.get(temp);
    }
    return oct;
}

// Function to check if binary String
// is divisible by 9 or not
function binString_div_9(S, N)
{

    // Stores octal representation
    // of S
    let oct = "";

    oct = ConvertequivalentBase8(S);

    // Stores sum of elements present
    // at odd positions of oct
    let oddSum = 0;

    // Stores sum of elements present
    // at odd positions of oct
    let evenSum = 0;

    // Stores length of oct
    let M = oct.length;

    // Traverse the String oct
    for(let i = 0; i < M; i += 2)

        // Update oddSum
        oddSum += (oct[i] - '0');

    // Traverse the String oct
    for(let i = 1; i < M; i += 2)
    {

        // Update evenSum
        evenSum += (oct[i] - '0');
    }

    // Stores octal representation
    // of 9
    let Oct_9 = 11;

    // If absolute value of (oddSum
    // - evenSum) is divisible by Oct_9
    if (Math.abs(oddSum - evenSum) % Oct_9 == 0)
    {
        return "Yes";
    }
    return "No";
}

// Driver Code
let S = "1010001";
let N = S.length;

document.write(binString_div_9(S, N));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)