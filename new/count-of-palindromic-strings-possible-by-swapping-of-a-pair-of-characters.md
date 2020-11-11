# 通过交换一对字符可以计算回文字符串

> 原文：[https://www.geeksforgeeks.org/count-of-palindromic-strings-possible-by-swapping-of-a-pair-of-characters/](https://www.geeksforgeeks.org/count-of-palindromic-strings-possible-by-swapping-of-a-pair-of-characters/)

给定[回文字符串](https://www.geeksforgeeks.org/string-palindrome/)`S`，任务是通过一次交换一对字符来查找回文字符串的数量。

**示例**：

> **输入**：`s = "abba"`
>
> **输出**：2
>
> **说明**：
>
> 第一个交换：`abba -> abba`
>
> 第二个交换：`abba -> abba`
>
> 所有其他交换将导致非回文字符串。
>
> 因此，可能的字符串数为 2。
> 
> **输入**：`s = "aaabaaa"`
>
> **输出**：15

**朴素的方法**：

解决该问题的最简单方法是[从给定的字符串中生成所有可能的字符对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，如果每对字符交换，它们是否会生成回文字符串 。 如果发现是真的，则增加`count`。 最后，打印`count`的值。

**时间复杂度**：`P(N ^ 3)`

**辅助空间**：`O(1)`

**有效方法**：

为了优化上述方法，请计算字符串中每个字符的**频率**。 为了使字符串保持回文，只能在字符串中交换相同的字符。

请按照以下步骤解决问题：

*   遍历字符串。

*   对于第`i`个字符，请以该字符的当前频率增加**计数**。 这增加了当前角色与其之前出现的交换次数。

*   增加第`i`个字符的频率。

*   最后，在完全遍历字符串之后，打印`count`。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the count of 
// possible palindromic strings 
long long findNewString(string s) 
{ 

    long long ans = 0; 

    // Stores the frequencies 
    // of each character 
    int freq[26]; 

    // Stores the length of 
    // the string 
    int n = s.length(); 

    // Initialize frequencies 
    memset(freq, 0, sizeof freq); 

    for (int i = 0; i < (int)s.length(); ++i) { 

        // Increase the number of swaps, 
        // the current character make with 
        // its previous occurrences 
        ans += freq[s[i] - 'a']; 

        // Increase frequency 
        freq[s[i] - 'a']++; 
    } 

    return ans; 
} 

// Driver Code 
int main() 
{ 
    string s = "aaabaaa"; 
    cout << findNewString(s) << '\n'; 

    return 0; 
} 

```

## Java

```java

// Java Program to implement 
// the above approach 
import java.util.*; 
class GFG{ 

// Function to return the count of 
// possible palindromic Strings 
static long findNewString(String s) 
{ 
    long ans = 0; 

    // Stores the frequencies 
    // of each character 
    int []freq = new int[26]; 

    // Stores the length of 
    // the String 
    int n = s.length(); 

    // Initialize frequencies 
    Arrays.fill(freq, 0); 

    for (int i = 0; i < (int)s.length(); ++i) 
    { 

        // Increase the number of swaps, 
        // the current character make with 
        // its previous occurrences 
        ans += freq[s.charAt(i) - 'a']; 

        // Increase frequency 
        freq[s.charAt(i) - 'a']++; 
    } 
    return ans; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    String s = "aaabaaa"; 
    System.out.print(findNewString(s)); 
} 
} 

// This code is contributed by sapnasingh4991

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to return the count of 
# possible palindromic strings 
def findNewString(s): 

    ans = 0

    # Stores the frequencies 
    # of each character 
    freq = [0] * 26

    # Stores the length of 
    # the string 
    n = len(s) 

    for i in range(n): 

        # Increase the number of swaps, 
        # the current character make with 
        # its previous occurrences 
        ans += freq[ord(s[i]) - ord('a')] 

        # Increase frequency 
        freq[ord(s[i]) - ord('a')] += 1

    return ans 

# Driver Code 
s = "aaabaaa"

print(findNewString(s)) 

# This code is contributed by code_hunt 

```

## C#

```cs

// C# Program to implement 
// the above approach 
using System; 
class GFG{ 

// Function to return the count of 
// possible palindromic Strings 
static long findNewString(String s) 
{ 
    long ans = 0; 

    // Stores the frequencies 
    // of each character 
    int []freq = new int[26]; 

    // Stores the length of 
    // the String 
    int n = s.Length; 

    for (int i = 0; i < (int)s.Length; ++i) 
    { 

        // Increase the number of swaps, 
        // the current character make with 
        // its previous occurrences 
        ans += freq[s[i] - 'a']; 

        // Increase frequency 
        freq[s[i] - 'a']++; 
    } 
    return ans; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    String s = "aaabaaa"; 
    Console.Write(findNewString(s)); 
} 
} 

// This code is contributed by sapnasingh4991

```

**输出**： 

```
15

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



