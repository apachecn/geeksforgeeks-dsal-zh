# 打印给定字符串的所有位置，该字符串的小写字符数在两侧均相等

> 原文：[https://www.geeksforgeeks.org/print-all-positions-of-a-given-string-having-count-of-smaller-characters-equal-on-both-sides/](https://www.geeksforgeeks.org/print-all-positions-of-a-given-string-having-count-of-smaller-characters-equal-on-both-sides/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/)`str`，任务是查找给定字符串的索引，以使该索引左侧和右侧的按字典顺序排列的较小字符数相等且非零。

**示例**：

> **输入**：`str = "aabacdabbb"`
>
> **输出**：2 4
>
> 索引 2 左侧的小字符计数是 2，索引 2 的右侧也是 2。
>
> 索引 4 左侧的小字符计数是 4，索引 4 的右侧也是 4。
> 
> **输入**：`"geeksforgeeks"`
>
> **输出**：5
>
> **说明**：
>
> 索引 5 左侧较小字符的计数为 2 并且索引 5 的右侧也为 2。
>
> 因此，所需的输出为 5。

**朴素的方法**：解决此问题的最简单方法是[遍历给定的字符串](https://www.geeksforgeeks.org/strings-in-c-2/)并计算给定字符串每个索引左侧和右侧的按字典顺序排列的较小字符数 。 对于每个索引，请检查当前索引左侧和右侧在字典上较小的字符数是否相等。 如果发现为真，则打印当前索引。

**时间复杂度**：`O(N ^ 2)`。

**辅助空间**：`O(1)`。

**高效方法**：要优化上述方法，其思想是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。 请按照以下步骤解决问题：

*   初始化一个数组，例如说`cntFre[]`，以存储给定字符串的每个字符的频率。

*   [遍历给定的字符串](https://www.geeksforgeeks.org/strings-in-c-2/)，并存储给定字符串的每个字符的频率。

*   初始化一个数组，例如说`cntLeftFreq[]`，以存储出现在给定字符串当前索引左侧的所有字符的频率。

*   [遍历给定的字符串](https://www.geeksforgeeks.org/strings-in-c-2/)，并存储出现在当前索引左侧的所有按字典顺序排列的较小字符的频率。

*   对于每个索引，请检查当前索引左侧和右侧的按字典顺序排列的较小字符数是否相等。 如果发现为 true，则打印给定字符串的当前索引。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find indexes 
// of the given string that  
// satisfy the condition 
void printIndexes(string str) 
{ 
    // Stores length of  
    // given string 
    int N = str.length(); 

    // Stores frequncy of 
    // each character of str 
    int cntFreq[256] = {0}; 

    for (int i = 0; i < N;  
                      i++) { 

        // Update frequency of 
        // current character 
        cntFreq[str[i]]++; 

    } 

    // cntLeftFreq[i] Stores frequncy 
    // of characters present on 
    // the left side of index i. 
    int cntLeftFreq[256] = {0}; 

    // Traverse the given string 
    for (int i = 0; i < N; i++) { 

        // Stores count of smaller 
        // characters on left side of i. 
        int cntLeft = 0; 

        // Stores count of smaller 
        // characters on Right side of i. 
        int cntRight = 0; 

        // Traverse smaller characters 
        // on left side of index i. 
        for (int j = str[i] - 1;  
                    j >= 0; j--) { 

            // Update cntLeft    
            cntLeft += cntLeftFreq[j]; 

            // Update cntRight 
            cntRight += cntFreq[j] 
                   - cntLeftFreq[j]; 
        } 

        // Update cntLeftFreq[str[i]] 
        cntLeftFreq[str[i]]++; 

        // If count of smaller elements 
        // on both sides equal 
        if (cntLeft == cntRight && 
                 cntLeft != 0) { 

            // Print current index; 
            cout<<i<<" "; 
        } 

    } 
} 

// Driver Code  
int main() 
{ 
    string str = "aabacdabbb"; 
    printIndexes(str); 
} 

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to find indexes 
# of the given that 
# satisfy the condition 
def printIndexes(strr): 

    # Stores length of 
    # given string 
    N = len(strr) 

    # Stores frequncy of 
    # each character of strr 
    cntFreq = [0] * 256

    for i in range(N): 

        # Update frequency of 
        # current character 
        cntFreq[ord(strr[i])] += 1

    # cntLeftFreq[i] Stores frequncy 
    # of characters present on 
    # the left side of index i. 
    cntLeftFreq = [0] * 256

    # Traverse the given strring 
    for i in range(N): 

        # Stores count of smaller 
        # characters on left side of i. 
        cntLeft = 0

        # Stores count of smaller 
        # characters on Right side of i. 
        cntRight = 0

        # Traverse smaller characters 
        # on left side of index i. 
        for j in range(ord(strr[i]) - 1, -1, -1): 

            # Update cntLeft 
            cntLeft += cntLeftFreq[j] 

            # Update cntRight 
            cntRight += (cntFreq[j] - 
                     cntLeftFreq[j]) 

        # Update cntLeftFreq[strr[i]] 
        cntLeftFreq[ord(strr[i])] += 1

        # If count of smaller elements 
        # on both sides equal 
        if (cntLeft == cntRight and cntLeft != 0): 

            # Print current index 
            print(i, end = " ") 

# Driver Code 
if __name__ == '__main__': 

    strr = "aabacdabbb"

    printIndexes(strr) 

# This code is contributed by mohit kumar 29

```

**输出**： 

```
2 4

```

**时间复杂度**：`O(N * 256)`。

**辅助空间**：`O(256)`。



* * *

* * *



