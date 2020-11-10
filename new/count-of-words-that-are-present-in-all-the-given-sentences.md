# 所有给定句子中出现的单词数

> 原文：[https://www.geeksforgeeks.org/count-of-words-that-are-present-in-all-the-given-sentences/](https://www.geeksforgeeks.org/count-of-words-that-are-present-in-all-the-given-sentences/)

给定`n`个句子。 任务是计算所有这些句子中出现的单词数。 **请注意**，每个单词仅由小写英文字母组成。

**示例**：

> **输入**：
>
> ```
> arr[] = {
>   "there is a cow",
>   "cow is our mother",
>   "cow gives us milk and milk is sweet",
>   "there is a boy who loves cow"
> }
> ```
> 
> **输出**：2
>
> 在所有句子中只有单词`"is"`和`"cow"`出现。
> 
> **输入**：
> 
> ```
> arr [] = {
>   "abc aac abcd ccc",
>   "ac aa abc cca",
>   "abca aaac abcd ccc"
> }
> ```
>
> **输出**：0

**朴素的方法**：朴素的方法是将第一句的每个单词都包含在所有行中，然后将其与其余行进行比较，然后增加计数。

**有效方法**：对于第一个句子的所有单词，我们可以使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来恒定时间检查它是否也存在于所有其他句子中。 将第一个句子的所有单词存储在映射中，并检查所有其他句子中有多少个存储的单词。

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the count of common words 
// in all the sentences 
int commonWords(vector<string> S) 
{ 
    int m, n, i, j; 

    // To store separate words 
    string str; 

    // It will be used to check if a word is present 
    // in a particuler string 
    unordered_map<string, bool> has; 

    // To store all the words of first string 
    vector<pair<string, bool> > ans; 

    pair<string, bool> tmp; 

    // m will store number of strings in given vector 
    m = S.size(); 

    i = 0; 

    // Extract all words of first string and store it in ans 
    while (i < S[0].size()) { 
        str = ""; 
        while (i < S[0].size() && S[0][i] != ' ') { 
            str += S[0][i]; 
            i++; 
        } 

        // Increase i to get at starting index 
        // of the next word 
        i++; 

        // If str is not empty store it in map 
        if (str != "") { 
            tmp = make_pair(str, true); 
            ans.push_back(tmp); 
        } 
    } 

    // Start from 2nd line check if any word of 
    // the first string did not match with 
    // some word in the current line 
    for (j = 1; j < m; j++) { 
        has.clear(); 
        i = 0; 

        while (i < S[j].size()) { 
            str = ""; 
            while (i < S[j].size() && S[j][i] != ' ') { 
                str += S[j][i]; 
                i++; 
            } 
            i++; 
            if (str != "") { 
                has[str] = true; 
            } 
        } 

        // Check all words of this vector 
        // if it is not present in current line 
        // make it false 
        for (int k = 0; k < ans.size(); k++) { 
            if (ans[k].second != false
                && has[ans[k].first] == false) { 
                ans[k].second = false; 
            } 

            // This line is used to consider only distinct words 
            else if (ans[k].second != false
                     && has[ans[k].first] == true) { 
                has[ans[k].first] = false; 
            } 
        } 
    } 

    // This function will print 
    // the count of common words 
    int cnt = 0; 

    // If current word appears in all the sentences 
    for (int k = 0; k < ans.size(); k++) { 
        if (ans[k].second == true) 
            cnt++; 
    } 

    return cnt; 
} 

// Driver code 
int main() 
{ 
    vector<string> S; 
    S.push_back("there is a cow"); 
    S.push_back("cow is our mother"); 
    S.push_back("cow gives us milk and milk is sweet"); 
    S.push_back("there is a boy who loves cow"); 

    cout << commonWords(S); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
import java.util.HashMap; 

class GFG 
{ 

    // Function to return the count of  
    // common words in all the sentences 
    static int commonWords(String[] s)  
    { 
        int m, i, j; 

        // To store separate words 
        String str; 

        // It will be used to check if a word  
        // is present in a particuler string 
        HashMap<String, Boolean> has = new HashMap<>(); 

        // To store all the words of first string 
        String[] ans1 = new String[100]; 
        boolean[] ans2 = new boolean[100]; 
        int track = 0; 

        // m will store number of strings  
        // in given vector 
        m = s.length; 
        i = 0; 

        // Extract all words of first string  
        // and store it in ans 
        while (i < s[0].length())  
        { 
            str = ""; 
            while (i < s[0].length() && 
                       s[0].charAt(i) != ' ') 
            { 
                str += s[0].charAt(i); 
                i++; 
            } 

            // Increase i to get at starting index 
            // of the next word 
            i++; 

            // If str is not empty store it in map 
            if (str.compareTo("") != 0) 
            { 
                ans1[track] = str; 
                ans2[track] = true; 
                track++; 
            } 
        } 

        // Start from 2nd line check if any word of 
        // the first string did not match with 
        // some word in the current line 
        for (j = 1; j < m; j++) 
        { 
            has.clear(); 
            i = 0; 
            while (i < s[j].length()) 
            { 
                str = ""; 
                while (i < s[j].length() && 
                           s[j].charAt(i) != ' ') 
                { 
                    str += s[j].charAt(i); 
                    i++; 
                } 

                i++; 
                if (str.compareTo("") != 0) 
                    has.put(str, true); 
            } 

            // Check all words of this vector 
            // if it is not present in current line 
            // make it false 
            for (int k = 0; k < track; k++) 
            { 
                // System.out.println(has.get(ans1[k])); 
                if (ans2[k] != false &&  
                    !has.containsKey(ans1[k])) 
                    ans2[k] = false; 

                // This line is used to consider 
                // only distinct words 
                else if (ans2[k] != false &&  
                         has.containsKey(ans1[k]) &&  
                         has.get(ans1[k]) == true) 
                    has.put(ans1[k], false); 
            } 
        } 

        // This function will print 
        // the count of common words 
        int cnt = 0; 

        // If current word appears  
        // in all the sentences 
        for (int k = 0; k < track; k++) 
            if (ans2[k] == true) 
                cnt++; 

        return cnt; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        String[] s = { "there is a cow", "cow is our mother", 
                       "cow gives us milk and milk is sweet", 
                       "there is a boy who loves cow" }; 

        System.out.println(commonWords(s)); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python3 implementation of the approach  
from collections import defaultdict 

# Function to return the count of  
# common words in all the sentences  
def commonWords(S):  

    # It will be used to check if a word  
    # is present in a particuler string  
    has = defaultdict(lambda:False)  

    # To store all the words of first string  
    ans = []  

    # m will store number of strings  
    # in given vector  
    m = len(S)  

    i = 0

    # Extract all words of first string  
    # and store it in ans  
    while i < len(S[0]):  
        string = ""  
        while i < len(S[0]) and S[0][i] != ' ':  
            string += S[0][i]  
            i += 1

        # Increase i to get at starting  
        # index of the next word  
        i += 1

        # If str is not empty store it in map  
        if string != "":  
            ans.append([string, True])  

    # Start from 2nd line check if any word  
    # of the first string did not match with  
    # some word in the current line  
    for j in range(1, m): 
        has.clear()  
        i = 0

        while i < len(S[j]):  
            string = ""  
            while i < len(S[j]) and S[j][i] != ' ':  
                string += S[j][i]  
                i += 1

            i += 1
            if string != "":  
                has[string] = True

        # Check all words of this vector  
        # if it is not present in current  
        # line make it false  
        for k in range(0, len(ans)):  
            if (ans[k][1] != False and
                has[ans[k][0]] == False):  
                ans[k][1] = False

            # This line is used to consider  
            # only distinct words  
            elif (ans[k][1] != False
                and has[ans[k][0]] == True):  
                has[ans[k][0]] = False

    # This function will print  
    # the count of common words  
    cnt = 0

    # If current word appears in all 
    # the sentences  
    for k in range(0, len(ans)):  
        if ans[k][1] == True:  
            cnt += 1

    return cnt  

# Driver code  
if __name__ == "__main__": 

    S = []  
    S.append("there is a cow")  
    S.append("cow is our mother")  
    S.append("cow gives us milk and milk is sweet")  
    S.append("there is a boy who loves cow")  

    print(commonWords(S))  

# This code is contributed by Rituraj Jain  

```

**输出**：

```
2

```



* * *

* * *



