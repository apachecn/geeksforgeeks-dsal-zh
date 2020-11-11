# C++ 程序，用于检查字符串是否为全字母短句

> 原文：[https://www.geeksforgeeks.org/c-program-to-check-whether-a-string-is-a-pangram-or-not/](https://www.geeksforgeeks.org/c-program-to-check-whether-a-string-is-a-pangram-or-not/)

给定字符串`str`，任务是检查在 C++ 中是否使用了字符串。

> [如果字符串包含所有英语字母，则该字符串为全字母短句](https://www.geeksforgeeks.org/pangram-checking/)。

**示例**：

> **输入**：`str = "We promptly judged antique ivory buckles for the next prize"`
> 
> **输出**：是
> 
> **说明**：在上面的字符串中，`str`具有所有英语字母。
> 
> **输入**：`str = "We promptly judged antique ivory buckles for the prize"`
> 
> **输出**：否

**方法 1：不使用 STL**

这种方法基于散列。

1.  创建大小为 26 的布尔类型的哈希数据结构，以使索引 0 表示字符`"a"`，索引 1 表示字符`"b"`，依此类推。

2.  逐字符遍历字符串，并将特定字符标记为哈希中的字符。

3.  在完成遍历和标记字符串之后，遍历哈希并查看是否存在所有字符，即每个索引都为`true`。 如果都标记了，则返回`true`，否则返回`False`。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to check if the given 
// string is a pangram or not 

#include <bits/stdc++.h> 
using namespace std; 

// Returns true if the string is 
// pangram else false 
bool checkPangram(string& str) 
{ 
    // Create a hash table to mark 
    // the characters 
    // present in the string 
    vector<bool> mark(26, false); 

    // For indexing in mark[] 
    int index; 

    // Traverse all characters 
    for (int i = 0; i < str.length(); i++) { 

        // If uppercase character, 
        // subtract 'A' to find index. 
        if ('A' <= str[i] && str[i] <= 'Z') 
            index = str[i] - 'A'; 

        // If lowercase character, 
        // subtract 'a' to find index. 
        else if ('a' <= str[i] 
                 && str[i] <= 'z') 
            index = str[i] - 'a'; 

        // If this character is not 
        // an alphabet, skip to next one. 
        else
            continue; 

        mark[index] = true; 
    } 

    // Return false 
    // if any character is unmarked 
    for (int i = 0; i <= 25; i++) 
        if (mark[i] == false) 
            return (false); 

    // If all characters were present 
    return (true); 
} 

// Driver Code 
int main() 
{ 
    string str = "We promptly judged"
                 " antique ivory"
                 " buckles for the next prize"; 

    if (checkPangram(str) == true) 
        printf("Yes"); 
    else
        printf("No"); 

    return (0); 
}

```

**输出**：

```
Yes
```

**时间复杂度**：`O(n)`，其中`N`为字符串的长度。

**辅助空间**：`O(1)`

**方法 2**：使用 [**STL**](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)

STL 的[`transform()`方法](https://www.geeksforgeeks.org/transform-c-stl-perform-operation-elements/)可用于检查给定的字符串是否为 Pangram。

**语法**：

```
transform(s.begin(), s.end(), s.begin(), ::toupper);
```

**方法**：

为了检查字符串是否包含英语字母的所有字母：

> **步骤 1**：首先将所有字母都转换为大写或小写，因为如果不进行转换就进行检查，则将小写和大写字母视为不同的字母。
> **步骤 2**：对字符串进行排序并检查不同的字母。
> **步骤 3**：空间也将被视为一个独立的实体。
> **步骤 4**：现在检查是否`count = 27`，则该字符串包含所有 26 个字母。

下面是上述方法的实现：

## CPP

```

// C++ Program to check whether 
// a string pangram or not using STL 

#include <bits/stdc++.h> 
using namespace std; 

// Function to return given string 
// str is pangrams yes or no 
string pangrams(string s) 
{ 

    // Initialization of count 
    int count = 0; 

    // Convert each letter into 
    // uppercase to avoid counting 
    // of both uppercase and 
    // lowercase as different letters 
    transform(s.begin(), 
              s.end(), 
              s.begin(), 
              ::toupper); 

    // Sort the string 
    sort(s.begin(), s.end()); 

    // Count distinct alphabets 
    for (int i = 0; i < s.size(); i++) { 
        if (s[i] != s[i + 1]) 
            count++; 
    } 

    // If count is 27 then the string 
    // contains all the alphabets 
    // including space as a 
    // distinct character 
    if (count == 27) 
        return "Yes"; 

    else
        return "No"; 
} 

// Driver code 
int main() 
{ 
    // Given string str 
    string str = "We promptly "
                 "judged antique"
                 "ivory buckles for "
                 "the next prize"; 

    // Function Call 
    cout << pangrams(str); 

    return 0; 
}

```

**输出**：

```
Yes
```

**时间复杂度**：`O(N)`，其中`N`为字符串的长度。

**辅助空间**：`O(1)`



* * *

* * *



