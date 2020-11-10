# 最大的子字符串，其中所有字符至少出现 K 次 | 系列 2

> 原文：[https://www.geeksforgeeks.org/largest-substring-where-all-characters-appear-at-least-k-times-set-2/](https://www.geeksforgeeks.org/largest-substring-where-all-characters-appear-at-least-k-times-set-2/)

给定字符串`str`和整数`K`，任务是找到最长子字符串`S`的长度，以使`S`中的每个字符出现至少`K`次。

**示例**：

> **输入**：`str = "aabbba", K = 3`
>
> **输出**：6
>
> **说明**：
>
> 在子字符串`aabbba`中，每个字符重复至少`K`次，其长度为 6。
> 
> **输入**：`str = "ababacb", K = 3`
>
> **输出**：0
>
> **说明**：
>
> 没有每个字符的子字符串 重复至少`k`次。

**朴素方法**：我们在[之前的文章](https://www.geeksforgeeks.org/largest-sub-string-where-all-the-characters-appear-at-least-k-times/)中讨论了朴素方法。

**方法**：在本文中，我们将讨论使用[分而治之](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)技术和[递归](https://www.geeksforgeeks.org/recursion/)的方法。 步骤如下：

1.  将给定字符串的每个字符的[频率存储在大小为`26`的频率数组中。](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/)

2.  初始化两个变量，`start = 0`，`end`是字符串`str`的长度。

3.  从`start`到`end`遍历字符串，并计算每个字符重复的次数并将其存储在数组中。

4.  如果有任何字符重复的**少于`K`次**，则将字符串分成两半。 如果`i`是我们发现`str[i]`重复少于`K`次的字符串的索引，则将字符串分为两半，从开始到`i`和`i + 1`到结束。

5.  在上述步骤中递归调用两个半部分，即从开始到`i`和`i + 1`到结束，然后重复**步骤 2 和 3** 并返回 通过上述递归调用获得两个值的最大值。

6.  如果`start`和`end`之间的所有字符至少重复`K`次，则答案是`end - start`。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach  
#include <bits/stdc++.h>  
using namespace std;  

// Function to find the longest substring  
int longestSubstring(int start, int end,  
                    string s, int k)  
{  
    int left, right;  

    // Array for counting the number of  
    // times each character repeats  
    // count the number of times each  
    // character repeats from start to end  
    int count[26] = { 0 };  

    // Store the frequency from s[start...end]  
    for (int i = start; i < end; i++) {  
        count[s[i] - 'a'] += 1;  
    }  

    // Iterate from [start, end]  
    for (int i = start; i < end; i++) {  

        if (count[s[i] - 'a'] < k) {  

            // Recursive call for left subpart  
            left = longestSubstring(start,  
                                    i,  
                                    s,  
                                    k);  

            // Recursive call for right subpart  
            right = longestSubstring(i + 1,  
                                    end,  
                                    s,  
                                    k);  

            // Return maximum of left & right  
            return max(left, right);  
        }  
    }  

    // If all the characters are repeated  
    // at least k times  
    return end - start;  
}  

// Driver Code  
int main()  
{  
    // Given String str  
    string str = "aabbba";  
    int k = 3;  

    // Function Call  
    cout << longestSubstring(0, str.length(),  
                            str, k)  
        << endl;  
    return 0;  
}  

```

## Java

```java

// Java program for the above approach  
import java.util.*;  

class GFG{  

// Function to find the longest subString  
static int longestSubString(int start, int end,  
                            String s, int k)  
{  
    int left, right;  

    // Array for counting the number of  
    // times each character repeats  
    // count the number of times each  
    // character repeats from start to end  
    int count[] = new int[26];  

    // Store the frequency from s[start...end]  
    for(int i = start; i < end; i++)  
    {  
        count[s.charAt(i) - 'a'] += 1;  
    }  

    // Iterate from [start, end]  
    for(int i = start; i < end; i++)  
    {  
        if (count[s.charAt(i) - 'a'] < k)  
        {  

            // Recursive call for left subpart  
            left = longestSubString(start, i,  
                                    s, k);  

            // Recursive call for right subpart  
            right = longestSubString(i + 1, end,  
                                    s, k);  

            // Return maximum of left & right  
            return Math.max(left, right);  
        }  
    }  

    // If all the characters are repeated  
    // at least k times  
    return end - start;  
}  

// Driver Code  
public static void main(String[] args)  
{  

    // Given String str  
    String str = "aabbba";  
    int k = 3;  

    // Function Call  
    System.out.print(longestSubString(0, str.length(),  
                                        str, k) + "\n");  
}  
}  

// This code is contributed by Amit Katiyar  

```

## Python3

```py

# Python3 program for the above approach  

# Function to find the longest substring  
def longestSubString(start, end, s, k):  

    # List for counting the number of  
    # times each character repeats  
    # count the number of times each  
    # chracter repeats from start to end  
    count = [0 for i in range(26)]  

    # Store the frequency from s[start...end]  
    for i in range(start, end):  
        count[ord(s[i]) - ord('a')] += 1

    # Iterate from [start, end]  
    for i in range(start, end):  
        if(count[ ord(s[i]) - ord('a')] < k):  

            # Recursive call for left subpart  
            left = longestSubString(start, i,  
                                        s, k)  

            # Recursive call for right subpart  
            right = longestSubString(i + 1, end,  
                                        s, k)  

            # Return maximum of left & right  
            return max(left, right)  

    # If all the characters are repeated  
    # at least k times  
    return end - start  

# Driver Code  

# Given String str  
str = "aabbba"
k = 3

# Function call  
print(longestSubString(0, len(str), str, k))  

# This code is contributed by dadimadhav 

```

## C#

```cs

// C# program for the above approach 
using System; 

class GFG{ 

// Function to find the longest subString 
static int longestSubString(int start, int end, 
                             string s, int k) 
{ 
    int left, right; 

    // Array for counting the number of 
    // times each character repeats 
    // count the number of times each 
    // character repeats from start to end 
    int []count = new int[26]; 

    // Store the frequency from s[start...end] 
    for(int i = start; i < end; i++) 
    { 
        count[s[i] - 'a'] += 1; 
    } 

    // Iterate from [start, end] 
    for(int i = start; i < end; i++) 
    { 
        if (count[s[i] - 'a'] < k)  
        { 

            // Recursive call for left subpart 
            left = longestSubString(start, i, 
                                    s, k); 

            // Recursive call for right subpart 
            right = longestSubString(i + 1, end, 
                                     s, k); 

            // Return maximum of left & right 
            return Math.Max(left, right); 
        } 
    } 

    // If all the characters are repeated 
    // at least k times 
    return end - start; 
} 

// Driver Code 
public static void Main(string[] args) 
{ 

    // Given String str 
    string str = "aabbba"; 
    int k = 3; 

    // Function call 
    Console.Write(longestSubString(0, str.Length, 
                                      str, k) + "\n"); 
} 
} 

// This code is contributed by rutvik_56 

```

**输出**：

```
6

```

**时间复杂度**：`O(N * log2(N))`



* * *

* * *



