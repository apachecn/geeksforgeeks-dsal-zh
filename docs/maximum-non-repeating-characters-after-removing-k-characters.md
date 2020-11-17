# 删除`K`个字符后的最大非重复字符数

> 原文：[https://www.geeksforgeeks.org/maximum-non-repeating-characters-after-removing-k-characters/](https://www.geeksforgeeks.org/maximum-non-repeating-characters-after-removing-k-characters/)

给定一个字符串`S`，其中包含长度为`N`的小写英语字母和一个整数`K`，使得`K ≤ N`。 任务是从字符串中删除`K`个字符后，找到最大数目的非重复字符。

**示例**：

> **输入**：`S = "geeksforgeeks", K = 3`
>
> **输出**：6
>
> **说明**：
>
> 删除出现 1 次的每个`g`，`k`和`s`，因此最终字符串为`"geeksforee`，而 6 个不同的元素为`g, k, s, f, o, r`。
> 
> **输入**：`S = "aabbccddeeffgghh", k = 1`
>
> **输出**：1
>
> **说明**：
>
> 删除任何字符的一次出现，只会有一个不会重复的字符。

**朴素的方法**：朴素的想法是删除给定字符串中所有可能的`K`个字符，然后在所有生成的字符串中找到非重复字符。 打印所有非重复字符中的最大值。

**时间复杂度**：`O(N!)`，其中`N`是给定字符串的长度。

**辅助空间**：`O(N - K)`。

**有效方法**：为了优化上述方法，

> [这个想法是按照频率的递增顺序删除`K`个字符，该频率至少为 2，以获得最大非重复字符数](https://www.geeksforgeeks.org/sort-a-string-according-to-the-frequency-of-characters/)。

步骤如下：

1.  创建一个[哈希表](https://www.geeksforgeeks.org/hashing-data-structure/)来[存储每个元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)。

2.  将每个元素的[频率](https://www.geeksforgeeks.org/program-to-find-frequency-of-each-element-in-a-vector-using-map-in-c/)插入向量`V`中，[以升序对向量`V`排序](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)。

3.  对于向量`V`的每个元素（例如`currentElement`），在`K`和`currentElement - 1`中找到最小值，并同时降低`K`和`V[i]`两者中的最小值。

4.  重复上述步骤，直到`K`不为零。

5.  向量`V`中`1s`的计数给出了删除`K`个字符后的最大非重复字符数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find maximum distinct 
// character after removing K character 
int maxDistinctChar(string s, int n, int k) 
{ 
    // Freq implemented as hash table to 
    // store frequency of each character 
    unordered_map<int, int> freq; 

    // Store frequency of each character 
    for (int i = 0; i < n; i++) 
        freq[s[i]]++; 

    vector<int> v; 

    // Insert each frequency in v 
    for (auto it = freq.begin(); 
         it != freq.end(); it++) { 
        v.push_back(it->second); 
    } 

    // Sort the freq of character in 
    // non-decresing order 
    sort(v.begin(), v.end()); 

    // Traverse the vector 
    for (int i = 0; i < v.size(); i++) { 
        int mn = min(v[i] - 1, k); 

        // Update v[i] and k 
        v[i] -= mn; 
        k -= mn; 
    } 

    // If K is still not 0 
    if (k > 0) { 

        for (int i = 0; i < v.size(); i++) { 
            int mn = min(v[i], k); 
            v[i] -= mn; 
            k -= mn; 
        } 
    } 

    // Store the final answer 
    int res = 0; 
    for (int i = 0; i < v.size(); i++) 

        // Count this character if freq 1 
        if (v[i] == 1) 
            res++; 

    // Return count of distinct characters 
    return res; 
} 

// Driver Code 
int main() 
{ 
    // Given string 
    string S = "geeksforgeeks"; 

    int N = S.size(); 

    // Given k 
    int K = 1; 

    // Function Call 
    cout << maxDistinctChar(S, N, K); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 
class GFG{ 

// Function to find maximum distinct 
// character after removing K character 
static int maxDistinctChar(char []s, int n, int k) 
{ 
    // Freq implemented as hash table to 
    // store frequency of each character 
    HashMap<Integer, 
            Integer> freq  = new HashMap<Integer, 
                                         Integer>(); 

    // Store frequency of each character 
    for (int i = 0; i < n; i++)  
    { 
        if(freq.containsKey((int)s[i])) 
        { 
            freq.put((int)s[i],  
                     freq.get((int)s[i]) + 1); 
        } 
        else
        { 
            freq.put((int)s[i], 1); 
        } 
    } 

    Vector<Integer> v = new Vector<Integer>(); 

    // Insert each frequency in v 
    for (Map.Entry<Integer, Integer> it : freq.entrySet())  
    { 
        v.add(it.getValue()); 
    } 

    // Sort the freq of character in 
    // non-decresing order 
    Collections.sort(v); 

    // Traverse the vector 
    for (int i = 0; i < v.size(); i++)  
    { 
        int mn = Math.min(v.get(i) - 1, k); 

        // Update v[i] and k 
        v.set(i, v.get(i) - mn); 
        k -= mn; 
    } 

    // If K is still not 0 
    if (k > 0)  
    { 
        for (int i = 0; i < v.size(); i++)  
        { 
            int mn = Math.min(v.get(i), k); 
            v.set(i, v.get(i) - mn); 
            k -= mn; 
        } 
    } 

    // Store the final answer 
    int res = 0; 
    for (int i = 0; i < v.size(); i++) 

        // Count this character if freq 1 
        if (v.get(i) == 1) 
            res++; 

    // Return count of distinct characters 
    return res; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    // Given String 
    String S = "geeksforgeeks"; 

    int N = S.length(); 

    // Given k 
    int K = 1; 

    // Function Call 
    System.out.print(maxDistinctChar(S.toCharArray(),  
                                     N, K)); 
} 
} 

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program for the above approach 
from collections import defaultdict 

# Function to find maximum distinct 
# character after removing K character 
def maxDistinctChar(s, n, k): 

    # Freq implemented as hash table to 
    # store frequency of each character 
    freq = defaultdict (int) 

    # Store frequency of each character 
    for i in range (n): 
        freq[s[i]] += 1

    v = [] 

    # Insert each frequency in v 
    for it in freq.values(): 
        v.append(it) 

    # Sort the freq of character in 
    # non-decresing order 
    v.sort() 

    # Traverse the vector 
    for i in range (len(v)): 
        mn = min(v[i] - 1, k) 

        # Update v[i] and k 
        v[i] -= mn 
        k -= mn 

    # If K is still not 0 
    if (k > 0): 
        for i in range (len(v)): 
            mn = min(v[i], k); 
            v[i] -= mn 
            k -= mn 

    # Store the final answer 
    res = 0
    for i in range (len(v)): 

        # Count this character if freq 1 
        if (v[i] == 1): 
            res += 1

    # Return count of distinct characters 
    return res 

# Driver Code 
if __name__ == "__main__": 

    # Given string 
    S = "geeksforgeeks"

    N = len(S) 

    # Given k 
    K = 1

    # Function Call 
    print(maxDistinctChar(S, N, K)) 

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find maximum distinct 
// character after removing K character 
static int maxDistinctChar(char []s, int n, int k) 
{ 

    // Freq implemented as hash table to 
    // store frequency of each character 
    Dictionary<int, 
               int> freq = new Dictionary<int, 
                                          int>(); 

    // Store frequency of each character 
    for(int i = 0; i < n; i++)  
    { 
        if(freq.ContainsKey((int)s[i])) 
        { 
            freq[(int)s[i]] = freq[(int)s[i]] + 1; 
        } 
        else
        { 
            freq.Add((int)s[i], 1); 
        } 
    } 

    List<int> v = new List<int>(); 

    // Insert each frequency in v 
    foreach(KeyValuePair<int, int> it in freq)  
    { 
        v.Add(it.Value); 
    } 

    // Sort the freq of character in 
    // non-decresing order 
    v.Sort(); 

    // Traverse the vector 
    for(int i = 0; i < v.Count; i++)  
    { 
        int mn = Math.Min(v[i] - 1, k); 

        // Update v[i] and k 
        v[i] = v[i] - mn; 
        k -= mn; 
    } 

    // If K is still not 0 
    if (k > 0)  
    { 
        for(int i = 0; i < v.Count; i++)  
        { 
            int mn = Math.Min(v[i], k); 
            v[i] = v[i] - mn; 
            k -= mn; 
        } 
    } 

    // Store the readonly answer 
    int res = 0; 
    for(int i = 0; i < v.Count; i++) 

        // Count this character if freq 1 
        if (v[i] == 1) 
            res++; 

    // Return count of distinct characters 
    return res; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 

    // Given String 
    String S = "geeksforgeeks"; 

    int N = S.Length; 

    // Given k 
    int K = 1; 

    // Function call 
    Console.Write(maxDistinctChar(S.ToCharArray(),  
                                  N, K)); 
} 
} 

// This code is contributed by Amit Katiyar

```

**输出**： 

```
4

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(26)`。



* * *

* * *



