# 在线检查回文的在线算法

> 原文： [https://www.geeksforgeeks.org/online-algorithm-for-checking-palindrome-in-a-stream/](https://www.geeksforgeeks.org/online-algorithm-for-checking-palindrome-in-a-stream/)

给定一串字符（一个接一个地接收字符），编写一个函数，如果一个字符构成完整的字符串回文，则输出`Yes`，否则输出`No`。

**示例**：

```
Input: str[] = "abcba"
Output: a Yes   // "a" is palindrome
        b No    // "ab" is not palindrome
        c No    // "abc" is not palindrome
        b No    // "abcb" is not palindrome
        a Yes   // "abcba" is palindrome

Input: str[] = "aabaacaabaa"
Output:  a Yes   // "a" is palindrome
         a Yes   // "aa" is palindrome
         b No    // "aab" is not palindrome 
         a No    // "aaba" is not palindrome  
         a Yes   // "aabaa" is palindrome  
         c No    // "aabaac" is not palindrome  
         a No    // "aabaaca" is not palindrome  
         a No    // "aabaacaa" is not palindrome  
         b No    // "aabaacaab" is not palindrome  
         a No    // "aabaacaaba" is not palindrome  
         a Yes   // "aabaacaabaa" is palindrome  

```

令输入字符串为`str[0..n-1]`。 **简单解决方案**将对输入字符串中的每个字符`str[i]`执行以下操作。 检查子字符串`str[0…i]`是否是回文，然后打印是，否则打印否。

**更好的解决方案**是使用 [Rabin Karp 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/)中使用的滚动哈希的想法。 这个想法是跟踪每个索引的上半部分和下半部分的倒数（我们也使用上半部分和下半部分的倒数）。 下面是完整的算法。

```
  1) The first character is always a palindrome, so print yes for 
     first character.

  2) Initialize reverse of first half as "a" and second half as "b".  
     Let the hash value of first half reverse be 'firstr' and that of 
     second half be 'second'.

  3) Iterate through string starting from second character, do following
      for every character str[i], i.e., i varies from 1 to n-1.
     a) If 'firstr' and 'second' are same, then character by character 
        check the substring ending with current character and print 
        "Yes" if palindrome.
        Note that if hash values match, then strings need not be same.
        For example, hash values of "ab" and "ba" are same, but strings
        are different. That is why we check complete string after hash.

     b) Update 'firstr' and 'second' for next iteration.  
           If 'i' is even, then add next character to the beginning of 
                           'firstr' and end of second half and update 
                            hash values.
           If 'i' is odd,  then keep 'firstr' as it is, remove leading 
                           character from second and append a next 
                           character at end.

```

让我们查看所有步骤，例如字符串`abcba`。

1.  `firstr`和`second`的初始值：`firstr=hash('a')`，`second=hash('b')`。

2.  从第二个字符开始，即`i = 1`。

    1.  比较`firstr`和`second`，它们不匹配，因此打印否。

    2.  计算下一次迭代的哈希值，即`i = 2`。由于`i`为奇数，因此`firstr`不变，并且`second`变为`hash('c')`。

3.  `i = 2`：

    1.  比较`firstr`和`second`，它们不匹配，因此打印否。

    2.  计算下一次迭代的哈希值，即，`i = 3`。由于`i`为偶数，因此`firstr`变为`hash('ba')`，而`second`变为`hash('cb')`。

4.  `i = 3`：

    1.  比较`firstr`和`second`，它们不匹配，因此打印否。

    2.  计算下一次迭代的哈希值，即，`i = 4`。由于`i`为奇数，因此`firstr`不变，而`second`变为`hash('ba')`。

5.  `i = 4`：

    1.  `firstr`和`second`匹配，比较整个字符串，它们匹配，所以打印是。

    2.  我们不需要计算下一个哈希值，因为这是最后一个索引。

使用滚动哈希的想法是，只需执行一定数量的算术运算，就可以根据`O(1)`时间中的前一个值来计算下一个哈希值。

以下是上述方法的实现。

## C/C++ 

```

// C program for online algorithm for palindrome checking 
#include<stdio.h> 
#include<string.h> 

// d is the number of characters in input alphabet 
#define d 256 

// q is a prime number used for evaluating Rabin Karp's Rolling hash 
#define q 103 

void checkPalindromes(char str[]) 
{ 
    // Length of input string 
    int N = strlen(str); 

    // A single character is always a palindrome 
    printf("%c Yes\n", str[0]); 

    // Return if string has only one character 
    if (N == 1) return; 

    // Initialize first half reverse and second half for  
    // as firstr and second characters 
    int firstr  = str[0] % q; 
    int second = str[1] % q; 

    int h = 1, i, j; 

    // Now check for palindromes from second character 
    // onward 
    for (i=1; i<N; i++) 
    { 
        // If the hash values of 'firstr' and 'second'  
        // match, then only check individual characters 
        if (firstr == second) 
        { 
            /* Check if str[0..i] is palindrome using 
               simple character by character match */
            for (j = 0; j < i/2; j++) 
            { 
                if (str[j] != str[i-j]) 
                    break; 
            } 
            (j == i/2)?  printf("%c Yes\n", str[i]): 
            printf("%c No\n", str[i]); 
        } 
        else printf("%c No\n", str[i]); 

        // Calculate hash values for next iteration. 
        // Don't calculate hash for next characters if 
        // this is the last character of string 
        if (i != N-1) 
        { 
            // If i is even (next i is odd)  
            if (i%2 == 0) 
            { 
                // Add next character after first half at beginning  
                // of 'firstr' 
                h = (h*d) % q; 
                firstr  = (firstr + h*str[i/2])%q; 

                // Add next character after second half at the end 
                // of second half. 
                second = (second*d + str[i+1])%q; 
            } 
            else
            { 
                // If next i is odd (next i is even) then we 
                // need not to change firstr, we need to remove 
                // first character of second and append a 
                // character to it. 
                second = (d*(second + q - str[(i+1)/2]*h)%q 
                          + str[i+1])%q; 
            } 
        } 
    } 
} 

/* Driver program to test above function */
int main() 
{ 
    char *txt = "aabaacaabaa"; 
    checkPalindromes(txt); 
    getchar(); 
    return 0; 
} 

```