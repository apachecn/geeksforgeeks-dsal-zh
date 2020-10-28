# 从数组

> 原文：[https://www.geeksforgeeks.org/find-the-longest-string-that-can-be-made-up-of-other-strings-from-the-array/](https://www.geeksforgeeks.org/find-the-longest-string-that-can-be-made-up-of-other-strings-from-the-array/)

中查找可以由其他字符串组成的最长字符串

给定一个字符串数组 **arr []** ，任务是在将数组中的其他字符串相互串联后，从数组中找到最大的字符串。 如果不存在这样的字符串，则打印 **-1** 。

**示例**：

> **输入**：arr [] = {“ geeks”，“ for”，“ geeksfor”，“ geeksforgeeks”}
> **输出**：geeksforgeeks
> （“极客” +“ for” +“极客”）。
> 即使“ geeksfor”也由其他字符串组成
> ，但它不是最大的字符串。
> 
> **输入**：arr [] = {“嘿”，“你”，“停止”，“右边”，“那里”}
> **输出**：-1

**方法**：

1.  [根据字符串的长度按降序对](https://www.geeksforgeeks.org/sort-c-stl/)进行排序。

2.  现在，从最长的字符串开始。 检查字符串的所有可能前缀是否存在于给定数组中以及字符串的其余部分，然后递归检查它是否可以由数组中的其他字符串组成。

3.  [映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)可用于检查数组中是否存在字符串。 满足上述条件的第一个字符串就是答案。

4.  如果不存在这样的字符串，则打印-1。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Comparator to sort the string by 
// their lengths in decreasing order 
bool compare(string s1, string s2) 
{ 
    return s1.size() > s2.size(); 
} 

// Function that returns true if string s can be 
// made up of by other two string from the array 
// after concatenating one after another 
bool canbuildword(string& s, bool isoriginalword, 
                  map<string, bool>& mp) 
{ 

    // If current string has been processed before 
    if (mp.find(s) != mp.end() && mp[s] == 0) 
        return false; 

    // If current string is found in the map and 
    // it is not the string under consideration 
    if (mp.find(s) != mp.end() && mp[s] == 1 
        && isoriginalword == 0) { 
        return true; 
    } 

    for (int i = 1; i < s.length(); i++) { 

        // Split the string into two 
        // contiguous sub-strings 
        string left = s.substr(0, i); 
        string right = s.substr(i); 

        // If left sub-string is found in the map and 
        // the right sub-string can be made from 
        // the strings from the given array 
        if (mp.find(left) != mp.end() && mp[left] == 1 
            && canbuildword(right, 0, mp)) { 
            return true; 
        } 
    } 

    // If everything failed, we return false 
    mp[s] = 0; 
    return false; 
} 

// Function to return the longest string 
// that can made be made up from the 
// other string of the given array 
string printlongestword(vector<string> listofwords) 
{ 

    // Put all the strings in the map 
    map<string, bool> mp; 
    for (string s : listofwords) { 
        mp[s] = 1; 
    } 

    // Sort the string in decreasing 
    // order of their lengths 
    sort(listofwords.begin(), listofwords.end(), compare); 

    // Starting from the longest string 
    for (string s : listofwords) { 

        // If current string can be made 
        // up from other strings 
        if (canbuildword(s, 1, mp)) 
            return s; 
    } 

    return "-1"; 
} 

// Driver code 
int main() 
{ 
    vector<string> listofwords = { "geeks", "for", "geeksfor", 
                                   "geeksforgeeks" }; 
    cout << printlongestword(listofwords); 

    return 0; 
} 

```

## Python3

```py

# Python implementation of the approach 

# Function that returns true if string s can be 
# made up of by other two string from the array 
# after concatenating one after another 
def canbuildword(s, isoriginalword, mp): 

    # If current string has been processed before 
    if s in mp and mp[s] == 0: 
        return False

    # If current string is found in the map and 
    # it is not the string under consideration 
    if s in mp and mp[s] == 1 and isoriginalword == 0: 
        return True

    for i in range(1, len(s)): 

        # Split the string into two 
        # contiguous sub-strings 
        left = s[:i] 
        right = s[i:] 

        # If left sub-string is found in the map and 
        # the right sub-string can be made from 
        # the strings from the given array 
        if left in mp and mp[left] == 1 and canbuildword(right, 0, mp): 
            return True

    # If everything failed, we return false 
    mp[s] = 0
    return False

# Function to return the longest string 
# that can made be made up from the 
# other string of the given array 
def printlongestword(listofwords): 

    # Put all the strings in the map 
    mp = dict() 
    for i in listofwords: 
        mp[i] = 1

    # Sort the string in decreasing 
    # order of their lengths 
    listofwords.sort(key=lambda x: len(x), reverse=True) 

    # Starting from the longest string 
    for i in listofwords: 

        # If current string can be made 
        # up from other strings 
        if canbuildword(i, 1, mp): 
            return i 

    return "-1"

# Driver code 
if __name__ == "__main__": 
    listofwords = ["geeks", "for", "geeksfor", 
                "geeksforgeeks"] 

    print(printlongestword(listofwords)) 

# This code is contributed by 
# sanjeev2552 

```

**Output:**

```
geeksforgeeks

```



* * *

* * *



