# 在不改变元音和辅音相对位置的情况下排列单词

> 原文：[https://www.geeksforgeeks.org/arrangement-of-words-without-changing-the-relative-position-of-vowel-and-consonants/](https://www.geeksforgeeks.org/arrangement-of-words-without-changing-the-relative-position-of-vowel-and-consonants/)

给定长度小于 10 的单词，任务是找到许多可以在不改变元音和辅音相对位置的情况下进行排列的方式。

**示例**：

```
Input: "GEEKS"
Output: 6

Input: "COMPUTER"
Output: 720

```

**方法**：

1.  计算单词中的元音和辅音

2.  现在查找仅安排元音的方法总数

3.  然后找到仅安排辅音的方法。

4.  将两个答案相乘即可得出总计方式= **（仅用于排列元音的方式）*（仅用于排列辅音的方式）**

下面是上述方法的实现：

## C++

```cpp

// C++ program for Arrangement of words 
// without changing the relative position of  
// vowel and consonants  
#include <bits/stdc++.h> 
using namespace std; 

#define ll long int 

// this function return n! 
ll factorial(ll n) 
{ 
    ll res = 1; 
    for (int i = 1; i <= n; i++) 
        res = res * i; 

    return res; 
} 

// this will return total number of ways 
ll count(string word) 
{ 

    // freq maintains frequency 
    // of each character in word 
    ll freq[27] = { 0 }; 

    ll vowel = 0, consonant = 0; 
    for (int i = 0; i < word.length(); i++) { 
        freq[word[i] - 'A']++; 

        // check character is vowel or not 
        if (word[i] == 'A' || word[i] == 'E'
            || word[i] == 'I'
            || word[i] == 'O' || word[i] == 'U') { 
            vowel++; 
        } 

        // the characters that are not vowel 
        // must be consonant 
        else
            consonant++; 
    } 

    // number of ways to arrange vowel 
    ll vowelArrange; 
    vowelArrange = factorial(vowel); 
    vowelArrange /= factorial(freq[0]); 
    vowelArrange /= factorial(freq[4]); 
    vowelArrange /= factorial(freq[8]); 
    vowelArrange /= factorial(freq[14]); 
    vowelArrange /= factorial(freq[20]); 

    ll consonantArrange; 
    consonantArrange = factorial(consonant); 
    for (int i = 0; i < 26; i++) { 
        if (i != 0 && i != 4 && i != 8 && i != 14 && i != 20) 
            consonantArrange /= factorial(freq[i]); 
    } 

    // multiply both as these are independent 
    ll total = vowelArrange * consonantArrange; 
    return total; 
} 

// Driver function 
int main() 
{ 
    // string contains only 
    // capital letters 
    string word = "COMPUTER"; 

    // this will contain ans 
    ll ans = count(word); 
    cout << ans << endl; 
    return 0; 
} 

```

## Java

```java

// Java program for Arrangement of words 
// without changing the relative position of  
// vowel and consonants  

class GFG 
{ 

    // this function return n! 
    static long factorial(long n) 
    { 
        long res = 1; 
        for (int i = 1; i <= n; i++) 
            res = res * i; 

        return res; 
    } 

    // this will return total number of ways 
    static long count(String word) 
    { 

        // freq maintains frequency 
        // of each character in word 
        int freq[] =new int[27]; 

        for(int i=0;i<27;i++) 
            freq[i]=0; 

        long vowel = 0, consonant = 0; 
        for (int i = 0; i < word.length(); i++) { 
            freq[word.charAt(i) - 'A']++; 

            // check character is vowel or not 
            if (word.charAt(i) == 'A' || word.charAt(i) == 'E'
                || word.charAt(i) == 'I'
                || word.charAt(i) == 'O' || word.charAt(i) == 'U') { 
                vowel++; 
            } 

            // the characters that are not vowel 
            // must be consonant 
            else
                consonant++; 
        } 

        // number of ways to arrange vowel 
        long vowelArrange; 
        vowelArrange = factorial(vowel); 
        vowelArrange /= factorial(freq[0]); 
        vowelArrange /= factorial(freq[4]); 
        vowelArrange /= factorial(freq[8]); 
        vowelArrange /= factorial(freq[14]); 
        vowelArrange /= factorial(freq[20]); 

        long consonantArrange; 
        consonantArrange = factorial(consonant); 
        for (int i = 0; i < 26; i++) { 
            if (i != 0 && i != 4 && i != 8 && i != 14 && i != 20) 
                consonantArrange /= factorial(freq[i]); 
        } 

        // multiply both as these are independent 
        long total = vowelArrange * consonantArrange; 
        return total; 
    } 

    // Driver function 
    public static void main(String []args) 
    { 
        // string contains only 
        // capital letters 
        String word = "COMPUTER"; 

        // this will contain ans 
        long ans = count(word); 
        System.out.println(ans); 

    } 

} 

// This code is contributed by ihritik 

```

## Python3

```py

# Python3 program for Arrangement of words 
# without changing the relative position of  
# vowel and consonants  

# this function return n! 
def factorial(n): 
    res = 1
    for i in range(1, n + 1): 
        res = res * i 
    return res 

# this will return total number of ways  
def count(word): 

    # freq maintains frequency 
    # of each character in word  
    freq = [0 for i in range(30)] 
    vowel = 0
    consonant = 0
    for i in range(len(word)): 
        freq[ord(word[i]) -65 ] += 1

        # check character is vowel or not  
        if(word[i] == 'A'or word[i] == 'E' or 
           word[i] == 'I' or word[i] == 'O'or 
           word[i] == 'U'): 
            vowel += 1

        # the characters that are not  
        # vowel must be consonant 
        else: 
            consonant += 1

    # number of ways to arrange vowel 
    vowelArrange = factorial(vowel) 
    vowelArrange //= factorial(freq[0]) 
    vowelArrange //= factorial(freq[4]) 
    vowelArrange //= factorial(freq[8]) 
    vowelArrange //= factorial(freq[14]) 
    vowelArrange //= factorial(freq[20]) 

    consonantArrange = factorial(consonant) 
    for i in range(26): 
        if(i != 0 and i != 4 and i != 8 and 
           i != 14 and i != 20): 
            consonantArrange//= factorial(freq[i]) 

    # multiply both as these are independent 
    total = vowelArrange * consonantArrange 
    return total 

# Driver code 

# string contains only 
# capital letters 
word = "COMPUTER"

# this will contain ans 
ans = count(word) 
print(ans) 

# This code is contributed  
# by sahilshelangia 

```

## C#

```cs

// C# program for Arrangement of words 
// without changing the relative position of  
// vowel and consonants  
using System; 
class GFG 
{ 

    // this function return n! 
    static long factorial(long n) 
    { 
        long res = 1; 
        for (int i = 1; i <= n; i++) 
            res = res * i; 

        return res; 
    } 

    // this will return total number of ways 
    static long count(string word) 
    { 

        // freq maintains frequency 
        // of each character in word 
        int []freq =new int[27]; 

        for(int i=0;i<27;i++) 
            freq[i]=0; 

        long vowel = 0, consonant = 0; 
        for (int i = 0; i < word.Length; i++) { 
            freq[word[i] - 'A']++; 

            // check character is vowel or not 
            if (word[i] == 'A' || word[i] == 'E'
                || word[i] == 'I'
                || word[i] == 'O' || word[i] == 'U') { 
                vowel++; 
            } 

            // the characters that are not vowel 
            // must be consonant 
            else
                consonant++; 
        } 

        // number of ways to arrange vowel 
        long vowelArrange; 
        vowelArrange = factorial(vowel); 
        vowelArrange /= factorial(freq[0]); 
        vowelArrange /= factorial(freq[4]); 
        vowelArrange /= factorial(freq[8]); 
        vowelArrange /= factorial(freq[14]); 
        vowelArrange /= factorial(freq[20]); 

        long consonantArrange; 
        consonantArrange = factorial(consonant); 
        for (int i = 0; i < 26; i++) { 
            if (i != 0 && i != 4 && i != 8 && i != 14 && i != 20) 
                consonantArrange /= factorial(freq[i]); 
        } 

        // multiply both as these are independent 
        long total = vowelArrange * consonantArrange; 
        return total; 
    } 

    // Driver function 
    public static void Main() 
    { 
        // string contains only 
        // capital letters 
        string word = "COMPUTER"; 

        // this will contain ans 
        long ans = count(word); 
        Console.WriteLine(ans); 

    } 

} 
// This code is contributed by ihritik 

```

## PHP

```php

<?php 
// PHP program for Arrangement of words 
// without changing the relative position  
// of vowel and consonants  

// this function return n! 
function factorial($n) 
{ 
    $res = 1; 
    for ($i = 1; $i <= $n; $i++) 
        $res = $res * $i; 

    return $res; 
} 

// this will return total  
// number of ways 
function count1($word) 
{ 

    // freq maintains frequency 
    // of each character in word 
    $freq = array_fill(0, 27, 0); 

    for($i = 0; $i < 27; $i++) 
        $freq[$i] = 0; 

    $vowel = 0; 
    $consonant = 0; 
    for ($i = 0; $i < strlen($word); $i++) 
    { 
        $freq[ord($word[$i]) - 65]++; 

        // check character is vowel or not 
        if ($word[$i] == 'A' || $word[$i] == 'E' || 
            $word[$i] == 'I' || $word[$i] == 'O' ||  
            $word[$i] == 'U')  
        { 
            $vowel++; 
        } 

        // the characters that are not  
        // vowel must be consonant 
        else
            $consonant++; 
    } 

    // number of ways to arrange vowel 
    $vowelArrange = factorial($vowel); 
    $vowelArrange /= factorial($freq[0]); 
    $vowelArrange /= factorial($freq[4]); 
    $vowelArrange /= factorial($freq[8]); 
    $vowelArrange /= factorial($freq[14]); 
    $vowelArrange /= factorial($freq[20]); 

    $consonantArrange = factorial($consonant); 
    for ($i = 0; $i < 26; $i++)  
    { 
        if ($i != 0 && $i != 4 && $i != 8 &&  
                       $i != 14 && $i != 20) 
            $consonantArrange /= factorial($freq[$i]); 
    } 

    // multiply both as these  
    // are independent 
    $total = $vowelArrange * $consonantArrange; 
    return $total; 
} 

// Driver Code 

// string contains only 
// capital letters 
$word = "COMPUTER"; 

// this will contain ans 
$ans = count1($word); 
echo ($ans); 

// This code is contributed by mits 
?> 

```

**Output:**

```
720

```



* * *

* * *



