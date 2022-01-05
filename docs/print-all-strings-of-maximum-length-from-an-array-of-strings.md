# 打印字符串数组中最大长度的所有字符串

> 原文:[https://www . geesforgeks . org/print-从字符串数组中打印最大长度的所有字符串/](https://www.geeksforgeeks.org/print-all-strings-of-maximum-length-from-an-array-of-strings/)

给定一个字符串的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]**，任务是打印给定数组中所有最大长度的字符串。

**示例:**

> **输入:**arr[]= {“ABA”、“aa”、“ad”、“vcd”、“ABA”}
> **输出:** aba vcd aba
> **解释:**
> 给定数组中所有字符串的最大长度为 3。
> 数组中长度等于 3 的字符串为“aba”、“vcd”、“aba”。
> 
> **输入:**arr[]= {“abb”、“abcd”、“guw”、“v”}
> **输出:** abcd
> **解释:**
> 给定数组中所有字符串的最大长度为 4。
> 数组中长度等于 4 的字符串是“abcd”。

**方法:**按照以下步骤解决问题:

1.  [遍历给定的字符串数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。计算数组中所有字符串的最大长度，并将其存储在一个变量中，比如 **len** 。
2.  现在，再次遍历字符串数组，打印数组中长度等于 **len** 的字符串。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length
// of the longest string from
// the given array of strings
int maxLength(vector<string> arr)
{
    int len = INT_MIN;
    int N = arr.size();

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores the length
        // of current string
        int l = arr[i].size();

        // Update maximum length
        if (len < l) {

            len = l;
        }
    }

    // Return the maximum length
    return len;
}

// Function to print the
// longest strings from the array
void maxStrings(vector<string> arr, int len)
{
    int N = arr.size();
    vector<string> ans;

    // Find the strings having length
    // equals to len
    for (int i = 0; i < N; i++) {
        if (len == arr[i].size()) {
            ans.push_back(arr[i]);
        }
    }

    // Print the resultant
    // vector of strings
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
}

// Function to print all the
// longest strings from the array
void printStrings(vector<string>& arr)
{
    // Find the length of longest string
    int max = maxLength(arr);

    // Find and print all the strings
    // having length equals to max
    maxStrings(arr, max);
}

// Driver Code
int main()
{
    vector<string> arr
        = { "aba", "aa", "ad", "vcd", "aba" };
    printStrings(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the length
// of the longest String from
// the given array of Strings
static int maxLength(String []arr)
{
    int len = Integer.MIN_VALUE;
    int N = arr.length;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores the length
        // of current String
        int l = arr[i].length();

        // Update maximum length
        if (len < l)
        {
            len = l;
        }
    }

    // Return the maximum length
    return len;
}

// Function to print the
// longest Strings from the array
static void maxStrings(String []arr, int len)
{
    int N = arr.length;
    Vector<String> ans = new Vector<String>();

    // Find the Strings having length
    // equals to len
    for(int i = 0; i < N; i++)
    {
        if (len == arr[i].length())
        {
            ans.add(arr[i]);
        }
    }

    // Print the resultant
    // vector of Strings
    for(int i = 0; i < ans.size(); i++)
    {
        System.out.print(ans.get(i) + " ");
    }
}

// Function to print all the
// longest Strings from the array
static void printStrings(String [] arr)
{

    // Find the length of longest String
    int max = maxLength(arr);

    // Find and print all the Strings
    // having length equals to max
    maxStrings(arr, max);
}

// Driver Code
public static void main(String[] args)
{
    String []arr = { "aba", "aa", "ad",
                     "vcd", "aba" };

    printStrings(arr);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the length
# of the longest string from
# the given array of strings
def maxLength(arr):

    lenn = -sys.maxsize - 1
    N = len(arr)

    # Traverse the array
    for i in range(N):

        # Stores the length
        # of current string
        l = len(arr[i])

        # Update maximum length
        if (lenn < l):
            lenn = l

    # Return the maximum length
    return lenn

# Function to print the
# longest strings from the array
def maxStrings(arr, lenn):

    N = len(arr)
    ans = []

    # Find the strings having length
    # equals to lenn
    for i in range(N):
        if (lenn == len(arr[i])):
            ans.append(arr[i])

    # Print the resultant
    # vector of strings
    for i in range(len(ans)):
        print(ans[i], end = " ")

# Function to print all the
# longest strings from the array
def printStrings(arr):

    # Find the length of longest string
    max = maxLength(arr)

    # Find and print all the strings
    # having length equals to max
    maxStrings(arr, max)

# Driver Code
if __name__ == '__main__':

    arr = [ "aba", "aa", "ad",
            "vcd", "aba" ]

    printStrings(arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the length
// of the longest String from
// the given array of Strings
static int maxLength(String []arr)
{
    int len = int.MinValue;
    int N = arr.Length;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {       
        // Stores the length
        // of current String
        int l = arr[i].Length;

        // Update maximum length
        if (len < l)
        {
            len = l;
        }
    }

    // Return the maximum length
    return len;
}

// Function to print the
// longest Strings from the array
static void maxStrings(String []arr,
                       int len)
{
    int N = arr.Length;
    List<String> ans = new List<String>();

    // Find the Strings having length
    // equals to len
    for(int i = 0; i < N; i++)
    {
        if (len == arr[i].Length)
        {
            ans.Add(arr[i]);
        }
    }

    // Print the resultant
    // vector of Strings
    for(int i = 0; i < ans.Count; i++)
    {
        Console.Write(ans[i] + " ");
    }
}

// Function to print all the
// longest Strings from the array
static void printStrings(String [] arr)
{   
    // Find the length of longest String
    int max = maxLength(arr);

    // Find and print all the Strings
    // having length equals to max
    maxStrings(arr, max);
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = {"aba", "aa", "ad",
                    "vcd", "aba"};                    
    printStrings(arr);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the length
// of the longest String from
// the given array of Strings
function  maxLength(arr)
{
    let len = Number.MIN_VALUE;
    let N = arr.length;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Stores the length
        // of current String
        let l = arr[i].length;

        // Update maximum length
        if (len < l)
        {
            len = l;
        }
    }

    // Return the maximum length
    return len;
}

// Function to print the
// longest Strings from the array
function maxStrings(arr,len)
{
    let N = arr.length;
    let ans = [];

    // Find the Strings having length
    // equals to len
    for(let i = 0; i < N; i++)
    {
        if (len == arr[i].length)
        {
            ans.push(arr[i]);
        }
    }

    // Print the resultant
    // vector of Strings
    for(let i = 0; i < ans.length; i++)
    {
        document.write(ans[i] + " ");
    }
}

// Function to print all the
// longest Strings from the array
function printStrings(arr)
{
    // Find the length of longest String
    let max = maxLength(arr);

    // Find and print all the Strings
    // having length equals to max
    maxStrings(arr, max);
}

// Driver Code
let arr=["aba", "aa", "ad",
                     "vcd", "aba" ];
printStrings(arr);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
aba vcd aba
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)