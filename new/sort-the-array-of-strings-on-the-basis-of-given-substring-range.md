# 根据给定的子字符串范围对字符串数组进行排序

> 原文：[https://www.geeksforgeeks.org/sort-the-array-of-strings-on-the-basis-of-given-substring-range/](https://www.geeksforgeeks.org/sort-the-array-of-strings-on-the-basis-of-given-substring-range/)

给定两个正整数`I`和`X`以及字符串`arr[]`的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，任务是[对给定的字符串进行排序 从大小为`X`的索引`I`开始的怀疑字符串基础上的字符串数组](https://www.geeksforgeeks.org/c-program-sort-array-names-strings/)。

**示例**：

> **输入**：`I = 2, X = 2, arr[] = {"baqwer", "zacaeaz", "aaqzzaa", "aacaap", "abbatyo", "bbbacztr", "bbbdaaa"}`
> **输出**：`abbatyo bbbacztr bbbdaaa aacaap zacaeaz baqwer aaqzzaa`。
> **解释**：所有从`I = 2`起始长度为`X = 2`的子串为`{"qw", "ca", "qz", "ca", "ba", "ba", "bd"}`
> 按照字典顺序升序对它们进行排序，得到`{"ba", "ba", "bd", "ca", "ca", "qw", "qz"}`，然后按此顺序打印相应的原始字符串。
> 
> **输入**：`I = 1, X = 3, arr[] = {"submit", "source", "skills", "epidemic", "ample", "apple"}`
> **输出**：`submit epidemic skills ample apple source`

**方法**：这个想法是根据大小为`X`的索引`I`创建给定数组中所有字符串的子字符串，并保留子字符串对的计数 与成对映射中的相应字符串。 成对插入映射后。 插入后，遍历映射并打印字符串。

下面是上述方法的实现：

## CPP

```

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to sort the given array 
// of strings based on substring 
void sortArray(vector<string> s, 
               int l, int x) 
{ 
    // Map of pairs to sort vector 
    // of strings 
    map<pair<string, string>, int> mp; 

    for (int i = 0; i < s.size(); i++) { 

        // Create substring from index 
        // 'l' and of size 'X' 
        string part = s[i].substr(l, x); 

        // Insert in Map 
        mp[{ part, s[i] }] += 1; 
    } 

    // Print the sorted vector of strings 
    for (auto it = mp.begin(); 
         it != mp.end(); ++it) { 

        // Traverse the number of time 
        // a string is present 
        for (int j = 0; j < it->second; j++) { 

            // Print the string 
            cout << it->first.second << ' '; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    // Given array of strings 
    vector<string> arr; 
    arr = { "baqwer", "zacaeaz", "aaqzzaa", 
            "aacaap", "abbatyo", "bbbacztr", 
            "bbbdaaa" }; 

    // Given I and X 
    int I = 2, X = 2; 

    // Function Call 
    sortArray(arr, I, X); 
    return 0; 
} 

```

**输出**：

```
abbatyo bbbacztr bbbdaaa aacaap zacaeaz baqwer aaqzzaa

```

**时间复杂度**：`O(N * log N)`

**辅助空间**：`O(n)`



* * *

* * *



