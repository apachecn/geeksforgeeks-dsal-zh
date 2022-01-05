# 将二进制数转换为八进制

> 原文:[https://www.geeksforgeeks.org/convert-binary-number-octal/](https://www.geeksforgeeks.org/convert-binary-number-octal/)

问题是将给定的二进制数(表示为字符串)转换为其等效的八进制数。输入可能非常大，甚至可能不适合无符号长整型。

示例:

```
Input : 110001110
Output : 616

Input  : 1111001010010100001.010110110011011
Output : 1712241.26633 
```

其思想是将二进制输入视为字符串，然后按照以下步骤操作:

1.  获取小数点左右两边的子字符串长度('.')为**左 _ len****右 _len** 。
2.  如果 **left_len** 不是 3 的倍数，则在开头加上 0 的最小数，使左子串的长度为 3 的倍数。
3.  如果 **right_len** 不是 3 的倍数，则在末尾添加 0 的最小数，使右子串的长度为 3 的倍数。
4.  现在，从左边一个接一个地提取长度为 3 的子串，并将其对应的八进制代码添加到结果中。
5.  如果在小数点('.'之间)然后将其添加到结果中。

## C++

```
// C++ implementation to convert a binary number
// to octal number
#include <bits/stdc++.h>
using namespace std;

// function to create map between binary
// number and its equivalent octal
void createMap(unordered_map<string, char> *um)
{
    (*um)["000"] = '0';
    (*um)["001"] = '1';
    (*um)["010"] = '2';
    (*um)["011"] = '3';
    (*um)["100"] = '4';
    (*um)["101"] = '5';
    (*um)["110"] = '6';
    (*um)["111"] = '7';   
}

// Function to find octal equivalent of binary
string convertBinToOct(string bin)
{
    int l = bin.size();
    int t = bin.find_first_of('.');

    // length of string before '.'
    int len_left = t != -1 ? t : l;

    // add min 0's in the beginning to make
    // left substring length divisible by 3
    for (int i = 1; i <= (3 - len_left % 3) % 3; i++)
        bin = '0' + bin;

    // if decimal point exists   
    if (t != -1)   
    {
        // length of string after '.'
        int len_right = l - len_left - 1;

        // add min 0's in the end to make right
        // substring length divisible by 3
        for (int i = 1; i <= (3 - len_right % 3) % 3; i++)
            bin = bin + '0';
    }

    // create map between binary and its
    // equivalent octal code
    unordered_map<string, char> bin_oct_map;
    createMap(&bin_oct_map);

    int i = 0;
    string octal = "";

    while (1)
    {
        // one by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map[bin.substr(i, 3)];
        i += 3;
        if (i == bin.size())
            break;

        // if '.' is encountered add it to result
        if (bin.at(i) == '.')   
        {
            octal += '.';
            i++;
        }
    }

    // required octal number
    return octal;   
}

// Driver program to test above
int main()
{
    string bin = "1111001010010100001.010110110011011";
    cout << "Octal number = "
         << convertBinToOct(bin);
    return 0;    
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to convert a
// binary number to octal number
import java.io.*;
import java.util.*;

class GFG{

// Function to create map between binary
// number and its equivalent hexadecimal
static void createMap(Map<String, Character> um)
{
    um.put("000", '0');
    um.put("001", '1');
    um.put("010", '2');
    um.put("011", '3');
    um.put("100", '4');
    um.put("101", '5');
    um.put("110", '6');
    um.put("111", '7');
}

// Function to find octal equivalent of binary
static String convertBinToOct(String bin)
{
    int l = bin.length();
    int t = bin.indexOf('.');

    // Length of string before '.'
    int len_left = t != -1 ? t : l;

    // Add min 0's in the beginning to make
    // left substring length divisible by 3
    for(int i = 1;
            i <= (3 - len_left % 3) % 3;
            i++)
        bin = '0' + bin;

    // If decimal point exists
    if (t != -1)
    {

        // Length of string after '.'
        int len_right = l - len_left - 1;

        // add min 0's in the end to make right
        // substring length divisible by 3
        for(int i = 1;
                i <= (3 - len_right % 3) % 3;
                i++)
            bin = bin + '0';
    }

    // Create map between binary and its
    // equivalent octal code
    Map<String,
        Character> bin_oct_map = new HashMap<String,
                                             Character>();
    createMap(bin_oct_map);

    int i = 0;
    String octal = "";

    while (true)
    {

        // One by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map.get(
            bin.substring(i, i + 3));
        i += 3;

        if (i == bin.length())
            break;

        // If '.' is encountered add it to result
        if (bin.charAt(i) == '.')
        {
            octal += '.';
            i++;
        }
    }

    // Required octal number
    return octal;
}

// Driver code
public static void main(String[] args)
{
    String bin = "1111001010010100001.010110110011011";
    System.out.println("Octal number = " +
                        convertBinToOct(bin));
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 implementation to convert a binary number
# to octal number

# function to create map between binary
# number and its equivalent octal
def createMap(bin_oct_map):
    bin_oct_map["000"] = '0'
    bin_oct_map["001"] = '1'
    bin_oct_map["010"] = '2'
    bin_oct_map["011"] = '3'
    bin_oct_map["100"] = '4'
    bin_oct_map["101"] = '5'
    bin_oct_map["110"] = '6'
    bin_oct_map["111"] = '7'

# Function to find octal equivalent of binary
def convertBinToOct(bin):
    l = len(bin)

    # length of string before '.'
    t = -1
    if '.' in bin:
        t = bin.index('.')
        len_left = t
    else:
        len_left = l

    # add min 0's in the beginning to make
    # left substring length divisible by 3
    for i in range(1, (3 - len_left % 3) % 3 + 1):
        bin = '0' + bin

    # if decimal point exists
    if (t != -1):

        # length of string after '.'
        len_right = l - len_left - 1

        # add min 0's in the end to make right
        # substring length divisible by 3
        for i in range(1, (3 - len_right % 3) % 3 + 1):
            bin = bin + '0'

    # create dictionary between binary and its
    # equivalent octal code
    bin_oct_map = {}
    createMap(bin_oct_map)
    i = 0
    octal = ""

    while (True) :

        # one by one extract from left, substring
        # of size 3 and add its octal code
        octal += bin_oct_map[bin[i:i + 3]]
        i += 3
        if (i == len(bin)):
            break

        # if '.' is encountered add it to result
        if (bin[i] == '.'):
            octal += '.'
            i += 1

    # required octal number
    return octal

# Driver Code
bin = "1111001010010100001.010110110011011"
print("Octal number = ",
       convertBinToOct(bin))

# This code is contributed
# by Atul_kumar_Shrivastava
```

## C#

```
// C# implementation to convert a
// binary number to octal number

using System;
using System.Collections.Generic;

public class GFG{

// Function to create map between binary
// number and its equivalent hexadecimal
static void createMap(Dictionary<String, char> um)
{
    um.Add("000", '0');
    um.Add("001", '1');
    um.Add("010", '2');
    um.Add("011", '3');
    um.Add("100", '4');
    um.Add("101", '5');
    um.Add("110", '6');
    um.Add("111", '7');
}

// Function to find octal equivalent of binary
static String convertBinToOct(String bin)
{
    int l = bin.Length;
    int t = bin.IndexOf('.');
    int i = 0;
    // Length of string before '.'
    int len_left = t != -1 ? t : l;

    // Add min 0's in the beginning to make
    // left substring length divisible by 3
    for(i = 1;
            i <= (3 - len_left % 3) % 3;
            i++)
        bin = '0' + bin;

    // If decimal point exists
    if (t != -1)
    {

        // Length of string after '.'
        int len_right = l - len_left - 1;

        // add min 0's in the end to make right
        // substring length divisible by 3
        for(i = 1;
                i <= (3 - len_right % 3) % 3;
                i++)
            bin = bin + '0';
    }

    // Create map between binary and its
    // equivalent octal code
    Dictionary<String,
        char> bin_oct_map = new Dictionary<String,
                                             char>();
    createMap(bin_oct_map);

    i = 0;
    String octal = "";

    while (true)
    {

        // One by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map[
            bin.Substring(i,  3)];
        i += 3;

        if (i == bin.Length)
            break;

        // If '.' is encountered add it to result
        if (bin[i] == '.')
        {
            octal += '.';
            i++;
        }
    }

    // Required octal number
    return octal;
}

// Driver code
public static void Main(String[] args)
{
    String bin = "1111001010010100001.010110110011011";
    Console.WriteLine("Octal number = " +
                        convertBinToOct(bin));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to convert a
// binary number to octal number

// Function to create map between binary
// number and its equivalent hexadecimal
function createMap(um)
{
    um.set("000", '0');
    um.set("001", '1');
    um.set("010", '2');
    um.set("011", '3');
    um.set("100", '4');
    um.set("101", '5');
    um.set("110", '6');
    um.set("111", '7');
}

// Function to find octal equivalent of binary
function convertBinToOct(bin)
{

    let l = bin.length;
    let t = bin.indexOf('.');

    // Length of string before '.'
    let len_left = t != -1 ? t : l;

    // Add min 0's in the beginning to make
    // left substring length divisible by 3
    for(let i = 1;
            i <= (3 - len_left % 3) % 3;
            i++)
        bin = '0' + bin;

    // If decimal point exists
    if (t != -1)
    {

        // Length of string after '.'
        let len_right = l - len_left - 1;

        // add min 0's in the end to make right
        // substring length divisible by 3
        for(let i = 1;
                i <= (3 - len_right % 3) % 3;
                i++)
            bin = bin + '0';
    }

    // Create map between binary and its
    // equivalent octal code
    let bin_oct_map = new Map();

    createMap(bin_oct_map);

    let i = 0;
    let octal = "";

    while (true)
    {

        // One by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map.get(bin.substr(i, 3));
        i += 3;

        if (i == bin.length)
            break;

        // If '.' is encountered add it to result
        if (bin.charAt(i) == '.')
        {
            octal += '.';
            i++;
        }
    }

    // Required octal number
    return octal;
}

// Driver code
let bin = "1111001010010100001.010110110011011";
document.write("Octal number = " +
               convertBinToOct(bin));

// This code is contributed by gfgking

</script>
```

**输出:**

```
Octal number = 1712241.26633
```

时间复杂度:O(n)，其中 n 是字符串的长度。

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。