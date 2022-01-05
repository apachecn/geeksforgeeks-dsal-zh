# 一个字符串可以构成的平衡括号表达式的数量

> 原文:[https://www . geesforgeks . org/number-of-balanced-括号-expressions-可由字符串构成/](https://www.geeksforgeeks.org/number-of-balanced-bracket-expressions-that-can-be-formed-from-a-string/)

给定由字符 **(** 、 **)** 、 **{** 、 **}** 、 **[** 、 **]** 和**组成的字符串**字符串**？**。任务是找到**时形成的平衡括号表达式总数？**可以用任何括号字符替换。
下面是一些平衡括号表达式的例子: **{([])}** ， **{()}[{}]** 等。
和，不平衡括号表达式: **{[}** ， **{()]** ， **{()}[)** 等。

**示例:**

> **输入:** str =(？([?)]?}?"
> **输出:** 3
> ({([()]]})、()([()]{})和([([])]{})是唯一可以从输入生成的平衡表达式。
> 
> **输入:** str =？？？[?？？？？？？]?？？?"
> T3】产量: 392202

**进场:**

1.  如果 **n** 为**奇数，**则结果始终为 **0** ，因为不可能有平衡的表达式。
2.  如果 **n** id **偶数，**则创建一个 **dp** 数组来存储预计算。
3.  使用以下操作调用递归函数:
    *   如果**起始指数>结束指数**那么你返回 **1** 。
    *   如果已经计算出 **dp【开始】【结束】**，则返回 **dp【开始】【结束】**。
    *   从**开始+ 1** 直到**结束**运行一个循环，递增 **2** 找到其配对括号或“？”。
    *   然后将字符串分成两半，通过调用递归函数检查从 **start + 1** 到**I–1**和 **i + 1** 到结束的正确后续括号表达式。
    *   如果 **st[start] = '？'**和 **st[i] = '？'**则总共可以形成括号对的 **3** 组合，从而将递归函数的结果乘以 **3** 。
4.  返回 DP[开始][结束]

下面是上述方法的实现:

## C++

```
// C++ program to find number of balanced
// bracket expressions possible
#include <bits/stdc++.h>
using namespace std;
typedef long long int lli;

// Max string length
const int MAX = 300;

// Function to check whether index start
// and end can form a bracket pair or not
int checkFunc(int i, int j, string st)
{
    // Check for brackets ( )
    if (st[i] == '(' && st[j] == ')')
        return 1;
    if (st[i] == '(' && st[j] == '?')
        return 1;
    if (st[i] == '?' && st[j] == ')')
        return 1;

    // Check for brackets [ ]
    if (st[i] == '[' && st[j] == ']')
        return 1;
    if (st[i] == '[' && st[j] == '?')
        return 1;
    if (st[i] == '?' && st[j] == ']')
        return 1;

    // Check for brackets { }
    if (st[i] == '{' && st[j] == '}')
        return 1;
    if (st[i] == '{' && st[j] == '?')
        return 1;
    if (st[i] == '?' && st[j] == '}')
        return 1;

    return 0;
}

// Function to find number of
// proper bracket expressions
int countRec(int start, int end, int dp[][MAX],
             string st)
{
    int sum = 0;

    // If starting index is greater
    // than ending index
    if (start > end)
        return 1;

    // If dp[start][end] has already been computed
    if (dp[start][end] != -1)
        return dp[start][end];

    lli i, r = 0;

    // Search for the bracket in from next index
    for (i = start + 1; i <= end; i += 2) {

        // If bracket pair is formed,
        // add number of combination
        if (checkFunc(start, i, st)) {

            sum = sum
                  + countRec(start + 1, i - 1, dp, st)
                        * countRec(i + 1, end, dp, st);
        }

        // If ? comes then all three bracket
        // expressions are possible
        else if (st[start] == '?' && st[i] == '?') {

            sum = sum
                  + countRec(start + 1, i - 1, dp, st)
                        * countRec(i + 1, end, dp, st)
                        * 3;
        }
    }

    // Return answer
    return dp[start][end] = sum;
}

int countWays(string st)
{
    int n = st.length();

    // If n is odd, string cannot be balanced
    if (n % 2 == 1)
        return 0;
    int dp[MAX][MAX];
    memset(dp, -1, sizeof(dp));
    return countRec(0, n - 1, dp, st);
}

// Driving function
int main()
{
    string st = "(?([?)]?}?";
    cout << countWays(st);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of balanced
// bracket expressions possible

class GFG {
    // Max string length
    static int MAX = 300;

    // Function to check whether index start
    // and end can form a bracket pair or not
    static int checkFunc(int i, int j, String st)
    {
        // Check for brackets ( )
        if (st.charAt(i) == '(' && st.charAt(j) == ')')
            return 1;
        if (st.charAt(i) == '(' && st.charAt(j) == '?')
            return 1;
        if (st.charAt(i) == '?' && st.charAt(j) == ')')
            return 1;

        // Check for brackets [ ]
        if (st.charAt(i) == '[' && st.charAt(j) == ']')
            return 1;
        if (st.charAt(i) == '[' && st.charAt(j) == '?')
            return 1;
        if (st.charAt(i) == '?' && st.charAt(j) == ']')
            return 1;

        // Check for brackets { }
        if (st.charAt(i) == '{' && st.charAt(j) == '}')
            return 1;
        if (st.charAt(i) == '{' && st.charAt(j) == '?')
            return 1;
        if (st.charAt(i) == '?' && st.charAt(j) == '}')
            return 1;

        return 0;
    }

    // Function to find number of
    // proper bracket expressions
    static int countRec(int start, int end, int dp[][],
                        String st)
    {
        int sum = 0;

        // If starting index is greater
        // than ending index
        if (start > end)
            return 1;

        // If dp[start][end] has already been computed
        if (dp[start][end] != -1)
            return dp[start][end];

        int i, r = 0;

        // Search for the bracket in from next index
        for (i = start + 1; i <= end; i += 2) {

            // If bracket pair is formed,
            // add number of combination
            if (checkFunc(start, i, st) == 1) {

                sum = sum
                      + countRec(start + 1, i - 1, dp, st)
                            * countRec(i + 1, end, dp, st);
            }

            // If ? comes then all three bracket
            // expressions are possible
            else if (st.charAt(start) == '?' && st.charAt(i) == '?') {

                sum = sum
                      + countRec(start + 1, i - 1, dp, st)
                            * countRec(i + 1, end, dp, st)
                            * 3;
            }
        }

        // Return answer
        return dp[start][end] = sum;
    }

    static int countWays(String st)
    {
        int n = st.length();

        // If n is odd, string cannot be balanced
        if (n % 2 == 1)
            return 0;

        int dp[][] = new int[MAX][MAX];

        for (int i = 0; i < MAX; i++)
            for (int j = 0; j < MAX; j++)
                dp[i][j] = -1;

        return countRec(0, n - 1, dp, st);
    }

    // Driving function
    public static void main(String[] args)
    {

        String st = "(?([?)]?}?";
        System.out.println(countWays(st));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 program to find number of balanced
# bracket expressions possible

# Max string length
MAX = 300

# Function to check whether index start
# and end can form a bracket pair or not
def checkFunc(i, j, st):

    # Check for brackets ( )
    if (st[i] == '(' and st[j] == ')'):
        return 1
    if (st[i] == '(' and st[j] == '?'):
        return 1
    if (st[i] == '?' and st[j] == ')'):
        return 1

    # Check for brackets [ ]
    if (st[i] == '[' and st[j] == ']'):
        return 1
    if (st[i] == '[' and st[j] == '?'):
        return 1
    if (st[i] == '?' and st[j] == ']'):
        return 1

    # Check for brackets { }
    if (st[i] == '{' and st[j] == '}'):
        return 1
    if (st[i] == '{' and st[j] == '?'):
        return 1
    if (st[i] == '?' and st[j] == '}'):
        return 1

    return 0

# Function to find number of
# proper bracket expressions
def countRec(start, end, dp, st):

    sum = 0

    # If starting index is greater
    # than ending index
    if (start > end):
        return 1

    # If dp[start][end] has already
    # been computed
    if (dp[start][end] != -1):
        return dp[start][end]

    r = 0

    # Search for the bracket in from next index
    for i in range(start + 1, end + 1, 2):

        # If bracket pair is formed,
        # add number of combination
        if (checkFunc(start, i, st)):

            sum = (sum + countRec(start + 1, i - 1, dp, st) *
                         countRec(i + 1, end, dp, st))

        # If ? comes then all three bracket
        # expressions are possible
        elif (st[start] == '?' and st[i] == '?'):

            sum = (sum + countRec(start + 1, i - 1, dp, st) *
                         countRec(i + 1, end, dp, st) * 3)

    # Return answer
    dp[start][end] = sum
    return dp[start][end]

def countWays( st):

    n = len(st)

    # If n is odd, string cannot be balanced
    if (n % 2 == 1):
        return 0
    dp = [[-1 for i in range(MAX)]
              for i in range(MAX)]
    return countRec(0, n - 1, dp, st)

# Driver Code
if __name__ =="__main__":

    st = "(?([?)]?}?"
    print(countWays(st))

# This code is contributed by ita_c
```

## C#

```
// C# program to find number of balanced
// bracket expressions possible

using System;
class GFG {
    // Max string length
    static int MAX = 300;

    // Function to check whether index start
    // and end can form a bracket pair or not
    static int checkFunc(int i, int j, string st)
    {
        // Check for brackets ( )
        if (st[i] == '(' && st[j] == ')')
            return 1;
        if (st[i] == '(' && st[j] == '?')
            return 1;
        if (st[i] == '?' && st[j] == ')')
            return 1;

        // Check for brackets [ ]
        if (st[i] == '[' && st[j] == ']')
            return 1;
        if (st[i] == '[' && st[j] == '?')
            return 1;
        if (st[i] == '?' && st[j] == ']')
            return 1;

        // Check for brackets { }
        if (st[i] == '{' && st[j] == '}')
            return 1;
        if (st[i] == '{' && st[j] == '?')
            return 1;
        if (st[i] == '?' && st[j] == '}')
            return 1;

        return 0;
    }

    // Function to find number of
    // proper bracket expressions
    static int countRec(int start, int end, int[, ] dp,
                        string st)
    {
        int sum = 0;

        // If starting index is greater
        // than ending index
        if (start > end)
            return 1;

        // If dp[start, end] has already been computed
        if (dp[start, end] != -1)
            return dp[start, end];

        int i;

        // Search for the bracket in from next index
        for (i = start + 1; i <= end; i += 2) {

            // If bracket pair is formed,
            // add number of combination
            if (checkFunc(start, i, st) == 1) {

                sum = sum
                      + countRec(start + 1, i - 1, dp, st)
                            * countRec(i + 1, end, dp, st);
            }

            // If ? comes then all three bracket
            // expressions are possible
            else if (st[start] == '?' && st[i] == '?') {

                sum = sum
                      + countRec(start + 1, i - 1, dp, st)
                            * countRec(i + 1, end, dp, st)
                            * 3;
            }
        }

        // Return answer
        return dp[start, end] = sum;
    }

    static int countWays(string st)
    {
        int n = st.Length;

        // If n is odd, string cannot be balanced
        if (n % 2 == 1)
            return 0;

        int[, ] dp = new int[MAX, MAX];

        for (int i = 0; i < MAX; i++)
            for (int j = 0; j < MAX; j++)
                dp[i, j] = -1;

        return countRec(0, n - 1, dp, st);
    }

    // Driving function
    public static void Main()
    {

        string st = "(?([?)]?}?";
        Console.WriteLine(countWays(st));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
// Javascript program to find number of balanced
// bracket expressions possible

    // Max string length
    let MAX = 300;
    // Function to check whether index start
    // and end can form a bracket pair or not
    function checkFunc(i,j,st)
    {
        // Check for brackets ( )
        if (st[i] == '(' && st[j] == ')')
            return 1;
        if (st[i] == '(' && st[j] == '?')
            return 1;
        if (st[i] == '?' && st[j] == ')')
            return 1;

        // Check for brackets [ ]
        if (st[i] == '[' && st[j] == ']')
            return 1;
        if (st[i] == '[' && st[j] == '?')
            return 1;
        if (st[i] == '?' && st[j] == ']')
            return 1;

        // Check for brackets { }
        if (st[i] == '{' && st[j] == '}')
            return 1;
        if (st[i] == '{' && st[j] == '?')
            return 1;
        if (st[i] == '?' && st[j] == '}')
            return 1;

        return 0;
    }

    // Function to find number of
    // proper bracket expressions
    function countRec(start,end,dp,st)
    {
        let sum = 0;

        // If starting index is greater
        // than ending index
        if (start > end)
            return 1;

        // If dp[start][end] has already been computed
        if (dp[start][end] != -1)
            return dp[start][end];

        let i, r = 0;

        // Search for the bracket in from next index
        for (i = start + 1; i <= end; i += 2) {

            // If bracket pair is formed,
            // add number of combination
            if (checkFunc(start, i, st) == 1) {

                sum = sum
                      + countRec(start + 1, i - 1, dp, st)
                            * countRec(i + 1, end, dp, st);
            }

            // If ? comes then all three bracket
            // expressions are possible
            else if (st[start] == '?' && st[i] == '?') {

                sum = sum
                      + countRec(start + 1, i - 1, dp, st)
                            * countRec(i + 1, end, dp, st)
                            * 3;
            }
        }

        // Return answer
        return dp[start][end] = sum;
    }

    function countWays(st)
    {
        let n = st.length;

        // If n is odd, string cannot be balanced
        if (n % 2 == 1)
            return 0;

        let dp = new Array(MAX);

        for (let i = 0; i < MAX; i++)
        {   
            dp[i]=new Array(MAX);
            for (let j = 0; j < MAX; j++)
                dp[i][j] = -1;
          }
        return countRec(0, n - 1, dp, st);
    }

    // Driving function
    let st = "(?([?)]?}?";
    document.write(countWays(st));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
3
```