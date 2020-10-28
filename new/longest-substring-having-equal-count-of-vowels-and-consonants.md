# 带有相等数量的元音和辅音的最长子串

> 原文：[https://www.geeksforgeeks.org/longest-substring-having-equal-count-of-vowels-and-consonants/](https://www.geeksforgeeks.org/longest-substring-having-equal-count-of-vowels-and-consonants/)

给定由小写英文字母组成的字符串 **S** ，任务是从给定的字符串中找到具有相等数量的元音和辅音的最长子字符串的长度。

**示例**：

> **输入**：S =“ geeksforgeeks” 。 剩下的字符只是辅音。 因此，任何更长的子串都不会具有相等数量的元音和辅音。
> **输入**：S =“ qwertyuiop”
> **输出**：8
> **说明**：
> 子字符串“ wertyuio”由 4 个元音组成 和 4 个辅音

**天真的方法**：最简单的解决方案是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有子字符串，并针对每个子字符串检查元音和辅音的数量是否相等。 最后，打印获得的具有相等数量的元音和辅音的子串的最大长度。

***时间复杂度**：O（N <sup>3</sup> ）*

***辅助空间**：O（1）*

**有效方法**：的想法是考虑一个长度等于给定字符串长度的数组，分别存储与元音和辅音对应的 **1** 和 **-1** 使用 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 打印最长[子数组的长度，其总和等于 0](https://www.geeksforgeeks.org/find-subarray-with-given-sum-in-array-of-integers/) 。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// the longest substring having equal
// number of vowel and consonant
int maxsubstringLength(string S, int N)
{
    int arr[N];

    // Generate the array
    for (int i = 0; i < N; i++)
        if (S[i] == 'a' || S[i] == 'e' || S[i] == 'i'
            || S[i] == 'o' || S[i] == 'u')
            arr[i] = 1;
        else
            arr[i] = -1;

    // Initialize variable
    // to store result
    int maxLen = 0;

    // Stores the sum of subarray
    int curr_sum = 0;

    // Map to store indices of the sum
    unordered_map<int, int> hash;

    // Loop through the array
    for (int i = 0; i < N; i++) {
        curr_sum += arr[i];

        // If sum is 0
        if (curr_sum == 0)

            // Count of vowels and consonants
            // are equal
            maxLen = max(maxLen, i + 1);

        // Update the maximum length
        // of substring in HashMap
        if (hash.find(curr_sum) != hash.end())
            maxLen = max(maxLen, i - hash[curr_sum]);

        // Store the index of the sum
        else
            hash[curr_sum] = i;
    }

    // Return the maximum
    // length of required substring
    return maxLen;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    int n = sizeof(S) / sizeof(S[0]);
    cout << maxsubstringLength(S, n);
    return 0;
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to return the length of
// the longest subString having equal
// number of vowel and consonant
static int maxsubStringLength(char[] S, int N)
{
    int arr[] = new int[N];

    // Generate the array
    for(int i = 0; i < N; i++)
    if (S[i] == 'a' || S[i] == 'e' ||
        S[i] == 'i' || S[i] == 'o' ||
        S[i] == 'u')
        arr[i] = 1;
    else
        arr[i] = -1;

    // Initialize variable
    // to store result
    int maxLen = 0;

    // Stores the sum of subarray
    int curr_sum = 0;

    // Map to store indices of the sum
    HashMap<Integer, Integer> hash = new HashMap<>();

    // Loop through the array
    for(int i = 0; i < N; i++)
    {
        curr_sum += arr[i];

        // If sum is 0
        if (curr_sum == 0)

            // Count of vowels and consonants
            // are equal
            maxLen = Math.max(maxLen, i + 1);

        // Update the maximum length
        // of subString in HashMap
        if (hash.containsKey(curr_sum))
            maxLen = Math.max(maxLen, 
                              i - hash.get(curr_sum));

        // Store the index of the sum
        else

            // hash[curr_sum] = i;
            hash.put(curr_sum, i);
    }

    // Return the maximum
    // length of required subString
    return maxLen;
}

// Driver Code
public static void main(String[] args)
{
    String S = "geeksforgeeks";
    int n = S.length();

    System.out.print(
        maxsubStringLength(S.toCharArray(), n));
}
}

// This code is contributed by PrinciRaj1992

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to return the length of
# the longest substring having equal
# number of vowel and consonant
def maxsubstringLength(S, N):

    arr = [0] * N

    # Generate the array
    for i in range(N):
        if(S[i] == 'a' or S[i] == 'e' or
           S[i] == 'i' or S[i] == 'o' or
           S[i] == 'u'):
            arr[i] = 1
        else:
            arr[i] = -1

    # Initialize variable
    # to store result
    maxLen = 0

    # Stores the sum of subarray
    curr_sum = 0

    # Map to store indices of the sum
    hash = {}

    # Loop through the array
    for i in range(N):
        curr_sum += arr[i]

        # If sum is 0
        if(curr_sum == 0):

            # Count of vowels and consonants
            # are equal
            maxLen = max(maxLen, i + 1)

        # Update the maximum length
        # of substring in HashMap
        if(curr_sum in hash.keys()):
            maxLen = max(maxLen, i - hash[curr_sum])

        # Store the index of the sum
        else:
            hash[curr_sum] = i

    # Return the maximum
    # length of required substring 
    return maxLen

# Driver Code
S = "geeksforgeeks"
n = len(S)

# Function call
print(maxsubstringLength(S, n))

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the length of
// the longest subString having equal
// number of vowel and consonant
static int maxsubStringLength(char[] S, int N)
{
    int []arr = new int[N];

    // Generate the array
    for(int i = 0; i < N; i++)
    if (S[i] == 'a' || S[i] == 'e' ||
        S[i] == 'i' || S[i] == 'o' ||
        S[i] == 'u')
        arr[i] = 1;
    else
        arr[i] = -1;

    // Initialize variable
    // to store result
    int maxLen = 0;

    // Stores the sum of subarray
    int curr_sum = 0;

    // Map to store indices of the sum
    Dictionary<int, 
                 int> hash = new Dictionary<int,
                                            int>();

    // Loop through the array
    for(int i = 0; i < N; i++)
    {
        curr_sum += arr[i];

        // If sum is 0
        if (curr_sum == 0)

            // Count of vowels and consonants
            // are equal
            maxLen = Math.Max(maxLen, i + 1);

        // Update the maximum length
        // of subString in Dictionary
        if (hash.ContainsKey(curr_sum))
            maxLen = Math.Max(maxLen, 
                              i - hash[curr_sum]);

        // Store the index of the sum
        else

            // hash[curr_sum] = i;
            hash.Add(curr_sum, i);
    }

    // Return the maximum
    // length of required subString
    return maxLen;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "geeksforgeeks";
    int n = S.Length;

    Console.Write(maxsubStringLength(
                    S.ToCharArray(), n));
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
10

```

***时间复杂度**：O（NlogN）*

***辅助空间**：O（N）*



* * *

* * *



