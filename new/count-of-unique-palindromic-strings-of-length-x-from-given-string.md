# 给定字符串

> 原文：[https://www.geeksforgeeks.org/count-of-unique-palindromic-strings-of-length-x-from-given-string/](https://www.geeksforgeeks.org/count-of-unique-palindromic-strings-of-length-x-from-given-string/)

中长度为 X 的唯一回文字符串的计数

给定**字符串 s** 和**整数 X** ，我们的任务是从给定字符串中找到长度为 X 的不同回文字符串的数量。

**示例**：

> **输入**：s =“ aaa”，X = 2
> **输出**：1
> **说明**：
> 这里的字符串的所有字符 是相同的，因此我们只能制作一个长度为 2 的不同字符串{aa}。
> 
> **输入**：s =“ aabaabbc”，X = 3
> **输出**：6
> **说明**：
> 制作长度为回文的字符串 3 我们有 6 个可能的字符串 aaa，aba，aca，bab，bcb，bbb。

**朴素的方法**：朴素的方法是生成长度 X 的所有可能子序列，然后检查该子序列是否形成回文。

**时间复杂度**：O（2 <sup>N</sup> ）

**辅助空间**：O（X）

**高效方法**：想法是找到字符串中所有字符的 [**频率**](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/) 。 计算可以放在特定位置的字符的不同数量，并将计数数量减少 2，因为回文字符串的位置**（i）和（X – i）**相同。 如果 X 的长度为奇数，则我们必须在该位置 X / 2 处放置唯一的一个字符。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to count different 
// palindromic string of length X 
// from the given string S 

#include <bits/stdc++.h> 
using namespace std; 

// Function to count different 
// palindromic string of length X 
// from the given string S 
long long findways(string s, int x) 
{ 
    // Base case 
    if (x > (int)s.length()) 
        return 0; 

    long long int n = (int)s.length(); 

    // Create the frequency array 
    int freq[26]; 

    // Intitalise frequency array with 0 
    memset(freq, 0, sizeof freq); 

    // Count the frequency in the string 
    for (int i = 0; i < n; ++i) 
        freq[s[i] - 'a']++; 

    multiset<int> se; 

    for (int i = 0; i < 26; ++i) 
        if (freq[i] > 0) 
            // Store frequency of the char 
            se.insert(freq[i]); 

    long long ans = 1; 

    for (int i = 0; i < x / 2; ++i) { 
        long long int count = 0; 
        for (auto u : se) { 
            // check the frequency which 
            // is greater than zero 
            if (u >= 2) 

                // No. of different char we can 
                // put at the position of 
                // the i and x - i 
                count++; 
        } 

        if (count == 0) 
            return 0; 

        else
            ans = ans * count; 

        // Iterator pointing to the 
        // last element of the set 
        auto p = se.end(); 
        p--; 
        int val = *p; 
        se.erase(p); 
        if (val > 2) 
            // decrease the value of the char 
            // we put on the position i and n - i 
            se.insert(val - 2); 
    } 

    if (x % 2 != 0) { 
        long long int count = 0; 
        for (auto u : se) 
            // different no of char we can 
            // put at the position x/2 
            if (u > 0) 
                count++; 

        ans = ans * count; 
    } 

    // Return total no of 
    // different string 
    return ans; 
} 

// Driver code 
int main() 
{ 
    string s = "aaa"; 
    int x = 2; 
    cout << findways(s, x); 

    return 0; 
} 

```

## Python3

```py

# Python3 implementation to count  
# different palindromic string of 
# length X from the given string S 

# Function to count different 
# palindromic string of length X 
# from the given string S 
def findways(s, x): 

    # Base case 
    if(x > len(s)): 
        return 0

    n = len(s) 

    # Create the frequency array 
    # Intitalise frequency array with 0 
    freq = [0] * 26

    # Count the frequency in the string 
    for i in range(n): 
        freq[ord(s[i]) - ord('a')] += 1

    se = set() 

    for i in range(26): 
        if(freq[i] > 0): 

            # Store frequency of the char 
            se.add(freq[i]) 

    ans = 1
    for i in range(x // 2): 
        count = 0
        for u in se: 

            # Check the frequency which 
            # is greater than zero 
            if(u >= 2): 

                # No. of different char we can 
                # put at the position of 
                # the i and x - i 
                count += 1

        if(count == 0): 
            return 0
        else: 
            ans *= count 

        # Iterator pointing to the 
        # last element of the set 
        p = list(se) 
        val = p[-1] 
        p.pop(-1) 
        se = set(p) 

        if(val > 2): 

            # Decrease the value of the char 
            # we put on the position i and n - i 
            se.add(val - 2) 

    if(x % 2 != 0): 
        count = 0
        for u in se: 

            # Different no of char we can 
            # put at the position x/2 
            if(u > 0): 
                count += 1

        ans = ans * count 

    # Return total no of 
    # different string  
    return ans 

# Driver code 
if __name__ == '__main__': 

    s = "aaa"
    x = 2

    print(findways(s, x)) 

# This code is contributed by Shivam Singh 

```

**Output:**

```
1

```

**时间复杂度**：O（N + 26 * X）



* * *

* * *



