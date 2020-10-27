# 打印使用任意一对给定字符串形成的所有可能的回文字符串

给定[字符串](https://www.geeksforgeeks.org/introduction-to-arrays/)字符串 **arr []** 包含 **N** 个字的数组，任务是通过组合给定数组中的任何两个字符串来打印所有可能的回文字符串。
**范例：**

> **输入**：arr [] = [“ geekf”，“ geeks”，“ or”，“ keeg”，“ abc”，“ ba”]
> **输出**：[“ **，**
> **解释：**
> 以下对构成组合中的回文字符串：
> 1.“ geekf” +“ keeg” =“ geekfkeeg”
> 2.“ geeks” +“ keeg” =“ geekskeeg”
> 3.“ abc” +“ ba” =“ abcba”
> 
> **输入**：arr [] = [“ dcb”，“ yz”，“ xy”，“ efg”，“ yx”]
> **输出**： [“ xyyx”，“ yxxy”]
> **说明：**
> 1.“ xy” +“ yz” =“ xyyz”
> 2.“ yx” +“ xy” =“ yxxy”

**朴素的方法：**朴素的方法是迭代[给定字符串数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中的所有可能对，并检查字符串的连接是否形成回文。 如果是，则打印该对并检查下一对。

 ***时间复杂度：** *O（N <sup>2</sup> ）*
**辅助空间：** *O（1）*

**有效方法：**可以使用[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)优化上述方法。 步骤如下：

1.  将所有单词存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，其中**单词**作为**键**和**索引**作为**值。**
2.  对于 **arr []** 中的每个单词（例如 **str** ），将字符串分成字符串 **s1** 和 **s2** ，这样 **s1 + s2 ＝ str** 。
3.  完成上述步骤后，出现两种情况：
    *   **情况 1：**如果 **s1** 是回文字符串，并且 **s2** 的反向出现在哈希图中，则我们得到所需的对（**反向 s2** + **当前单词**的形式）。
    *   **情况 2：**如果 **s2** 是回文字符串，并且如果哈希图中存在反向 **s1** ，那么我们得到一个对（**当前字词** + s1 的反向**）。**
4.  对数组中的所有字符串重复上述步骤。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check whether the string 
// word is palindrome or not 
bool ispalin(string word) 
{ 

    if (word.length() == 1 
        || word.empty()) { 
        return true; 
    } 

    int l = 0; 
    int r = word.length() - 1; 

    // Iterate word 
    while (l <= r) { 

        if (word[l] != word[r]) { 
            return false; 
        } 
        l++; 
        r--; 
    } 

    return true; 
} 

// Function to find the palindromicPairs 
vector<string> 
palindromicPairs(vector<string>& words) 
{ 

    vector<string> output; 
    if (words.size() == 0 
        || words.size() == 1) { 
        return output; 
    } 

    // Insert all the strings with 
    // their indices in the hash map 
    unordered_map<string, int> mp; 

    for (int i = 0; i < words.size(); i++) { 
        mp[words[i]] = i; 
    } 

    // Iterate over all the words 
    for (int i = 0; i < words.size(); i++) { 

        // If the word is empty then 
        // we simply pair it will all the 
        // words which are palindrome 
        // present in the array 
        // except the word itself 
        if (words[i].empty()) { 

            for (auto x : mp) { 

                if (x.second == i) { 
                    continue; 
                } 

                if (ispalin(x.first)) { 
                    output.push_back(x.first); 
                } 
            } 
        } 

        // Create all possible substrings 
        // s1 and s2 
        for (int j = 0; 
             j < words[i].length(); j++) { 

            string s1 = words[i].substr(0, j + 1); 
            string s2 = words[i].substr(j + 1); 

            // Case 1 
            // If s1 is palindrome and 
            // reverse of s2 is 
            // present in hashmap at 
            // index other than i 
            if (ispalin(s1)) { 

                reverse(s2.begin(), 
                        s2.end()); 

                string temp = s2; 

                if (mp.count(s2) == 1 
                    && mp[s2] != i) { 
                    string ans = s2 + words[i]; 
                    output.push_back(ans); 
                } 

                s2 = temp; 
            } 

            // Case 2 
            // If s2 is palindrome and 
            // reverse of s1 is 
            // present in hashmap 
            // at index other than i 
            if (ispalin(s2)) { 

                string temp = s1; 
                reverse(s1.begin(), 
                        s1.end()); 

                if (mp.count(s1) == 1 
                    && mp[s1] != i) { 
                    string ans = words[i] + s1; 
                    output.push_back(ans); 
                } 

                s1 = temp; 
            } 
        } 
    } 

    // Return output 
    return output; 
} 

// Driver Code 
int main() 
{ 

    vector<string> words; 

    // Given array of words 
    words = { "geekf", "geeks", "or", 
              "keeg", "abc", "ba" }; 

    // Function call 
    vector<string> result 
        = palindromicPairs(words); 

    // Print the palindromic strings 
    // after combining them 
    for (auto x : result) { 
        cout << x << endl; 
    } 

    return 0; 
}

```

**Output:**

```
geekfkeeg
geekskeeg
abcba

```

**时间复杂度：** *O（N）*
**辅助空间：** *O（N）*



* * *

* * *



