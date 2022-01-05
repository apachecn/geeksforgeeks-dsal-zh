# 使用给定的操作

检查一个字符串是否可以转换成其他字符串

> 原文:[https://www . geesforgeks . org/check-if-one-string-can-convert-to-other-use-given-operation/](https://www.geeksforgeeks.org/check-if-one-string-can-be-converted-to-other-using-given-operation/)

给定两根相同长度的弦 **S** 和 **T** 。任务是通过执行以下操作来确定我们是否可以构建一个等于字符串 T 的字符串 A(最初为空)。

1.  删除 **S** 第一个字符，加在 **A** 前面。

2.  删除 **S** 的第一个字符，加在 **A** 后面。

**示例:**

> **输入:** S = "abab" T = "baab"
> **输出:** YES
> **说明:**
> 先在 A 前面加‘A’，再在 A 前面加 A =“A”和 S =“Bab”
> 再在 A 前面加‘b’，再在 A 后面加 A =“ba”和 S =“ab”
> 再在 A 后面加‘A’，再在 A 后面加 A =“baa”和 S =“b”
> 再在 然后 A =“baab”和 S =“
> 这样我们就可以让字符串 A 等于字符串 T
> **输入:**S =“geeks”T =“Teeks”
> **输出:** NO

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决这个问题。
每个角色都有两种可能的招式(前招或后招)。因此，对于每个字符，我们将检查是否有可能在新字符串的前面或后面添加该字符。如果有可能的话，我们会移到下一个角色。如果不可能，那么操作将在该点停止，并打印**否**。

1.  首先，我们将制作一个 2D 布尔数组 **dp[][]** ，其行和列等于字符串 S 的长度，其中 **dp[i][j] = 1** 表示从索引 I 到 n-1 的字符串 S 的所有字符都可以放在新的字符串 A 中，其中 j 向前移动，使其等于字符串 t。

2.  如果我们将第(i-1)个字符作为前移，或者将第(i-1)个字符作为后移，我们可以[从后面遍历字符串 S](https://www.geeksforgeeks.org/print-words-string-reverse-order/)并以两种方式为每个字符更新 dp[][]。

3.  最后，我们将检查第一行的任何值是否等于 1。

下面是上述方法的实现

## C++

```
// C++ implementation of above
// approach
#include <bits/stdc++.h>
using namespace std;

// Function that prints whether
// is it possible to make a
// string equal to T by
// performing given operations
void twoStringsEquality(string s,
                        string t)
{
    int n = s.length();

    vector<vector<int> > dp(
        n, vector<int>(
               n + 1, 0));

    // Base case, if we put the
    // last character at front
    // of A
    if (s[n - 1] == t[0])
        dp[n - 1][1] = 1;

    // Base case, if we put the
    // last character at back
    // of A
    if (s[n - 1] == t[n - 1])
        dp[n - 1][0] = 1;

    for (int i = n - 1; i > 0; i--) {
        for (int j = 0; j <= n - i; j++) {

            // Condition if current
            // sequence is matchable
            if (dp[i][j]) {
                // Condition for front
                // move to (i - 1)th
                // character
                if (s[i - 1] == t[j])
                    dp[i - 1][j + 1] = 1;

                // Condition for back
                // move to (i - 1)th
                // character
                if (s[i - 1] == t[i + j - 1])
                    dp[i - 1][j] = 1;
            }
        }
    }

    bool ans = false;

    for (int i = 0; i <= n; i++) {
        // Condition if it is
        // possible to make
        // string A equal to
        // string T
        if (dp[0][i] == 1) {
            ans = true;
            break;
        }
    }

    // Print final
    // answer
    if (ans == true)
        cout << "Yes"
             << "\n";
    else
        cout << "No"
             << "\n";
}

// Driver Code
int main()
{
    string S = "abab";

    string T = "baab";

    twoStringsEquality(S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above
// approach
import java.util.*;

class GFG{

// Function that prints whether
// is it possible to make a
// String equal to T by
// performing given operations
static void twoStringsEquality(String s,
                               String t)
{
    int n = s.length();

    int [][]dp = new int[n][n + 1];

    // Base case, if we put the
    // last character at front
    // of A
    if (s.charAt(n - 1) == t.charAt(0))
        dp[n - 1][1] = 1;

    // Base case, if we put the
    // last character at back
    // of A
    if (s.charAt(n - 1) == t.charAt(n - 1))
        dp[n - 1][0] = 1;

    for(int i = n - 1; i > 0; i--)
    {
       for(int j = 0; j <= n - i; j++)
       {

          // Condition if current
          // sequence is matchable
          if (dp[i][j] > 0)
          {

              // Condition for front
              // move to (i - 1)th
              // character
              if (s.charAt(i - 1) ==
                  t.charAt(j))
                  dp[i - 1][j + 1] = 1;

              // Condition for back
              // move to (i - 1)th
              // character
              if (s.charAt(i - 1) ==
                  t.charAt(i + j -1))
                  dp[i - 1][j] = 1;
          }
       }
    }

    boolean ans = false;

    for(int i = 0; i <= n; i++)
    {

       // Condition if it is possible
       // to make String A equal to
       // String T
       if (dp[0][i] == 1)
       {
           ans = true;
           break;
       }
    }

    // Print final answer
    if (ans == true)
        System.out.print("Yes" + "\n");
    else
        System.out.print("No" + "\n");
}

// Driver Code
public static void main(String[] args)
{
    String S = "abab";
    String T = "baab";

    twoStringsEquality(S, T);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above
# approach

# Function that prints whether
# is it possible to make a
# equal to T by
# performing given operations
def twoStringsEquality(s, t):
    n = len(s)

    dp = [[0 for i in range(n + 1)]
             for i in range(n)]

    # Base case, if we put the
    # last character at front
    # of A
    if (s[n - 1] == t[0]):
        dp[n - 1][1] = 1

    # Base case, if we put the
    # last character at back
    # of A
    if (s[n - 1] == t[n - 1]):
        dp[n - 1][0] = 1

    for i in range(n - 1, -1, -1):
        for j in range(n - i + 1):

            # Condition if current
            # sequence is matchable
            if (dp[i][j]):

                # Condition for front
                # move to (i - 1)th
                # character
                if (s[i - 1] == t[j]):
                    dp[i - 1][j + 1] = 1

                # Condition for back
                # move to (i - 1)th
                # character
                if (s[i - 1] == t[i + j - 1]):
                    dp[i - 1][j] = 1

    ans = False

    for i in range(n + 1):

        # Condition if it is
        # possible to make
        # A equal to T
        if (dp[0][i] == 1):
            ans = True
            break

    # Print final answer
    if (ans == True):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    S = "abab"
    T = "baab"

    twoStringsEquality(S, T)

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# implementation of above
// approach
using System;
class GFG{

// Function that prints whether
// is it possible to make a
// String equal to T by
// performing given operations
static void twoStringsEquality(String s,
                               String t)
{
    int n = s.Length;

    int [,]dp = new int[n, n + 1];

    // Base case, if we put the
    // last character at front
    // of A
    if (s[n - 1] == t[0])
        dp[n - 1, 1] = 1;

    // Base case, if we put the
    // last character at back
    // of A
    if (s[n - 1] == t[n - 1])
        dp[n - 1, 0] = 1;

    for(int i = n - 1; i > 0; i--)
    {
        for(int j = 0; j <= n - i; j++)
        {

            // Condition if current
            // sequence is matchable
            if (dp[i, j] > 0)
            {

                // Condition for front
                // move to (i - 1)th
                // character
                if (s[i - 1] == t[j])
                    dp[i - 1, j + 1] = 1;

                // Condition for back
                // move to (i - 1)th
                // character
                if (s[i - 1] == t[i + j - 1])
                    dp[i - 1, j] = 1;
            }
        }
    }

    bool ans = false;

    for(int i = 0; i <= n; i++)
    {

        // Condition if it is possible
        // to make String A equal to
        // String T
        if (dp[0, i] == 1)
        {
            ans = true;
            break;
        }
    }

    // Print readonly answer
    if (ans == true)
        Console.Write("Yes" + "\n");
    else
        Console.Write("No" + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    String S = "abab";
    String T = "baab";

    twoStringsEquality(S, T);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of above
// approach

// Function that prints whether
// is it possible to make a
// string equal to T by
// performing given operations
function twoStringsEquality(s, t)
{
    var n = s.length;

    var dp = Array.from(Array(n), ()=>Array(n+1).fill(0));

    // Base case, if we put the
    // last character at front
    // of A
    if (s[n - 1] == t[0])
        dp[n - 1][1] = 1;

    // Base case, if we put the
    // last character at back
    // of A
    if (s[n - 1] == t[n - 1])
        dp[n - 1][0] = 1;

    for (var i = n - 1; i > 0; i--) {
        for (var j = 0; j <= n - i; j++) {

            // Condition if current
            // sequence is matchable
            if (dp[i][j]) {
                // Condition for front
                // move to (i - 1)th
                // character
                if (s[i - 1] == t[j])
                    dp[i - 1][j + 1] = 1;

                // Condition for back
                // move to (i - 1)th
                // character
                if (s[i - 1] == t[i + j - 1])
                    dp[i - 1][j] = 1;
            }
        }
    }

    var ans = false;

    for (var i = 0; i <= n; i++) {
        // Condition if it is
        // possible to make
        // string A equal to
        // string T
        if (dp[0][i] == 1) {
            ans = true;
            break;
        }
    }

    // Print final
    // answer
    if (ans == true)
        document.write( "Yes" + "<br>");
    else
        document.write( "No" + "<br>");
}

// Driver Code
var S = "abab";
var T = "baab";
twoStringsEquality(S, T);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N <sup>2</sup> )