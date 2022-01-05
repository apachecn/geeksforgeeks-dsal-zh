# 按照字典顺序生成给定字符串的不同子序列

> 原文:[https://www . geeksforgeeks . org/按字典顺序生成给定字符串的不同子序列/](https://www.geeksforgeeks.org/generating-distinct-subsequences-of-a-given-string-in-lexicographic-order/)

给定一个字符串 s，列出给定字符串 s 的所有可能的字母组合。如果有两个字符串具有相同的字符集，打印这两个字符串的字典最小排列
对于字符串 abc，按字典顺序排列的子序列列表是，a ab abc ac b bc c
示例:

```
Input : s = "ab"
Output : a ab b

Input  : xyzx
Output : x xx xy xyx xyz xyzx xz xzx y
         yx yz yzx z zx
```

其思想是使用一个集合(使用[自平衡 BST](https://www.geeksforgeeks.org/tag/self-balancing-bst/) 实现)来存储子序列，以便可以测试副本。
为了生成所有的子序列，我们一个接一个地删除每个字符，并对剩余的字符串重复。

## C++

```
// C++ program to print all distinct subsequences
// of a string.
#include <bits/stdc++.h>
using namespace std;

// Finds and stores result in st for a given
// string s.
void generate(set<string>& st, string s)
{
    if (s.size() == 0)
        return;

    // If current string is not already present.
    if (st.find(s) == st.end()) {
        st.insert(s);

        // Traverse current string, one by one
        // remove every character and recur.
        for (int i = 0; i < s.size(); i++) {
            string t = s;
            t.erase(i, 1);
            generate(st, t);
        }
    }
    return;
}

// Driver code
int main()
{
    string s = "xyz";
    set<string> st;
    set<string>::iterator it;
    generate(st, s);
    for (auto it = st.begin(); it != st.end(); it++)
        cout << *it << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all distinct subsequences
// of a string.
import java.util.*;

class GFG {

    // Finds and stores result in st for a given
    // string s.
    static void generate(Set<String> st, String s)
    {
        if (s.length() == 0) {
            return;
        }

        // If current string is not already present.
        if (!st.contains(s)) {
            st.add(s);

            // Traverse current string, one by one
            // remove every character and recur.
            for (int i = 0; i < s.length(); i++) {
                String t = s;
                t = t.substring(0, i) + t.substring(i + 1);
                generate(st, t);
            }
        }
        return;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "xyz";
        TreeSet<String> st = new TreeSet<>();
        generate(st, s);
        for (String str : st) {
            System.out.println(str);
        }
    }
}

// This code has been contributed by 29AjayKumar
// modified by rahul_107
```

## 蟒蛇 3

```
# Python program to print all distinct
# subsequences of a string.

# Finds and stores result in st for a given
# string s.
def generate(st, s):
    if len(s) == 0:
        return

    # If current string is not already present.
    if s not in st:
        st.add(s)

        # Traverse current string, one by one
        # remove every character and recur.
        for i in range(len(s)):
            t = list(s).copy()
            t.remove(s[i])
            t = ''.join(t)
            generate(st, t)

    return

# Driver Code
if __name__ == "__main__":
    s = "xyz"
    st = set()
    generate(st, s)
    for i in st:
        print(i)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print all distinct subsequences
// of a string.
using System;
using System.Collections.Generic;

class GFG {

    // Finds and stores result in st for a given
    // string s.
    static void generate(HashSet<String> st, String s)
    {
        if (s.Length == 0) {
            return;
        }

        // If current string is not already present.
        if (!st.Contains(s)) {
            st.Add(s);

            // Traverse current string, one by one
            // remove every character and recur.
            for (int i = 0; i < s.Length; i++) {
                String t = s;
                t = t.Substring(0, i) + t.Substring(i + 1);
                generate(st, t);
            }
        }
        return;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "xyz";
        HashSet<String> st = new HashSet<String>();
        generate(st, s);
        foreach(String str in st)
        {
            Console.WriteLine(str);
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to print
// all distinct subsequences
// of a string.

// Finds and stores result in st for a given
// string s.
function generate(st,s){
    if (s.length == 0)
        return st;

    // If current string is not already present.
    if (!st.has(s)) {
        st.add(s);
        // Traverse current string, one by one
        // remove every character and recur.
        for (let i = 0; i < s.length; i++) {
            let t = s;
            t = t.substr(0, i) + t.substr(i + 1);
            st = generate(st, t);
        }
    }
    return st;
}

// Driver code
let s = "xyz";

let st = new Set();
st = generate(st, s);

let str = '';
console.log(st)
for(item of st.values())
    str += item + '<br> '

document.write(str);

</script>
```

**输出:**

```
x
xy
xyz
xz
y
yz
z
```

本文由 **SANDEEP GAUR MNNIT** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。