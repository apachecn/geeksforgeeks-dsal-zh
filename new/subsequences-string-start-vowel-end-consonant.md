# 打印所有以元音开头和辅音结尾的字符串子序列。

给定一个字符串，返回所有可能的子序列，这些子序列以元音开头，以辅音结尾。 字符串是给定字符串的子序列，它是通过删除给定字符串的某些字符而不更改其顺序而生成的。

**范例**：

```
Input : 'abc'
Output : ab, ac, abc

Input : 'aab'
Output : ab, aab

```

问题来源： [Yatra.com 采访经历| 设置 7](https://www.geeksforgeeks.org/yatra-com-interview-experience-set-7/)

**算法说明**：

```
Step 1: Iterate over the entire String
Step 2: check if the ith character for vowel
Step 3: If true iterate the string from the end,
        if false move to next iteration
Step 4: check the jth character for consonent
        if false move to next iteration 
        if true perform the following 
Step 5: Add the substring starting at index i and
        ending at index j to the hastset.
Step 6: Iterate over the substring drop each character 
        and recur to generate all its subString

```

## C++

```cpp

// C++ program to generate all the subse-quence 
// starting with vowel and ending with consonant. 
#include <bits/stdc++.h> 
using namespace std; 

// Set to store all the subsequences 
set<string> st; 

// Utility method to check vowel 
bool isVowel(char c) 
{ 
    return (c == 'a' or c == 'e' or 
            c == 'i' or c == 'o' or 
            c == 'u'); 
} 

// Utility method to check consonant 
bool isConsonant(char c) 
{ 
    return !isVowel(c); 
} 

// It computes all the possible substring that 
// starts with vowel and end with consonent 
void subsequence(string str) 
{ 
    // iterate over the entire string 
    for (int i = 0; i < str.length(); i++) 
    { 
        // test ith character for vowel 
        if (isVowel(str[i])) 
        { 
            // if the ith character is vowel 
            // iterate from end of the string 
            // and check for consonant. 
            for (int j = str.length() - 1; j >= i; j--) 
            { 
                // test jth character for consonant. 
                if (isConsonant(str[j])) 
                { 
                    // once we get a consonant add it to 
                    // the hashset 
                    string str_sub = str.substr(i, j + 1); 
                    st.insert(str_sub); 

                    // drop each character of the substring 
                    // and recur to generate all subsequence 
                    // of the substring 
                    for (int k = 1; k < str_sub.length() - 1; k++) 
                    { 
                        string sb = str_sub; 
                        sb.erase(sb.begin() + k); 
                        subsequence(sb); 
                    } 
                } 
            } 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    string s = "xabcef"; 
    subsequence(s); 

    for (auto i : st) 
        cout << i << " "; 
    cout << endl; 

    return 0; 
} 

// This code is contributed by 
// sanjeev2552 

```

## Java

```java

// Java Program to generate all the subsequence 
// starting with vowel and ending with consonant. 
import java.util.HashSet; 

public class Subsequence { 

    // Set to store all the subsequences 
    static HashSet<String> st = new HashSet<>(); 

    // It computes all the possible substring that 
    // starts with vowel and end with consonent 
    static void subsequence(String str) 
    { 
        // iterate over the entire string 
        for (int i = 0; i < str.length(); i++) { 

            // test ith character for vowel 
            if (isVowel(str.charAt(i))) { 

                // if the ith character is vowel 
                // iterate from end of the string 
                // and check for consonant. 
                for (int j = (str.length() - 1); j >= i; j--) { 

                    // test jth character for consonant. 
                    if (isConsonant(str.charAt((j)))) { 

                        // once we get a consonant add it to  
                        // the hashset 
                        String str_sub = str.substring(i, j + 1); 
                        st.add(str_sub); 

                        // drop each character of the substring 
                        // and recur to generate all subsequence 
                        // of the substring 
                        for (int k = 1; k < str_sub.length() - 1; k++) { 
                            StringBuffer sb = new StringBuffer(str_sub); 
                            sb.deleteCharAt(k); 
                            subsequence(sb.toString()); 
                        } 
                    } 
                } 
            } 
        } 
    } 

    // Utility method to check vowel 
    static boolean isVowel(char c) 
    { 
        return (c == 'a' || c == 'e' || c == 'i' || c == 'o'
                                              || c == 'u'); 
    } 

    // Utility method to check consonant 
    static boolean isConsonant(char c) 
    { 
        return !isVowel(c); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        String s = "xabcef"; 
        subsequence(s); 
        System.out.println(st); 
    } 
} 

```

## C#

```cs

// C# Program to generate all the subsequence 
// starting with vowel and ending with consonant. 
using System; 
using System.Collections.Generic; 
using System.Text; 

class Subsequence 
{ 

    // Set to store all the subsequences 
    static HashSet<String> st = new HashSet<String>(); 

    // It computes all the possible substring that 
    // starts with vowel and end with consonent 
    static void subsequence(String str) 
    { 
        // iterate over the entire string 
        for (int i = 0; i < str.Length; i++) 
        { 

            // test ith character for vowel 
            if (isVowel(str[i])) 
            { 

                // if the ith character is vowel 
                // iterate from end of the string 
                // and check for consonant. 
                for (int j = (str.Length - 1); j >= i; j--) 
                { 

                    // test jth character for consonant. 
                    if (isConsonant(str[j])) 
                    { 

                        // once we get a consonant add it to  
                        // the hashset 
                        String str_sub = str.Substring(i, j -i + 1); 
                        st.Add(str_sub); 

                        // drop each character of the substring 
                        // and recur to generate all subsequence 
                        // of the substring 
                        for (int k = 1; k < str_sub.Length - 1; k++) 
                        { 
                            StringBuilder sb = new StringBuilder(str_sub); 
                            sb.Remove(k, 1); 
                            subsequence(sb.ToString()); 
                        } 
                    } 
                } 
            } 
        } 
    } 

    // Utility method to check vowel 
    static bool isVowel(char c) 
    { 
        return (c == 'a' || c == 'e' || c == 'i' || c == 'o'
                                            || c == 'u'); 
    } 

    // Utility method to check consonant 
    static bool isConsonant(char c) 
    { 
        return !isVowel(c); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        String s = "xabcef"; 
        subsequence(s); 
        foreach(String str in st) 
            Console.Write(str + ", "); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
[ef, ab, ac, aef, abc, abf, af, acf, abcef, abcf, acef, abef]

```

本文由 **Sumit Ghosh** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

