# 具有至少 K 个成对区分字符且具有相同频率的子字符串的计数

> 原文：[https://www.geeksforgeeks.org/count-of-substrings-with-at-least-k-pairwise-distinct-characters-having-same-frequency/](https://www.geeksforgeeks.org/count-of-substrings-with-at-least-k-pairwise-distinct-characters-having-same-frequency/)

给定字符串 **S** 和整数 **K** ，任务是找到至少由 **K** 成对的具有相同频率的成对字符组成的子串数。

**示例**：

> **输入**：S =“ abasa”，K = 2
> **输出**：5
> **说明**：
> 中的子字符串具有成对的两个成对的 具有相同频率的字符为{“ ab”，“ ba”，“ as”，“ sa”，“ bas”}。
> 
> **输入**：S =“ abhay”，K = 3
> **输出**：4
> **说明**：
> 子字符串具有 3 个成对的不同字符 频率相同的是{“ abh”，“ bha”，“ hay”，“ bhay”}。

**朴素的方法**：解决此问题的最简单方法是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有可能的子字符串，并检查两个条件是否都满足。 如果发现是真的，请增加**计数**。 最后，打印**计数**。

**时间复杂度**：O（N <sup>3</sup> ）

**辅助空间**：`O(1)`

**高效方法**：要优化上述方法，请按照以下步骤解决问题：

*   检查每个字符的频率是否相同。 如果确定为真，则只需生成所有子字符串以检查每个字符是否满足至少 ***N** 成对的不同字符*的条件。

*   预计算字符的频率以检查每个子字符串的条件。

下面是上述方法的实现：

## C++

```cpp

// C++ Program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the substring with K 
// pairwise distinct characters and 
// with same frequency 
int no_of_substring(string s, int N) 
{ 
    // Stores the occurrence of each 
    // character in the substring 
    int fre[26]; 

    int str_len; 

    // Length of the string 
    str_len = (int)s.length(); 

    int count = 0; 

    // Iterate over the string 
    for (int i = 0; i < str_len; i++) { 

        // Set all values at each index to zero 
        memset(fre, 0, sizeof(fre)); 
        int max_index = 0; 

        // Stores the count of 
        // unique characters 
        int dist = 0; 

        // Moving the substring ending at j 
        for (int j = i; j < str_len; j++) { 

            // Calculate the index of 
            // character in frequency array 
            int x = s[j] - 'a'; 

            if (fre[x] == 0) 
                dist++; 

            // Increment the frequency 
            fre[x]++; 

            // Update the maximum index 
            max_index = max(max_index, fre[x]); 

            // Check for both the conditions 
            if (dist >= N && ((max_index * dist) 
                              == (j - i + 1))) 
                count++; 
        } 
    } 

    // Return the answer 
    return count; 
} 

// Driver Code 
int main() 
{ 
    string s = "abhay"; 
    int N = 3; 

    // Function call 
    cout << no_of_substring(s, N); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG{ 

// Function to find the subString with K 
// pairwise distinct characters and 
// with same frequency 
static int no_of_subString(String s, int N) 
{ 

    // Stores the occurrence of each 
    // character in the subString 
    int fre[] = new int[26]; 

    int str_len; 

    // Length of the String 
    str_len = (int)s.length(); 

    int count = 0; 

    // Iterate over the String 
    for(int i = 0; i < str_len; i++) 
    { 

        // Set all values at each index to zero 
        Arrays.fill(fre, 0); 

        int max_index = 0; 

        // Stores the count of 
        // unique characters 
        int dist = 0; 

        // Moving the subString ending at j 
        for(int j = i; j < str_len; j++)  
        { 

            // Calculate the index of 
            // character in frequency array 
            int x = s.charAt(j) - 'a'; 

            if (fre[x] == 0) 
                dist++; 

            // Increment the frequency 
            fre[x]++; 

            // Update the maximum index 
            max_index = Math.max(max_index, fre[x]); 

            // Check for both the conditions 
            if (dist >= N && ((max_index * dist) == 
                              (j - i + 1))) 
                count++; 
        } 
    } 

    // Return the answer 
    return count; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    String s = "abhay"; 
    int N = 3; 

    // Function call 
    System.out.print(no_of_subString(s, N)); 
} 
} 

// This code is contributed by Amit Katiyar 

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to find the substring with K 
# pairwise distinct characters and 
# with same frequency 
def no_of_substring(s, N): 

    # Length of the string 
    str_len = len(s) 

    count = 0

    # Iterate over the string 
    for i in range(str_len): 

        # Stores the occurrence of each 
        # character in the substring 
        # Set all values at each index to zero 
        fre = [0] * 26

        max_index = 0

        # Stores the count of 
        # unique characters 
        dist = 0

        # Moving the substring ending at j 
        for j in range(i, str_len): 

            # Calculate the index of 
            # character in frequency array 
            x = ord(s[j]) - ord('a') 

            if (fre[x] == 0): 
                dist += 1

            # Increment the frequency 
            fre[x] += 1

            # Update the maximum index 
            max_index = max(max_index, fre[x]) 

            # Check for both the conditions 
            if(dist >= N and 
             ((max_index * dist) == (j - i + 1))): 
                count += 1

    # Return the answer 
    return count 

# Driver Code 
s = "abhay"
N = 3

# Function call 
print(no_of_substring(s, N)) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program for the above approach 
using System; 

class GFG{ 

// Function to find the subString with K 
// pairwise distinct characters and 
// with same frequency 
static int no_of_subString(String s, int N) 
{ 

    // Stores the occurrence of each 
    // character in the subString 
    int []fre = new int[26]; 

    int str_len; 

    // Length of the String 
    str_len = (int)s.Length; 

    int count = 0; 

    // Iterate over the String 
    for(int i = 0; i < str_len; i++) 
    { 

        // Set all values at each index to zero 
        fre = new int[26]; 

        int max_index = 0; 

        // Stores the count of 
        // unique characters 
        int dist = 0; 

        // Moving the subString ending at j 
        for(int j = i; j < str_len; j++)  
        { 

            // Calculate the index of 
            // character in frequency array 
            int x = s[j] - 'a'; 

            if (fre[x] == 0) 
                dist++; 

            // Increment the frequency 
            fre[x]++; 

            // Update the maximum index 
            max_index = Math.Max(max_index, fre[x]); 

            // Check for both the conditions 
            if (dist >= N && ((max_index * dist) == 
                              (j - i + 1))) 
                count++; 
        } 
    } 

    // Return the answer 
    return count; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    String s = "abhay"; 
    int N = 3; 

    // Function call 
    Console.Write(no_of_subString(s, N)); 
} 
} 

// This code is contributed by Amit Katiyar

```

**Output:** 

```
4

```

**时间复杂度**：O（N <sup>2</sup> ）

**辅助空间**：`O(1)`



* * *

* * *



