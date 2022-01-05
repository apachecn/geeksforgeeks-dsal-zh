# 构建具有给定数组指定的最长公共前缀的字符串数组

> 原文:[https://www . geeksforgeeks . org/construct-由给定数组指定的具有最长公共前缀的字符串数组/](https://www.geeksforgeeks.org/construct-an-array-of-strings-having-longest-common-prefix-specified-by-the-given-array/)

给定一个大小为 **N** 的整数数组 **arr[]** ，任务是构造一个由长度为 **N** 的 **N+1** 串组成的数组，使得 **arr[i]** 等于**I<sup>th</sup>T15】串和**(I+1)<sup>th</sup>T19】串的[最长公共前缀](https://www.geeksforgeeks.org/longest-common-prefix-using-binary-search/)。****

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:**{“abb”、“aab”、“aaa”、“AAA”}
> **解释:**
> 字符串“abb”和“aab”有单个字符“a”作为最长公共前缀。
> 字符串“aab”和“aaa”有“aa”作为最长公共前缀。
> 字符串“aaa”和“aaa”有“aa”作为最长公共前缀。
> 
> **输入** **:** arr[]={2，0，3}
> **输出:**{“bab”、“baa”、“aaa”、“AAA”}
> **解释:**
> 字符串“Bab”和“baa”有“ba”作为最长公共前缀。
> 字符串“baa”和“aaa”没有共同的前缀。
> 字符串“aaa”和“aaa”有“aaa”作为最长公共前缀。

**进场:**

按照以下步骤解决问题:

*   其思想是观察如果**I<sup>th</sup>T3】字符串已知，那么**(I-1)<sup>th</sup>T7】字符串可以由**I<sup>th</sup>T11】字符串通过将**N–arr【I-1】**字符从**I<sup>th</sup>T17】字符串更改而成。********
*   从右向左开始构造字符串，生成 **N + 1** 字符串。

> **图解:**
> N = 3，arr[] = {2，0，3}
> 让第(N + 1) <sup>个</sup>字符串为“AAA”
> 因此，从右到左剩余的字符串为{“AAA”、“baa”、“Bab”}

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the array of strings
vector<string> solve(int n, int arr[])
{
    // Marks the (N+1)th string
    string s = string(n, 'a');

    vector<string> ans;
    ans.push_back(s);

    // To generate remaining N strings
    for (int i = n - 1; i >= 0; i--) {

        // Find i-th string using
        // (i+1)-th string
        char ch = s[arr[i]];

        // Check if current character
        // is b
        if (ch == 'b')
            ch = 'a';

        // Otherwise
        else
            ch = 'b';
        s[arr[i]] = ch;

        // Insert the string
        ans.push_back(s);
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{

    int arr[] = { 2, 0, 3 };
    int n = sizeof arr / sizeof arr[0];
    vector<string> ans = solve(n, arr);

    // Print the strings
    for (int i = ans.size() - 1; i >= 0; i--) {
        cout << ans[i] << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find the array of strings
  static Vector<String> solve(int n, int arr[])
  {

    // Marks the (N+1)th string
    String s = "aaa";
    Vector<String> ans = new Vector<String>();
    ans.add(s);

    // To generate remaining N strings
    for (int i = n-1 ; i >= 0; i--)
    {

      // Check if current character
      // is b
      if(s.length() - 1 >= arr[i])
      {

        // Find i-th string using
        // (i+1)-th string
        char ch = s.charAt(arr[i]);
        if (ch == 'b')
          ch = 'a';

        // Otherwise
        else
          ch = 'b';
        char[] myNameChars =s.toCharArray();
        myNameChars[arr[i]] = ch;
        s = String.valueOf(myNameChars);
      }

      // Insert the string
      ans.add(s);
    }

    // Return the answer
    return ans;
  }

  // Driver Code
  public static void main(String []args)
  {

    int []arr = { 2, 0, 3};
    int n = arr.length;
    Vector<String> ans = solve(n, arr);

    // Print the strings
    for (int i = ans.size()-1; i >= 0; i--)
    {
      System.out.println(ans.get(i));
    }
  }
}

// This code is contributed by bgangwar59.
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find the array
# of strings
def solve(n, arr):

    # Marks the (N+1)th
    # string
    s = 'a' * (n)
    ans = []
    ans.append(s)

    # To generate remaining
    # N strings
    for i in range(n - 1,
                   -1, -1):

        # Find i-th string using
        # (i+1)-th string   
        if len(s) - 1 >= arr[i]:
           ch = s[arr[i]]

           # Check if current
           # character
           # is b
           if (ch == 'b'):
               ch = 'a'

           # Otherwise
           else:
               ch = 'b'

           p = list(s)
           p[arr[i]] = ch
           s = ''.join(p)

        # Insert the string
        ans.append(s)

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    arr = [2, 0, 3]
    n = len(arr)
    ans = solve(n, arr)

    # Print the strings
    for i in range(len(ans) - 1,
                   -1, -1):
        print(ans[i])

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find the array of strings
  static List<string> solve(int n, int []arr)
  {

    // Marks the (N+1)th string
    string s = "aaa";

    List<string> ans = new List<string>();
    ans.Add(s);

    // To generate remaining N strings
    for (int i = n - 1; i >= 0; i--) {

      // Find i-th string using
      // (i+1)-th string
      if(s.Length-1>=arr[i]){
        char ch = s[arr[i]];

        // Check if current character
        // is b
        if (ch == 'b')
          ch = 'a';

        // Otherwise
        else
          ch = 'b';
        char[] chr = s.ToCharArray();
        chr[arr[i]] = ch;
        s =  new string(chr);
      }

      // Insert the string
      ans.Add(s);
    }

    // Return the answer
    return ans;
  }

  // Driver Code
  public static void Main()
  {

    int []arr = { 2, 0, 3 };
    int n = arr.Length;
    List<string> ans = solve(n, arr);

    // Print the strings
    for (int i = ans.Count - 1; i >= 0; i--) {
      Console.WriteLine(ans[i]);
    }
  }
}        

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to find the array of strings
function solve(n, arr)
{
    // Marks the (N+1)th string
    var s = ['a','a','a']

    var ans = [];
    ans.push(s.join(""));

    // To generate remaining N strings
    for (var i = n - 1; i >= 0; i--) {

        if(s.length-1>=arr[i])
        {
        // Find i-th string using
        // (i+1)-th string
        var ch = s[arr[i]];

        // Check if current character
        // is b
        if (ch == 'b')
            ch = 'a';

        // Otherwise
        else
            ch = 'b';
        s[arr[i]] = ch;
        }
        // Insert the string
        ans.push(s.join(""));
    }

    // Return the answer
    return ans;
}

// Driver Code
var arr = [ 2, 0, 3 ];
var n = arr.length;
var ans = solve(n, arr);

// Print the strings
for (var i = ans.length - 1; i >= 0; i--) {
    document.write( ans[i] + "<br>");
}  

// This code iscontributed by rutvik_56.
</script>
```

**Output:** 

```
bab
baa
aaa
aaa
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)