# 所有子串的计数，权重总和最多为 K

> 原文：[https://www.geeksforgeeks.org/count-of-all-sub-strings-with-sum-of-weights-at-most-k/](https://www.geeksforgeeks.org/count-of-all-sub-strings-with-sum-of-weights-at-most-k/)

给定由小英文字母组成的字符串 S 和由英文字母所有字符的权重组成的字符串 W，其中所有 i 均为![0 \leq Qi \leq 9 ](img/1a0542546fd5c88cb155251f79c599b2.png "Rendered by QuickLaTeX.com")。 我们必须找到唯一的子字符串的总数，其权重之和最多为 K。

**示例**：

> **输入**：P =“ ababab”，Q =“ 12345678912345678912345678”，K = 5
> **输出**：7
> **说明**：
> 唯一的子字符串是：“ a”，“ ab”，“ b”，“ bc”，“ c”，“ d”，“ e”。
> 因此，计数为 7。
> 
> **输入**：P =“ acbacbacaa”，Q =“ 12300045600078900012345000”，K = 2
> **输出**：3
> **说明**：唯一的子字符串是 ：“ a”，“ b”，“ aa”
> 因此，计数为 3。

**方法**：

为了解决上述问题，主要思想是简单地循环访问所有子字符串，并保持到目前为止遇到的所有字符的权重之和。 如果字符的总和不大于 K，则将其插入哈希映射中，否则将其丢弃并与另一个子字符串一起前进。 最后，结果将是哈希映射的大小，因为它存储了权重小于或等于 K 的所有子字符串。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to Count all 
// sub-strings with sum of weights at most K 

#include <bits/stdc++.h> 
using namespace std; 

// Function to count all substrings 
int distinctSubstring(string& P, string& Q, 
                      int K, int N) 
{ 

    // Hashmap to store substrings 
    unordered_set<string> S; 

    // iterate over all substrings 
    for (int i = 0; i < N; ++i) { 

        // variable to maintain sum 
        // of all characters encountered 
        int sum = 0; 

        // variable to maintain 
        // substring till current position 
        string s; 

        for (int j = i; j < N; ++j) { 
            // get position of 
            // character in string W 
            int pos = P[j] - 'a'; 

            // add weight to current sum 
            sum += Q[pos] - '0'; 

            // add current character to substring 
            s += P[j]; 

            // check if sum of characters 
            // is <=K insert in Hashmap 
            if (sum <= K) { 
                S.insert(s); 
            } 
            else { 
                break; 
            } 
        } 
    } 

    return S.size(); 
} 

// Driver code 
int main() 
{ 
    // initialise string 
    string S = "abcde"; 

    // initialise weight 
    string W = "12345678912345678912345678"; 

    int K = 5; 

    int N = S.length(); 

    cout << distinctSubstring(S, W, K, N); 

    return 0; 
} 

```

## Java

```java

// Java implementation to count all  
// sub-strings with sum of weights at most K  
import java.io.*; 
import java.util.*;  

class GFG{ 

// Function to count all substrings  
static int distinctSubstring(String P, String Q,  
                             int K, int N)  
{  

    // Hashmap to store substrings  
    Set<String> S = new HashSet<>();  

    // Iterate over all substrings  
    for(int i = 0; i < N; ++i) 
    {  

        // Variable to maintain sum  
        // of all characters encountered  
        int sum = 0;  

        // Variable to maintain substring 
        // till current position  
        String s = "";  

        for(int j = i; j < N; ++j) 
        { 

            // Get position of  
            // character in string W  
            int pos = P.charAt(j) - 'a';  

            // Add weight to current sum  
            sum += Q.charAt(pos) - '0';  

            // Add current character to substring  
            s += P.charAt(j);  

            // Check if sum of characters  
            // is <=K insert in Hashmap  
            if (sum <= K) 
            {  
                S.add(s);  
            }  
            else
            {  
                break;  
            }  
        }  
    }  
    return S.size();  
}  

// Driver Code  
public static void main(String args[]) 
{  

    // Initialise string  
    String S = "abcde";  

    // Initialise weight  
    String W = "12345678912345678912345678";  

    int K = 5;  
    int N = S.length();  

    System.out.println(distinctSubstring(S, W, K, N));  
} 
}  

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 implementation to Count all 
# sub-strings with sum of weights at most K 

# Function to count all substrings 
def distinctSubstring(P, Q, K, N): 

    # Hashmap to store substrings 
    S = set() 

    # iterate over all substrings 
    for i in range(N): 

        # variable to maintain sum 
        # of all characters encountered 
        sum = 0

        # variable to maintain 
        # substring till current position 
        s = "" 

        for j in range(i, N): 

            # get position of 
            # character in string W 
            pos = ord(P[j]) - 97

            # add weight to current sum 
            sum += ord(Q[pos]) - 48

            # add current character to substring 
            s += P[j] 

            # check if sum of characters 
            # is <=K insert in Hashmap 
            if (sum <= K): 
                S.add(s) 

            else: 
                break

    return len(S) 

# Driver code 
if __name__ == '__main__': 
    # initialise string 
    S = "abcde"

    # initialise weight 
    W = "12345678912345678912345678"

    K = 5

    N = len(S) 

    print(distinctSubstring(S, W, K, N)) 

# This code is contributed by Surendra_Gangwar 

```

**Output:** 

```
7

```



* * *

* * *



