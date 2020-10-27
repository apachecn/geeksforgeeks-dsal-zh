# 子字符串的最小长度，其旋转会生成回文子字符串

给定字符串 **str** ，任务是找到旋转所需的子字符串的最小长度，以从给定字符串生成回文子字符串。

**示例：**

> **输入：** str =“ abcbd”
> **输出：** 0
> **说明：**无法生成回文子字符串，字符串中没有重复字符 。
> 
> **输入：** str =“ abcdeba”
> **输出：** 3
> **说明：**旋转子字符串“ deb”将给定的字符串转换为 **bcb** eda，回文子串为“ bcb”。

**方法：**

*   如果字符串中没有重复字符，则不会生成回文子字符串。
*   对于每个重复字符，请检查其先前出现的索引是否在当前索引的一两个索引内。 如果是这样，则回文子串已经存在。
*   否则，计算**的长度（当前索引–先前出现的索引– 1）**。
*   返回所有此类长度中的最小值作为答案

下面是上述方法的实现：

## C++

```cpp

// C++ Program to find the minimum 
// length of substring whose rotation 
// generates a palindromic substring 

#include <bits/stdc++.h> 
using namespace std; 

// Function to return the 
// minimum lenth of substring 
int count_min_length(string s) 
{ 

    // Store the index of 
    // previous occurrence 
    // of the character 
    int hash[26]; 

    // Variable to store 
    // the maximum length 
    // of substring 
    int ans = INT_MAX; 

    for (int i = 0; i < 26; i++) 
        hash[i] = -1; 

    for (int i = 0; i < s.size(); i++) { 
        // If the current character 
        // hasn't appeared yet 
        if (hash[s[i] - 'a'] == -1) 
            hash[s[i] - 'a'] = i; 
        else { 
            // If the character has occured 
            // within one or two previous 
            // index, a palindromic substring 
            // already exists 
            if (hash[s[i] - 'a'] == i - 1 
                || hash[s[i] - 'a'] == i - 2) 
                return 0; 

            // Update the maximum 
            ans = min(ans, 
                      i - hash[s[i] - 'a'] - 1); 

            // Replace the previous 
            // index of the character by 
            // the current index 
            hash[s[i] - 'a'] = i; 
        } 
    } 

    // If character appeared 
    // at least twice 
    if (ans == INT_MAX) 
        return -1; 

    return ans; 
} 
// Driver Code 
int main() 
{ 
    string str = "abcdeba"; 
    cout << count_min_length(str); 
} 

```

## Java

```java

// Java Program to find the minimum 
// length of substring whose rotation 
// generates a palindromic substring 
import java.util.*; 
import java.lang.*; 
class GFG{ 

// Function to return the 
// minimum lenth of substring 
static int count_min_length(String s) 
{ 

    // Store the index of 
    // previous occurrence 
    // of the character 
    int[] hash = new int[26]; 

    // Variable to store 
    // the maximum length 
    // of substring 
    int ans = Integer.MAX_VALUE; 

    for (int i = 0; i < 26; i++) 
        hash[i] = -1; 

    for (int i = 0; i < s.length(); i++)  
    { 
        // If the current character 
        // hasn't appeared yet 
        if (hash[s.charAt(i) - 'a'] == -1) 
            hash[s.charAt(i) - 'a'] = i; 
        else 
        { 
            // If the character has occured 
            // within one or two previous 
            // index, a palindromic substring 
            // already exists 
            if (hash[s.charAt(i) - 'a'] == i - 1 ||  
                hash[s.charAt(i) - 'a'] == i - 2) 
                return 0; 

            // Update the maximum 
            ans = Math.min(ans,  
                       i - hash[s.charAt(i) - 'a'] - 1); 

            // Replace the previous 
            // index of the character by 
            // the current index 
            hash[s.charAt(i) - 'a'] = i; 
        } 
    } 

    // If character appeared 
    // at least twice 
    if (ans == Integer.MAX_VALUE) 
        return -1; 

    return ans; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    String str = "abcdeba"; 

    System.out.println(count_min_length(str)); 
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program to find the minimum  
# length of substring whose rotation  
# generates a palindromic substring  
import sys 

INT_MAX = sys.maxsize; 

# Function to return the  
# minimum lenth of substring  
def count_min_length(s):  

    # Store the index of  
    # previous occurrence  
    # of the character  
    hash = [0] * 26;  

    # Variable to store  
    # the maximum length  
    # of substring  
    ans = sys.maxsize;  

    for i in range(26): 
        hash[i] = -1;  

    for i in range(len(s)): 

        # If the current character  
        # hasn't appeared yet  
        if (hash[ord(s[i]) - ord('a')] == -1): 
            hash[ord(s[i]) - ord('a')] = i;  
        else : 

            # If the character has occured  
            # within one or two previous  
            # index, a palindromic substring  
            # already exists  
            if (hash[ord(s[i]) - ord('a')] == i - 1 or 
                hash[ord(s[i]) - ord('a')] == i - 2) : 
                return 0;  

            # Update the maximum  
            ans = min(ans, i - hash[ord(s[i]) - 
                                    ord('a')] - 1);  

            # Replace the previous  
            # index of the character by  
            # the current index  
            hash[ord(s[i]) - ord('a')] = i;  

    # If character appeared  
    # at least twice  
    if (ans == INT_MAX): 
        return -1;  

    return ans;  

# Driver Code  
if __name__ == "__main__":  

    string = "abcdeba";  

    print(count_min_length(string));  

# This code is contributed by AnkitRai01 

```

## C#

```cs

// C# Program to find the minimum 
// length of substring whose rotation 
// generates a palindromic substring 
using System; 
class GFG{ 

// Function to return the 
// minimum lenth of substring 
static int count_min_length(string s) 
{ 

    // Store the index of 
    // previous occurrence 
    // of the character 
    int[] hash = new int[26]; 

    // Variable to store 
    // the maximum length 
    // of substring 
    int ans = int.MaxValue; 

    for (int i = 0; i < 26; i++) 
        hash[i] = -1; 

    for (int i = 0; i < s.Length; i++)  
    { 
        // If the current character 
        // hasn't appeared yet 
        if (hash[s[i] - 'a'] == -1) 
            hash[s[i] - 'a'] = i; 
        else
        { 
            // If the character has occured 
            // within one or two previous 
            // index, a palindromic substring 
            // already exists 
            if (hash[s[i] - 'a'] == i - 1 ||  
                hash[s[i] - 'a'] == i - 2) 
                return 0; 

            // Update the maximum 
            ans = Math.Min(ans,  
                      i - hash[s[i] - 'a'] - 1); 

            // Replace the previous 
            // index of the character by 
            // the current index 
            hash[s[i] - 'a'] = i; 
        } 
    } 

    // If character appeared 
    // at least twice 
    if (ans == int.MaxValue) 
        return -1; 

    return ans; 
} 

// Driver code 
public static void Main(string[] args) 
{ 
    string str = "abcdeba"; 

    Console.WriteLine(count_min_length(str)); 
} 
} 

// This code is contributed by AnkitRai01 

```

**Output:**

```
3

```

**时间复杂度：** *O（N）*

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



