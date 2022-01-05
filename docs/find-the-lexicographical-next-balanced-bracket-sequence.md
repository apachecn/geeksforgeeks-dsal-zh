# 找到词典编纂的下一个平衡括号序列

> 原文:[https://www . geeksforgeeks . org/find-the-词典-next-balanced-括号-sequence/](https://www.geeksforgeeks.org/find-the-lexicographical-next-balanced-bracket-sequence/)

给定一个平衡括号序列作为包含字符**(“**或**)“**的字符串**字符串**，任务是找到下一个字典顺序平衡序列(如果可能的话)否则打印 **-1** 。
**举例:**

> **输入:**str =(())”
> **输出:** ()()
> **输入:**str =(())”
> **输出:**(()()))

**方法:**首先找到最右边的左括号，我们可以用一个右括号来代替它，得到字典上较大的括号串。更新后的字符串可能不平衡，我们可以用字典最小的字符串填充字符串的剩余部分:即首先用尽可能多的左括号填充，然后用右括号填充剩余的位置。换句话说，我们试图保持一个尽可能长的前缀不变，而后缀被字典上的最小前缀所取代。
要找到这个位置，可以从右到左迭代字符，保持开括号和闭括号的平衡深度。当我们遇到左括号时，我们会减少深度，当我们遇到右括号时，我们会增加深度。如果我们在某个点遇到一个左括号，并且处理这个符号后的余额为正，那么我们找到了可以改变的最右边的位置。我们改变符号，计算我们必须添加到右侧的左括号和右括号的数量，并以字典最小化的方式排列它们。
如果我们找不到合适的位置，那么这个序列已经是最大可能的序列了，没有答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// next balanced bracket
// expression if possible
string next_balanced_sequence(string& s)
{
    string next = "-1";
    int length = s.size();
    int depth = 0;
    for (int i = length - 1; i >= 0; --i) {

        // Decrement the depth for
        // every opening bracket
        if (s[i] == '(')
            depth--;

        // Increment for the
        // closing brackets
        else
            depth++;

        // Last opening bracket
        if (s[i] == '(' && depth > 0) {
            depth--;
            int open = (length - i - 1 - depth) / 2;
            int close = length - i - 1 - open;

            // Generate the required string
            next = s.substr(0, i) + ')'
                   + string(open, '(')
                   + string(close, ')');
            break;
        }
    }
    return next;
}

// Driver code
int main()
{
    string s = "((()))";

    cout << next_balanced_sequence(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class Sol
{

// makes a string containing char d
// c number of times
static String string(int c, char d)
{
    String s = "";
    for(int i = 0; i < c; i++)
    s += d;

    return s;
}

// Function to find the lexicographically
// next balanced bracket
// expression if possible
static String next_balanced_sequence(String s)
{
    String next = "-1";
    int length = s.length();
    int depth = 0;
    for (int i = length - 1; i >= 0; --i)
    {

        // Decrement the depth for
        // every opening bracket
        if (s.charAt(i) == '(')
            depth--;

        // Increment for the
        // closing brackets
        else
            depth++;

        // Last opening bracket
        if (s.charAt(i) == '(' && depth > 0)
        {
            depth--;
            int open = (length - i - 1 - depth) / 2;
            int close = length - i - 1 - open;

            // Generate the required String
            next = s.substring(0, i) + ')'
                + string(open, '(')
                + string(close, ')');
            break;
        }
    }
    return next;
}

// Driver code
public static void main(String args[])
{
    String s = "((()))";

    System.out.println(next_balanced_sequence(s));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the lexicographically
# next balanced bracket
# expression if possible
def next_balanced_sequence(s) :

    next = "-1";
    length = len(s);
    depth = 0;

    for i in range(length - 1, -1, -1) :

        # Decrement the depth for
        # every opening bracket
        if (s[i] == '(') :
            depth -= 1;

        # Increment for the
        # closing brackets
        else :
            depth += 1;

        # Last opening bracket
        if (s[i] == '(' and depth > 0) :

            depth -= 1;
            open = (length - i - 1 - depth) // 2;
            close = length - i - 1 - open;

            # Generate the required string
            next = s[0 : i] + ')' + open * '(' + close* ')';
            break;

    return next;

# Driver code
if __name__ == "__main__" :

    s = "((()))";

    print(next_balanced_sequence(s));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// makes a string containing char d
// c number of times
static String strings(int c, char d)
{
    String s = "";
    for(int i = 0; i < c; i++)
    s += d;

    return s;
}

// Function to find the lexicographically
// next balanced bracket
// expression if possible
static String next_balanced_sequence(String s)
{
    String next = "-1";
    int length = s.Length;
    int depth = 0;
    for (int i = length - 1; i >= 0; --i)
    {

        // Decrement the depth for
        // every opening bracket
        if (s[i] == '(')
            depth--;

        // Increment for the
        // closing brackets
        else
            depth++;

        // Last opening bracket
        if (s[i] == '(' && depth > 0)
        {
            depth--;
            int open = (length - i - 1 - depth) / 2;
            int close = length - i - 1 - open;

            // Generate the required String
            next = s.Substring(0, i) + ')' +
                        strings(open, '(') +
                        strings(close, ')');
            break;
        }
    }
    return next;
}

// Driver code
public static void Main(String []args)
{
    String s = "((()))";

    Console.WriteLine(next_balanced_sequence(s));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// makes a string containing char d
// c number of times
function string(c, d)
{
    let s = "";
    for(let i = 0; i < c; i++)
    s += d;

    return s;
}

// Function to find the lexicographically
// next balanced bracket
// expression if possible
function next_balanced_sequence(s)
{
    let next = "-1";
    let length = s.length;
    let depth = 0;
    for (let i = length - 1; i >= 0; --i)
    {

        // Decrement the depth for
        // every opening bracket
        if (s[i] == '(')
            depth--;

        // Increment for the
        // closing brackets
        else
            depth++;

        // Last opening bracket
        if (s[i] == '(' && depth > 0)
        {
            depth--;
            let open = (length - i - 1 - depth) / 2;
            let close = length - i - 1 - open;

            // Generate the required String
            next = s.substr(0, i) + ')'
                + string(open, '(')
                + string(close, ')');
            break;
        }
    }
    return next;
}

// Driver Code

    let s = "((()))";

    document.write(next_balanced_sequence(s));

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
(()())
```