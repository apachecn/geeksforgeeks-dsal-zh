# 检查支架顺序是否可以通过最多一次支架位置变化来平衡

> 原文:[https://www . geeksforgeeks . org/check-if-the-bracket-sequence-can-balanced-in-at-one-change-in-a-bracket/](https://www.geeksforgeeks.org/check-if-the-bracket-sequence-can-be-balanced-with-at-most-one-change-in-the-position-of-a-bracket/)

给定一个不平衡的括号序列作为字符串 **str** ，任务是找出给定的字符串是否可以通过最多将一个括号从序列中的原始位置移动到任何其他位置来平衡。
**例:**

> **输入:**str =(()”
> **输出:**是
> As 通过将 s[0]移动到最后将使其有效。
> "()"
> **输入:**str = "())(()"
> **输出:**否

**方法:**考虑 **X** 作为有效括号，那么肯定 **(X)** 也是有效的。如果 **X** 无效，并且只需在某个支架中改变一次位置就可以平衡，那么它必须是类型**X =(“**”，其中**)“**已经放在了**(“**)之前。
现在 **X** 可以换成 **(X)** ，因为不会影响 **X** 的平衡性质。新弦变成平衡的**X =“()”**。
因此，如果 **(X)** 是平衡的，那么我们可以说 **X** 最多只需要改变一个支架的位置就可以平衡。
以下是上述方法的实施:

## C++

```
// CPP implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the sequence
// can be balanced by changing the
// position of at most one bracket
bool canBeBalanced(string s, int n)
{
    // Odd length string can
    // never be balanced
    if (n % 2 == 1)
        return false;

    // Add '(' in the beginning and ')'
    // in the end of the string
    string k = "(";
    k += s + ")";

    vector<string> d;
    int cnt = 0;

    for (int i = 0; i < k.length(); i++)
    {
        // If its an opening bracket then
        // append it to the temp string
        if (k[i] == '(')
            d.push_back("(");

        // If its a closing bracket
        else
        {
            // There was an opening bracket
            // to match it with
            if (d.size() != 0)
                d.pop_back();

            // No opening bracket to
            // match it with
            else
                return false;
        }
    }

    // Sequence is balanced
    if (d.empty())
        return true;
    return false;
}

// Driver Code
int main(int argc, char const *argv[])
{
    string s = ")(()";
    int n = s.length();

    (canBeBalanced(s, n)) ? cout << "Yes"
                  << endl : cout << "No" << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Vector;

class GFG
{

    // Function that returns true if the sequence
    // can be balanced by changing the
    // position of at most one bracket
    static boolean canBeBalanced(String s, int n)
    {

        // Odd length string can
        // never be balanced
        if (n % 2 == 1)
            return false;

        // Add '(' in the beginning and ')'
        // in the end of the string
        String k = "(";
        k += s + ")";
        Vector<String> d = new Vector<>();

        for (int i = 0; i < k.length(); i++)
        {

            // If its an opening bracket then
            // append it to the temp string
            if (k.charAt(i) == '(')
                d.add("(");

            // If its a closing bracket
            else
            {

                // There was an opening bracket
                // to match it with
                if (d.size() != 0)
                    d.remove(d.size() - 1);

                // No opening bracket to
                // match it with
                else
                    return false;
            }
        }

        // Sequence is balanced
        if (d.isEmpty())
            return true;
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = ")(()";
        int n = s.length();

        if (canBeBalanced(s, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the sequence
# can be balanced by changing the
# position of at most one bracket
def canBeBalanced(s, n):

    # Odd length string can
    # never be balanced
    if n % 2 == 1:
        return False

    # Add '(' in the beginning and ')'
    # in the end of the string
    k = "("
    k = k + s+")"
    d = []
    count = 0
    for i in range(len(k)):

        # If its an opening bracket then
        # append it to the temp string
        if k[i] == "(":
            d.append("(")

        # If its a closing bracket
        else:

            # There was an opening bracket
            # to match it with
            if len(d)!= 0:
                d.pop()

            # No opening bracket to
            # match it with
            else:
                return False

    # Sequence is balanced
    if len(d) == 0:
        return True
    return False

# Driver code
S = ")(()"
n = len(S)
if(canBeBalanced(S, n)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function that returns true if the sequence
    // can be balanced by changing the
    // position of at most one bracket
    static bool canBeBalanced(string s, int n)
    {

        // Odd length string can
        // never be balanced
        if (n % 2 == 1)
            return false;

        // Add '(' in the beginning and ')'
        // in the end of the string
        string k = "(";
        k += s + ")";
        List<string> d = new List<string>();

        for (int i = 0; i < k.Length; i++)
        {

            // If its an opening bracket then
            // append it to the temp string
            if (k[i] == '(')
                d.Add("(");

            // If its a closing bracket
            else
            {

                // There was an opening bracket
                // to match it with
                if (d.Count != 0)
                    d.RemoveAt(d.Count - 1);

                // No opening bracket to
                // match it with
                else
                    return false;
            }
        }

        // Sequence is balanced
        if (d.Count == 0)
            return true;
        return false;
    }

    // Driver Code
    public static void Main()
    {
        string s = ")(()";
        int n = s.Length;

        if (canBeBalanced(s, n))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by
// mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if the sequence
    // can be balanced by changing the
    // position of at most one bracket
function canBeBalanced(s,n)
{
    // Odd length string can
        // never be balanced
        if (n % 2 == 1)
            return false;

        // Add '(' in the beginning and ')'
        // in the end of the string
        let k = "(";
        k += s + ")";
        let d = [];

        for (let i = 0; i < k.length; i++)
        {

            // If its an opening bracket then
            // append it to the temp string
            if (k[i] == '(')
                d.push("(");

            // If its a closing bracket
            else
            {

                // There was an opening bracket
                // to match it with
                if (d.length != 0)
                    d.pop();

                // No opening bracket to
                // match it with
                else
                    return false;
            }
        }

        // Sequence is balanced
        if (d.length==0)
            return true;
        return false;
}

// Driver Code
let s = ")(()";
        let n = s.length;

        if (canBeBalanced(s, n))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```