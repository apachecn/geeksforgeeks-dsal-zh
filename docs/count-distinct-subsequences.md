# 计数不同的子序列

> 原文:[https://www.geeksforgeeks.org/count-distinct-subsequences/](https://www.geeksforgeeks.org/count-distinct-subsequences/)

给定一个字符串，找到它的不同子序列的计数。

**示例:**

```
Input  : str = "gfg"
Output : 7
The seven distinct subsequences are "", "g", "f",
"gf", "fg", "gg" and "gfg" 

Input  : str = "ggg"
Output : 4
The four distinct subsequences are "", "g", "gg"
and "ggg"
```

如果输入字符串的所有字符都是不同的，那么计算不同子序列的问题很容易。计数等于<sup>n</sup>C<sub>0</sub>+<sup>n</sup>C<sub>1</sub>+<sup>n</sup>C<sub>2</sub>+…<sup>n</sup>C<sub>n</sub>= 2<sup>n</sup>。
输入字符串中可以有重复时，如何统计不同的子序列？
计算重复字符串中不同子序列的简单方法是生成所有子序列。对于每个子序列，如果它还不存在的话，把它存储在散列表中。这个解决方案的时间复杂度是指数级的，它需要指数级的额外空间。

**方法 1(朴素方法):使用集合(无动态规划)**

**方法:**生成给定字符串的所有可能的子序列。字符串的子序列可以通过以下方式生成:
**a)** 在输出数组中包含一个特定的元素(比如 i <sup>th</sup> )，并递归调用输入字符串其余部分的函数。这导致字符串的子序列具有第 i <sup>个</sup>字符。
**b)** 排除某个特定元素(比如说 i <sup>th</sup> )并递归调用输入字符串剩余部分的函数。这包含所有没有第 i <sup>个</sup>字符的子序列。
一旦我们生成了一个子序列，在函数的基本情况下，我们将生成的子序列插入一个无序的集合中。无序集是一种数据结构，它以无序的方式存储不同的元素。这样，我们将所有生成的子序列插入到集合中，并打印集合的大小作为我们的答案，因为最后，集合将只包含不同的子序列。

## C++

```
// C++ program to print distinct
// subsequences of a given string
#include <bits/stdc++.h>
using namespace std;

// Create an empty set to store the subsequences
unordered_set<string> sn;

// Function for generating the subsequences
void subsequences(char s[], char op[], int i, int j)
{

    // Base Case
    if (s[i] == '\0') {
        op[j] = '\0';

        // Insert each generated
        // subsequence into the set
        sn.insert(op);
        return;
    }

    // Recursive Case
    else {
        // When a particular character is taken
        op[j] = s[i];
        subsequences(s, op, i + 1, j + 1);

        // When a particular character isn't taken
        subsequences(s, op, i + 1, j);
        return;
    }
}

// Driver Code
int main()
{
    char str[] = "ggg";
    int m = sizeof(str) / sizeof(char);
    int n = pow(2, m) + 1;

    // Output array for storing
    // the generating subsequences
    // in each call
    char op[m+1]; //extra one for having \0 at the end

    // Function Call
    subsequences(str, op, 0, 0);

    // Output will be the number
    // of elements in the set
    cout << sn.size();
    sn.clear();
    return 0;

    // This code is contributed by Kishan Mishra
}
```

## 蟒蛇 3

```
# Python3 program to print
# distinct subsequences of
# a given string
import math

# Create an empty set
# to store the subsequences
sn = []
global m
m = 0

# Function for generating
# the subsequences

def subsequences(s, op, i, j):

    # Base Case
    if(i == m):
        op[j] = None
        temp = "".join([i for i in op if i])

        # Insert each generated
        # subsequence into the set
        sn.append(temp)
        return

    # Recursive Case
    else:

        # When a particular
        # character is taken
        op[j] = s[i]

        subsequences(s, op,
                     i + 1, j + 1)

        # When a particular
        # character isn't taken
        subsequences(s, op,
                     i + 1, j)
        return

# Driver Code
str = "ggg"
m = len(str)
n = int(math.pow(2, m) + 1)

# Output array for storing
# the generating subsequences
# in each call
op = [None for i in range(n)]

# Function Call
subsequences(str, op, 0, 0)

# Output will be the number
# of elements in the set
print(len(set(sn)))

# This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program to print distinct
// subsequences of a given string

// Create an empty set to store the subsequences
let  sn = new Set();
let m = 0;

// Function for generating the subsequences
function subsequences(s, op, i, j)
{
    // Base Case
    if (i == m) {
        op[j] = '\0';

        // Insert each generated
        // subsequence into the set
        sn.add(op.join(""));
        return;
    }

    // Recursive Case
    else
    {

        // When a particular character is taken
        op[j] = s[i];
        subsequences(s, op, i + 1, j + 1);

        // When a particular character isn't taken
        subsequences(s, op, i + 1, j);
        return;
    }
}

// Driver Code
let str= "ggg";
m = str.length;
let n = Math.pow(2, m) + 1;

// Output array for storing
// the generating subsequences
// in each call
let op=new Array(n);

// Function Call
subsequences(str, op, 0, 0);

// Output will be the number
// of elements in the set
document.write(sn.size);

// This code is contributed by patel2127
</script>
```

**Output**

```
4
```

**时间复杂度** : O(2^n)
**腋空间:** O(n)
其中 n 为弦的长度。

**方法 2(有效方法):使用动态规划**

高效的解决方案不需要生成子序列。

```
Let countSub(n) be count of subsequences of 
first n characters in input string. We can
recursively write it as below. 

countSub(n) = 2*Count(n-1) - Repetition

If current character, i.e., str[n-1] of str has
not appeared before, then 
   Repetition = 0

Else:
   Repetition  =  Count(m)
   Here m is index of previous occurrence of
   current character. We basically remove all
   counts ending with previous occurrence of
   current character.
```

**这是如何工作的？**
如果没有重复，那么 count 变成 n-1 的 count 的两倍，因为我们通过在 n-1 长度的所有可能子序列的末尾添加当前字符来获得 count(n-1)更多的子序列。
如果有重复，那么我们找到以前一次出现结束的所有不同子序列的计数。这个计数可以通过递归调用前一次出现的索引来获得。
由于上述递推有重叠子问题，我们可以用动态规划法求解。

以下是上述想法的实现。

## C++

```
// C++ program to count number of distinct
// subsequences of a given string.
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 256;

// Returns count of distinct sunsequences of str.
int countSub(string str)
{
    // Create an array to store index
    // of last
    vector<int> last(MAX_CHAR, -1);

    // Length of input string
    int n = str.length();

    // dp[i] is going to store count of distinct
    // subsequences of length i.
    int dp[n + 1];

    // Empty substring has only one subsequence
    dp[0] = 1;

    // Traverse through all lengths from 1 to n.
    for (int i = 1; i <= n; i++) {
        // Number of subsequences with substring
        // str[0..i-1]
        dp[i] = 2 * dp[i - 1];

        // If current character has appeared
        // before, then remove all subsequences
        // ending with previous occurrence.
        if (last[str[i - 1]] != -1)
            dp[i] = dp[i] - dp[last[str[i - 1]]];

        // Mark occurrence of current character
        last[str[i - 1]] = (i - 1);
    }

    return dp[n];
}

// Driver code
int main()
{
    cout << countSub("gfg");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of distinct
// subsequences of a given string.
import java.util.ArrayList;
import java.util.Arrays;
public class Count_Subsequences {

    static final int MAX_CHAR = 256;

    // Returns count of distinct sunsequences of str.
    static int countSub(String str)
    {
        // Create an array to store index
        // of last
        int[] last = new int[MAX_CHAR];
        Arrays.fill(last, -1);

        // Length of input string
        int n = str.length();

        // dp[i] is going to store count of distinct
        // subsequences of length i.
        int[] dp = new int[n + 1];

        // Empty substring has only one subsequence
        dp[0] = 1;

        // Traverse through all lengths from 1 to n.
        for (int i = 1; i <= n; i++) {
            // Number of subsequences with substring
            // str[0..i-1]
            dp[i] = 2 * dp[i - 1];

            // If current character has appeared
            // before, then remove all subsequences
            // ending with previous occurrence.
            if (last[(int)str.charAt(i - 1)] != -1)
                dp[i] = dp[i] - dp[last[(int)str.charAt(i - 1)]];

            // Mark occurrence of current character
            last[(int)str.charAt(i - 1)] = (i - 1);
        }

        return dp[n];
    }

    // Driver code
    public static void main(String args[])
    {
        System.out.println(countSub("gfg"));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to count number of
# distinct subsequences of a given string

MAX_CHAR = 256

def countSub(ss):

    # create an array to store index of last
    last = [-1 for i in range(MAX_CHAR + 1)]

    # length of input string
    n = len(ss)

    # dp[i] is going to store count of
    # discount subsequence of length of i
    dp = [-2 for i in range(n + 1)]

    # empty substring has only
    # one subsequence
    dp[0] = 1

    # Traverse through all lengths
    # from 1 to n
    for i in range(1, n + 1):

        # number of subsequence with
        # substring str[0...i-1]
        dp[i] = 2 * dp[i - 1]

        # if current character has appeared
        # before, then remove all subsequences
        # ending with previous occurrence.
        if last[ord(ss[i - 1])] != -1:
            dp[i] = dp[i] - dp[last[ord(ss[i - 1])]]
        last[ord(ss[i - 1])] = i - 1

    return dp[n]

# Driver code
print(countSub("gfg"))

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# program to count number of distinct
// subsequences of a given string.
using System;

public class Count_Subsequences {

    static readonly int MAX_CHAR = 256;

    // Returns count of distinct sunsequences of str.
    static int countSub(String str)
    {
        // Create an array to store index
        // of last
        int[] last = new int[MAX_CHAR];

        for (int i = 0; i < MAX_CHAR; i++)
            last[i] = -1;

        // Length of input string
        int n = str.Length;

        // dp[i] is going to store count of
        // distinct subsequences of length i.
        int[] dp = new int[n + 1];

        // Empty substring has only one subsequence
        dp[0] = 1;

        // Traverse through all lengths from 1 to n.
        for (int i = 1; i <= n; i++) {
            // Number of subsequences with substring
            // str[0..i-1]
            dp[i] = 2 * dp[i - 1];

            // If current character has appeared
            // before, then remove all subsequences
            // ending with previous occurrence.
            if (last[(int)str[i - 1]] != -1)
                dp[i] = dp[i] - dp[last[(int)str[i - 1]]];

            // Mark occurrence of current character
            last[(int)str[i - 1]] = (i - 1);
        }
        return dp[n];
    }

    // Driver code
    public static void Main(String[] args)
    {
        Console.WriteLine(countSub("gfg"));
    }
}

// This code is contributed 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to count number of
// distinct subsequences of a given string.
let MAX_CHAR = 256;

// Returns count of distinct sunsequences
// of str.
function countSub(str)
{

    // Create an array to store index
    // of last
    let last = new Array(MAX_CHAR);
    last.fill(-1);

    // Length of input string
    let n = str.length;

    // dp[i] is going to store count of distinct
    // subsequences of length i.
    let dp = new Array(n + 1);

    // Empty substring has only one subsequence
    dp[0] = 1;

    // Traverse through all lengths from 1 to n.
    for(let i = 1; i <= n; i++)
    {

        // Number of subsequences with substring
        // str[0..i-1]
        dp[i] = 2 * dp[i - 1];

        // If current character has appeared
        // before, then remove all subsequences
        // ending with previous occurrence.
        if (last[str[i - 1].charCodeAt()] != -1)
            dp[i] = dp[i] - dp[last[str[i - 1].charCodeAt()]];

        // Mark occurrence of current character
        last[str[i - 1].charCodeAt()] = (i - 1);
    }
    return dp[n];
}

// Driver code
document.write(countSub("gfg"));

// This code is contributed by mukesh07

</script>
```

**Output**

```
7
```