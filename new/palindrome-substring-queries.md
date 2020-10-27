# 回文子串查询

给定一个字符串和对给定输入字符串的子字符串的几个查询，以检查该子字符串是否是回文。

**示例：**

> 假设我们的输入字符串为“ abaaabaaaba”，并且查询为[0，10]，[5，8]，[2，5]，[5，9]
> 
> 我们必须告诉我们，具有上述开始和结束索引的子字符串是否是回文。
> 
> [0，10]→子字符串是回文“ abaaabaaaba”。
> [5，8]→子字符串是“ baaa”，不是回文。
> [2，5]→子字符串是“ aaab”，不是回文。
> [5，9]→子串是回文的“ baaab”。

让我们假设有 Q 个这样的查询要回答，N 是我们输入字符串的长度。 有以下两种方式来回答这些查询

<center>**Method 1 (Naive)**</center>

One by one we go through all the substrings of the queries and check whether the substring under consideration is a palindrome or not.

由于存在 Q 个查询，每个查询可能需要 O（N）个最坏情况的时间来回答，因此此方法在最坏情况下需要 O（Q.N）个时间。 尽管这是一种就地/空间高效的算法，但仍有一种更有效的方法可以做到这一点。

<center>**Method 2 (Cumulative Hash)**</center>

The idea is similar to [Rabin Karp string matching](https://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/). We use string hashing. What we do is that we calculate cumulative hash values of the string in the original string as well as the reversed string in two arrays- prefix[] and suffix[].

如何计算累积哈希值？

假设我们的字符串是 str []，则填充我们使用的 prefix []数组的累积哈希函数为-

> prefix [0] = 0
> prefix [i] = str [0] + str [1] * 101 + str [2] * 101 <sup>2</sup> +……+ str [i-1] * 101 <sup>i-1</sup>
> 
> 例如，使用字符串“ abaaabxyaba”
> 
> prefix [0] = 0
> prefix [1] = 97（“ a”的 ASCII 值为 97）
> prefix [2] = 97 + 98 * 101
> prefix [3] = 97 + 98 * 101 + 97 * 101 <sup>2</sup>
> …………………………
> …………………………
> 前缀[11] = 97 + 98 * 101 + 97 * 101 <sup>2</sup> +…….. + 97 * 101 <sup>10</sup>

现在以这种方式进行存储的原因是，我们可以轻松地在 O（1）时间中找到任何子字符串的哈希值-

```
 hash(L, R) = prefix[R+1] – prefix[L]

```

例如，哈希（1，5）=哈希（“ baaab”）=前缀[6] –前缀[1] = 98 * 101 + 97 * 101 <sup>2</sup> + 97 * 101 <sup>3</sup> + 97 * 101 <sup>4</sup> + 98 * 101 <sup>5</sup> = 1040184646587 [我们稍后将使用此怪异值来解释发生的事情]。

与此类似，我们将 suffix []数组填充为-

> 后缀[0] = 0
> 后缀[i] = str [n-1] + str [n-2] * 10 <sup>1</sup> + str [n-3] * 101 <sup>2</sup> +……+ str [ni] * 101 <sup>i-1</sup>
> 
> 例如，使用字符串“ abaaabxyaba”
> 
> 后缀[0] = 0
> 后缀[1] = 97（'a'的 ASCII 值为 97）
> 后缀[2] = 97 + 98 * 101
> 后缀[3] = 97 + 98 * 101 + 97 * 101 <sup>2</sup>
> …………………………
> …………………………后缀
> 后缀[11] = 97 + 98 * 101 + 97 * 101 <sup>2</sup> +…….. + 97 * 101 <sup>10</sup>
> 
> 现在以这种方式存储的原因是，我们可以使用 O（1）时间轻松找到任何子字符串的反向哈希值
> 
> ```
> reverse_hash(L, R) = hash (R, L) = suffix[n-L] – suffix[n-R-1] 
> ```
> 
> 其中 n =字符串的长度。
> 
> > 对于“ abaaabxyaba”，n = 11
> > reverse_hash（1，5）= reverse_hash（“ baaab”）= hash（“ baaab”）[反转“ baaab”即得出“ baaab”]
> > 
> > hash（“ baaab”）=后缀[11-1] –后缀[11-5-1] =后缀[10] –后缀[5] = 98 * 101 <sup>5</sup> + 97 * 101 <sup>6</sup> + 97 * 101 <sup>7</sup> + 97 * 101 <sup>8</sup> + 98 * 101 <sup>9</sup> = 108242031437886501387
> 
> 现在，这两个怪异的整数之间似乎没有任何关系– 1040184646587 和 108242031437886501387
> 
> 再想一想。 这两个大整数之间有关系吗？
> 
> 是的，确实存在，这种观察是本程序/文章的核心。
> 
> > 1040184646587 * 101 <sup>4</sup> = 108242031437886501387
> 
> 尝试考虑一下，您将发现任何从索引 L 开始到索引 R 结束的子串（包括两端）将是回文
> 
> > （前缀[R + 1] –前缀[L]）/（101 <sup>L</sup> ）=（后缀[n – L] –后缀[n – R-1]）/（101 <sup>n – R – 1</sup> ）
> 
> 其余部分只是实现。
> 
> 程序中的功能 computerPowers（）使用动态编程来计算 101 的幂。
> 
> **溢出问题：**
> 同样，我们可以看到，即使是很小的字符串，哈希值和反向哈希值也可能变得很大–8。因为 C 和 C++不提供对此类哈希值的支持 大量，因此将导致溢出。 为避免这种情况，我们将对素数取模（出于某些特定的数学原因选择质数）。 我们选择适合整数的最大可能素数。 最好的此类值为 1000000007。因此，所有运算都以 1000000007 为模。
> 
> 但是，Java 和 Python 没有这些问题，可以在没有模运算符的情况下实现。
> 
> 下面列出了程序中广泛使用的基本模运算。
> **1）添加-**
> 
> > （a + b）％M =（a％M + b％M）％M
> > （a + b + c）％M =（a％M + b％M + c％M）％M
> > （a + b + c + d）％M =（a％M + b％M + c％M + d％M）％M
> > …。 …..…..……
> > …。 …..…..……
> 
> **2）乘法-**
> 
> > （a * b）％M =（a * b）％M
> > （a * b * c）％M =（（a * b）％M * c％M）％M
> > （a * b * c * d）％M =（（（（（（a * b）％M * c）％M）* d）％M
> > …。 …..…..……
> > …。 …..…..……
> 
> 此属性由 modPow（）函数使用，该函数计算 M 的模数幂
> **3）加法和乘法混合-**
> 
> > （a * x + b * y + c）％M =（（a * x）％M +（b * y）％M + c％M）％M
> 
> **4）减法-**
> 
> > （a – b）％M =（a％M – b％M + M）％M [正确]
> > （a – b）％M =（a％M – b％M）％M [错误]
> 
> **5）分区-**
> 
> > （a / b）％M =（a * MMI（b））％M
> > 
> > 其中 MMI（）是用于计算[模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)的函数。 在我们的程序中，这是通过功能 findMMI（）实现的。
> 
> ## C++
> 
> ```
> 
> /* A C++ program to answer queries to check whether  
> the substrings are palindrome or not efficiently */
> #include <bits/stdc++.h> 
> using namespace std; 
>   
> #define p 101 
> #define MOD 1000000007 
>   
> // Structure to represent a query. A query consists 
> // of (L, R) and we have to answer whether the substring 
> // from index-L to R is a palindrome or not 
> struct Query { 
>     int L, R; 
> }; 
>   
> // A function to check if a string str is palindrome 
> // in the ranfe L to R 
> bool isPalindrome(string str, int L, int R) 
> { 
>     // Keep comparing characters while they are same 
>     while (R > L) 
>         if (str[L++] != str[R--]) 
>             return (false); 
>     return (true); 
> } 
>   
> // A Function to find pow (base, exponent) % MOD 
> // in log (exponent) time 
> unsigned long long int modPow( 
>     unsigned long long int base, 
>     unsigned long long int exponent) 
> { 
>     if (exponent == 0) 
>         return 1; 
>     if (exponent == 1) 
>         return base; 
>   
>     unsigned long long int temp = modPow(base, exponent / 2); 
>   
>     if (exponent % 2 == 0) 
>         return (temp % MOD * temp % MOD) % MOD; 
>     else
>         return (((temp % MOD * temp % MOD) % MOD) 
>                 * base % MOD) 
>                % MOD; 
> } 
>   
> // A Function to calculate Modulo Multiplicative Inverse of 'n' 
> unsigned long long int findMMI(unsigned long long int n) 
> { 
>     return modPow(n, MOD - 2); 
> } 
>   
> // A Function to calculate the prefix hash 
> void computePrefixHash( 
>     string str, int n, 
>     unsigned long long int prefix[], 
>     unsigned long long int power[]) 
> { 
>     prefix[0] = 0; 
>     prefix[1] = str[0]; 
>   
>     for (int i = 2; i <= n; i++) 
>         prefix[i] = (prefix[i - 1] % MOD 
>                      + (str[i - 1] % MOD 
>                         * power[i - 1] % MOD) 
>                            % MOD) 
>                     % MOD; 
>   
>     return; 
> } 
>   
> // A Function to calculate the suffix hash 
> // Suffix hash is nothing but the prefix hash of 
> // the reversed string 
> void computeSuffixHash( 
>     string str, int n, 
>     unsigned long long int suffix[], 
>     unsigned long long int power[]) 
> { 
>     suffix[0] = 0; 
>     suffix[1] = str[n - 1]; 
>   
>     for (int i = n - 2, j = 2; i >= 0 && j <= n; i--, j++) 
>         suffix[j] = (suffix[j - 1] % MOD 
>                      + (str[i] % MOD 
>                         * power[j - 1] % MOD) 
>                            % MOD) 
>                     % MOD; 
>     return; 
> } 
>   
> // A Function to answer the Queries 
> void queryResults(string str, Query q[], int m, int n, 
>                   unsigned long long int prefix[], 
>                   unsigned long long int suffix[], 
>                   unsigned long long int power[]) 
> { 
>     for (int i = 0; i <= m - 1; i++) { 
>         int L = q[i].L; 
>         int R = q[i].R; 
>   
>         // Hash Value of Substring [L, R] 
>         unsigned long long hash_LR 
>             = ((prefix[R + 1] - prefix[L] + MOD) % MOD 
>                * findMMI(power[L]) % MOD) 
>               % MOD; 
>   
>         // Reverse Hash Value of Substring [L, R] 
>         unsigned long long reverse_hash_LR 
>             = ((suffix[n - L] - suffix[n - R - 1] + MOD) % MOD 
>                * findMMI(power[n - R - 1]) % MOD) 
>               % MOD; 
>   
>         // If both are equal then 
>         // the substring is a palindrome 
>         if (hash_LR == reverse_hash_LR) { 
>             if (isPalindrome(str, L, R) == true) 
>                 printf("The Substring [%d %d] is a "
>                        "palindrome\n", 
>                        L, R); 
>             else
>                 printf("The Substring [%d %d] is not a "
>                        "palindrome\n", 
>                        L, R); 
>         } 
>   
>         else
>             printf("The Substring [%d %d] is not a "
>                    "palindrome\n", 
>                    L, R); 
>     } 
>   
>     return; 
> } 
>   
> // A Dynamic Programming Based Approach to compute the 
> // powers of 101 
> void computePowers(unsigned long long int power[], int n) 
> { 
>     // 101^0 = 1 
>     power[0] = 1; 
>   
>     for (int i = 1; i <= n; i++) 
>         power[i] = (power[i - 1] % MOD * p % MOD) % MOD; 
>   
>     return; 
> } 
>   
> /* Driver program to test above function */
> int main() 
> { 
>     string str = "abaaabaaaba"; 
>     int n = str.length(); 
>   
>     // A Table to store the powers of 101 
>     unsigned long long int power[n + 1]; 
>   
>     computePowers(power, n); 
>   
>     // Arrays to hold prefix and suffix hash values 
>     unsigned long long int prefix[n + 1], suffix[n + 1]; 
>   
>     // Compute Prefix Hash and Suffix Hash Arrays 
>     computePrefixHash(str, n, prefix, power); 
>     computeSuffixHash(str, n, suffix, power); 
>   
>     Query q[] = { { 0, 10 }, { 5, 8 }, { 2, 5 }, { 5, 9 } }; 
>     int m = sizeof(q) / sizeof(q[0]); 
>   
>     queryResults(str, q, m, n, prefix, suffix, power); 
>     return (0); 
> } 
> 
> ```
> 
> ## Java
> 
> ```
> 
> /* A Java program to answer queries to check whether  
> the substrings are palindrome or not efficiently */
>   
> public class GFG { 
>   
>     static int p = 101; 
>     static int MOD = 1000000007; 
>   
>     // Structure to represent a query. A query consists 
>     // of (L, R) and we have to answer whether the substring 
>     // from index-L to R is a palindrome or not 
>     static class Query { 
>   
>         int L, R; 
>   
>         public Query(int L, int R) 
>         { 
>             this.L = L; 
>             this.R = R; 
>         } 
>     }; 
>   
>     // A function to check if a string str is palindrome 
>     // in the ranfe L to R 
>     static boolean isPalindrome(String str, int L, int R) 
>     { 
>         // Keep comparing characters while they are same 
>         while (R > L) { 
>             if (str.charAt(L++) != str.charAt(R--)) { 
>                 return (false); 
>             } 
>         } 
>         return (true); 
>     } 
>   
>     // A Function to find pow (base, exponent) % MOD 
>     // in log (exponent) time 
>     static int modPow(int base, int exponent) 
>     { 
>         if (exponent == 0) { 
>             return 1; 
>         } 
>         if (exponent == 1) { 
>             return base; 
>         } 
>   
>         int temp = modPow(base, exponent / 2); 
>   
>         if (exponent % 2 == 0) { 
>             return (temp % MOD * temp % MOD) % MOD; 
>         } 
>         else { 
>             return (((temp % MOD * temp % MOD) % MOD) 
>                     * base % MOD) 
>                 % MOD; 
>         } 
>     } 
>   
>     // A Function to calculate 
>     // Modulo Multiplicative Inverse of 'n' 
>     static int findMMI(int n) 
>     { 
>         return modPow(n, MOD - 2); 
>     } 
>   
>     // A Function to calculate the prefix hash 
>     static void computePrefixHash(String str, int n, 
>                                   int prefix[], int power[]) 
>     { 
>         prefix[0] = 0; 
>         prefix[1] = str.charAt(0); 
>   
>         for (int i = 2; i <= n; i++) { 
>             prefix[i] = (prefix[i - 1] % MOD 
>                          + (str.charAt(i - 1) % MOD 
>                             * power[i - 1] % MOD) 
>                                % MOD) 
>                         % MOD; 
>         } 
>   
>         return; 
>     } 
>   
>     // A Function to calculate the suffix hash 
>     // Suffix hash is nothing but the prefix hash of 
>     // the reversed string 
>     static void computeSuffixHash(String str, int n, 
>                                   int suffix[], int power[]) 
>     { 
>         suffix[0] = 0; 
>         suffix[1] = str.charAt(n - 1); 
>   
>         for (int i = n - 2, j = 2; i >= 0 && j <= n; i--, j++) { 
>             suffix[j] = (suffix[j - 1] % MOD 
>                          + (str.charAt(i) % MOD 
>                             * power[j - 1] % MOD) 
>                                % MOD) 
>                         % MOD; 
>         } 
>         return; 
>     } 
>   
>     // A Function to answer the Queries 
>     static void queryResults( 
>         String str, Query q[], int m, int n, 
>         int prefix[], int suffix[], int power[]) 
>     { 
>         for (int i = 0; i <= m - 1; i++) { 
>             int L = q[i].L; 
>             int R = q[i].R; 
>   
>             // Hash Value of Substring [L, R] 
>             long hash_LR 
>                 = ((prefix[R + 1] - prefix[L] + MOD) % MOD 
>                    * findMMI(power[L]) % MOD) 
>                   % MOD; 
>   
>             // Reverse Hash Value of Substring [L, R] 
>             long reverse_hash_LR 
>                 = ((suffix[n - L] - suffix[n - R - 1] + MOD) % MOD 
>                    * findMMI(power[n - R - 1]) % MOD) 
>                   % MOD; 
>   
>             // If both are equal then the substring is a palindrome 
>             if (hash_LR == reverse_hash_LR) { 
>                 if (isPalindrome(str, L, R) == true) { 
>                     System.out.printf("The Substring [%d %d] is a "
>                                           + "palindrome\n", 
>                                       L, R); 
>                 } 
>                 else { 
>                     System.out.printf("The Substring [%d %d] is not a "
>                                           + "palindrome\n", 
>                                       L, R); 
>                 } 
>             } 
>             else { 
>                 System.out.printf("The Substring [%d %d] is not a "
>                                       + "palindrome\n", 
>                                   L, R); 
>             } 
>         } 
>   
>         return; 
>     } 
>   
>     // A Dynamic Programming Based Approach to compute the 
>     // powers of 101 
>     static void computePowers(int power[], int n) 
>     { 
>         // 101^0 = 1 
>         power[0] = 1; 
>   
>         for (int i = 1; i <= n; i++) { 
>             power[i] = (power[i - 1] % MOD * p % MOD) % MOD; 
>         } 
>   
>         return; 
>     } 
>   
>     /* Driver code */
>     public static void main(String[] args) 
>     { 
>         String str = "abaaabaaaba"; 
>         int n = str.length(); 
>   
>         // A Table to store the powers of 101 
>         int[] power = new int[n + 1]; 
>   
>         computePowers(power, n); 
>   
>         // Arrays to hold prefix and suffix hash values 
>         int[] prefix = new int[n + 1]; 
>         int[] suffix = new int[n + 1]; 
>   
>         // Compute Prefix Hash and Suffix Hash Arrays 
>         computePrefixHash(str, n, prefix, power); 
>         computeSuffixHash(str, n, suffix, power); 
>   
>         Query q[] = { new Query(0, 10), new Query(5, 8), 
>                       new Query(2, 5), new Query(5, 9) }; 
>         int m = q.length; 
>   
>         queryResults(str, q, m, n, prefix, suffix, power); 
>     } 
> } 
>   
> // This code is contributed by Princi Singh 
> 
> ```
> 
> ## C#
> 
> ```
> 
> /* A C# program to answer queries to check whether  
> the substrings are palindrome or not efficiently */
> using System; 
>   
> class GFG { 
>   
>     static int p = 101; 
>     static int MOD = 1000000007; 
>   
>     // Structure to represent a query. A query consists 
>     // of (L, R) and we have to answer whether the substring 
>     // from index-L to R is a palindrome or not 
>     public class Query { 
>   
>         public int L, R; 
>   
>         public Query(int L, int R) 
>         { 
>             this.L = L; 
>             this.R = R; 
>         } 
>     }; 
>   
>     // A function to check if a string str is palindrome 
>     // in the ranfe L to R 
>     static Boolean isPalindrome(String str, int L, int R) 
>     { 
>         // Keep comparing characters while they are same 
>         while (R > L) { 
>             if (str[L++] != str[R--]) { 
>                 return (false); 
>             } 
>         } 
>         return (true); 
>     } 
>   
>     // A Function to find pow (base, exponent) % MOD 
>     // in log (exponent) time 
>     static int modPow(int Base, int exponent) 
>     { 
>         if (exponent == 0) { 
>             return 1; 
>         } 
>         if (exponent == 1) { 
>             return Base; 
>         } 
>   
>         int temp = modPow(Base, exponent / 2); 
>   
>         if (exponent % 2 == 0) { 
>             return (temp % MOD * temp % MOD) % MOD; 
>         } 
>         else { 
>             return (((temp % MOD * temp % MOD) % MOD) * Base % MOD) % MOD; 
>         } 
>     } 
>   
>     // A Function to calculate Modulo Multiplicative Inverse of 'n' 
>     static int findMMI(int n) 
>     { 
>         return modPow(n, MOD - 2); 
>     } 
>   
>     // A Function to calculate the prefix hash 
>     static void computePrefixHash(String str, int n, 
>                                   int[] prefix, int[] power) 
>     { 
>         prefix[0] = 0; 
>         prefix[1] = str[0]; 
>   
>         for (int i = 2; i <= n; i++) { 
>             prefix[i] = (prefix[i - 1] % MOD 
>                          + (str[i - 1] % MOD * power[i - 1] % MOD) % MOD) 
>                         % MOD; 
>         } 
>   
>         return; 
>     } 
>   
>     // A Function to calculate the suffix hash 
>     // Suffix hash is nothing but the prefix hash of 
>     // the reversed string 
>     static void computeSuffixHash(String str, int n, 
>                                   int[] suffix, int[] power) 
>     { 
>         suffix[0] = 0; 
>         suffix[1] = str[n - 1]; 
>   
>         for (int i = n - 2, j = 2; i >= 0 && j <= n; i--, j++) { 
>             suffix[j] = (suffix[j - 1] % MOD 
>                          + (str[i] % MOD * power[j - 1] % MOD) % MOD) 
>                         % MOD; 
>         } 
>         return; 
>     } 
>   
>     // A Function to answer the Queries 
>     static void queryResults(String str, Query[] q, int m, int n, 
>                              int[] prefix, int[] suffix, int[] power) 
>     { 
>         for (int i = 0; i <= m - 1; i++) { 
>             int L = q[i].L; 
>             int R = q[i].R; 
>   
>             // Hash Value of Substring [L, R] 
>             long hash_LR 
>                 = ((prefix[R + 1] - prefix[L] + MOD) % MOD 
>                    * findMMI(power[L]) % MOD) 
>                   % MOD; 
>   
>             // Reverse Hash Value of Substring [L, R] 
>             long reverse_hash_LR 
>                 = ((suffix[n - L] - suffix[n - R - 1] + MOD) % MOD 
>                    * findMMI(power[n - R - 1]) % MOD) 
>                   % MOD; 
>   
>             // If both are equal then the substring is a palindrome 
>             if (hash_LR == reverse_hash_LR) { 
>                 if (isPalindrome(str, L, R) == true) { 
>                     Console.Write("The Substring [{0} {1}] is a "
>                                       + "palindrome\n", 
>                                   L, R); 
>                 } 
>                 else { 
>                     Console.Write("The Substring [{0} {1}] is not a "
>                                       + "palindrome\n", 
>                                   L, R); 
>                 } 
>             } 
>             else { 
>                 Console.Write("The Substring [{0} {1}] is not a "
>                                   + "palindrome\n", 
>                               L, R); 
>             } 
>         } 
>   
>         return; 
>     } 
>   
>     // A Dynamic Programming Based Approach to compute the 
>     // powers of 101 
>     static void computePowers(int[] power, int n) 
>     { 
>         // 101^0 = 1 
>         power[0] = 1; 
>   
>         for (int i = 1; i <= n; i++) { 
>             power[i] = (power[i - 1] % MOD * p % MOD) % MOD; 
>         } 
>   
>         return; 
>     } 
>   
>     /* Driver code */
>     public static void Main(String[] args) 
>     { 
>         String str = "abaaabaaaba"; 
>         int n = str.Length; 
>   
>         // A Table to store the powers of 101 
>         int[] power = new int[n + 1]; 
>   
>         computePowers(power, n); 
>   
>         // Arrays to hold prefix and suffix hash values 
>         int[] prefix = new int[n + 1]; 
>         int[] suffix = new int[n + 1]; 
>   
>         // Compute Prefix Hash and Suffix Hash Arrays 
>         computePrefixHash(str, n, prefix, power); 
>         computeSuffixHash(str, n, suffix, power); 
>   
>         Query[] q = { new Query(0, 10), new Query(5, 8), 
>                       new Query(2, 5), new Query(5, 9) }; 
>         int m = q.Length; 
>   
>         queryResults(str, q, m, n, prefix, suffix, power); 
>     } 
> } 
>   
> // This code is contributed by Rajput-Ji 
> 
> ```
> 
> **Output:**
> 
> ```
> The Substring [0 10] is a palindrome
> The Substring [5 8] is not a palindrome
> The Substring [2 5] is not a palindrome
> The Substring [5 9] is a palindrome
> 
> ```
> 
> 本文由 **Rachit Belwariar** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以写一篇文章，并将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
> 
> 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。
> 
> 注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。