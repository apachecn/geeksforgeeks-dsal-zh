# 通过用指定的替换字符替换给定字符的所有出现来修改字符串

> 原文:[https://www . geesforgeks . org/modify-string-by-replacement-by-specified-replacement-characters/](https://www.geeksforgeeks.org/modify-string-by-replacing-all-occurrences-of-given-characters-by-specified-replacing-characters/)

给定由 **N** 小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和由[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)字符 **P[][2]** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，任务是通过将字符 **P[i][0]** 的所有出现替换为字符 **P[i][1]** 来修改给定字符串 **S**

**示例:**

> **输入:**S =“aabbgg”，P[][2] = {{a，b}，{b，g}，{g，a}}
> **输出:** bbggaa
> **说明:**
> 将原字符串中的‘a’替换为‘b’。现在字符串 S 修改为“bbbbgg”。
> 将原字符串中的“b”替换为“g”。现在字符串 S 修改为“bbgggg”。
> 将原字符串中的“g”替换为“a”。现在字符串 S 修改为“bbggaa”。
> 
> **输入:** S = "abc "，P[][2] = {{a，b } }
> T3】输出: bbc

**天真方法:**解决给定问题的最简单方法是[创建原始字符串](https://www.geeksforgeeks.org/strcpy-in-c-cpp/) **S** 的副本，然后对于每对 **(a，b)** [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，如果找到字符 **'a'** ，则在原始字符串的副本中用字符 **'b'** 替换它。检查所有配对后，[打印修改后的字符串](https://www.geeksforgeeks.org/print-string-specified-character-occurred-given-no-times/) **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify given string
// by replacement of characters
void replaceCharacters(
    string s, vector<vector<char> > p)
{

    // Store the length of the string
    // and the number of pairs
    int n = s.size(), k = p.size();

    // Create a copy of the string s
    string temp = s;

    // Traverse the pairs of characters
    for (int j = 0; j < k; j++) {

        // a -> Character to be replaced
        // b -> Replacing character
        char a = p[j][0], b = p[j][1];

        // Traverse the original string
        for (int i = 0; i < n; i++) {

            // If an occurrence of a is found
            if (s[i] == a) {

                // Replace with b
                temp[i] = b;
            }
        }
    }

    // Print the result
    cout << temp;
}

// Driver Code
int main()
{
    string S = "aabbgg";
    vector<vector<char> > P{ { 'a', 'b' },
                             { 'b', 'g' },
                             { 'g', 'a' } };
    replaceCharacters(S, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to modify given string
// by replacement of characters
static void replaceCharacters(String s, char p[][])
{

    // Store the length of the string
    // and the number of pairs
    int n = s.length(), k = p.length;

    // Create a copy of the string s
    char temp[] = s.toCharArray();

    // Traverse the pairs of characters
    for(int j = 0; j < k; j++)
    {

        // a -> Character to be replaced
        // b -> Replacing character
        char a = p[j][0], b = p[j][1];

        // Traverse the original string
        for(int i = 0; i < n; i++)
        {

            // If an occurrence of a is found
            if (s.charAt(i) == a)
            {

                // Replace with b
                temp[i] = b;
            }
        }
    }

    // Print the result
    System.out.println(new String(temp));
}

// Driver Code
public static void main(String[] args)
{
    String S = "aabbgg";
    char P[][] = { { 'a', 'b' },
                   { 'b', 'g' },
                   { 'g', 'a' } };
    replaceCharacters(S, P);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to modify given string
# by replacement of characters
def replaceCharacters(s, p):

    # Store the length of the string
    # and the number of pairs
    n = len(s)
    k = len(p)

    # Create a copy of the string s
    temp = s

    # Traverse the pairs of characters
    for j in range(k):

        # a -> Character to be replaced
        # b -> Replacing character
        a = p[j][0]
        b = p[j][1]

        # Traverse the original string
        for i in range(n):

            # If an occurrence of a is found
            if (s[i] == a):

                # Replace with b
                temp = list(temp)
                temp[i] = b
                temp = ''.join(temp)

    # Print the result
    print(temp)

# Driver Code
if __name__ == '__main__':

    S = "aabbgg"
    P = [ [ 'a', 'b' ],
          [ 'b', 'g' ],
          [ 'g', 'a' ] ]

    replaceCharacters(S, P)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to modify given string
// by replacement of characters
static void replaceCharacters(string s, char[,] p)
{

    // Store the length of the string
    // and the number of pairs
    int n = s.Length, k = p.GetLength(0);

    // Create a copy of the string s
    char[] temp = s.ToCharArray();

    // Traverse the pairs of characters
    for(int j = 0; j < k; j++)
    {

        // a -> Character to be replaced
        // b -> Replacing character
        char a = p[j, 0], b = p[j, 1];

        // Traverse the original string
        for(int i = 0; i < n; i++)
        {

            // If an occurrence of a is found
            if (s[i] == a)
            {

                // Replace with b
                temp[i] = b;
            }
        }
    }

    // Print the result
    Console.WriteLine(new string(temp));
}

// Driver Code
public static void Main(string[] args)
{
    string S = "aabbgg";
    char [,]P = { { 'a', 'b' },
                  { 'b', 'g' },
                  { 'g', 'a' } };

    replaceCharacters(S, P);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to modify given string
// by replacement of characters
function replaceCharacters(s, p)
{

    // Store the length of the string
    // and the number of pairs
    var n = s.length, k = p.length;

    // Create a copy of the string s
    var temp = s;

    // Traverse the pairs of characters
    for(j = 0; j < k; j++)
    {

        // a -> Character to be replaced
        // b -> Replacing character
        var a = p[j][0], b = p[j][1];

        // Traverse the original string
        for(i = 0; i < n; i++)
        {

            // If an occurrence of a is found
            if (s.charAt(i) == a)
            {

                // Replace with b
                temp[i] = b;
                temp = temp.substring(0, i) + b +
                       temp.substring(i + 1, n);
            }
        }
    }

    // Print the result
    document.write((temp));
}

// Driver Code
var S = "aabbgg";
var P = [ [ 'a', 'b' ],
          [ 'b', 'g' ],
          [ 'g', 'a' ] ];

replaceCharacters(S, P);

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
bbggaa
```

***时间复杂度:** O(K * N)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过使用大小为 **26** 的两个辅助数组将替换存储在[数组](https://www.geeksforgeeks.org/array-data-structure/)中来优化。按照以下步骤解决问题:

*   初始化两个数组，大小为 **26** 的 **arr[]** 和 **brr[]** ，并将字符串的字符 **S** 存储在两个数组中。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)对 **P** ，并执行以下步骤:
    *   将 **A** 初始化为**P【I】【0】**，将 **B** 初始化为**P【I】【1】**，表示字符 **A** 将被字符 **B** 替换。
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，25】**，如果**arr【j】**等于 **A** ，则将**brr【j】**更新为 **B** 。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，对于每个**S【I】**将其更新为**brr【S【I】–‘a’】**。
*   完成上述步骤后，打印修改后的字符串 **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify given
// string by replacing characters
void replaceCharacters(
    string s, vector<vector<char> > p)
{
    // Store the size of string
    // and the number of pairs
    int n = s.size(), k = p.size();

    // Initialize 2 character arrays
    char arr[26];
    char brr[26];

    // Traverse the string s
    // Update arrays arr[] and brr[]
    for (int i = 0; i < n; i++) {
        arr[s[i] - 'a'] = s[i];
        brr[s[i] - 'a'] = s[i];
    }

    // Traverse the array of pairs p
    for (int j = 0; j < k; j++) {

        // a -> Character to be replaced
        // b -> Replacing character
        char a = p[j][0], b = p[j][1];

        // Iterate over the range [0, 25]
        for (int i = 0; i < 26; i++) {

            // If it is equal to current
            // character, then replace it
            // in the array b
            if (arr[i] == a) {
                brr[i] = b;
            }
        }
    }

    // Print the array brr[]
    for (int i = 0; i < n; i++) {
        cout << brr[s[i] - 'a'];
    }
}

// Driver Code
int main()
{
    string S = "aabbgg";
    vector<vector<char> > P{ { 'a', 'b' },
                             { 'b', 'g' },
                             { 'g', 'a' } };
    replaceCharacters(S, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to modify given
// string by replacing characters
static void replaceCharacters(String s, char[][] p)
{

    // Store the size of string
    // and the number of pairs
    int n = s.length(), k = p.length;

    // Initialize 2 character arrays
    char[] arr = new char[26];
    char[] brr = new char[26];

    // Traverse the string s
    // Update arrays arr[] and brr[]
    for(int i = 0; i < n; i++)
    {
        arr[s.charAt(i) - 'a'] = s.charAt(i);
        brr[s.charAt(i) - 'a'] = s.charAt(i);
    }

    // Traverse the array of pairs p
    for(int j = 0; j < k; j++)
    {

        // a -> Character to be replaced
        // b -> Replacing character
        char a = p[j][0], b = p[j][1];

        // Iterate over the range [0, 25]
        for(int i = 0; i < 26; i++)
        {

            // If it is equal to current
            // character, then replace it
            // in the array b
            if (arr[i] == a)
            {
                brr[i] = b;
            }
        }
    }

    // Print the array brr[]
    for(int i = 0; i < n; i++)
    {
       System.out.print(brr[s.charAt(i) - 'a']);
    }
}

// Driver code
public static void main(String[] args)
{
    String S = "aabbgg";
    char[][] P = { { 'a', 'b' },
                   { 'b', 'g' },
                   { 'g', 'a' } };

    replaceCharacters(S, P);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to modify given
# string by replacing characters
def replaceCharacters(s, p):

    # Store the size of string
    # and the number of pairs
    n, k = len(s), len(p)

    # Initialize 2 character arrays
    arr = [0] * 26
    brr = [0] * 26

    # Traverse the string s
    # Update arrays arr[] and brr[]
    for i in range(n):
        arr[ord(s[i]) - ord('a')] = s[i]
        brr[ord(s[i]) - ord('a')] = s[i]

    # Traverse the array of pairs p
    for j in range(k):

        # a -> Character to be replaced
        # b -> Replacing character
        a, b = p[j][0], p[j][1]

        # Iterate over the range [0, 25]
        for i in range(26):

            # If it is equal to current
            # character, then replace it
            # in the array b
            if (arr[i] == a):
                brr[i] = b

    # Print the array brr[]
    for i in range(n):
        print(brr[ord(s[i]) - ord('a')], end = "")

# Driver Code
if __name__ == '__main__':

    S = "aabbgg"
    P = [ [ 'a', 'b' ],
          [ 'b', 'g' ],
          [ 'g', 'a' ] ]

    replaceCharacters(S, P)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
public class GFG{

  // Function to modify given
  // string by replacing characters
  static void replaceCharacters(string s, char[,] p)
  {

    // Store the size of string
    // and the number of pairs
    int n = s.Length, k = p.GetLength(0);

    // Initialize 2 character arrays
    char[] arr = new char[26];
    char[] brr = new char[26];

    // Traverse the string s
    // Update arrays arr[] and brr[]
    for(int i = 0; i < n; i++)
    {
      arr[s[i] - 'a'] = s[i];
      brr[s[i] - 'a'] = s[i];
    }

    // Traverse the array of pairs p
    for(int j = 0; j < k; j++)
    {

      // a -> Character to be replaced
      // b -> Replacing character
      char a = p[j,0], b = p[j,1];

      // Iterate over the range [0, 25]
      for(int i = 0; i < 26; i++)
      {

        // If it is equal to current
        // character, then replace it
        // in the array b
        if (arr[i] == a)
        {
          brr[i] = b;
        }
      }
    }

    // Print the array brr[]
    for(int i = 0; i < n; i++)
    {
      Console.Write(brr[s[i] - 'a']);
    }
  }

  // Driver code

  static public void Main ()
  {

    String S = "aabbgg";
    char[,] P = { { 'a', 'b' },
                 { 'b', 'g' },
                 { 'g', 'a' } };

    replaceCharacters(S, P);

  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to modify given
      // string by replacing characters
      function replaceCharacters(s, p) {
        // Store the size of string
        // and the number of pairs
        var n = s.length,
          k = p.length;

        // Initialize 2 character arrays
        var arr = new Array(26).fill(0);
        var brr = new Array(26).fill(0);

        // Traverse the string s
        // Update arrays arr[] and brr[]
        for (var i = 0; i < n; i++) {
          arr[s[i].charCodeAt(0) - "a".charCodeAt(0)] = s[i];
          brr[s[i].charCodeAt(0) - "a".charCodeAt(0)] = s[i];
        }

        // Traverse the array of pairs p
        for (var j = 0; j < k; j++) {
          // a -> Character to be replaced
          // b -> Replacing character
          var a = p[j][0],
            b = p[j][1];

          // Iterate over the range [0, 25]
          for (var i = 0; i < 26; i++) {
            // If it is equal to current
            // character, then replace it
            // in the array b
            if (arr[i] === a) {
              brr[i] = b;
            }
          }
        }

        // Print the array brr[]
        for (var i = 0; i < n; i++) {
          document.write(brr[s[i].charCodeAt(0) -
          "a".charCodeAt(0)]);
        }
      }

      // Driver code
      var S = "aabbgg";
      var P = [
        ["a", "b"],
        ["b", "g"],
        ["g", "a"],
      ];

      replaceCharacters(S, P);

</script>
```

**Output:** 

```
bbggaa
```

***时间复杂度:** O(N + K)*
***辅助空间:** O(1)*