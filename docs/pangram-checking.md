# 庞拉姆检查

> 原文:[https://www.geeksforgeeks.org/pangram-checking/](https://www.geeksforgeeks.org/pangram-checking/)

给定一个字符串，检查它是否是 Pangram。单词是包含英语字母表中每个字母的句子。
例:“快棕狐狸跳过懒狗”是一只庞格朗[包含从‘a’到‘z’的所有字符]
“快棕狐狸跳过狗”不是庞格朗[不包含从‘a’到‘z’的所有字符，因为‘l’、‘z’、‘y’都不见了]

我们创建一个布尔类型的标记[]数组。我们遍历字符串的所有字符，每当我们看到一个字符，我们就标记它。小写和大写被认为是相同的。所以‘A’和‘A’标记在索引 0 中，类似地‘Z’和‘Z’标记在索引 25 中。

在遍历所有字符后，我们检查是否所有字符都被标记了。如果不是，那么返回假，因为这不是一个庞加莱，否则返回真。

## C++

```
// A C++ Program to check if the given
// string is a pangram or not
#include <bits/stdc++.h>
using namespace std;

// Returns true if the string is pangram else false
bool checkPangram(string& str)
{
    // Create a hash table to mark the characters
    // present in the string
    vector<bool> mark(26, false);

    // For indexing in mark[]
    int index;

    // Traverse all characters
    for (int i = 0; i < str.length(); i++) {

        // If uppercase character, subtract 'A'
        // to find index.
        if ('A' <= str[i] && str[i] <= 'Z')
            index = str[i] - 'A';

        // If lowercase character, subtract 'a'
        // to find index.
        else if ('a' <= str[i] && str[i] <= 'z')
            index = str[i] - 'a';

        // If this character is other than english
        // lowercase and uppercase characters.
        else
            continue;

        mark[index] = true;
    }

    // Return false if any character is unmarked
    for (int i = 0; i <= 25; i++)
        if (mark[i] == false)
            return (false);

    // If all characters were present
    return (true);
}

// Driver Program to test above functions
int main()
{
    string str = "The quick brown fox jumps over the"
                 " lazy dog";

    if (checkPangram(str) == true)
        printf(" %s is a pangram", str.c_str());
    else
        printf(" %s is not a pangram", str.c_str());

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to illustrate Pangram
class GFG {

    // Returns true if the string
    // is pangram else false
    public static boolean checkPangram(String str)
    {
        // Create a hash table to mark the
        // characters present in the string
        // By default all the elements of
        // mark would be false.
        boolean[] mark = new boolean[26];

        // For indexing in mark[]
        int index = 0;

        // Traverse all characters
        for (int i = 0; i < str.length(); i++) {
            // If uppercase character, subtract 'A'
            // to find index.
            if ('A' <= str.charAt(i) && str.charAt(i) <= 'Z')
                index = str.charAt(i) - 'A';

            // If lowercase character, subtract 'a'
            // to find index.
            else if ('a' <= str.charAt(i) && str.charAt(i) <= 'z')

                index = str.charAt(i) - 'a';

            // If this character is other than english
            // lowercase and uppercase characters.
            else
                continue;
            mark[index] = true;
        }

        // Return false if any character is unmarked
        for (int i = 0; i <= 25; i++)
            if (mark[i] == false)
                return (false);

        // If all characters were present
        return (true);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "The quick brown fox jumps over the lazy dog";

        if (checkPangram(str) == true)
            System.out.print(str + " is a pangram.");
        else
            System.out.print(str + " is not a pangram.");
    }
}
```

## 计算机编程语言

```
# A Python Program to check if the given
# string is a pangram or not

def checkPangram(s):
    List = []
    # create list of 26 characters and set false each entry
    for i in range(26):
        List.append(False)

    # converting the sentence to lowercase and iterating
    # over the sentence
    for c in s.lower():
        if not c == " ":

            # make the corresponding entry True
            List[ord(c) -ord('a')]= True

    # check if any character is missing then return False
    for ch in List:
        if ch == False:
            return False
    return True

# Driver Program to test above functions
sentence = "The quick brown fox jumps over the little lazy dog"

if (checkPangram(sentence)):
    print '"'+sentence+'"'
    print "is a pangram"
else:
    print '"'+sentence+'"'
    print "is not a pangram"

# This code is contributed by Danish Mushtaq 
```

## C#

```
// C# Program to illustrate Pangram
using System;
class GFG {

    // Returns true if the string
    // is pangram else false
    public static bool checkPangram(string str)
    {

        // Create a hash table to mark the
        // characters present in the string
        // By default all the elements of
        // mark would be false.
        bool[] mark = new bool[26];

        // For indexing in mark[]
        int index = 0;

        // Traverse all characters
        for (int i = 0; i < str.Length; i++) {
            // If uppercase character, subtract 'A'
            // to find index.
            if ('A' <= str[i] && str[i] <= 'Z')
                index = str[i] - 'A';

            // If lowercase character,
            // subtract 'a' to find
            // index.
            else if ('a' <= str[i] && str[i] <= 'z')
                index = str[i] - 'a';

            // If this character is other than english
            // lowercase and uppercase characters.
            else
                continue;

            mark[index] = true;
        }

        // Return false if any
        // character is unmarked
        for (int i = 0; i <= 25; i++)
            if (mark[i] == false)
                return (false);

        // If all characters
        // were present
        return (true);
    }

    // Driver Code
    public static void Main()
    {
        string str = "The quick brown fox jumps over the lazy dog";

        if (checkPangram(str) == true)
            Console.WriteLine(str + " is a pangram.");
        else
            Console.WriteLine(str + " is not a pangram.");
    }
}

// This code is contributed by nitin mittal.
```

输出:

```
 "The quick brown fox jumps over the lazy dog"
 is a pangram
```

时间复杂度:O(n)，其中 n 是我们字符串的长度
辅助空间–O(1)。

https://youtu.be/Yv4ARV

-Hrow
本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息