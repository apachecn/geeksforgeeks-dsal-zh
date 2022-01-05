# 打印去掉最外面括号后得到的字符串

> 原文:[https://www . geeksforgeeks . org/print-去除最外面括号后获得的字符串/](https://www.geeksforgeeks.org/print-the-string-obtained-after-removal-of-outermost-parentheses/)

给定一个由小写字母、左括号和右括号组成的[有效括号字符串](https://www.geeksforgeeks.org/check-if-given-parentheses-expression-is-balanced-or-not/) **字符串**，任务是通过移除最外面的括号来找到该字符串，从而使该字符串保持为有效的括号字符串。

**示例:**

> **输入:**S =(((a)(BCD)(e)))”
> **输出:** (a)(bcd)(e)
> **解释:**
> 最外面的括括号是:{ S[0]，S[1]，S[13]，S[14] }。
> 去掉 str 中最外面的方括号将 str 改为“(a)(bcd)(e)”。
> 因此，要求的输出是(a)(bcd)(e)。
> 
> **输入:**str =((ab)(BC))d "
> **输出:** ((ab)(bc))d
> **解释:**
> 因为字符串中不存在最外面的包围括号。因此，所需的输出是((ab)(bc))d

**方法:**思路是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，分别统计字符串两端连续的左括号和右括号的个数。然后，[遍历出现在内部字符串中的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并计算平衡字符串所需的左括号的数量。按照以下步骤解决问题:

按照以下步骤解决问题:

*   初始化一个变量，比如 **cnt = 0** ，以存储有效括号的计数，使得 **str[cnt] == '('** 和**str[N–CNT–1]= ')'**。
*   要用外括号平衡字符串的内括号，遍历[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **{str[cnt]，…，str[N–CNT–1]}**，计算平衡内子串所需的最小左括号或右括号，比如说 **cntMinpar** 。
*   最后，更新 **cnt += cntMinPair** 并打印子字符串 **{ str[cnt]，…，str[N–CNT]}**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove outermost
// enclosing brackets from both end
void removeBrakets(string str)
{

    // Stores length of the string
    int n = str.length();

    // Stores count of parenthesis such
    // that str[cnt] == cnt[N - cnt - 1]
    int cnt = 0;

    // Calculating maximum number of
    // bracket pair from the end side
    while (cnt < n && str[cnt] == '(' &&
              str[n - cnt - 1] == ')')
    {

        // Update cnt
        cnt++;
    }

    // Stores minimum outer parenthesis
    // required to balance the substring
    // { str[cnt], ..., [n - cnt -1]
    int error = 0;

    // Stores count of unbalanced parenthesis
    // in { str[cnt], ..., [n - cnt -1]
    int open = 0;

    // Traverse the substring
    // { str[cnt], ..., [n - cnt -1]
    for(int i = cnt; i < n - cnt; i++)
    {

        // If current character is '('
        if (str[i] == '(')
        {

            // Update cntUnbal
            open++;
        }

        // Decrease num, if the current
        // character is ')'
        else if (str[i] == ')')
        {

            // Update cntUnbal
            if(open>0){
              open--;
            }
              else{
              error++;
            }
        }
    }

    int rem=cnt-error;

    // Print resultant string
    cout << str.substr(rem, n - 2*rem) << endl;    
}

// Driver Code
int main()
{

    // Input string
    string str = "((((a)b)(c)))";
    removeBrakets(str);

    return 0;
}

// This code is contributed by susmitakundugoaldanga
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;
import java.lang.*;
class GFG {

    // Function to remove outermost
    // enclosing brackets from both end
    static void removeBrakets(String str)
    {
        // Stores length of the string
        int n = str.length();

        // Stores count of parenthesis such
        // that str[cnt] == cnt[N - cnt - 1]
        int cnt = 0;

        // Calculating maximum number of
        // bracket pair from the end side
        while (cnt < n && str.charAt(cnt) == '('
               && str.charAt(n - cnt - 1) == ')') {

            // Update cnt
            cnt++;
        }

        // Stores minimum outer parenthesis
        // required to balance the substring
        // { str[cnt], ..., [n - cnt -1]
        int cntMinPar = 0;

        // Stores count of unbalanced parenthesis
        // in { str[cnt], ..., [n - cnt -1]
        int cntUnbal = 0;

        // Traverse the substring
        // { str[cnt], ..., [n - cnt -1]
        for (int i = cnt; i < n - cnt;
             i++) {

            // If current character is '('
            if (str.charAt(i) == '(') {

                // Update cntUnbal
                cntUnbal++;
            }

            // Decrease num, if the current
            // character is ')'
            else if (str.charAt(i) == ')') {

                // Update cntUnbal
                cntUnbal--;
            }

            // Update cntMinPar
            cntMinPar = Math.min(
                cntMinPar, cntUnbal);
        }

        // Update cnt
        cnt += cntMinPar;

        // Print resultant string
        System.out.println(
            str.substring(cnt, n - cnt));
    }

    // Driver Code
    public static void main(
        String[] args)
    {
        // Input string
        String str = "((((a)b)(c)))";
        removeBrakets(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to remove outermost
# enclosing brackets from both end
def removeBrakets(str):

    # Stores length of the string
    n = len(str)

    # Stores count of parenthesis such
    # that str[cnt] == cnt[N - cnt - 1]
    cnt = 0

    # Calculating maximum number of
    # bracket pair from the end side
    while (cnt < n and str[cnt] == '(' and
               str[n - cnt - 1] == ')'):

        # Update cnt
        cnt += 1

    # Stores minimum outer parenthesis
    # required to balance the substring
    # { str[cnt], ..., [n - cnt -1]
    cntMinPar = 0

    # Stores count of unbalanced parenthesis
    # in { str[cnt], ..., [n - cnt -1]
    cntUnbal = 0

    # Traverse the substring
    # { str[cnt], ..., [n - cnt -1]
    for i in range(cnt, n - cnt):

        # If current character is '('
        if (str[i] == '('):

            # Update cntUnbal
            cntUnbal += 1

        # Decrease num, if the current
        # character is ')'
        elif str[i] == ')':

            # Update cntUnbal
            cntUnbal -= 1

        # Update cntMinPar
        cntMinPar = min(cntMinPar,
                        cntUnbal)

    # Update cnt
    cnt += cntMinPar

    # Print resultant string
    print(str[cnt: n - cnt])

# Driver Code
if __name__ == '__main__':

    # Input string
    str = "((((a)b)(c)))"

    removeBrakets(str)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG {

    // Function to remove outermost
    // enclosing brackets from both end
    static void removeBrakets(String str)
    {
        // Stores length of the string
        int n = str.Length;

        // Stores count of parenthesis such
        // that str[cnt] == cnt[N - cnt - 1]
        int cnt = 0;

        // Calculating maximum number of
        // bracket pair from the end side
        while (cnt < n && str[cnt] == '('
               && str[n - cnt - 1] == ')')
        {

            // Update cnt
            cnt++;
        }

        // Stores minimum outer parenthesis
        // required to balance the substring
        // { str[cnt], ..., [n - cnt -1]
        int cntMinPar = 0;

        // Stores count of unbalanced parenthesis
        // in { str[cnt], ..., [n - cnt -1]
        int cntUnbal = 0;

        // Traverse the substring
        // { str[cnt], ..., [n - cnt -1]
        for (int i = cnt; i < n - cnt;
             i++)
        {

            // If current character is '('
            if (str[i] == '(')
            {

                // Update cntUnbal
                cntUnbal++;
            }

            // Decrease num, if the current
            // character is ')'
            else if (str[i] == ')')
            {

                // Update cntUnbal
                cntUnbal--;
            }

            // Update cntMinPar
            cntMinPar = Math.Min(
                cntMinPar, cntUnbal);
        }

        // Update cnt
        cnt += cntMinPar;

        // Print resultant string
        Console.WriteLine(
            str.Substring(cnt, n - cnt - 2));
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // Input string
        string str = "((((a)b)(c)))";
        removeBrakets(str);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to remove outermost
// enclosing brackets from both end
function removeBrakets(str)
{

    // Stores length of the string
    var n = str.length;

    // Stores count of parenthesis such
    // that str[cnt] == cnt[N - cnt - 1]
    var cnt = 0;

    // Calculating maximum number of
    // bracket pair from the end side
    while (cnt < n && str[cnt] == '(' &&
              str[n - cnt - 1] == ')')
    {

        // Update cnt
        cnt++;
    }

    // Stores minimum outer parenthesis
    // required to balance the substring
    // { str[cnt], ..., [n - cnt -1]
    var error = 0;

    // Stores count of unbalanced parenthesis
    // in { str[cnt], ..., [n - cnt -1]
    var open = 0;

    // Traverse the substring
    // { str[cnt], ..., [n - cnt -1]
    for(var i = cnt; i < n - cnt; i++)
    {

        // If current character is '('
        if (str[i] == '(')
        {

            // Update cntUnbal
            open++;
        }

        // Decrease num, if the current
        // character is ')'
        else if (str[i] == ')')
        {

            // Update cntUnbal
            if (open > 0)
            {
              open--;
            }
            else
            {
                error++;
            }
        }
    }
    var rem = cnt - error;

    // Print resultant string
    document.write(str.substring(
        rem, rem + n - 2 * rem));
}

// Driver Code

// Input string
var str = "((((a)b)(c)))";
removeBrakets(str);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
((a)b)(c)
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*