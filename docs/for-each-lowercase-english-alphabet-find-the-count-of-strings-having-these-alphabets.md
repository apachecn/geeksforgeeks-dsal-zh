# 对于每一个小写英文字母，找出有这些字母的字符串的数量

> 原文:[https://www . geesforgeks . org/for-ever-小写-English-alphabet-find-the-count-of-strings-having-thes-alphabets/](https://www.geeksforgeeks.org/for-each-lowercase-english-alphabet-find-the-count-of-strings-having-these-alphabets/)

给定一组小写英文字母字符串。任务是为每个字母[a-z]找到包含这些字母的字符串的数量。
**例:**

> **输入:** str = {“极客”、“for”、“code”}
> **输出:**{ 0 0 1 1 2 1 0 0 0 0 2 0 1 0 0 1 0 0 0 0 }
> **解释:**
> 对于一个字母，说‘e’，它存在于{“极客”、“code”}，因此它的计数是 2。
> 同样对于另一个字母的结果可以找到。
> 
> **输入:** str = {“我”、“会”、“练习”、“日常”}
> **输出:**2 0 1 2 0 0 3 0 0 0 0 1 0 0 1 0 1 0 1 1 0 1 0
> T6】解释:
> 对于一个字母，说‘我’，它存在于{“我”、“会”、“练习”}，因此它的计数是 3。
> 同样对于另一个字母的结果可以找到。

**天真方法:**

1.  为每个大小为 26 的字母创建一个全局计数器，用 0 初始化它。
2.  对每个小字母的英文字母进行循环。如果在当前字符串中找到当前字母，则增加计数器的值，比如字母“x”。
3.  对所有小写英文字母重复此步骤。

**时间复杂度:** O(26*N)，其中 N 为所有字符串长度之和。

**有效方法:**

*   而不是对每个英文字母运行一个循环，并检查它是否存在于当前字符串中。相反，我们可以对每个字符串单独运行一个循环，并为该字符串中的任何字母递增全局计数器。
*   此外，为了避免重复计数，我们创建了一个访问布尔数组来标记到目前为止遇到的字符。这种方法将复杂度降低到 0(N)。

下面是上述方法的实现:

## C++

```
// C++ program to find count of strings
// for each letter [a-z] in english alphabet
#include <bits/stdc++.h>
using namespace std;

// Function to find the countStrings
// for each letter [a-z]
void CountStrings(vector<string>& str)
{
    int size = str.size();

    // Initialize result as zero
    vector<int> count(26, 0);

    // Mark all letter as not visited
    vector<bool> visited(26, false);

    // Loop through each strings
    for (int i = 0; i < size; ++i)
    {

        for (int j = 0; j < str[i].length(); ++j)
        {

            // Increment the global counter
            // for current character of string
            if (visited[str[i][j]] == false)
                count[str[i][j] - 'a']++;

            visited[str[i][j]] = true;
        }

        // Instead of re-initialising boolean
        // vector every time we just reset
        // all visited letter to false
        for (int j = 0; j < str[i].length(); ++j)
        {
            visited[str[i][j]] = false;
        }
    }

    // Print count for each letter
    for (int i = 0; i < 26; ++i)
    {
        cout << count[i] << " ";
    }
}

// Driver program
int main()
{
    // Given array of strings
    vector<string> str = {"i", "will",
                          "practice", "everyday"};

    // Call the countStrings function
    CountStrings(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of Strings
// for each letter [a-z] in english alphabet
class GFG{

// Function to find the countStrings
// for each letter [a-z]
static void CountStrings(String []str)
{
    int size = str.length;

    // Initialize result as zero
    int []count = new int[26];

    // Mark all letter as not visited
    boolean []visited = new boolean[26];
    // Loop through each Strings
    for (int i = 0; i < size; ++i)
    {
        for (int j = 0; j < str[i].length(); ++j)
        {
            // Increment the global counter
            // for current character of String
            if (visited[str[i].charAt(j) - 'a'] == false)
                count[str[i].charAt(j) - 'a']++;

            visited[str[i].charAt(j) - 'a'] = true;
        }

        // Instead of re-initialising boolean
        // vector every time we just reset
        // all visited letter to false
        for (int j = 0; j < str[i].length(); ++j)
        {
            visited[str[i].charAt(j) - 'a'] = false;
        }
    }

    // Print count for each letter
    for (int i = 0; i < 26; ++i)
    {
        System.out.print(count[i] + " ");
    }
}

// Driver program
public static void main(String[] args)
{
    // Given array of Strings
    String []str = {"i", "will",
                    "practice", "everyday"};

    // Call the countStrings function
    CountStrings(str);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to find count of 
# strings for each letter [a-z] in 
# english alphabet

# Function to find the countStrings 
# for each letter [a-z] 
def CountStrings(s):

    size = len(s)

    # Initialize result as zero
    count = [0] * 26

    # Mark all letter as not visited
    visited = [False] * 26

    # Loop through each strings
    for i in range(size):
        for j in range(len(s[i])):

            # Increment the global counter
            # for current character of string
            if visited[ord(s[i][j]) - 
                       ord('a')] == False:
                count[ord(s[i][j]) - 
                      ord('a')] += 1

            visited[ord(s[i][j]) - 
                    ord('a')] = True

        # Instead of re-initialising boolean
        # vector every time we just reset
        # all visited letter to false
        for j in range(len(s[i])):
            visited[ord(s[i][j]) - 
                    ord('a')] = False

    # Print count for each letter
    for i in range(26):
        print(count[i], end = ' ')

# Driver code
if __name__=='__main__':

    # Given array of strings
    s = [ "i", "will", 
          "practice", "everyday" ]

    # Call the countStrings function
    CountStrings(s)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find count of Strings
// for each letter [a-z] in english alphabet
using System;

class GFG{

// Function to find the countStrings
// for each letter [a-z]
static void CountStrings(String []str)
{
    int size = str.Length;

    // Initialize result as zero
    int []count = new int[26];

    // Mark all letter as not visited
    bool []visited = new bool[26];

    // Loop through each Strings
    for(int i = 0; i < size; ++i)
    {
        for(int j = 0; j < str[i].Length; ++j)
        {

            // Increment the global counter
            // for current character of String
            if (visited[str[i][j] - 'a'] == false)
                count[str[i][j] - 'a']++;

            visited[str[i][j] - 'a'] = true;
        }

        // Instead of re-initialising bool
        // vector every time we just reset
        // all visited letter to false
        for(int j = 0; j < str[i].Length; ++j)
        {
            visited[str[i][j] - 'a'] = false;
        }
    }

    // Print count for each letter
    for(int i = 0; i < 26; ++i)
    {
        Console.Write(count[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{

    // Given array of Strings
    String []str = { "i", "will",
                     "practice", "everyday"};

    // Call the countStrings function
    CountStrings(str);
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
2 0 1 1 2 0 0 0 3 0 0 1 0 0 0 1 0 2 0 1 0 1 1 0 1 0

```

**时间复杂度:** O(N)，其中 N 为所有字符串长度之和。