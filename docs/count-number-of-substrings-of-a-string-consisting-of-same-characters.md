# 计算由相同字符组成的字符串的子字符串数量

> 原文:[https://www . geeksforgeeks . org/count-由相同字符组成的字符串的子字符串数/](https://www.geeksforgeeks.org/count-number-of-substrings-of-a-string-consisting-of-same-characters/)

给定一个字符串。任务是找出由相同字符组成的子串的数量。

**示例:**

> **输入:**ABBA
> T3】输出: 5
> 想要的子串是{a}、{b}、{b}、{a}、{bb}
> 
> **输入:**bbbcbb
> T3】输出: 10

**方法:**已知一串长度 **n** ，共有 **n*(n+1)/2** 个数的子串。
将**结果**初始化为 0。遍历字符串，找到相同字符的连续元素数(比如**计数**)。每当我们找到另一个字符时，将**结果**增加**计数*(计数+1)/2** ，将**计数**设置为 1，并从该索引开始，重复上述过程。
记住，对于每个不同的字符，我们想要的子串的数量是 1。

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// number of substrings of
// same characters
void findNumbers(string s)
{
      if (s.empty()) return 0;
    // Size of the string
    int n = s.size();

    // Initialize count to 1
    int count = 1;
    int result = 0;

    // Initialize left to 0 and
    // right to 1 to traverse the
    // string
    int left = 0;
    int right = 1;

    while (right < n) {

        // Checking if consecutive
        // characters are same and
        // increment the count
        if (s[left] == s[right]) {
            count++;
        }

        // When we encounter a
        // different characters
        else {

            // Increment the result
            result += count * (count + 1) / 2;

            // To repeat the whole
            // process set left equals
            // right and count variable to 1
            left = right;
            count = 1;
        }

        right++;
    }

    // Store the final
    // value of result
    result += count * (count + 1) / 2;

    cout << result << endl;
}

// Driver code
int main()
{
    string s = "bbbcbb";

    findNumbers(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the
    // number of substrings of
    // same characters
    static void findNumbers(String s)
    {
        // Size of the string
        int n = s.length();

        // Initialize count to 1
        int count = 1;
        int result = 0;

        // Initialize left to 0 and
        // right to 1 to traverse the
        // string
        int left = 0;
        int right = 1;

        while (right < n)
        {

            // Checking if consecutive
            // characters are same and
            // increment the count
            if (s.charAt(left) == s.charAt(right))
            {
                count++;
            }

            // When we encounter a
            // different characters
            else
            {

                // Increment the result
                result += count * (count + 1) / 2;

                // To repeat the whole
                // process set left equals
                // right and count variable to 1
                left = right;
                count = 1;
            }

            right++;
        }

        // Store the final
        // value of result
        result += count * (count + 1) / 2;

        System.out.println(result);
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "bbbcbb";

        findNumbers(s);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the number of
# substrings of same characters
def findNumbers(s):

    # Size of the string
    n = len(s)

    # Initialize count to 1
    count = 1
    result = 0

    # Initialize left to 0 and right to 1
    # to traverse the string
    left = 0
    right = 1

    while (right < n):

        # Checking if consecutive
        # characters are same and
        # increment the count
        if (s[left] == s[right]):
            count += 1

        # When we encounter a
        # different characters
        else:

            # Increment the result
            result += count * (count + 1) // 2

            # To repeat the whole
            # process set left equals
            # right and count variable to 1
            left = right
            count = 1

        right += 1

    # Store the final value of result
    result += count * (count + 1) // 2

    print(result)

# Driver code
s = "bbbcbb"

findNumbers(s)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the
    // number of substrings of
    // same characters
    static void findNumbers(String s)
    {
        // Size of the string
        int n = s.Length;

        // Initialize count to 1
        int count = 1;
        int result = 0;

        // Initialize left to 0 and
        // right to 1 to traverse the
        // string
        int left = 0;
        int right = 1;

        while (right < n)
        {
            // Checking if consecutive
            // characters are same and
            // increment the count
            if (s[left] == s[right])
                count++;

            // When we encounter a
            // different characters
            else
            {
                // Increment the result
                result += count * (count + 1) / 2;

                // To repeat the whole
                // process set left equals
                // right and count variable to 1
                left = right;
                count = 1;
            }
            right++;
        }

        // Store the final
        // value of result
        result += count * (count + 1) / 2;

        Console.WriteLine(result);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "bbbcbb";

        findNumbers(s);
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

// Javascript implementation
// of the above approach

// Function to return the
// number of substrings of
// same characters
function findNumbers(s)
{

    // Size of the string
    var n = s.length;

    // Initialize count to 1
    var count = 1;
    var result = 0;

    // Initialize left to 0 and
    // right to 1 to traverse the
    // string
    var left = 0;
    var right = 1;

    while (right < n)
    {

        // Checking if consecutive
        // characters are same and
        // increment the count
        if (s[left] == s[right])
        {
            count++;
        }

        // When we encounter a
        // different characters
        else
        {

            // Increment the result
            result += parseInt(count * (count + 1) / 2);

            // To repeat the whole
            // process set left equals
            // right and count variable to 1
            left = right;
            count = 1;
        }
        right++;
    }

    // Store the final
    // value of result
    result += parseInt(count * (count + 1) / 2);

    document.write(result);
}

// Driver code
var s = "bbbcbb";

findNumbers(s);

// This code is contributed by itsok

</script>
```

**Output:** 

```
10
```