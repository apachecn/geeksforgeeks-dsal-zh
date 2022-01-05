# 检查字符串是否遵循模式定义的字符顺序|设置 3

> 原文:[https://www . geesforgeks . org/check-if-string-follow-order-of-characters-by-pattern-or-not-set-3/](https://www.geeksforgeeks.org/check-if-string-follows-order-of-characters-defined-by-a-pattern-or-not-set-3/)

给定输入字符串和模式，检查输入字符串中的字符是否遵循由模式中的字符确定的相同顺序。假设模式中没有任何重复的字符。
**例:**

```
Input: string = "engineers rock", pattern = "er";
Output: true
All 'e' in the input string are before all 'r'.

Input: string = "engineers rock", pattern = "egr";
Output: false
There are two 'e' after 'g' in the input string.

Input: string = "engineers rock", pattern = "gsr";
Output: false
There are one 'r' before 's' in the input string.
```

我们已经讨论了解决这个问题的两种方法。
[检查字符串是否遵循模式定义的字符顺序|设置 1](https://www.geeksforgeeks.org/check-string-follows-order-characters-defined-pattern-not/)
[检查字符串是否遵循模式定义的字符顺序|设置 2](https://www.geeksforgeeks.org/check-if-string-follows-order-of-characters-defined-by-a-pattern-or-not-set-2/)

在这种方法中，我们首先给模式的字符分配一个标签(或顺序)。标签按递增顺序分配。
例如，图案“gsr”标记如下

```
"g" => 1
"s" => 2
"r" => 3
```

意思是‘g’会先出现，然后是‘s’，然后是‘r’
给模式字符分配标签后，我们遍历字符串。遍历时，我们跟踪最后访问的字符的标签(或顺序)。如果当前字符的标签小于前一个字符，我们返回 false。否则我们更新最后一个标签。如果所有字符都遵循顺序，我们返回 true。
以下是实施情况

## C++

```
// C++ program to find if a string follows order
// defined by a given pattern.
#include <bits/stdc++.h>
using namespace std;

const int CHAR_SIZE = 256;

// Returns true if characters of str follow
// order defined by a given ptr.
bool checkPattern(string str, string pat)
{
    // Initialize all orders as -1
    vector<int> label(CHAR_SIZE, -1);

    // Assign an order to pattern characters
    // according to their appearance in pattern
    int order = 1;
    for (int i = 0; i < pat.length() ; i++)
    {
        // give the pattern characters order
        label[pat[i]] = order;

        // increment the order
        order++;
    }

    //  Now one by check if string characters
    // follow above order
    int last_order = -1;
    for (int i = 0; i < str.length(); i++)
    {
        if (label[str[i]] != -1)
        {
            // If order of this character is less
            // than order of previous, return false.
            if (label[str[i]] < last_order)
                return false;

            // Update last_order for next iteration
            last_order =  label[str[i]];
        }
    }

    // return that str followed pat
    return true;
}

// Driver code
int main()
{
    string str = "engineers rock";
    string pattern = "gsr";

    cout << boolalpha << checkPattern(str, pattern);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a string follows order
// defined by a given pattern.
class GFG
{
    static int CHAR_SIZE = 256;

    // Returns true if characters of str follow
    // order defined by a given ptr.
    static boolean checkPattern(String str,
                                String pat)
    {
        int[] label = new int[CHAR_SIZE];

        // Initialize all orders as -1
        for (int i = 0; i < CHAR_SIZE; i++)
            label[i] = -1;

        // Assign an order to pattern characters
        // according to their appearance in pattern
        int order = 1;
        for (int i = 0; i < pat.length(); i++)
        {

            // give the pattern characters order
            label[pat.charAt(i)] = order;

            // increment the order
            order++;
        }

        // Now one by check if string characters
        // follow above order
        int last_order = -1;
        for (int i = 0; i < str.length(); i++)
        {
            if (label[str.charAt(i)] != -1)
            {

                // If order of this character is less
                // than order of previous, return false.
                if (label[str.charAt(i)] < last_order)
                    return false;

                // Update last_order for next iteration
                last_order = label[str.charAt(i)];
            }
        }

        // return that str followed pat
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "engineers rock";
        String pattern = "gsr";
        System.out.println(checkPattern(str, pattern));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find if a string follows
# order defined by a given pattern
CHAR_SIZE = 256

# Returns true if characters of str follow
# order defined by a given ptr.
def checkPattern(Str, pat):

    # Initialize all orders as -1
    label = [-1] * CHAR_SIZE

    # Assign an order to pattern characters
    # according to their appearance in pattern
    order = 1

    for i in range(len(pat)):

        # Give the pattern characters order
        label[ord(pat[i])] = order

        # Increment the order
        order += 1

    # Now one by one check if string
    # characters follow above order
    last_order = -1

    for i in range(len(Str)):
        if (label[ord(Str[i])] != -1):

            # If order of this character is less
            # than order of previous, return false
            if (label[ord(Str[i])] < last_order):
                return False

            # Update last_order for next iteration
            last_order = label[ord(Str[i])]

    # return that str followed pat
    return True

# Driver Code
if __name__ == '__main__':

    Str = "engineers rock"
    pattern = "gsr"

    print(checkPattern(Str, pattern))

# This code is contributed by himanshu77
```

## C#

```
// C# program to find if a string follows order
// defined by a given pattern.
using System;

class GFG
{
    static int CHAR_SIZE = 256;

    // Returns true if characters of str follow
    // order defined by a given ptr.
    static bool checkPattern(String str,
                                String pat)
    {
        int[] label = new int[CHAR_SIZE];

        // Initialize all orders as -1
        for (int i = 0; i < CHAR_SIZE; i++)
            label[i] = -1;

        // Assign an order to pattern characters
        // according to their appearance in pattern
        int order = 1;
        for (int i = 0; i < pat.Length; i++)
        {

            // give the pattern characters order
            label[pat[i]] = order;

            // increment the order
            order++;
        }

        // Now one by check if string characters
        // follow above order
        int last_order = -1;
        for (int i = 0; i < str.Length; i++)
        {
            if (label[str[i]] != -1)
            {

                // If order of this character is less
                // than order of previous, return false.
                if (label[str[i]] < last_order)
                    return false;

                // Update last_order for next iteration
                last_order = label[str[i]];
            }
        }

        // return that str followed pat
        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "engineers rock";
        String pattern = "gsr";
        Console.WriteLine(checkPattern(str, pattern));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find if a string follows order
// defined by a given pattern.

let CHAR_SIZE = 256;

 // Returns true if characters of str follow
    // order defined by a given ptr.
function checkPattern(str,pat)
{
    let label = new Array(CHAR_SIZE);

        // Initialize all orders as -1
        for (let i = 0; i < CHAR_SIZE; i++)
            label[i] = -1;

        // Assign an order to pattern characters
        // according to their appearance in pattern
        let order = 1;
        for (let i = 0; i < pat.length; i++)
        {

            // give the pattern characters order
            label[pat[i].charCodeAt(0)] = order;

            // increment the order
            order++;
        }

        // Now one by check if string characters
        // follow above order
        let last_order = -1;
        for (let i = 0; i < str.length; i++)
        {
            if (label[str[i].charCodeAt(0)] != -1)
            {

                // If order of this character is less
                // than order of previous, return false.
                if (label[str[i].charCodeAt(0)] < last_order)
                    return false;

                // Update last_order for next iteration
                last_order = label[str[i].charCodeAt(0)];
            }
        }

        // return that str followed pat
        return true;
}

// Driver code
let str = "engineers rock";
let pattern = "gsr";
document.write(checkPattern(str, pattern));   

// This code is contributed by rag2127
</script>
```

**输出:**

```
false
```

这个程序的时间复杂度是 O(n)，额外空间不变(数组标签大小不变，256)。
本文由**穆罕默德·伊夫泰哈罗尔·伊斯拉姆·鲁潘**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。