# 排列一个单词使所有元音一起出现的方法数量

> 原文:[https://www . geeksforgeeks . org/排列单词的方法数-所有元音都出现在一起/](https://www.geeksforgeeks.org/number-of-ways-to-arrange-a-word-such-that-all-vowels-occur-together/)

给定一个包含元音和辅音的单词。任务是找出单词有多少种排列方式，以便元音总是连在一起。假设单词的长度< 10。

**示例:**

```
Input: str = "geek"
Output: 6
Ways such that both 'e' comes together are 6 
i.e. geek, gkee, kgee, eekg, eegk, keeg

Input: str = "corporation"
Output: 50400
```

**处理方法:**因为单词包含元音和辅音。所有的元音都需要保持在一起，然后我们将把所有的元音看作一个字母。

> 因为，在单词“geeksforgeeks”中，我们可以把元音“eeoee”看作一个字母。
> 于是，我们有了 **gksfrgks (eeoee)** 。
> 这有 9 个(8 + 1)字母，其中 g、k、s 各出现 2 次，其余各不相同。
> 排列这些字母的方式数= 9！/(2!)x(2！)x(2！)= 45360 方式
> 现在，5 个‘e’出现 4 次，‘o’出现 1 次的元音，可以排列成 5 个！/4!= 5 种方式。
> 所需路数= (45360 x 5) = 226800

下面是上述方法的实现:

## C++

```
// C++ program to calculate the no. of ways
// to arrange the word having vowels together
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Factorial of a number
ll fact(int n)
{
    ll f = 1;
    for (int i = 2; i <= n; i++)
        f = f * i;
    return f;
}

// calculating ways for arranging consonants
ll waysOfConsonants(int size1, int freq[])
{
    ll ans = fact(size1);
    for (int i = 0; i < 26; i++) {

        // Ignore vowels
        if (i == 0 || i == 4 || i == 8 || i == 14 || i == 20)
            continue;
        else
            ans = ans / fact(freq[i]);
    }

    return ans;
}

// calculating ways for arranging vowels
ll waysOfVowels(int size2, int freq[])
{
    return fact(size2) / (fact(freq[0]) * fact(freq[4]) * fact(freq[8])
                    * fact(freq[14]) * fact(freq[20]));
}

// Function to count total no. of ways
ll countWays(string str)
{

    int freq[26] = { 0 };
    for (int i = 0; i < str.length(); i++)
        freq[str[i] - 'a']++;

    // Count vowels and consonant
    int vowel = 0, consonant = 0;
    for (int i = 0; i < str.length(); i++) {

        if (str[i] != 'a' && str[i] != 'e' && str[i] != 'i'
            && str[i] != 'o' && str[i] != 'u')
            consonant++;
        else
            vowel++;
    }

    // total no. of ways
    return waysOfConsonants(consonant+1, freq) *
           waysOfVowels(vowel, freq);
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    cout << countWays(str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the no. of
// ways to arrange the word having
// vowels together
import java.util.*;

class GFG{

// Factorial of a number
static int fact(int n)
{
    int f = 1;
    for(int i = 2; i <= n; i++)
        f = f * i;

    return f;
}

// Calculating ways for arranging consonants
static int waysOfConsonants(int size1,
                            int []freq)
{
    int ans = fact(size1);
    for(int i = 0; i < 26; i++)
    {

        // Ignore vowels
        if (i == 0 || i == 4 || i == 8 ||
            i == 14 || i == 20)
            continue;
        else
            ans = ans / fact(freq[i]);
    }
    return ans;
}

// Calculating ways for arranging vowels
static int waysOfVowels(int size2, int [] freq)
{
    return fact(size2) / (fact(freq[0]) *
          fact(freq[4]) * fact(freq[8]) *
         fact(freq[14]) * fact(freq[20]));
}

// Function to count total no. of ways
static int countWays(String str)
{
    int []freq = new int [200];
    for(int i = 0; i < 200; i++)
        freq[i] = 0;

    for(int i = 0; i < str.length(); i++)
        freq[str.charAt(i) - 'a']++;

    // Count vowels and consonant
    int vowel = 0, consonant = 0;
    for(int i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) != 'a' && str.charAt(i) != 'e' &&
            str.charAt(i) != 'i' && str.charAt(i) != 'o' &&
            str.charAt(i) != 'u')
            consonant++;
        else
            vowel++;
    }

    // Total no. of ways
    return waysOfConsonants(consonant + 1, freq) *
           waysOfVowels(vowel, freq);
}

// Driver code
public static void main(String []args)
{
    String str = "geeksforgeeks";

    System.out.println(countWays(str));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to calculate
# the no. of ways to arrange
# the word having vowels together

# Factorial of a number
def fact(n):

    f = 1
    for i in range(2, n + 1):
        f = f * i
    return f

# calculating ways for
# arranging consonants
def waysOfConsonants(size1, freq):

    ans = fact(size1)
    for i in range(26):

        # Ignore vowels
        if (i == 0 or i == 4 or
            i == 8 or i == 14 or
            i == 20):
            continue
        else:
            ans = ans // fact(freq[i])

    return ans

# calculating ways for
# arranging vowels
def waysOfVowels(size2, freq):

    return (fact(size2) // (fact(freq[0]) *
            fact(freq[4]) * fact(freq[8]) *
            fact(freq[14]) * fact(freq[20])))

# Function to count total no. of ways
def countWays(str1):

    freq = [0] * 26
    for i in range(len(str1)):
        freq[ord(str1[i]) -
             ord('a')] += 1

    # Count vowels and consonant
    vowel = 0
    consonant = 0
    for i in range(len(str1)):

        if (str1[i] != 'a' and str1[i] != 'e' and
            str1[i] != 'i' and str1[i] != 'o' and
            str1[i] != 'u'):
            consonant += 1
        else:
            vowel += 1

    # total no. of ways
    return (waysOfConsonants(consonant + 1, freq) *
            waysOfVowels(vowel, freq))

# Driver code
if __name__ == "__main__":

    str1 = "geeksforgeeks"
    print(countWays(str1))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to calculate the no. of
// ways to arrange the word having
// vowels together
using System.Collections.Generic;
using System;

class GFG{

// Factorial of a number
static int fact(int n)
{
    int f = 1;
    for(int i = 2; i <= n; i++)
        f = f * i;

    return f;
}

// Calculating ways for arranging consonants
static int waysOfConsonants(int size1,
                            int []freq)
{
    int ans = fact(size1);
    for(int i = 0; i < 26; i++)
    {

        // Ignore vowels
        if (i == 0 || i == 4 || i == 8 ||
            i == 14 || i == 20)
            continue;
        else
            ans = ans / fact(freq[i]);
    }
    return ans;
}

// Calculating ways for arranging vowels
static int waysOfVowels(int size2, int [] freq)
{
    return fact(size2) / (fact(freq[0]) *
          fact(freq[4]) * fact(freq[8]) *
         fact(freq[14]) * fact(freq[20]));
}

// Function to count total no. of ways
static int countWays(string str)
{
    int []freq = new int [200];
    for(int i = 0; i < 200; i++)
        freq[i] = 0;

    for(int i = 0; i < str.Length; i++)
        freq[str[i] - 'a']++;

    // Count vowels and consonant
    int vowel = 0, consonant = 0;
    for(int i = 0; i < str.Length; i++)
    {
        if (str[i] != 'a' && str[i] != 'e' &&
            str[i] != 'i' && str[i] != 'o' &&
            str[i] != 'u')
            consonant++;
        else
            vowel++;
    }

    // Total no. of ways
    return waysOfConsonants(consonant + 1, freq) *
           waysOfVowels(vowel, freq);
}

// Driver code
public static void Main()
{
    string str = "geeksforgeeks";

    Console.WriteLine(countWays(str));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
// Javascript program to calculate the no. of
// ways to arrange the word having
// vowels together

// Factorial of a number
function fact(n)
{
       let f = 1;
    for(let i = 2; i <= n; i++)
        f = f * i;

    return f;
}

// Calculating ways for arranging consonants
function waysOfConsonants(size1,freq)
{
    let ans = fact(size1);
    for(let i = 0; i < 26; i++)
    {

        // Ignore vowels
        if (i == 0 || i == 4 || i == 8 ||
            i == 14 || i == 20)
            continue;
        else
            ans = Math.floor(ans / fact(freq[i]));
    }
    return ans;
}

// Calculating ways for arranging vowels
function waysOfVowels(size2,freq)
{
    return Math.floor(fact(size2) / (fact(freq[0]) *
          fact(freq[4]) * fact(freq[8]) *
         fact(freq[14]) * fact(freq[20])));
}

// Function to count total no. of ways
function countWays(str)
{
    let freq = new Array(200);
    for(let i = 0; i < 200; i++)
        freq[i] = 0;

    for(let i = 0; i < str.length; i++)
        freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // Count vowels and consonant
    let vowel = 0, consonant = 0;
    for(let i = 0; i < str.length; i++)
    {
        if (str[i] != 'a' && str[i] != 'e' &&
            str[i] != 'i' && str[i] != 'o' &&
            str[i] != 'u')
            consonant++;
        else
            vowel++;
    }

    // Total no. of ways
    return waysOfConsonants(consonant + 1, freq) *
           waysOfVowels(vowel, freq);
}

// Driver code
let str = "geeksforgeeks";
document.write(countWays(str));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
226800
```

**进一步优化:**我们可以预先计算所需的阶乘值，以避免重新计算。