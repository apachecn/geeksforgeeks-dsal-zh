# 生成与所有给定字符串仅相差一个字符的字符串

> 原文:[https://www . geesforgeks . org/generate-a-string-该字符串仅与所有给定字符串中的单个字符不同/](https://www.geeksforgeeks.org/generate-a-string-which-differs-by-only-a-single-character-from-all-given-strings/)

给定一个由相同长度的字符串组成的字符串数组**str[]****N**，任务是从所有给定的字符串中找出仅相差一个字符的字符串。如果不能生成这样的字符串，打印 **-1** 。如果有多个可能的答案，请打印其中任何一个。

**示例:**

> **输入:**str[]= {“ABAC”、“zdac”、“bdac”}
> **输出:** adac
> **解释:**
> 字符串“adac”与所有给定的字符串仅相差一个字符。
> 
> **输入:** str[] = {“极客”、“缇丝”}
> **输出:**缇丝

**方法:**按照以下步骤解决问题:

*   将第一个字符串设置为答案。
*   现在，将字符串的第一个字符替换为所有可能的字符，并检查它是否与其他字符串有单个字符的不同。
*   对第一个字符串中的所有字符重复此过程。
*   如果从上面的步骤中找到任何所需类型的字符串，则打印该字符串。
*   如果没有出现替换第一个字符串的单个字符生成所需类型的字符串的情况，请打印-1。

下面是上述方法的实现。

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
#define ll long long

using namespace std;

// Function to check if a given string
// differs by a single character from
// all the strings in an array
bool check(string ans, vector<string>& s,
           int n, int m)
{

    // Traverse over the strings
    for (int i = 1; i < n; ++i) {

        // Stores the count of characters
        // differing from the strings
        int count = 0;
        for (int j = 0; j < m; ++j) {
            if (ans[j] != s[i][j])
                count++;
        }

        // If differs by more than one
        // character
        if (count > 1)
            return false;
    }

    return true;
}

// Function to find the string which only
// differ at one position from the all
// given strings of the array
string findString(vector<string>& s)
{

    // Size of the array
    int n = s.size();

    // Length of a string
    int m = s[0].size();

    string ans = s[0];

    int flag = 0;

    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < 26; ++j) {

            string x = ans;

            // Replace i-th character by all
            // possible characters
            x[i] = (j + 'a');

            // Check if it differs by a
            // single character from all
            // other strings
            if (check(x, s, n, m)) {
                ans = x;
                flag = 1;
                break;
            }
        }

        // If desired string is obtained
        if (flag == 1)
            break;
    }

    // Print the answer
    if (flag == 0)
        return "-1";
    else
        return ans;
}

// Driver code
int main()
{

    vector<string> s = { "geeks", "teeds" };

    // Function call
    cout << findString(s) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if a given string
// differs by a single character from
// all the strings in an array
static boolean check(String ans, String[] s,
                     int n, int m)
{

    // Traverse over the strings
    for(int i = 1; i < n; ++i)
    {

        // Stores the count of characters
        // differing from the strings
        int count = 0;
        for(int j = 0; j < m; ++j)
        {
            if (ans.charAt(j) != s[i].charAt(j))
                count++;
        }

        // If differs by more than one
        // character
        if (count > 1)
            return false;
    }
    return true;
}

// Function to find the string which only
// differ at one position from the all
// given strings of the array
static String findString(String[] s)
{

    // Size of the array
    int n = s.length;
    String ans = s[0];

    // Length of a string
    int m = ans.length();

    int flag = 0;

    for(int i = 0; i < m; ++i)
    {
        for(int j = 0; j < 26; ++j)
        {
            String x = ans;

            // Replace i-th character by all
            // possible characters
            x = x.replace(x.charAt(i), (char)(j + 'a'));

            // Check if it differs by a
            // single character from all
            // other strings
            if (check(x, s, n, m))
            {
                ans = x;
                flag = 1;
                break;
            }
        }

        // If desired string is obtained
        if (flag == 1)
            break;
    }

    // Print the answer
    if (flag == 0)
        return "-1";
    else
        return ans;
}

// Driver code
public static void main(String []args)
{
    String s[] = { "geeks", "teeds" };

    // Function call
    System.out.println(findString(s));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a given string
# differs by a single character from
# all the strings in an array
def check(ans, s, n, m):

    # Traverse over the strings
    for i in range(1, n):

        # Stores the count of characters
        # differing from the strings
        count = 0
        for j in range(m):
            if(ans[j] != s[i][j]):
                count += 1

        # If differs by more than one
        # character
        if(count > 1):
            return False

    return True

# Function to find the string which only
# differ at one position from the all
# given strings of the array
def findString(s):

    # Size of the array
    n = len(s)

    # Length of a string
    m = len(s[0])

    ans = s[0]
    flag = 0

    for i in range(m):
        for j in range(26):
            x = list(ans)

            # Replace i-th character by all
            # possible characters
            x[i] = chr(j + ord('a'))

            # Check if it differs by a
            # single character from all
            # other strings
            if(check(x, s, n, m)):
                ans = x
                flag = 1
                break

        # If desired string is obtained
        if(flag == 1):
            break

    # Print the answer
    if(flag == 0):
        return "-1"
    else:
        return ''.join(ans)

# Driver Code

# Given array of strings
s = [ "geeks", "teeds" ]

# Function call
print(findString(s))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to check if a given string
// differs by a single character from
// all the strings in an array
static bool check(String ans, String[] s,
                  int n, int m)
{

    // Traverse over the strings
    for(int i = 1; i < n; ++i)
    {

        // Stores the count of characters
        // differing from the strings
        int count = 0;
        for(int j = 0; j < m; ++j)
        {
            if (ans[j] != s[i][j])
                count++;
        }

        // If differs by more than one
        // character
        if (count > 1)
            return false;
    }
    return true;
}

// Function to find the string which only
// differ at one position from the all
// given strings of the array
static String findString(String[] s)
{

    // Size of the array
    int n = s.Length;
    String ans = s[0];

    // Length of a string
    int m = ans.Length;

    int flag = 0;

    for(int i = 0; i < m; ++i)
    {
        for(int j = 0; j < 26; ++j)
        {
            String x = ans;

            // Replace i-th character by all
            // possible characters
            x = x.Replace(x[i], (char)(j + 'a'));

            // Check if it differs by a
            // single character from all
            // other strings
            if (check(x, s, n, m))
            {
                ans = x;
                flag = 1;
                break;
            }
        }

        // If desired string is obtained
        if (flag == 1)
            break;
    }

    // Print the answer
    if (flag == 0)
        return "-1";
    else
        return ans;
}

// Driver code
public static void Main(String []args)
{
    String []s = { "geeks", "teeds" };

    // Function call
    Console.WriteLine(findString(s));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach
      // Function to check if a given string
      // differs by a single character from
      // all the strings in an array
      function check(ans, s, n, m)
      {

        // Traverse over the strings
        for (var i = 1; i < n; ++i)
        {

          // Stores the count of characters
          // differing from the strings
          var count = 0;
          for (var j = 0; j < m; ++j) {
            if (ans[j] !== s[i][j]) count++;
          }

          // If differs by more than one
          // character
          if (count > 1) return false;
        }
        return true;
      }

      // Function to find the string which only
      // differ at one position from the all
      // given strings of the array
      function findString(s)
      {

        // Size of the array
        var n = s.length;
        var ans = s[0];

        // Length of a string
        var m = ans.length;

        var flag = 0;

        for (var i = 0; i < m; ++i) {
          for (var j = 0; j < 26; ++j) {
            var x = ans;

            // Replace i-th character by all
            // possible characters
            x = x.replace(x[i], String.fromCharCode(j + "a".charCodeAt(0)));

            // Check if it differs by a
            // single character from all
            // other strings
            if (check(x, s, n, m)) {
              ans = x;
              flag = 1;
              break;
            }
          }

          // If desired string is obtained
          if (flag === 1) break;
        }

        // Print the answer
        if (flag === 0) return "-1";
        else return ans;
      }

      // Driver code
      var s = ["geeks", "teeds"];

      // Function call
      document.write(findString(s));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
teeks
```

***时间复杂度:**O(N * M<sup>2</sup>* 26)*
***辅助空间:** O(M)*