# 由一个恰好是子串 K 倍的串 S 组成的最小串

> 原文:[https://www . geesforgeks . org/minist-string-composed-a-string-s-just-k-times-as-substring/](https://www.geeksforgeeks.org/smallest-string-consisting-of-a-string-s-exactly-k-times-as-a-substring/)

给定长度为 **N** 和整数 **K** 的字符串 **S** ，找到包含字符串 **S** 作为子字符串的最小长度字符串，精确到 **K** 次。

**示例:**

> **输入:**S =“abba”，K = 3
> **输出:**abbabb
> **解释:**字符串“ABBA”在字符串 abbbaba 中出现 K 次，即{**ABBA**bbaba，abb **abba** bba，abbb**ABBA**
> 
> **输入:** S =“极客 forgeeks”，K = 3
> **输出:**“极客 forgeeksforgeeks”

**方法:**为了优化上述方法，找到[最长的固有前缀](https://www.geeksforgeeks.org/longest-prefix-also-suffix/)，它也是给定字符串 **S** 的后缀，然后生成一个排除最长公共前缀的 **S** 的子串，并将这个子串精确地添加到答案中**K–1**次到原始字符串。按照以下步骤解决问题:

*   使用 [KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)找到最长的合适前缀的长度。
*   将子串 **S.substring(N-lps[N-1])** 追加到 S，精确到 **K-1** 次。
*   Print the answer.

    下面是上述方法的实现。

    ## C++

    ```
    // C++ Program to implement 
    // the above approach 
    #include <bits/stdc++.h> 
    using namespace std; 

    // KMP algorithm 
    int* kmp(string& s) 
    { 

        int n = s.size(); 
        int* lps = new int[n]; 

        lps[0] = 0; 
        int i = 1, len = 0; 
        while (i < n) { 

            if (s[i] == s[len]) { 
                len++; 
                lps[i] = len; 
                i++; 
            } 
            else { 
                if (len != 0) { 
                    len = lps[len - 1]; 
                } 
                else { 
                    lps[i] = 0; 
                    i++; 
                } 
            } 
        } 

        return lps; 
    } 

    // Function to return the required string 
    string findString(string& s, int k) 
    { 

        int n = s.length(); 

        // Finding the longest proper prefix 
        // which is also suffix 
        int* lps = kmp(s); 

        // ans string 
        string ans = ""; 

        string suff 
            = s.substr(0, n - lps[n - 1]); 

        for (int i = 0; i < k - 1; ++i) { 

            // Update ans appending the 
            // substring K - 1 times 
            ans += suff; 
        } 

        // Append the original string 
        ans += s; 

        // Returning min length string 
        // which contain exactly k 
        // substring of given string 
        return ans; 
    } 

    // Driver Code 
    int main() 
    { 

        int k = 3; 

        string s = "geeksforgeeks"; 

        cout << findString(s, k) << endl; 
    } 
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to implement 
    // the above approach 
    import java.util.*;

    class GFG{

    // KMP algorithm 
    static int[] kmp(String s) 
    { 
        int n = s.length(); 
        int[] lps = new int[n]; 
        lps[0] = 0; 

        int i = 1, len = 0; 

        while (i < n)
        {
            if (s.charAt(i) == s.charAt(len))
            { 
                len++; 
                lps[i] = len; 
                i++; 
            } 
            else 
            { 
                if (len != 0)
                { 
                    len = lps[len - 1]; 
                } 
                else
                { 
                    lps[i] = 0; 
                    i++; 
                } 
            } 
        } 
        return lps; 
    } 

    // Function to return the required string 
    static String findString(String s, int k) 
    { 
        int n = s.length(); 

        // Finding the longest proper prefix 
        // which is also suffix 
        int[] lps = kmp(s); 

        // ans string 
        String ans = ""; 

        String suff    = s.substring(0, n - lps[n - 1]); 

        for(int i = 0; i < k - 1; ++i) 
        { 

            // Update ans appending the 
            // substring K - 1 times 
            ans += suff; 
        } 

        // Append the original string 
        ans += s; 

        // Returning min length string 
        // which contain exactly k 
        // substring of given string 
        return ans; 
    }

    // Driver code
    public static void main (String[] args) 
    {
        int k = 3; 

        String s = "geeksforgeeks"; 

        System.out.println(findString(s, k)); 
    }
    }

    // This code is contributed by offbeat
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to implement 
    # the above approach 

    # KMP algorithm 
    def kmp(s): 

        n = len(s) 
        lps = [None] * n 
        lps[0] = 0

        i, Len = 1, 0

        while (i < n):

            if (s[i] == s[Len]):
                Len += 1
                lps[i] = Len
                i += 1

            else:
                if (Len != 0): 
                    Len = lps[Len - 1]
                else:
                    lps[i] = 0
                    i += 1

        return lps

    # Function to return the required string 
    def findString(s, k): 

        n = len(s) 

        # Finding the longest proper prefix 
        # which is also suffix 
        lps = kmp(s) 

        # ans string 
        ans = "" 

        suff = s[0: n - lps[n - 1] : 1]

        for i in range(k - 1): 

            # Update ans appending the 
            # substring K - 1 times 
            ans += suff

        # Append the original string 
        ans += s

        # Returning min length string 
        # which contain exactly k 
        # substring of given string 
        return ans

    # Driver code
    k = 3

    s = "geeksforgeeks"

    print(findString(s, k)) 

    # This code is contributed by divyeshrabadiya07 
    ```

    ## C#

    ```
    // C# program to implement 
    // the above approach 
    using System;

    class GFG{

    // KMP algorithm 
    static int[] kmp(string s) 
    { 
        int n = s.Length; 
        int[] lps = new int[n]; 
        lps[0] = 0; 

        int i = 1, len = 0; 

        while (i < n)
        {
            if (s[i] == s[len])
            { 
                len++; 
                lps[i] = len; 
                i++; 
            } 
            else
            { 
                if (len != 0)
                { 
                    len = lps[len - 1]; 
                } 
                else
                { 
                    lps[i] = 0; 
                    i++; 
                } 
            } 
        } 
        return lps; 
    } 

    // Function to return the required string 
    static string findString(string s, int k) 
    { 
        int n = s.Length; 

        // Finding the longest proper prefix 
        // which is also suffix 
        int[] lps = kmp(s); 

        // ans string 
        string ans = ""; 

        string suff = s.Substring(0, 
                                  n - lps[n - 1]); 

        for(int i = 0; i < k - 1; ++i) 
        { 

            // Update ans appending the 
            // substring K - 1 times 
            ans += suff; 
        } 

        // Append the original string 
        ans += s; 

        // Returning min length string 
        // which contain exactly k 
        // substring of given string 
        return ans; 
    }

    // Driver code
    public static void Main (string[] args) 
    {
        int k = 3; 

        string s = "geeksforgeeks"; 

        Console.Write(findString(s, k)); 
    }
    }

    // This code is contributed by rutvik_56
    ```

    **Output:**

    ```
    geeksforgeeksforgeeksforgeeks

    ```

    ***时间复杂度:** O(N*K )*
    ***辅助空间:** O(K* N)*