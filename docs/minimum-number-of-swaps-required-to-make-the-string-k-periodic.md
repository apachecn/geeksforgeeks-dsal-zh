# 使字符串`K`变为周期性所需的最小交换数量

> 原文：[https://www.geeksforgeeks.org/minimum-number-of-swaps-required-to-make-the-string-k-periodic/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-to-make-the-string-k-periodic/)

给定长度为`N`的字符串`S`以及由小写字母组成的数组`A`。 还给出一个正整数`K`。 任务是找到使字符串`S`具有周期`K`所需的最小交换次数（在`S`和`A`之间）。

**注意**：

*   如果对于字符串中的每个位置`i`，`S[i] = S[i + K]`，则该字符串都称为具有周期`K`。

*   一次只能将`S`的一个字符替换为`A`的字符。

*   `A`中的字符可以多次使用。

**示例**：

> **输入**：`S = "nihsiakyt", K = 3, A = ['n', 'i', 'p', 's', 'q']`
>
> **输出**：6
>
> **说明**：
>
> 考虑字符串`S`从 0 开始的位置：
>
> 位置 3、6 应替换为`n`。
>
> 位置 7 应该替换为`i`。
>
> 位置 2、5、8 可以用`A`中的任何字符替换，以使字符串变为`K`周期性。
>
> 最后为周期为 3 的字符串：`"nisnisnis"`。
>
> 因此，所需的最小替换为 6
> 
> **输入**：`S = "abcdeactr", K = 4, A = ['a', 'c', 'p']`
>
> **输出**：5
>
> **说明**：
>
> 总共需要进行 5 次更改才能使字符串具有周期 4。

**方法**：可以借助[频率计数](https://www.geeksforgeeks.org/tag/frequency-counting/)和[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)解决此问题。

1.  为了解决上述问题，我们使用二维数组`freq[K][26]`将所有`0 <= j < N`的字符频率存储在`j % K`位置。

2.  使用**布尔数组**标记数组`A`中存在的所有字符。

3.  对于 0 到`K`范围内的所有字符，将有`N / K`或`N / K + 1`字符，它们应该相同。

4.  因此，对于所有这些字符，我们检查哪个字符在位置`i`处具有**最大频率**，并且也出现在数组`A`中。

5.  将其添加到答案中，即`N / K - maxfrequency`。

6.  如果`i % K < N % K`我们还将在答案中加 1

7.  因为所有此类字符都会有`N / K + 1`个字符`i`。

下面是上述方法的实现：

## C++

```cpp

// C++ code to find the minimum 
// number of swaps required to 
// make the string K periodic 

#include <bits/stdc++.h> 
using namespace std; 

int minFlip(string s, int n, 
            int k, char a[], 
            int p) 
{ 
    bool allowed[26] = { 0 }; 

    for (int i = 0; i < p; i++) { 

        // Mark all allowed 
        // characters as true 
        allowed[a[i] - 'a'] = true; 
    } 
    char freq[k][26]; 

    // Initialize the freq array to 0 
    for (int i = 0; i < k; i++) 
        for (int j = 0; j < 26; j++) 
            freq[i][j] = 0; 

    for (int i = 0; i < n; i++) { 

        // Increase the frequency 
        // of each character 
        freq[i % k][s[i] - 'a'] += 1; 
    } 

    int ans = 0; 

    // Total number of periods of 
    // size K in the string 
    int totalpositions = n / k; 

    for (int i = 0; i < k; i++) { 
        int maxfrequency = 0; 

        for (int j = 0; j < 26; j++) { 

            // Check if the current character 
            // is present in allowed 
            // and whether the current 
            // frequency is greater than 
            // all previous frequencies 
            // for this position 
            if (freq[i][j] > maxfrequency 
                and allowed[j] == true) 
                maxfrequency = freq[i][j]; 
        } 

        // update the answer by 
        // subtracting the maxfrequency 
        // from total positions 
        // if there exist extra character 
        // at the end of the string 
        // apart from the n/k characters 
        // then add 1\. 
        ans 
            += (totalpositions 
                - maxfrequency 
                + ((i % k < n % k) 
                       ? 1 
                       : 0)); 
    } 
    cout << ans << endl; 
} 

// Driver code 
int main() 
{ 
    string S = "nihsiakyt"; 
    int n = S.length(); 

    int K = 3; 

    char A[5] 
        = { 'n', 'i', 'p', 's', 'q' }; 
    int p = sizeof(A) / sizeof(A[0]); 

    minFlip(S, n, K, A, p); 

    return 0; 
} 

```

## Java

```java

// Java code to find the minimum 
// number of swaps required to 
// make the String K periodic 
import java.util.*; 

class GFG{ 

static void minFlip(String s, int n, 
                    int k, char a[], 
                    int p) 
{ 
    boolean allowed[] = new boolean[26]; 

    for(int i = 0; i < p; i++) 
    { 

       // Mark all allowed 
       // characters as true 
       allowed[a[i] - 'a'] = true; 
    } 
    char [][]freq = new char[k][26]; 

    // Initialize the freq array to 0 
    for(int i = 0; i < k; i++) 
       for(int j = 0; j < 26; j++) 
          freq[i][j] = 0; 

    for(int i = 0; i < n; i++) 
    { 

       // Increase the frequency 
       // of each character 
       freq[i % k][s.charAt(i) - 'a'] += 1; 
    } 

    int ans = 0; 

    // Total number of periods  
    // of size K in the String 
    int totalpositions = n / k; 

    for(int i = 0; i < k; i++) 
    { 
       int maxfrequency = 0; 
       for(int j = 0; j < 26; j++) 
       { 

          // Check if the current character 
          // is present in allowed 
          // and whether the current 
          // frequency is greater than 
          // all previous frequencies 
          // for this position 
          if (freq[i][j] > maxfrequency &&  
              allowed[j] == true) 
              maxfrequency = freq[i][j]; 
       } 

       // Update the answer by 
       // subtracting the maxfrequency 
       // from total positions 
       // if there exist extra character 
       // at the end of the String 
       // apart from the n/k characters 
       // then add 1\. 
       ans += (totalpositions -  
                 maxfrequency +  
                  ((i % k < n %  
                    k) ? 1 : 0)); 
    } 
    System.out.print(ans + "\n"); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    String S = "nihsiakyt"; 
    int n = S.length(); 
    int K = 3; 

    char []A = { 'n', 'i', 'p', 's', 'q' }; 
    int p = A.length; 

    minFlip(S, n, K, A, p); 
} 
} 

// This code is contributed by Amit Katiyar 

```

## Python3

```py

# Python3 code to find the minimum 
# number of swaps required to 
# make the string K periodic 
def minFlip(s, n, k, a, p): 

    allowed = [0] * 26

    for i in range(p): 

        # Mark all allowed 
        # characters as true 
        allowed[ord(a[i]) - ord('a')] = True

    freq = [[0 for x in range(26)] 
               for y in range(k)] 

    # Initialize the freq array to 0 
    for i in range(k): 
        for j in range(26): 
            freq[i][j] = 0

    for i in range(n): 

        # Increase the frequency 
        # of each character 
        freq[i % k][ord(s[i]) - ord('a')] += 1

    ans = 0

    # Total number of periods of 
    # size K in the string 
    totalpositions = n // k 

    for i in range(k): 
        maxfrequency = 0
        for j in range(26): 

            # Check if the current character 
            # is present in allowed 
            # and whether the current 
            # frequency is greater than 
            # all previous frequencies 
            # for this position 
            if (freq[i][j] > maxfrequency and 
                allowed[j] == True): 
                maxfrequency = freq[i][j] 

        # Update the answer by 
        # subtracting the maxfrequency 
        # from total positions 
        # if there exist extra character 
        # at the end of the string 
        # apart from the n/k characters 
        # then add 1.  
        ans += (totalpositions - maxfrequency) 
        if (i % k < n % k): 
            ans += 1

    print(ans) 

# Driver code 
if __name__ == "__main__": 

    S = "nihsiakyt"
    n = len(S) 

    K = 3

    A = [ 'n', 'i', 'p', 's', 'q' ] 
    p = len(A) 

    minFlip(S, n, K, A, p) 

# This code is contributed by chitranayal 

```

## C#

```cs

// C# code to find the minimum 
// number of swaps required to 
// make the String K periodic 
using System; 

class GFG{ 

static void minFlip(String s, int n, 
                    int k, char []a, 
                    int p) 
{ 
    bool []allowed = new bool[26]; 

    for(int i = 0; i < p; i++) 
    { 

       // Mark all allowed 
       // characters as true 
       allowed[a[i] - 'a'] = true; 
    } 
    char [,]freq = new char[k, 26]; 

    // Initialize the freq array to 0 
    for(int i = 0; i < k; i++) 
       for(int j = 0; j < 26; j++) 
          freq[i, j] = (char)0; 

    for(int i = 0; i < n; i++) 
    { 

       // Increase the frequency 
       // of each character 
       freq[i % k, s[i] - 'a'] += (char)1; 
    } 

    int ans = 0; 

    // Total number of periods  
    // of size K in the String 
    int totalpositions = n / k; 

    for(int i = 0; i < k; i++) 
    { 
       int maxfrequency = 0; 
       for(int j = 0; j < 26; j++) 
       { 

          // Check if the current character 
          // is present in allowed 
          // and whether the current 
          // frequency is greater than 
          // all previous frequencies 
          // for this position 
          if (freq[i, j] > maxfrequency &&  
              allowed[j] == true) 
              maxfrequency = freq[i, j]; 
       } 

       // Update the answer by 
       // subtracting the maxfrequency 
       // from total positions 
       // if there exist extra character 
       // at the end of the String 
       // apart from the n/k characters 
       // then add 1\. 
       ans += (totalpositions -  
                 maxfrequency +  
                  ((i % k < n %  
                    k) ? 1 : 0)); 
    } 
    Console.Write(ans + "\n"); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    String S = "nihsiakyt"; 
    int n = S.Length; 
    int K = 3; 

    char []A = { 'n', 'i', 'p', 's', 'q' }; 
    int p = A.Length; 

    minFlip(S, n, K, A, p); 
} 
} 

// This code is contributed by Rohit_ranjan 

```

**输出**： 

```
6

```



* * *

* * *



