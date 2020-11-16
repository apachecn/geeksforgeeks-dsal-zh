# 按出现顺序打印奇数频率的字符

> 原文：[https://www.geeksforgeeks.org/print-characters-having-odd-frequencies-in-order-of-occurrence/](https://www.geeksforgeeks.org/print-characters-having-odd-frequencies-in-order-of-occurrence/)

给定仅包含小写字符的字符串`str`。 任务是按照出现的频率打印出具有奇数频率的字符。

**注意**：具有奇数频率的重复元素按出现的次数打印多次。

**示例**：

> **输入**：`str = "geeksforgeeks"`
>
> **输出**：`for`
> 
> | 字符 | 频率 |
> | --- | --- |
> | `g` | 2 |
> | `e` | 4 |
> | `k` | 2 |
> | `s` | 2 |
> | `f` | 1 |
> | `o` | 1 |
> | `r` | 1 |
> 
> `f`，`o`和`r`是唯一具有奇数频率的字符。
> 
> **输入**：`str = "elephant"`
>
> **输出**：`lphant`

**方法**：创建一个频率数组，以存储给定字符串`str`的每个字符的频率。 再次遍历字符串`str`，并检查该字符的频率是否为奇数。 如果是，则打印字符。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 
#define SIZE 26 

// Function to print the odd frequency characters 
// in the order of their occurrence 
void printChar(string str, int n) 
{ 

    // To store the frequency of each of 
    // the character of the string 
    int freq[SIZE]; 

    // Initialize all elements of freq[] to 0 
    memset(freq, 0, sizeof(freq)); 

    // Update the frequency of each character 
    for (int i = 0; i < n; i++) 
        freq[str[i] - 'a']++; 

    // Traverse str character by character 
    for (int i = 0; i < n; i++) { 

        // If frequency of current character is odd 
        if (freq[str[i] - 'a'] % 2 == 1) { 
            cout << str[i]; 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    string str = "geeksforgeeks"; 
    int n = str.length(); 
    printChar(str, n); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG { 
    // Function to print the odd frequency characters 
    // in the order of their occurrence 
    public static void printChar(String str, int n) 
    { 

        // To store the frequency of each of 
        // the character of the string 
        int[] freq = new int[26]; 

        // Update the frequency of each character 
        for (int i = 0; i < n; i++) 
            freq[str.charAt(i) - 'a']++; 

        // Traverse str character by character 
        for (int i = 0; i < n; i++) { 

            // If frequency of current character is odd 
            if (freq[str.charAt(i) - 'a'] % 2 == 1) { 
                System.out.print(str.charAt(i)); 
            } 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        String str = "geeksforgeeks"; 
        int n = str.length(); 
        printChar(str, n); 
    } 
} 

// This code is contributed by Naman_Garg. 

```

## Python3

```py

# Python3 implementation of the approach 
import sys 
import math 

# Function to print the odd frequency characters  
# in the order of their occurrence  
def printChar(str_, n): 

    # To store the frequency of each of  
    # the character of the string and 
    # Initialize all elements of freq[] to 0  
    freq = [0] * 26

    # Update the frequency of each character  
    for i in range(n): 
        freq[ord(str_[i]) - ord('a')] += 1

    # Traverse str character by character  
    for i in range(n): 

        # If frequency of current character is odd  
        if (freq[ord(str_[i]) - 
                 ord('a')]) % 2 == 1: 
            print("{}".format(str_[i]), end = "") 

# Driver code 
if __name__=='__main__': 
    str_ = "geeksforgeeks"
    n = len(str_) 
    printChar(str_, n) 

# This code is contributed by Vikash Kumar 37 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG { 
    // Function to print the odd frequency characters 
    // in the order of their occurrence 
    public static void printChar(String str, int n) 
    { 

        // To store the frequency of each of 
        // the character of the string 
        int[] freq = new int[26]; 

        // Update the frequency of each character 
        for (int i = 0; i < n; i++) 
            freq[str[i] - 'a']++; 

        // Traverse str character by character 
        for (int i = 0; i < n; i++) { 

            // If frequency of current character is odd 
            if (freq[str[i] - 'a'] % 2 == 1) { 
                Console.Write(str[i]); 
            } 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        String str = "geeksforgeeks"; 
        int n = str.Length; 
        printChar(str, n); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
for

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。



* * *

* * *



