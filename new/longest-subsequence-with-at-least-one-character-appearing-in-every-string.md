# 最长子序列，每个字符串中至少出现一个字符

> 原文：[https://www.geeksforgeeks.org/longest-subsequence-with-at-least-one-character-appearing-in-every-string/](https://www.geeksforgeeks.org/longest-subsequence-with-at-least-one-character-appearing-in-every-string/)

给定一个字符串数组`arr[]`，任务是找到该数组的最长子序列，并且在所有字符串中至少出现一个字符。 **请注意**，所有字符串仅包含小写英文字母。

**示例**：

> **输入**：`str = {"ab", "bc", "de"}`
>
> **输出**：2
>
> `{"ab", "bc"}`是必需的子序列，带有`'b'`作为公共字符。
> 
> **输入**：`str = {"a", "b", "c"}`
>
> **输出**：1

**方法**：创建一个 **count []** 数组，以便 **count [0]** 将存储包含**'a'**的字符串数， **count [1]** 将存储包含**'b'**等的字符串的数量…

现在，很明显，答案将是**中的最大值 ] count []** 数组。 为了更新此数组，开始遍历字符串数组，对于每个字符串，在 **hash []** 数组中标记当前字符串中存在哪些字符。

遍历之后，对于当前字符串中存在的每个字符，更新其在 **count []** 数组中的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

#define MAX 26 

// Function to return the length of the longest 
// sub-sequence with at least one 
// common character in every string 
int largestSubSeq(string arr[], int n) 
{ 

    // count[0] will store the number of strings 
    // which contain 'a', count[1] will store the 
    // number of strings which contain 'b' and so on.. 
    int count[MAX] = { 0 }; 

    // For every string 
    for (int i = 0; i < n; i++) { 
        string str = arr[i]; 

        // Hash array to set which character is 
        // present in the current string 
        bool hash[MAX] = { 0 }; 
        for (int j = 0; j < str.length(); j++) { 
            hash[str[j] - 'a'] = true; 
        } 

        for (int j = 0; j < MAX; j++) { 

            // If current character appears in the 
            // string then update its count 
            if (hash[j]) 
                count[j]++; 
        } 
    } 

    return *(max_element(count, count + MAX)); 
} 

// Driver code 
int main() 
{ 
    string arr[] = { "ab", "bc", "de" }; 
    int n = sizeof(arr) / sizeof(string); 

    cout << largestSubSeq(arr, n); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 

class GFG 
{ 

    static int MAX = 26; 

    // Function to return the length of the longest 
    // sub-sequence with at least one 
    // common character in every string 
    static int largestSubSeq(String arr[], int n) 
    { 

        // count[0] will store the number of strings 
        // which contain 'a', count[1] will store the 
        // number of strings which contain 'b' and so on.. 
        int [] count = new int[MAX]; 

        // For every string 
        for (int i = 0; i < n; i++) { 
            String str = arr[i]; 

            // Hash array to set which character is 
            // present in the current string 
            boolean [] hash = new boolean[MAX]; 

            for (int j = 0; j < str.length(); j++) { 
                hash[str.charAt(j) - 'a'] = true; 
            } 

            for (int j = 0; j < MAX; j++) { 

                // If current character appears in the 
                // string then update its count 
                if (hash[j]) 
                    count[j]++; 
            } 
        } 

        int max = -1; 

        for(int i=0;i< MAX; i++) 
        { 
            if(max < count[i]) 
                max = count[i]; 
        } 
        return max; 
    } 

    // Driver code 
    public static void main (String[] args)  
    { 

        String arr[] = { "ab", "bc", "de" }; 
        int n = arr.length; 

        System.out.println(largestSubSeq(arr, n)); 

    } 

} 

// This code is contributed by ihritik 

```

## Python3

```py

# Python3 implementation of the approach  
MAX = 26

# Function to return the length of the longest  
# sub-sequence with at least one  
# common character in every string  
def largestSubSeq(arr, n): 

    # count[0] will store the number of strings  
    # which contain 'a', count[1] will store the  
    # number of strings which contain 'b' and so on..  
    count = [0] * MAX

    # For every string  
    for i in range(n): 
        string = arr[i] 

        # Hash array to set which character is  
        # present in the current string  
        _hash = [False] * MAX
        for j in range(len(string)): 
            _hash[ord(string[j]) - ord('a')] = True

        for j in range(MAX): 

            # If current character appears in the  
            # string then update its count  
            if _hash[j] == True: 
                count[j] += 1

    return max(count) 

# Driver code  
if __name__ == "__main__": 
    arr = [ "ab", "bc", "de" ] 
    n = len(arr) 
    print(largestSubSeq(arr, n)) 

# This code is contributed by 
# sanjeev2552 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

    static int MAX = 26; 

    // Function to return the length of the longest 
    // sub-sequence with at least one 
    // common character in every string 
    static int largestSubSeq(string [] arr, int n) 
    { 

        // count[0] will store the number of strings 
        // which contain 'a', count[1] will store the 
        // number of strings which contain 'b' and so on.. 
        int [] count = new int[MAX]; 

        // For every string 
        for (int i = 0; i < n; i++) 
        { 
            string str = arr[i]; 

            // Hash array to set which character is 
            // present in the current string 
            bool [] hash = new bool[MAX]; 

            for (int j = 0; j < str.Length; j++) 
            { 
                hash[str[j] - 'a'] = true; 
            } 

            for (int j = 0; j < MAX; j++)  
            { 

                // If current character appears in the 
                // string then update its count 
                if (hash[j]) 
                    count[j]++; 
            } 
        } 

        int max = -1; 

        for(int i=0;i< MAX; i++) 
        { 
            if(max < count[i]) 
                max = count[i]; 
        } 
        return max; 
    } 

    // Driver code 
    public static void Main ()  
    { 

        string [] arr = { "ab", "bc", "de" }; 
        int n = arr.Length; 

        Console.WriteLine(largestSubSeq(arr, n)); 
    } 
} 

// This code is contributed by ihritik 

```

**Output:**

```
2

```



* * *

* * *



