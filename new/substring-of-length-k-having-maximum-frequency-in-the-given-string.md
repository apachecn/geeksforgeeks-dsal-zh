# 在给定字符串中具有最大频率的长度为`K`的子字符串

> 原文：[https://www.geeksforgeeks.org/substring-of-length-k-having-maximum-frequency-in-the-given-string/](https://www.geeksforgeeks.org/substring-of-length-k-having-maximum-frequency-in-the-given-string/)



给定字符串`str`，任务是找到出现次数最多的长度为`K`的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)。 如果多个字符串出现最多，请打印按字典顺序最小的子字符串。

**示例**：

> **输入**：`str = "bbbbbaaaaabbabababa", K = 5`
>
> **输出**：`ababa`
>
> **说明**：
>
> 长度为 5 的子字符串 上面的字符串是`{bbbbb, bbbba, bbbaa, bbaaa, baaaa, aaaaa, aaaab, aaabb, aabba, abbab, bbaba, babab, ababa, babab, ababa}`。
>
> 在所有字符串中，子字符串`{ababa, babab}`占最大次数（为 2）。
>
> 从`{ababa, babab}`开始的词典上最小的字符串是`ababa`。
>
> 因此，`"ababa"`是所需答案。
> 
> **输入**：`str = "heisagoodboy", K = 5`
>
> **输出**：`agood`
>
> **说明**：
>
> 长度为 5 的子字符串 上面的字符串是`{heisa, eisag, isago, sagoo, agood, goodb, oodbo, odboy}`。
>
> 所有这些仅发生一次。 但是，按字典顺序，最小的字符串是`"agood"`。
>
> 因此，`"agood"`是必需的答案。

**朴素的方法**：解决问题的最简单方法是[从给定的字符串中生成大小为 **K** 的所有子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并将每个子字符串的频率存储在一个[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。 然后，遍历**映射**并找到出现次数最多的字典上最小的子字符串并将其打印出来。

**时间复杂度**：`O(N *(K + log K))`

**辅助空间**：`O(N * K)`

**有效方法**：为了优化上述方法，其想法是使用[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)。 考虑一个大小为`K`的窗口，[来生成长度为`K`的所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中[计算生成的所有子字符串的频率](https://www.geeksforgeeks.org/frequency-substring-string/)。 遍历映射，找到出现次数最多的子字符串并打印。 如果它们中的几个存在，则按字典顺序打印[最小的子字符串](https://www.geeksforgeeks.org/lexicographically-next-string/)。

下面是上述方法的实现。

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using ll = long long int; 
using namespace std; 

// Function that generates substring 
// of length K that occurs maximum times 
void maximumOccurringString(string s, ll K) 
{ 
    // Store the frequency of substrings 
    map<deque<char>, ll> M; 

    ll i; 

    // Deque to maintain substrings 
    // window size K 
    deque<char> D; 

    for (i = 0; i < K; i++) { 
        D.push_back(s[i]); 
    } 

    // Update the frequency of the 
    // first substring in the Map 
    M[D]++; 

    // Remove the first character of 
    // the previous K length substring 
    D.pop_front(); 

    // Traverse the string 
    for (ll j = i; j < s.size(); j++) { 

        // Insert the current character 
        // as last character of 
        // current substring 
        D.push_back(s[j]); 

        M[D]++; 

        // Pop the first character of 
        // previous K length substring 
        D.pop_front(); 
    } 

    ll maxi = INT_MIN; 

    deque<char> ans; 

    // Find the substring that occurs 
    // maximum number of times 
    for (auto it : M) { 
        if (it.second > maxi) { 
            maxi = it.second; 
            ans = it.first; 
        } 
    } 

    // Print the substring 
    for (ll i = 0; i < ans.size(); i++) { 
        cout << ans[i]; 
    } 
} 

// Driver Code 
int main() 
{ 
    // Given string 
    string s = "bbbbbaaaaabbabababa"; 

    // Given K size of substring 
    ll K = 5; 

    // Function Call 
    maximumOccurringString(s, K); 

    return 0; 
} 

```

## Python3

```py

# Python3 program for the above approach 
from collections import deque, Counter, defaultdict 
import sys 

# Function that generates substring 
# of length K that occurs maximum times 
def maximumOccurringString(s, K): 

    # Store the frequency of substrings 
    M = {} 

    # Deque to maintain substrings 
    # window size K 
    D = deque() 

    for i in range(K): 
        D.append(s[i]) 

    # Update the frequency of the 
    # first subin the Map 
    # E="".join(list(D 
    M[str("".join(list(D)))] = M.get( 
        str("".join(list(D))), 0) + 1

    # Remove the first character of 
    # the previous K length substring 
    D.popleft() 

    # Traverse the string 
    for j in range(i, len(s)): 

        # Insert the current character 
        # as last character of 
        # current substring 
        D.append(s[j]) 

        M[str("".join(list(D)))] = M.get( 
            str("".join(list(D))), 0) + 1

        # Pop the first character of 
        # previous K length substring 
        D.popleft() 

    maxi = -sys.maxsize - 1

    ans = deque() 

    # Find the subthat occurs 
    # maximum number of times 
    # print(M) 
    for it in M: 

        # print(it[0]) 
        if (M[it] >= maxi): 
            maxi = M[it] 

            # print(maxi) 
            ans = it 

    # Print the substring 
    for i in range(len(ans)): 
        print(ans[i], end = "") 

# Driver Code 
if __name__ == '__main__': 

    # Given string 
    s = "bbbbbaaaaabbabababa"

    # Given K size of substring 
    K = 5

    # Function call 
    maximumOccurringString(s, K) 

# This code is contributed by mohit kumar 29

```

**输出**： 

```
ababa

```

**时间复杂度**：`O((N - K)* log(N - K))`

**辅助空间**：`O(N - K)`



* * *

* * *



