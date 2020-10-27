# 计算具有不同首尾字符的子字符串

给定字符串 **S** ，任务是打印给定字符串的子字符串计数，该字符串的首字符和尾字符不同。

**示例**：

> **输入**：S =“ abcab”
> **输出**：8
> **说明**：。
> 有 8 个子字符串，其首尾字符不同{ ab，abc，abcab，bc，bca，ca，cab，ab}。
> 
> **输入**：S =“ aba”
> **输出**：2
> **说明**：
> 有 2 个子字符串，其首尾字符不同{ ab，ba}。

**天真的方法**：的想法是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有可能的子字符串，并为每个子字符串检查第一个和最后一个字符是否不同。 如果发现是真的，则将**计数**加 1，然后检查下一个子字符串。 遍历所有子字符串后打印计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to count the substrings 
// having different first and last 
// characters 
int countSubstring(string s, int n) 
{ 
    // Store the final count 
    int ans = 0; 

    // Loop to traverse the string 
    for (int i = 0; i < n; i++) { 

        // Counter for each iteration 
        int cnt = 0; 

        // Iterate over substrings 
        for (int j = i + 1; j < n; j++) { 

            // Compare the characters 
            if (s[j] != s[i]) 

                // Increase count 
                cnt++; 
        } 

        // Adding count of substrings 
        // to the final count 
        ans += cnt; 
    } 

    // Print the final count 
    cout << ans; 
} 

// Driver Code 
int main() 
{ 
    // Given string 
    string S = "abcab"; 

    // Length of the string 
    int N = 5; 

    // Function Call 
    countSubstring(S, N); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach  
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class GFG{ 

// Function to count the substrings 
// having different first and last 
// characters 
static void countSubstring(String s, int n) 
{ 

    // Store the final count 
    int ans = 0; 

    // Loop to traverse the string 
    for(int i = 0; i < n; i++) 
    { 

        // Counter for each iteration 
        int cnt = 0; 

        // Iterate over substrings 
        for(int j = i + 1; j < n; j++) 
        { 

            // Compare the characters 
            if (s.charAt(j) != s.charAt(i)) 

                // Increase count 
                cnt++; 
        } 

        // Adding count of substrings 
        // to the final count 
        ans += cnt; 
    } 

    // Print the final count 
    System.out.print(ans); 
} 

// Driver Code 
public static void main(String[] args) 
{ 

    // Given string 
    String S = "abcab"; 

    // Length of the string 
    int N = 5; 

    // Function call 
    countSubstring(S, N); 
} 
} 

// This code is contributed by code_hunt 

```

## Python3

```py

# Python3 program for the above approach 

# Function to count the substrings 
# having different first and last 
# characters 
def countSubstring(s, n): 

    # Store the final count 
    ans = 0

    # Loop to traverse the string 
    for i in range(n): 

        # Counter for each iteration 
        cnt = 0

        # Iterate over substrings 
        for j in range(i + 1, n): 

            # Compare the characters 
            if (s[j] != s[i]): 

                # Increase count 
                cnt += 1

        # Adding count of substrings 
        # to the final count 
        ans += cnt 

    # Print the final count 
    print(ans) 

# Driver Code 

# Given string 
S = "abcab"

# Length of the string 
N = 5

# Function call 
countSubstring(S, N) 

# This code is contributed by code_hunt 

```

## C#

```cs

// C# program for the above approach 
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  

class GFG{ 

// Function to count the substrings 
// having different first and last 
// characters 
static void countSubstring(string s, int n) 
{ 

    // Store the final count 
    int ans = 0; 

    // Loop to traverse the string 
    for(int i = 0; i < n; i++) 
    { 

        // Counter for each iteration 
        int cnt = 0; 

        // Iterate over substrings 
        for(int j = i + 1; j < n; j++) 
        { 

            // Compare the characters 
            if (s[j] != s[i]) 

                // Increase count 
                cnt++; 
        } 

        // Adding count of substrings 
        // to the final count 
        ans += cnt; 
    } 

    // Print the final count 
    Console.Write(ans); 
} 

// Driver Code 
public static void Main(string[] args) 
{ 

    // Given string 
    string S = "abcab"; 

    // Length of the string 
    int N = 5; 

    // Function call 
    countSubstring(S, N); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output:** 

```
8

```

***时间复杂度**：O（N <sup>2</sup> ）*
***辅助空间**：O（1）*

**高效方法**：可以使用[通过](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)[映射](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)来优化上述方法，以存储字符串字符的频率。 请按照以下步骤解决问题：

1.  初始化**两个**变量，一个用于为每次迭代计数不同的字符（例如 **cur** ），另一个用于存储子字符串的最终计数（例如 **an** ）。
2.  初始化映射 **M** 以在其中存储所有字符的频率。
3.  [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，对于每个字符，请按照以下步骤操作：
    *   迭代映射 **M** 。
    *   如果地图的第一个元素（即**键**）与当前字符不同，则继续操作。
    *   否则，添加与当前字符对应的值。
4.  遍历**映射**后，将 **cur** 添加到最终结果，即 **ans + = cur** 。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to count the substrings 
// having different first & last character 
int countSubstring(string s, int n) 
{ 
    // Stores frequency of each char 
    map<char, int> m; 

    // Loop to store frequency of 
    // the characters in a Map 
    for (int i = 0; i < n; i++) 
        m[s[i]]++; 

    // To store final result 
    int ans = 0; 

    // Traversal of string 
    for (int i = 0; i < n; i++) { 

        // Store answer for every 
        // iteration 
        int cnt = 0; 
        m[s[i]]--; 

        // Map traversal 
        for (auto value : m) { 

            // Compare current char 
            if (value.first == s[i]) { 
                continue; 
            } 
            else { 
                cnt += value.second; 
            } 
        } 

        ans += cnt; 
    } 

    // Print the final count 
    cout << ans; 
} 

// Driver Code 
int main() 
{ 
    // Given string 
    string S = "abcab"; 

    // Length of the string 
    int N = 5; 

    // Function Call 
    countSubstring(S, N); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG{ 

// Function to count the subStrings 
// having different first & last character 
static void countSubString(char []s, int n) 
{ 

    // Stores frequency of each char 
    HashMap<Character, 
            Integer> mp = new HashMap<Character, 
                                      Integer>(); 

    // Loop to store frequency of 
    // the characters in a Map 
    for(int i = 0; i < n; i++) 

        if (mp.containsKey(s[i])) 
        { 
            mp.put(s[i], mp.get(s[i]) + 1); 
        } 
        else
        { 
            mp.put(s[i], 1); 
        } 

    // To store final result 
    int ans = 0; 

    // Traversal of String 
    for(int i = 0; i < n; i++) 
    { 

        // Store answer for every 
        // iteration 
        int cnt = 0; 
        if (mp.containsKey(s[i])) 
        { 
            mp.put(s[i], mp.get(s[i]) - 1); 

            // Map traversal 
            for(Map.Entry<Character, 
                          Integer> value : mp.entrySet()) 
            { 

                // Compare current char 
                if (value.getKey() == s[i]) 
                { 
                    continue; 
                } 
                else 
                { 
                    cnt += value.getValue(); 
                } 
            } 
            ans += cnt; 
        } 
    } 

    // Print the final count 
    System.out.print(ans); 
} 

// Driver Code 
public static void main(String[] args) 
{ 

    // Given String 
    String S = "abcab"; 

    // Length of the String 
    int N = 5; 

    // Function call 
    countSubString(S.toCharArray(), N); 
} 
} 

// This code is contributed by Amit Katiyar

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to count the subStrings 
// having different first & last character 
static void countSubString(char []s, int n) 
{ 

    // Stores frequency of each char 
    Dictionary<char, 
               int> mp = new Dictionary<char, 
                                        int>(); 

    // Loop to store frequency of 
    // the characters in a Map 
    for(int i = 0; i < n; i++) 

        if (mp.ContainsKey(s[i])) 
        { 
            mp[s[i]] = mp[s[i]] + 1; 
        } 
        else
        { 
            mp.Add(s[i], 1); 
        } 

    // To store readonly result 
    int ans = 0; 

    // Traversal of String 
    for(int i = 0; i < n; i++) 
    { 

        // Store answer for every 
        // iteration 
        int cnt = 0; 
        if (mp.ContainsKey(s[i])) 
        { 
            mp[s[i]] = mp[s[i]] - 1; 

            // Map traversal 
            foreach(KeyValuePair<char, 
                                 int> value in mp) 
            { 

                // Compare current char 
                if (value.Key == s[i]) 
                { 
                    continue; 
                } 
                else
                { 
                    cnt += value.Value; 
                } 
            } 
            ans += cnt; 
        } 
    } 

    // Print the readonly count 
    Console.Write(ans); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 

    // Given String 
    String S = "abcab"; 

    // Length of the String 
    int N = 5; 

    // Function call 
    countSubString(S.ToCharArray(), N); 
} 
} 

// This code is contributed by Amit Katiyar

```

**Output:** 

```
8

```

***时间复杂度**：O（N * 26）*
***辅助空间**：O（N）*



* * *

* * *



