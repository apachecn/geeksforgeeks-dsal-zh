# 通过递归删除一个给定的子字符串来检查一个字符串是否可以变为空

> 原文:[https://www . geesforgeks . org/check-string-can-变空-递归-删除-给定-子字符串/](https://www.geeksforgeeks.org/check-string-can-become-empty-recursively-deleting-given-sub-string/)

给定一个字符串“str”和另一个字符串“sub_str”。我们可以多次从“字符串”中删除“sub_str”。还假定“sub_str”一次只出现一次。任务是通过一次又一次地移除“sub_str”来发现“str”是否可以变成空的。
**例:**

```
Input  : str = "GEEGEEKSKS", sub_str = "GEEKS"
Output : Yes
Explanation : In the string GEEGEEKSKS, we can first 
              delete the substring GEEKS from position 4.
              The new string now becomes GEEKS. We can 
              again delete sub-string GEEKS from position 1\. 
              Now the string becomes empty.

Input  : str = "GEEGEEKSSGEK", sub_str = "GEEKS"
Output : No
Explanation : In the string it is not possible to make the
              string empty in any possible manner.
```

解决这个问题的简单方法是使用内置的[字符串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/)函数 find()和 erase()。首先在原始字符串中输入用于搜索目的的子字符串 substr，然后使用 find()迭代原始字符串以找到子字符串的索引，如果没有找到，则返回原始字符串中子字符串的起始索引 else -1，并使用 erase()擦除该子字符串，直到原始字符串的长度大于 0。
以上简单的解决方案是可行的，因为给定的子串一次只出现一次。

## C++

```
// C++ Program to check if a string can be
// converted to an empty string by deleting
// given sub-string from any position, any
// number of times.
#include<bits/stdc++.h>
using namespace std;

// Returns true if str can be made empty by
// recursively removing sub_str.
bool canBecomeEmpty(string str, string sub_str)
{
    while (str.size() > 0)
    {
        // idx: to store starting index of sub-
        //      string found in the original string
        int idx = str.find(sub_str);
        if (idx == -1)
            break;

        // Erasing the found sub-string from
        // the original string
        str.erase(idx, sub_str.size());
    }

    return (str.size() == 0);
}

// Driver code
int main()
{
    string str = "GEEGEEKSKS", sub_str = "GEEKS";
    if (canBecomeEmpty(str, sub_str))
        cout<<"\nYes";
    else
        cout<<"\nNo";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to check if a string can be
// converted to an empty string by deleting
// given sub-string from any position, any
// number of times.

class GFG {

// Returns true if str can be made empty by
// recursively removing sub_str.
    static boolean canBecomeEmpty(String str, String sub_str) {
        while (str.length() > 0) {
            // idx: to store starting index of sub-
            //      string found in the original string
            int idx = str.indexOf(sub_str);
            if (idx == -1) {
                break;
            }

            // Erasing the found sub-string from
            // the original string
            str = str.replaceFirst(sub_str,"");
        }

        return (str.length() == 0);
    }

// Driver code
    public static void main(String[] args) {
        String str = "GEEGEEKSKS", sub_str = "GEEKS";
        if (canBecomeEmpty(str, sub_str)) {
            System.out.print("\nYes");
        } else {
            System.out.print("\nNo");
        }
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if a string can be
# converted to an empty string by deleting
# given sub-string from any position, any
# number of times.

# Returns true if str can be made empty by
# recursively removing sub_str.
def canBecomeEmpty(string, sub_str):
    while len(string) > 0:

        # idx: to store starting index of sub-
        #     string found in the original string
        idx = string.find(sub_str)

        if idx == -1:
            break

        # Erasing the found sub-string from
        # the original string
        string = string.replace(sub_str, "", 1)

    return (len(string) == 0)

# Driver code
if __name__ == "__main__":
    string = "GEEGEEKSKS"
    sub_str = "GEEKS"
    if canBecomeEmpty(string, sub_str):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to check if a string can be
// converted to an empty string by deleting
// given sub-string from any position, any
// number of times.
using System;

class GFG
{

    // Returns true if str can be made empty by
    // recursively removing sub_str.
    static Boolean canBecomeEmpty(String str, String sub_str)
    {
        while (str.Length > 0)
        {
            // idx: to store starting index of sub-
            //     string found in the original string
            int idx = str.IndexOf(sub_str);
            if (idx == -1)
            {
                break;
            }

            // Erasing the found sub-string from
            // the original string
            str = str.Replace(sub_str,"");
        }

        return (str.Length == 0);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "GEEGEEKSKS", sub_str = "GEEKS";
        if (canBecomeEmpty(str, sub_str))
        {
            Console.Write("\nYes");
        }
        else
        {
            Console.Write("\nNo");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to check if a string can be
// converted to an empty string by deleting
// given sub-string from any position, any
// number of times.

// Returns true if str can be made empty by
// recursively removing sub_str
function canBecomeEmpty(str,sub_str)
{
    while (str.length > 0)
    {

            // idx: to store starting index of sub-
            //      string found in the original string
            let idx = str.indexOf(sub_str);
            if (idx == -1) {
                break;
            }

            // Erasing the found sub-string from
            // the original string
            str = str.replace(sub_str,"");
        }

        return (str.length == 0);
}

// Driver code
let str = "GEEGEEKSKS", sub_str = "GEEKS";
if (canBecomeEmpty(str, sub_str)) {
    document.write("<br>Yes");
} else {
    document.write("<br>No");
}

// This code is contributed by rag2127
</script>
```

**输出:**

```
Yes
```

本文由**希曼舒·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。