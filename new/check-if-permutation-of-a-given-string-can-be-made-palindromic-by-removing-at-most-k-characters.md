# 检查是否可以通过删除最多`K`个字符来使给定字符串的排列回文

> 原文：[https://www.geeksforgeeks.org/check-if-permutation-of-a-given-string-can-be-made-palindromic-by-removing-at-most-k-characters/](https://www.geeksforgeeks.org/check-if-permutation-of-a-given-string-can-be-made-palindromic-by-removing-at-most-k-characters/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/)`str`和整数`K`，任务是检查通过[从给定字符串中删除最多`K`个字符](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，给定字符串的排列是否可以变为[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

**示例**：

> **输入**：`str = "geeksforgeeks", K = 2`
> **输出**：`Yes`
> **说明**：
> 移除给定字符串中的（`str[5]`，`str[6]`）使其余字符串`"geeksrgeeks"`为回文。 因此，所需的输出是`Yes`。
> 
> **输入**：`str = "coder", K = 1`
> **输出**：`No`

**方法**：可以使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)解决问题。 想法是[遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符，并存储给定字符串的每个不同字符的[频率](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)。 如果给定字符串具有奇数频率的不同字符数小于或等于`K + 1`，则打印`Yes`。 否则，打印`No`。 请按照以下步骤解决问题：

*   初始化[数组](https://www.geeksforgeeks.org/array-data-structure/)，例如说`cntFreq[]`，以存储`str`的每个字符的频率。

*   [遍历给定的字符串](https://www.geeksforgeeks.org/strings-in-c-2/)，并将字符串`str`的每个不同字符的[频率](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)存储在`cntFreq[]`数组中。

*   初始化一个变量，例如说`cntOddFreq`，以存储给定字符串的不同字符的计数，其频率为奇数。

*   [遍历`cntFreq[]`数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查`cntFreq[i] % 2 == 1`，然后将`cntOddFreq`的值增加`1`。

*   最后，检查`cntOddFreq ≤ (K + 1)`，然后打印`True`。

*   否则，打印`False`。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to check if 
// the string satisfies 
// the given conditions or not 
bool checkPalinK(string str, int K) 
{ 
    // Stores length of 
    // given string 
    int N = str.length(); 

    // Stores frequency of 
    // each character of str 
    int cntFreq[256] = { 0 }; 

    for (int i = 0; i < N; 
         i++) { 

        // Update frequency of 
        // current character 
        cntFreq[str[i]]++; 
    } 

    // Stores count of 
    // distinct character 
    // whose frequency is odd 
    int cntOddFreq = 0; 

    // Traverse the cntFreq[] 
    // array. 
    for (int i = 0; i < 256; 
         i++) { 

        // If frequency of 
        // character i is odd 
        if (cntFreq[i] % 2 
            == 1) { 

            // Update cntOddFreq 
            cntOddFreq++; 
        } 
    } 

    // If count of distinct character 
    // having odd frequency is <= K + 1 
    if (cntOddFreq <= (K + 1)) { 
        return true; 
    } 

    return false; 
} 

// Driver Code 
int main() 
{ 
    string str = "geeksforgeeks"; 
    int K = 2; 

    // If str satisfy 
    // the given conditions 
    if (checkPalinK(str, K)) { 
        cout << "Yes"; 
    } 
    else { 
        cout << "No"; 
    } 
} 

```

## Java

```java

// Java program to implement  
// the above approach  
import java.util.*; 

class GFG{ 

// Function to check if 
// the string satisfies 
// the given conditions or not 
public static boolean checkPalinK(String str,  
                                  int K) 
{ 

    // Stores length of 
    // given string 
    int N = str.length(); 

    // Stores frequency of 
    // each character of str 
    int cntFreq[] = new int[257]; 

    for(int i = 0; i < N; i++) 
    { 

        // Update frequency of 
        // current character 
        cntFreq[str.charAt(i)]++; 
    } 

    // Stores count of 
    // distinct character 
    // whose frequency is odd 
    int cntOddFreq = 0; 

    // Traverse the cntFreq[] 
    // array. 
    for(int i = 0; i < 256; i++)  
    { 

        // If frequency of 
        // character i is odd 
        if (cntFreq[i] % 2 == 1) 
        { 

            // Update cntOddFreq 
            cntOddFreq++; 
        } 
    } 

    // If count of distinct character 
    // having odd frequency is <= K + 1 
    if (cntOddFreq <= (K + 1)) 
    { 
        return true; 
    } 
    return false; 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    String str = "geeksforgeeks"; 
    int K = 2; 

    // If str satisfy 
    // the given conditions 
    if (checkPalinK(str, K))  
    { 
        System.out.println("Yes"); 
    } 
    else 
    { 
        System.out.println("No"); 
    } 
} 
} 

// This code is contributed by hemanth gadarla

```

**输出**： 

```
Yes

```

**时间复杂度**：`O(N + 256)`，其中`N`是给定字符串的长度。

**辅助空间**：`O(256)`



* * *

* * *



