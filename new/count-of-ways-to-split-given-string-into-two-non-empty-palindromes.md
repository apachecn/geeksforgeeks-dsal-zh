# 将给定字符串拆分为两个非空回文的方法的数量

> 原文：[https://www.geeksforgeeks.org/count-of-ways-to-split-given-string-into-two-non-empty-palindromes/](https://www.geeksforgeeks.org/count-of-ways-to-split-given-string-into-two-non-empty-palindromes/)

给定字符串`S`，任务是找到将给定字符串`S`分为两个非空回文字符串的方法。

**示例**：

> **输入**：`S = "aaaaa"`
>
> **输出**：4
>
> **说明**：
>
> 可能的分割：`{"a", "aaaa"}, {"aa", "aaa"}, {"aaa", "aa"}, {"aaaa", "a"}`
> 
> **输入**：`S = "abacc"`
>
> **输出**：1
>
> **说明**：
>
> 仅可能的拆分是`"aba", "cc"`。

**朴素方法**：朴素方法是在每个可能的索引处分割字符串，并检查两个子字符串是否都是回文。 如果是，则增加该索引的**计数**。 打印最终的**计数**。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 
#include<bits/stdc++.h> 
using namespace std; 

// Function to check whether the 
// substring from l to r is 
// palindrome or not 
bool isPalindrome(int l, int r, 
                  string& s) 
{ 

    while (l <= r) { 

        // If characters at l and 
        // r differ 
        if (s[l] != s[r]) 

            // Not a palindrome 
            return false; 

        l++; 
        r--; 
    } 

    // If the string is 
    // a palindrome 
    return true; 
} 

// Function to count and return 
// the number of possible splits 
int numWays(string& s) 
{ 
    int n = s.length(); 

    // Stores the count 
    // of splits 
    int ans = 0; 
    for (int i = 0; 
         i < n - 1; i++) { 

        // Check if the two substrings 
        // after the split are 
        // palindromic or not 
        if (isPalindrome(0, i, s) 
            && isPalindrome(i + 1, 
                            n - 1, s)) { 

            // If both are palindromes 
            ans++; 
        } 
    } 

    // Print the final count 
    return ans; 
} 

// Driver Code 
int main() 
{ 
    string S = "aaaaa"; 

    cout << numWays(S); 
    return 0; 
} 

```

## Java

```java

// Java program to implement 
// the above approach 
class GFG{ 

// Function to check whether the 
// substring from l to r is 
// palindrome or not 
public static boolean isPalindrome(int l, int r, 
                                   String s) 
{ 
    while (l <= r) 
    { 

        // If characters at l and 
        // r differ 
        if (s.charAt(l) != s.charAt(r)) 

            // Not a palindrome 
            return false; 

        l++; 
        r--; 
    } 

    // If the string is 
    // a palindrome 
    return true; 
} 

// Function to count and return 
// the number of possible splits 
public static int numWays(String s) 
{ 
    int n = s.length(); 

    // Stores the count 
    // of splits 
    int ans = 0; 
    for(int i = 0; i < n - 1; i++) 
    { 

       // Check if the two substrings 
       // after the split are 
       // palindromic or not 
       if (isPalindrome(0, i, s) &&  
           isPalindrome(i + 1, n - 1, s)) 
       { 

           // If both are palindromes 
           ans++; 
       } 
    } 

    // Print the final count 
    return ans; 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    String S = "aaaaa"; 

    System.out.println(numWays(S)); 
} 
} 

// This code is contributed by SoumikMondal 

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to check whether the 
# substring from l to r is 
# palindrome or not 
def isPalindrome(l, r, s): 

    while (l <= r): 

        # If characters at l and 
        # r differ 
        if (s[l] != s[r]): 

            # Not a palindrome 
            return bool(False) 

        l += 1
        r -= 1

    # If the string is 
    # a palindrome 
    return bool(True) 

# Function to count and return 
# the number of possible splits 
def numWays(s): 

    n = len(s) 

    # Stores the count 
    # of splits 
    ans = 0
    for i in range(n - 1): 

        # Check if the two substrings 
        # after the split are 
        # palindromic or not 
        if (isPalindrome(0, i, s) and 
            isPalindrome(i + 1, n - 1, s)): 

            # If both are palindromes 
            ans += 1

    # Print the final count 
    return ans 

# Driver Code 
S = "aaaaa"

print(numWays(S)) 

# This code is contributed by divyeshrabadiya07 

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 
class GFG{ 

// Function to check whether the 
// substring from l to r is 
// palindrome or not 
public static bool isPalindrome(int l, int r, 
                                string s) 
{ 
    while (l <= r) 
    { 

        // If characters at l and 
        // r differ 
        if (s[l] != s[r]) 

            // Not a palindrome 
            return false; 

        l++; 
        r--; 
    } 

    // If the string is 
    // a palindrome 
    return true; 
} 

// Function to count and return 
// the number of possible splits 
public static int numWays(string s) 
{ 
    int n = s.Length; 

    // Stores the count 
    // of splits 
    int ans = 0; 
    for(int i = 0; i < n - 1; i++) 
    { 

       // Check if the two substrings 
       // after the split are 
       // palindromic or not 
       if (isPalindrome(0, i, s) &&  
           isPalindrome(i + 1, n - 1, s)) 
       { 

           // If both are palindromes 
           ans++; 
       } 
    } 

    // Print the final count 
    return ans; 
} 

// Driver Code 
public static void Main(string []args) 
{ 
    string S = "aaaaa"; 

    Console.Write(numWays(S)); 
} 
} 

// This code is contributed by Rutvik

```

**Output:** 

```
4

```

**时间复杂度**：`O(N ^ 2)`

**有效方法**：可以使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)和 [Rabin-Karp 算法](https://www.geeksforgeeks.org/rabin-karp-algorithm-for-pattern-searching/)来存储字符串的**前缀和后缀哈希**，从而优化上述方法 。 请按照以下步骤解决问题：

*   计算给定字符串的前缀和后缀哈希。

*   对于`[1, N – 1]`范围内的每个索引`i`，检查两个子字符串`[0, i – 1]`和`[i, N – 1]`是否为回文。

*   要检查子字符串`[l, r]`是否是回文，只需检查：

    ```
    PrefixHash[l - r] = SuffixHash[l - r]

    ```

*   对于每个发现有两个子串都是回文的索引`i`，增加**计数**。

*   打印**计数**的最终值。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement 
// the above approach 

#include  
using namespace std; 

// Modulo for rolling hash 
const int MOD = 1e9 + 9; 

// Small prime for rolling hash 
const int P = 37; 

// Maximum length of string 
const int MAXN = 1e5 + 5; 

// Stores prefix hash 
vector prefixHash(MAXN); 

// Stores suffix hash 
vector suffixHash(MAXN); 

// Stores inverse modulo 
// of P for prefix 
vector inversePrefix(MAXN); 

// Stores inverse modulo 
// of P for suffix 
vector inverseSuffix(MAXN); 

int n; 
int power(int x, int y, int mod) 
{ 
    // Function to compute 
    // power under modulo 
    if (x == 0) 
        return 0; 

    int ans = 1; 
    while (y > 0) { 
        if (y & 1) 
            ans = (1LL * ans * x) 
                % MOD; 

        x = (1LL * x * x) % MOD; 
        y >>= 1; 
    } 
    return ans; 
} 

// Precompte hashes for the 
// given string 
void preCompute(string& s) 
{ 

    int x = 1; 
    for (int i = 0; i 0) 
            prefixHash[i] 
                = (prefixHash[i] 
                + prefixHash[i - 1]) 
                % MOD; 

        // Compute inverse modulo 
        // of P ^ i for division 
        // using Fermat Little theorem 
        inversePrefix[i] = power(x, MOD - 2, 
                                MOD); 

        x = (1LL * x * P) % MOD; 
    } 

    x = 1; 

    // Calculate suffix hash 
    for (int i = n - 1; i >= 0; i--) { 

        // Calculate and store hash 
        suffixHash[i] 
            = (1LL * int(s[i] 
                        - 'a' + 1) 
            * x) 
            % MOD; 

        if (i 0 
                ? prefixHash[l - 1] 
                : 0); 
    h = (h + MOD) % MOD; 
    h = (1LL * h * inversePrefix[l]) 
        % MOD; 

    return h; 
} 

// Function to return Suffix 
// Hash of substring 
int getSuffixHash(int l, int r) 
{ 
    // Calculate suffix hash 
    // from l to r 
    int h = suffixHash[l] 
            - (r < n - 1 
                ? suffixHash[r + 1] 
                : 0); 

    h = (h + MOD) % MOD; 
    h = (1LL * h * inverseSuffix[r]) 
        % MOD; 

    return h; 
} 

int numWays(string& s) 
{ 
    n = s.length(); 

    // Compute prefix and 
    // suffix hashes 
    preCompute(s); 

    // Stores the number of 
    // possible splits 
    int ans = 0; 
    for (int i = 0; 
        i < n - 1; i++) { 

        int preHash = getPrefixHash(0, i); 
        int sufHash = getSuffixHash(0, i); 

        // If the substring s[0]...s[i] 
        // is not palindromic 
        if (preHash != sufHash) 
            continue; 

        preHash = getPrefixHash(i + 1, 
                                n - 1); 
        sufHash = getSuffixHash(i + 1, 
                                n - 1); 

        // If the substring (i + 1, n - 1) 
        // is not palindromic 
        if (preHash != sufHash) 
            continue; 

        // If both are palindromic 
        ans++; 
    } 

    return ans; 
} 

// Driver Code 
int main() 
{ 
    string s = "aaaaa"; 

    int ans = numWays(s); 

    cout << ans << endl; 

    return 0; 
} 

```

**Output:** 

```
4

```

**时间复杂度**：`O(N * log(10 ^ 9))`

**空间复杂度**：`O(n)`



* * *

* * *



