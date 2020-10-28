# 包含两个字符串中不常见字符的串联字符串

> 原文：[https://www.geeksforgeeks.org/concatenated-string-uncommon-characters-two-strings/](https://www.geeksforgeeks.org/concatenated-string-uncommon-characters-two-strings/)

给出了两个字符串，您必须修改第一个字符串，以便必须删除第二个字符串的所有常见字符，并且第二个字符串的不常见字符必须与第一个字符串的不常见字符连接在一起。

**示例**：

```
Input : S1 = "aacdb"
        S2 = "gafd"
Output : "cbgf"

Input : S1 = "abcs";
        S2 = "cxzca";
Output : "bsxz"

```

这个想法是使用哈希映射，其中键是字符，值是存在字符的字符串数。 如果一个字符存在于一个字符串中，则计数为 1，否则，如果字符存在于两个字符串中，则计数为 2。

1.  将结果初始化为空字符串。

2.  将计数为 1 的第二个字符串的所有字符推送到映射中。

3.  遍历第一个字符串，并将所有这些字符附加到 map 中不存在的结果中。 地图中显示的字符数为 2。

4.  遍历第二个字符串并附加所有这些字符，得出计数为 1 的结果。

## C++

```cpp

// C++ program Find concatenated string with 
// uncommon characters of given strings 
#include <bits/stdc++.h> 
using namespace std; 

string concatenetedString(string s1, string s2) 
{ 
    string res = ""; // result 

    // store all characters of s2 in map 
    unordered_map<char, int> m; 
    for (int i = 0; i < s2.size(); i++) 
        m[s2[i]] = 1; 

    // Find characters of s1 that are not 
    // present in s2 and append to result 
    for (int i = 0; i < s1.size(); i++) { 
        if (m.find(s1[i]) == m.end()) 
            res += s1[i]; 
        else
            m[s1[i]] = 2; 
    } 

    // Find characters of s2 that are not 
    // present in s1\. 
    for (int i = 0; i < s2.size(); i++) 
        if (m[s2[i]] == 1) 
            res += s2[i]; 
    return res; 
} 

/* Driver program to test above function */
int main() 
{ 
    string s1 = "abcs"; 
    string s2 = "cxzca"; 
    cout << concatenetedString(s1, s2); 
    return 0; 
} 

```

## Java

```java

// Java program Find concatenated string with 
// uncommon characters of given strings 
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class gfg { 
    public static String concatenatedString(String s1, String s2) 
    { 
        // Result 
        String res = ""; 
        int i; 

        // creating a hashMap to add characters in string s2 
        HashMap<Character, Integer> m = new HashMap<Character, Integer>(); 
        for (i = 0; i < s2.length(); i++) 
            m.put(s2.charAt(i), 1); 

        // Find characters of s1 that are not 
        // present in s2 and append to result 
        for (i = 0; i < s1.length(); i++) 
            if (!m.containsKey(s1.charAt(i))) 
                res += s1.charAt(i); 
            else
                m.put(s1.charAt(i), 2); 

        // Find characters of s2 that are not 
        // present in s1\. 
        for (i = 0; i < s2.length(); i++) 
            if (m.get(s2.charAt(i)) == 1) 
                res += s2.charAt(i); 

        return res; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        String s1 = "abcs"; 
        String s2 = "cxzca"; 
        System.out.println(concatenatedString(s1, s2)); 
    } 
} 

/* This code is contributed by Devarshi_Singh*/

```

## Python 3

```

# Python3 program Find concatenated string  
# with uncommon characters of given strings  
def concatenetedString(s1, s2): 
    res = "" # result  
    m = {} 

    # store all characters of s2 in map  
    for i in range(0, len(s2)): 
        m[s2[i]] = 1

    # Find characters of s1 that are not  
    # present in s2 and append to result  
    for i in range(0, len(s1)): 
        if(not s1[i] in m): 
            res = res + s1[i] 
        else: 
            m[s1[i]] = 2

    # Find characters of s2 that are not  
    # present in s1.          
    for i in range(0, len(s2)): 
        if(m[s2[i]] == 1): 
            res = res + s2[i] 

    return res      

# Driver Code 
if __name__ == "__main__": 
    s1 = "abcs"
    s2 = "cxzca"
    print(concatenetedString(s1, s2)) 

# This code is contributed 
# by Sairahul099 

```

## C#

```cs

// C# program Find concatenated string with 
// uncommon characters of given strings  
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    public static String concatenatedString(String s1,  
                                            String s2) 
    { 
        // Result 
        String res = ""; 
        int i; 

        // creating a hashMap to add characters 
        // in string s2 
        Dictionary<char,  
                   int> m = new Dictionary<char,  
                                           int>(); 
        for (i = 0; i < s2.Length; i++) 
            if (!m.ContainsKey(s2[i])) 
                m.Add(s2[i], 1); 

        // Find characters of s1 that are not 
        // present in s2 and append to result 
        for (i = 0; i < s1.Length; i++) 
            if (!m.ContainsKey(s1[i])) 
                res += s1[i]; 
            else
                m[s1[i]] = 2; 

        // Find characters of s2 that are not 
        // present in s1\. 
        for (i = 0; i < s2.Length; i++) 
            if (m[s2[i]] == 1) 
                res += s2[i]; 

        return res; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        String s1 = "abcs"; 
        String s2 = "cxzca"; 
        Console.WriteLine(concatenatedString(s1, s2)); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
bsxz

```

本文由 **Harshit Agrawal** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

