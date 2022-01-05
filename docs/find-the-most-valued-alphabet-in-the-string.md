# 找到字符串中最有价值的字母表

> 原文:[https://www . geesforgeks . org/find-字符串中最有价值的字母/](https://www.geeksforgeeks.org/find-the-most-valued-alphabet-in-the-string/)

给定一个字符串 **str** ，任务是在 **str** 中找到最大值字母表。特定字母表的值被定义为其最后一次和第一次出现的索引的差异。如果有多个这样的字母，那么找到字典上最小的字母。
**例:**

> **输入:** str = "abbba"
> **输出:** a
> 值(' a ')= 4–0 = 4
> 值(' b ')= 3–1 = 2
> **输入:** str = "bbb"
> **输出:** b

**方法:**想法是将每个字母的第一次和最后一次出现存储在两个辅助数组中，比如**第一[]** 和**最后[]** 。现在，这两个数组可以用来找到给定字符串中的最大值字母表。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to return the maximum
// valued alphabet
char maxAlpha(string str, int len)
{

    // To store the first and the last
    // occurrence of all the characters
    int first[MAX], last[MAX];

    // Set the first and the last occurrence
    // of all the characters to -1
    for (int i = 0; i < MAX; i++) {
        first[i] = -1;
        last[i] = -1;
    }

    // Update the occurrences of the characters
    for (int i = 0; i < len; i++) {

        int index = (str[i] - 'a');

        // Only set the first occurrence if
        // it hasn't already been set
        if (first[index] == -1)
            first[index] = i;

        last[index] = i;
    }

    // To store the result
    int ans = -1, maxVal = -1;

    // For every alphabet
    for (int i = 0; i < MAX; i++) {

        // If current alphabet doesn't appear
        // in the given string
        if (first[i] == -1)
            continue;

        // If the current character has
        // the highest value so far
        if ((last[i] - first[i]) > maxVal) {
            maxVal = last[i] - first[i];
            ans = i;
        }
    }

    return (char)(ans + 'a');
}

// Driver code
int main()
{
    string str = "abbba";
    int len = str.length();

    cout << maxAlpha(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAX = 26;

// Function to return the maximum
// valued alphabet
static char maxAlpha(String str, int len)
{

    // To store the first and the last
    // occurrence of all the characters
    int []first = new int[MAX];
    int []last = new int[MAX];

    // Set the first and the last occurrence
    // of all the characters to -1
    for (int i = 0; i < MAX; i++)
    {
        first[i] = -1;
        last[i] = -1;
    }

    // Update the occurrences of the characters
    for (int i = 0; i < len; i++)
    {

        int index = (str.charAt(i) - 'a');

        // Only set the first occurrence if
        // it hasn't already been set
        if (first[index] == -1)
            first[index] = i;

        last[index] = i;
    }

    // To store the result
    int ans = -1, maxVal = -1;

    // For every alphabet
    for (int i = 0; i < MAX; i++)
    {

        // If current alphabet doesn't appear
        // in the given String
        if (first[i] == -1)
            continue;

        // If the current character has
        // the highest value so far
        if ((last[i] - first[i]) > maxVal)
        {
            maxVal = last[i] - first[i];
            ans = i;
        }
    }
    return (char)(ans + 'a');
}

// Driver code
public static void main(String[] args)
{
    String str = "abbba";
    int len = str.length();

    System.out.print(maxAlpha(str, len));
}
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python implementation of the approach
MAX = 26

# Function to return the maximum
# valued alphabet
def maxAlpha(str, len):

    # To store the first and the last
    # occurrence of all the characters

    # Set the first and the last occurrence
    # of all the characters to -1

    first = [-1 for x in range(MAX)]
    last = [-1 for x in range(MAX)]

    # Update the occurrences of the characters
    for i in range(0,len):

        index = ord(str[i])-97

        # Only set the first occurrence if
        # it hasn't already been set
        if (first[index] == -1):
            first[index] = i

        last[index] = i

    # To store the result
    ans = -1
    maxVal = -1

    # For every alphabet
    for i in range(0,MAX):

        # If current alphabet doesn't appear
        # in the given string
        if (first[i] == -1):
            continue

        # If the current character has
        # the highest value so far
        if ((last[i] - first[i]) > maxVal):
            maxVal = last[i] - first[i];
            ans = i

    return chr(ans + 97)

# Driver code
str = "abbba"
len = len(str)

print(maxAlpha(str, len))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 26;

// Function to return the maximum
// valued alphabet
static char maxAlpha(String str, int len)
{

    // To store the first and the last
    // occurrence of all the characters
    int []first = new int[MAX];
    int []last = new int[MAX];

    // Set the first and the last occurrence
    // of all the characters to -1
    for (int i = 0; i < MAX; i++)
    {
        first[i] = -1;
        last[i] = -1;
    }

    // Update the occurrences of the characters
    for (int i = 0; i < len; i++)
    {

        int index = (str[i] - 'a');

        // Only set the first occurrence if
        // it hasn't already been set
        if (first[index] == -1)
            first[index] = i;

        last[index] = i;
    }

    // To store the result
    int ans = -1, maxVal = -1;

    // For every alphabet
    for (int i = 0; i < MAX; i++)
    {

        // If current alphabet doesn't appear
        // in the given String
        if (first[i] == -1)
            continue;

        // If the current character has
        // the highest value so far
        if ((last[i] - first[i]) > maxVal)
        {
            maxVal = last[i] - first[i];
            ans = i;
        }
    }
    return (char)(ans + 'a');
}

// Driver code
public static void Main(String[] args)
{
    String str = "abbba";
    int len = str.Length;

    Console.Write(maxAlpha(str, len));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach
      const MAX = 26;

      // Function to return the maximum
      // valued alphabet
      function maxAlpha(str, len)
      {
        // To store the first and the last
        // occurrence of all the characters
        var first = new Array(MAX);
        var last = new Array(MAX);

        // Set the first and the last occurrence
        // of all the characters to -1
        for (var i = 0; i < MAX; i++) {
          first[i] = -1;
          last[i] = -1;
        }

        // Update the occurrences of the characters
        for (var i = 0; i < len; i++) {
          var index = str[i].charCodeAt(0) -
          "a".charCodeAt(0);

          // Only set the first occurrence if
          // it hasn't already been set
          if (first[index] === -1) first[index] = i;

          last[index] = i;
        }

        // To store the result
        var ans = -1,
          maxVal = -1;

        // For every alphabet
        for (var i = 0; i < MAX; i++) {
          // If current alphabet doesn't appear
          // in the given String
          if (first[i] === -1) continue;

          // If the current character has
          // the highest value so far
          if (last[i] - first[i] > maxVal) {
            maxVal = last[i] - first[i];
            ans = i;
          }
        }
        return String.fromCharCode(ans + "a".charCodeAt(0));
      }

      // Driver code
      var str = "abbba";
      var len = str.length;

      document.write(maxAlpha(str, len));

</script>
```

**Output:** 

```
a
```

**时间复杂度:** O(N)