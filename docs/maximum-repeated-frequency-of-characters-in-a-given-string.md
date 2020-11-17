# 给定字符串中字符的最大重复频率

> 原文：[https://www.geeksforgeeks.org/maximum-repeated-frequency-of-characters-in-a-given-string/](https://www.geeksforgeeks.org/maximum-repeated-frequency-of-characters-in-a-given-string/)

给定字符串`S`，任务是查找给定字符串`S`中字符的最大重复频率计数。

**示例**：

> **输入**：`S = "geeksgeeks"`
>
> **输出**：频率 2 重复 3 次。
>
> **说明**：
>
> 给定字符的频率字符串：
>
> `{"g":2, "e”:4, "k":2, "s":2}`
>
> 频率 2 对于字符`"g"`，`"k"`，`"s"`重复三次。
> 
> **输入**：`S = "abcabcdedee"`
>
> **输出**：频率 2 重复 4 次。
>
> **说明**：
>
> 给定字符串中字符的频率：
>
> `{"a": 2, "b": 2, "c": 2, "d": 2, "e", 3}`
>
> 频率 2 对于字符`"a"`，`"b"`，`"c"`，`"d"`重复四次。

**有效方法**：

*   这个想法是首先将字符串的字符频率存储在大小为 26 的数组中。由于字符串的所有字符都在 26 个小写英文字母之间，因此我们可以将字符的频率存储在大小为 26 的数组中。

*   创建一个哈希映射，以存储字符的频率计数并返回出现次数最多的频率。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the 
// maximum repeated frequency of  
// characters in the given string 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the maximum 
// repeated frequency of the  
// characters in the given string 
void findMaxFrequency(string s) 
{ 
    // Hash-Array to store the  
    // frequency of characters 
    int arr[26] = { 0 }; 

    // Loop to find the frequency 
    // of the characters 
    for (int i = 0; i < s.length(); i++) 
        arr[s[i] - 'a']++; 

    // Hash map to store the occurrence 
    // of frequencies of characters 
    unordered_map<int, int> hash; 
    for (int i = 0; i < 26; i++) 
        if (arr[i] != 0) 
            hash[arr[i]]++; 

    // Loop to find the maximum 
    // Repeated frequency from hash-map 
    int max_count = 0, res = -1; 
    for (auto i : hash) { 
        if (max_count < i.second) { 
            res = i.first; 
            max_count = i.second; 
        } 
    } 

    cout <<"Frequency " << res << " is repeated " 
         << max_count<<" times"; 
} 

// Driver Code 
int main() 
{ 
    string s = "geeksgeeks"; 

    // Function Call 
    findMaxFrequency(s); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the 
// maximum repeated frequency of  
// characters in the given String 
import java.util.*; 

class GFG{ 

// Function to find the maximum 
// repeated frequency of the  
// characters in the given String 
static void findMaxFrequency(String s) 
{ 
    // Hash-Array to store the  
    // frequency of characters 
    int arr[] = new int[26]; 

    // Loop to find the frequency 
    // of the characters 
    for (int i = 0; i < s.length(); i++) 
        arr[s.charAt(i) - 'a']++; 

    // Hash map to store the occurrence 
    // of frequencies of characters 
    HashMap<Integer,Integer> hash = new HashMap<Integer,Integer>(); 
    for (int i = 0; i < 26; i++) 
        if (arr[i] != 0) { 
            if(hash.containsKey(arr[i])){ 
                hash.put(arr[i], hash.get(arr[i])+1); 
            } 
            else{ 
                hash.put(arr[i], 1); 
            } 
        } 

    // Loop to find the maximum 
    // Repeated frequency from hash-map 
    int max_count = 0, res = -1; 
    for (Map.Entry<Integer,Integer> i : hash.entrySet()){ 
        if (max_count < i.getValue()) { 
            res = i.getKey(); 
            max_count = i.getValue(); 
        } 
    } 

    System.out.println("Frequency " + res+ " is repeated "
        + max_count+" times"); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    String s = "geeksgeeks"; 

    // Function Call 
    findMaxFrequency(s); 
} 
} 

// This code is contributed by sapnasingh4991 

```

## Python3

```py

# Python3 implementation to find the 
# maximum repeated frequency of  
# characters in the given string 

# Function to find the maximum 
# repeated frequency of the  
# characters in the given string 
def findMaxFrequency(s): 

    # Hash-Array to store the  
    # frequency of characters 

    arr = [0]*26

    # Loop to find the frequency 
    # of the characters 
    for i in range(len(s)): 
        arr[ord(s[i]) - ord('a')] += 1

    # Hash map to store the occurrence 
    # of frequencies of characters 

    hash = {} 
    for i in range(26): 
        if (arr[i] != 0): 
            if arr[i] not in hash: 
                hash[arr[i]] = 0
            hash[arr[i]] += 1

    # Loop to find the maximum 
    # Repeated frequency from hash-map 
    max_count = 0
    res = -1
    for i in hash: 
        if (max_count < hash[i]): 
            res = i 
            max_count = hash[i] 

    print("Frequency", res, "is repeated", max_count, "times") 

# Driver Code 

s = "geeksgeeks"

# Function Call 
findMaxFrequency(s) 

# This code is contributed by shubhamsingh10 

```

## C#

```cs

// C# implementation to find the 
// maximum repeated frequency of  
// characters in the given String 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the maximum 
// repeated frequency of the  
// characters in the given String 
static void findMaxFrequency(String s) 
{ 
    // Hash-Array to store the  
    // frequency of characters 
    int []arr = new int[26]; 

    // Loop to find the frequency 
    // of the characters 
    for (int i = 0; i < s.Length; i++) 
        arr[s[i] - 'a']++; 

    // Hash map to store the occurrence 
    // of frequencies of characters 
    Dictionary<int,int> hash = new Dictionary<int,int>(); 
    for (int i = 0; i < 26; i++) 
        if (arr[i] != 0) { 
            if(hash.ContainsKey(arr[i])){ 
                hash[arr[i]] = hash[arr[i]]+1; 
            } 
            else{ 
                hash.Add(arr[i], 1); 
            } 
        } 

    // Loop to find the maximum 
    // Repeated frequency from hash-map 
    int max_count = 0, res = -1; 
    foreach( KeyValuePair<int,int> i in hash){ 
        if (max_count < i.Value) { 
            res = i.Key; 
            max_count = i.Value; 
        } 
    } 

    Console.WriteLine("Frequency " + res+ " is repeated "
        + max_count+" times"); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    String s = "geeksgeeks"; 

    // Function Call 
    findMaxFrequency(s); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Frequency 2 is repeated 3 times

```

**效果分析**：

*   **时间复杂度**：`O(n)`。

*   **辅助空间**：`O(n)`。



* * *

* * *



