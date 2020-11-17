# 通过在给定数组中重新排列字符串，可以得到的最长公共前缀的长度

> 原文：[https://www.geeksforgeeks.org/length-of-longest-common-prefix-possible-by-rearranging-strings-in-a-given-array/](https://www.geeksforgeeks.org/length-of-longest-common-prefix-possible-by-rearranging-strings-in-a-given-array/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/)`arr[]`的[数组](https://www.geeksforgeeks.org/array-data-structure/)，任务是通过重新排列以下字符来找到给定数组的每个字符串的[最长公共前缀的长度](https://www.geeksforgeeks.org/longest-common-prefix-using-sorting/)。

**示例**：

> **输入**：`arr[] = {"aabdc", "abcd", "aacd"}`
>
> **输出**：3
>
> **说明**：重新排列给定数组的每个字符串的字符，以使该数组成为`{"acdab", "acdb", "acda"}`。
>
> 因此，给定数组的所有字符串中最长的公共前缀是长度等于 3 的`"acd"`。
> 
> **输入**：`arr[] = {"abcdef", "adgfse", "fhfdd"}`
>
> **输出**：2
>
> **说明**：重新排列给定数组的每个字符串的字符，以使该数组成为`{"dfcaeb", "dfgase", "dffhd"}`。
>
> 因此，给定数组的所有字符串的最长公共前缀是长度等于 2 的`"df"`。

**朴素的方法**：解决此问题的最简单方法是[生成给定数组的每个字符串的所有可能排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，并找到所有字符串中最长的[公共前缀](https://www.geeksforgeeks.org/longest-common-prefix-using-binary-search/)。 最后，打印最长的公共前缀的长度。

***时间复杂度**：`O(N * log M * (M!) ^ N)`。

**辅助空间**：`O(M)`，`N`是字符串数，`M`是最长字符串的长度。

**高效方法**：要优化上述方法，其思想是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。 请按照以下步骤解决问题：

*   初始化 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，例如`freq[N][256]`，以便`freq[i][j]`存储字符的频率（字符串`arrx[i]`中的`j`）。

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将`arr[i][j]`的频率存储到`freq[i][arr[i][j]]`中。

*   初始化一个变量，例如说`maxLen`，以存储最长公共前缀的长度。

*   遍历所有可能的字符并找到最小频率，例如在给定数组的所有字符串中当前字符的`minRowVal`，然后将`maxLen`的值增加`minRowVal`。

*   最后，打印`maxLen`的值。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to get the length 
// of the longest common prefix 
// by rearranging the strings 
int longComPre(string arr[], int N) 
{ 
    // freq[i][j]: stores the frequency 
    // of a character(= j) in 
    // a string arr[i] 
    int freq[N][256]; 

    // Initilize freq[][] array. 
    memset(freq, 0, sizeof(freq)); 

    // Traverse the given array 
    for (int i = 0; i < N; i++) { 

        // Stores length of 
        // current string 
        int M = arr[i].length(); 

        // Traverse current string 
        // of the given array 
        for (int j = 0; j < M; 
             j++) { 

            // Update the value of 
            // freq[i][arr[i][j]] 
            freq[i][arr[i][j]]++; 
        } 
    } 

    // Stores the length of 
    // longest common prefix 
    int maxLen = 0; 

    // Count the minimum frequency 
    // of each character in 
    // in all the strings of arr[] 
    for (int j = 0; j < 256; j++) { 

        // Stores minimum value 
        // in each row of freq[][] 
        int minRowVal = INT_MAX; 

        // Calculate minimum frequency 
        // of current character 
        // in all the strings. 
        for (int i = 0; i < N; 
             i++) { 

            // Update minRowVal 
            minRowVal = min(minRowVal, 
                            freq[i][j]); 
        } 

        // Update maxLen 
        maxLen += minRowVal; 
    } 
    return maxLen; 
} 

// Driver Code 
int main() 
{ 
    string arr[] = { "aabdc", 
                     "abcd", 
                     "aacd" }; 
    int N = 3; 
    cout << longComPre(arr, N); 
} 

```

**输出**：

```
3

```

**时间复杂度**：`O(N * (M + 256))`。

**辅助空间**：`O(N * 256)`。



* * *

* * *



