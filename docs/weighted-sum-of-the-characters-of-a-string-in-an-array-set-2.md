# 数组中字符串字符的加权和|集合 2

> 原文:[https://www . geesforgeks . org/加权数组集字符串字符总和-2/](https://www.geeksforgeeks.org/weighted-sum-of-the-characters-of-a-string-in-an-array-set-2/)

给你一个字符串数组 **str[]** ，任务是从数组中找到给定字符串 **s** 的分数。字符串的分数定义为其字符的字母值与字符串在数组中的**位置**之和的**乘积**。
**举例:****** 

> **输入:**str[]= {“sahil”、“shashanak”、“sanjit”、“abhinav”、“mohit”}，s = "abhinav"
> **输出:**228
> abhinav " = 1+2+8+9+14+1+22 = 57
> str 中“abhinav”的位置为 4，57 x 4 = 228
> **输入:**str[]= {“geeksfs”

**方法:**
在 [SET 1](https://www.geeksforgeeks.org/sum-of-the-alphabetical-values-of-the-characters-of-a-string/) 中，我们看到了一种方法，每次执行查询时，必须通过对**str【】**的单次遍历来找到字符串的位置。当使用哈希表进行大量查询时，可以对此进行优化。

*   创建存在于**字符串[]** 中的所有字符串及其在数组中各自位置的哈希映射。
*   然后对于每个查询 **s** ，检查地图中是否存在 **s** 。如果是，则计算 **s** 的字母值之和，并将其存储在 **sum** 中。
*   打印**总和* pos** ，其中 **pos** 是与地图中的 **s** 相关联的值，即其在**str【】**中的位置。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required string score
int strScore(string str[], string s, int n)
{
    // create a hash map of strings in str
    unordered_map<string, int> m;

    // Store every string in the map
    // along with its position in the array
    for (int i = 0; i < n; i++)
        m[str[i]] = i + 1;

    // If given string is not present in str[]
    if (m.find(s) == m.end())
        return 0;

    int score = 0;

    for (int i = 0; i < s.length(); i++)
        score += s[i] - 'a' + 1;

    // Multiply sum of alphabets with position
    score = score * m[s];

    return score;
}

// Driver code
int main()
{
    string str[] = { "geeksforgeeks", "algorithms", "stack" };
    string s = "algorithms";
    int n = sizeof(str) / sizeof(str[0]);
    int score = strScore(str, s, n);
    cout << score;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;
import java.util.Map;

class GfG
{
    // Function to return the required string score
    static int strScore(String str[], String s, int n)
    {
        // create a hash map of strings in str
        HashMap<String, Integer> m = new HashMap<>();

        // Store every string in the map
        // along with its position in the array
        for (int i = 0; i < n; i++)
            m.put(str[i], i + 1);

        // If given string is not present in str[]
        if (!m.containsKey(s))
            return 0;

        int score = 0;

        for (int i = 0; i < s.length(); i++)
            score += s.charAt(i) - 'a' + 1;

        // Multiply sum of alphabets with position
        score = score * m.get(s);

        return score;
    }

    // Driver code
    public static void main(String []args)
    {
        String str[] = { "geeksforgeeks", "algorithms",
                                            "stack" };
        String s = "algorithms";
        int n = str.length;
        System.out.println(strScore(str, s, n));

    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required
# string score
def strScore(string, s, n) :

    # create a hash map of strings in str
    m = {}

    # Store every string in the map
    # along with its position in the array
    for i in range(n) :
        m[string[i]] = i + 1

    # If given string is not present in str[]
    if s not in m.keys() :
        return 0

    score = 0

    for i in range(len(s)) :
        score += ord(s[i]) - ord('a') + 1

    # Multiply sum of alphabets
    # with position
    score = score * m[s]

    return score

# Driver code
if __name__ == "__main__" :

    string = [ "geeksforgeeks",
               "algorithms", "stack" ]
    s = "algorithms"
    n = len(string)
    score = strScore(string, s, n);
    print(score)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GfG
{
    // Function to return the required string score
    static int strScore(string [] str, string s, int n)
    {
        // create a hash map of strings in str
        Dictionary<string, int> m = new Dictionary<string, int>();

        // Store every string in the map
        // along with its position in the array
        for (int i = 0; i < n; i++)
            m[str[i]] = i + 1;

        // If given string is not present in str[]
        if (!m.ContainsKey(s))
            return 0;

        int score = 0;

        for (int i = 0; i < s.Length; i++)
            score += s[i] - 'a' + 1;

        // Multiply sum of alphabets with position
        score = score * m[s];

        return score;
    }

    // Driver code
    public static void Main()
    {
        string [] str = { "geeksforgeeks", "algorithms",
                                            "stack" };
        string s = "algorithms";
        int n = str.Length;
        Console.WriteLine(strScore(str, s, n));

    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

    // Function to return the required string score
    function strScore(str, s, n)
    {
        // create a hash map of strings in str
        let m = new Map();

        // Store every string in the map
        // along with its position in the array
        for (let i = 0; i < n; i++)
            m.set(str[i], i + 1);

        // If given string is not present in str[]
        if (!m.has(s))
            return 0;

        let score = 0;

        for (let i = 0; i < s.length; i++)
            score += s[i].charCodeAt() - 'a'.charCodeAt() + 1;

        // Multiply sum of alphabets with position
        score = score * m.get(s);

        return score;
    }

// Driver Code

        let str = [ "geeksforgeeks", "algorithms",
                                            "stack" ];
        let s = "algorithms";
        let n = str.length;
        document.write(strScore(str, s, n));

</script>
```

**Output:** 

```
244
```