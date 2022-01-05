# 用至少一个不同的索引找到两个最大长度相等的子序列

> 原文:[https://www . geesforgeks . org/find-两个最大长度相等的子序列，至少有一个不同的索引/](https://www.geeksforgeeks.org/find-two-equal-subsequences-of-maximum-length-with-at-least-one-different-index/)

给定一个字符串 **str** ，任务是找到最大长度 **K** 使得存在两个子序列 **A** 和 **B** 每个长度 **K** 使得 **A = B** 并且 **A** 和 **B** 之间的公共索引数量最多为**K–1**。
**例:**

> **输入:**str =“geeksforgeks”
> T3】输出: 12
> 两个子序列为
> str[0…1]+str[3…12]=“geksforgeks”
> 和 str[0]+str[2…12]=“geksforgeks”。
> **输入:**str = " abcdefg "
> **输出:** 7

**方法:**找出任意一对相同字母之间有最小字母数的字母，假设这个最小数是 **X** ，现在问题的答案是**len(str)–(X+1)**。在 **X** 中增加一个，不计算该对中的一个字母。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to return the required
// length of the subsequences
int maxLength(string str, int len)
{
    // To store the result
    int res = 0;

    // To store the last visited
    // position of lowercase letters
    int lastPos[MAX];

    // Initialisation of frequency array to -1 to
    // indicate no character has previously occured
    for (int i = 0; i < MAX; i++) {
        lastPos[i] = -1;
    }

    // For every character of the string
    for (int i = 0; i < len; i++) {

        // Get the index of the current character
        int C = str[i] - 'a';

        // If the current character has
        // appeared before in the string
        if (lastPos[C] != -1) {

            // Update the result
            res = max(len - (i - lastPos[C] - 1) - 1, res);
        }

        // Update the last position
        // of the current character
        lastPos[C] = i;
    }

    return res;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int len = str.length();

    cout << maxLength(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAX = 26;

// Function to return the required
// length of the subsequences
static int maxLength(String str, int len)
{
    // To store the result
    int res = 0;

    // To store the last visited
    // position of lowercase letters
    int lastPos[] = new int[MAX];

    // Initialisation of frequency array to -1 to
    // indicate no character has previously occured
    for (int i = 0; i < MAX; i++)
    {
        lastPos[i] = -1;
    }

    // For every character of the String
    for (int i = 0; i < len; i++)
    {

        // Get the index of the current character
        int C = str.charAt(i) - 'a';

        // If the current character has
        // appeared before in the String
        if (lastPos[C] != -1)
        {

            // Update the result
            res = Math.max(len - (i -
                            lastPos[C] - 1) - 1, res);
        }

        // Update the last position
        // of the current character
        lastPos[C] = i;
    }
    return res;
}

// Driver code
public static void main(String args[])
{
    String str = "geeksforgeeks";
    int len = str.length();

    System.out.println(maxLength(str, len));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the approach
MAX = 26;

# Function to return the required
# length of the subsequences
def maxLength(str, len):

    # To store the result
    res = 0;

    # To store the last visited
    # position of lowercase letters
    lastPos = [0] * MAX;

    # Initialisation of frequency array to -1 to
    # indicate no character has previously occured
    for i in range(MAX):
        lastPos[i] = -1;

    # For every character of the String
    for i in range(len):

        # Get the index of the current character
        C = ord(str[i]) - ord('a');

        # If the current character has
        # appeared before in the String
        if (lastPos[C] != -1):

            # Update the result
            res = max(len - (i - lastPos[C] - 1) - 1, res);

        # Update the last position
        # of the current character
        lastPos[C] = i;

    return res;

# Driver code
if __name__ == '__main__':
    str = "geeksforgeeks";
    len = len(str);

    print(maxLength(str, len));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAX = 26;

    // Function to return the required
    // length of the subsequences
    static int maxLength(string str, int len)
    {
        // To store the result
        int res = 0;

        // To store the last visited
        // position of lowercase letters
        int []lastPos = new int[MAX];

        // Initialisation of frequency array to -1 to
        // indicate no character has previously occured
        for (int i = 0; i < MAX; i++)
        {
            lastPos[i] = -1;
        }

        // For every character of the String
        for (int i = 0; i < len; i++)
        {

            // Get the index of the current character
            int C = str[i] - 'a';

            // If the current character has
            // appeared before in the String
            if (lastPos[C] != -1)
            {

                // Update the result
                res = Math.Max(len - (i -
                                lastPos[C] - 1) - 1, res);
            }

            // Update the last position
            // of the current character
            lastPos[C] = i;
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
        string str = "geeksforgeeks";
        int len = str.Length;

        Console.WriteLine(maxLength(str, len));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 26;

// Function to return the required
// length of the subsequences
function maxLength(str, len)
{
    // To store the result
    var res = 0;

    // To store the last visited
    // position of lowercase letters
    var lastPos = Array(MAX);

    // Initialisation of frequency array to -1 to
    // indicate no character has previously occured
    for (var i = 0; i < MAX; i++) {
        lastPos[i] = -1;
    }

    // For every character of the string
    for (var i = 0; i < len; i++) {

        // Get the index of the current character
        var C = str[i].charCodeAt(0) - 'a'.charCodeAt(0);

        // If the current character has
        // appeared before in the string
        if (lastPos[C] != -1) {

            // Update the result
            res = Math.max(len - (i - lastPos[C] - 1) - 1, res);
        }

        // Update the last position
        // of the current character
        lastPos[C] = i;
    }

    return res;
}

// Driver code
var str = "geeksforgeeks";
var len = str.length;
document.write( maxLength(str, len));

</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(n)，其中 n 为输入字符串的长度。