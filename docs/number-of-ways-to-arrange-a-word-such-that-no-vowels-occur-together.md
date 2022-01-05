# 排列一个单词使得没有元音一起出现的方法数量

> 原文:[https://www . geeksforgeeks . org/排列单词的方法数量-这样-没有元音一起出现/](https://www.geeksforgeeks.org/number-of-ways-to-arrange-a-word-such-that-no-vowels-occur-together/)

给定一个长度不超过 20 个字符的英语单词。计算单词排列方式的数量，使元音不在一起出现。

**注意:**如果给定单词中元音的总数是 1，那么结果应该是 0。

**示例:**

```
Input : allahabad
Output : 7200

Input : geeksforgeeks
Output : 32205600

Input : abcd
Output : 0
```

因为这个词包含元音和辅音。计算排列给定单词的方法总数，并减去将所有元音连在一起的方法数。为了计算总数，我们将使用以下公式

```
No of ways = (n!) / (r1! * r2! * ... * rk!)
```

其中 n 是单词中不同字符的数量，r1，r2 … rk 是同类型字符的出现频率。
为了计算所有元音一起出现的方式的数量，我们将所有元音的组视为单个字符，使用上面的公式，我们将计算所有元音一起出现的方式的总数。现在从得到结果的方法总数中减去它。

下面是上述方法的实现:

## C++

```
// C++ code for above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to check if a character is vowel or consonent
bool isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u')
        return true;
    else
        return false;
}

// Function to calculate factorial of a number
ll fact(ll n)
{
    if (n < 2)
        return 1;
    return n * fact(n - 1);
}

// Calculating no of ways for arranging vowels
ll only_vowels(map<char, int>& freq)
{
    ll denom = 1;
    ll cnt_vwl = 0;

    // Iterate the map and count the number of vowels and calculate
    // no of ways to arrange vowels
    for (auto itr = freq.begin(); itr != freq.end(); itr++) {
        if (isVowel(itr->first)) {
            denom *= fact(itr->second);
            cnt_vwl += itr->second;
        }
    }

    return fact(cnt_vwl) / denom;
}

// calculating no of ways to arrange the given word such that all vowels
// come together
ll all_vowels_together(map<char, int>& freq)
{
    // calculate no of ways to arrange vowels
    ll vow = only_vowels(freq);

    // to store denominator of fraction
    ll denom = 1;

    // count of consonents
    ll cnt_cnst = 0;

    for (auto itr = freq.begin(); itr != freq.end(); itr++) {
        if (!isVowel(itr->first)) {
            denom *= fact(itr->second);
            cnt_cnst += itr->second;
        }
    }

    // calculate the number of ways to arrange the word such that
    // all vowels come together
    ll ans = fact(cnt_cnst + 1) / denom;

    return (ans * vow);
}

// To calculate total number of permutations
ll total_permutations(map<char, int>& freq)
{
    // To store length of the given word
    ll cnt = 0;

    // denominator of fraction
    ll denom = 1;

    for (auto itr = freq.begin(); itr != freq.end(); itr++) {
        denom *= fact(itr->second);
        cnt += itr->second;
    }

    // return total number of permutations of the given word
    return fact(cnt) / denom;
}

// Function to calculate number of permutations such that
// no vowels come together
ll no_vowels_together(string& word)
{
    // to store frequency of character
    map<char, int> freq;

    // count frequency of all characters
    for (int i = 0; i < word.size(); i++) {
        char ch = tolower(word[i]);
        freq[ch]++;
    }

    // calculate total number of permutations
    ll total = total_permutations(freq);

    // calculate total number of permutations such that
    // all vowels come together
    ll vwl_tgthr = all_vowels_together(freq);

    // subtract vwl_tgthr from total to get the result
    ll res = total - vwl_tgthr;

    // return the result
    return res;
}

// Driver code
int main()
{

    string word = "allahabad";
    ll ans = no_vowels_together(word);
    cout << ans << endl;

    word = "geeksforgeeks";
    ans = no_vowels_together(word);
    cout << ans << endl;

    word = "abcd";
    ans = no_vowels_together(word);
    cout << ans << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;
import java.lang.*;
class GFG
{
  // Function to check if a character
  // is vowel or consonent
  static boolean isVowel(char ch)
  {
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
      return true;
    else
      return false;
  }

  // Function to calculate factorial of a number
  static long fact(long n)
  {
    if (n < 2)
    {
      return 1;
    }
    return n * fact(n - 1);
  }

  // Calculating no of ways for arranging vowels
  static long only_vowels(HashMap<Character, Integer> freq)
  {
    long denom = 1;
    long cnt_vwl = 0;

    // Iterate the map and count the number
    // of vowels and calculate no of ways
    // to arrange vowels
    for (Map.Entry<Character, Integer> itr : freq.entrySet())
    {
      if (isVowel(itr.getKey()))
      {
        denom *= fact(itr.getValue());
        cnt_vwl += itr.getValue();
      }
    }

    return fact(cnt_vwl) / denom;
  }

  // Calculating no of ways to arrange
  // the given word such that all vowels
  // come together
  static long all_vowels_together(HashMap<Character, Integer> freq)
  {

    // Calculate no of ways to arrange vowels
    long vow = only_vowels(freq);

    // To store denominator of fraction
    long denom = 1;

    // Count of consonents
    long cnt_cnst = 0;

    for (Map.Entry<Character, Integer> itr : freq.entrySet())
    {
      if (!isVowel(itr.getKey()))
      {
        denom *= fact(itr.getValue());
        cnt_cnst += itr.getValue();
      }
    }

    // Calculate the number of ways to
    // arrange the word such that
    // all vowels come together
    long ans = fact(cnt_cnst + 1) / denom;

    return (ans * vow);
  }

  // To calculate total number of permutations
  static long total_permutations(HashMap<Character, Integer> freq)
  {

    // To store length of the given word
    long cnt = 0;

    // Denominator of fraction
    long denom = 1;       
    for (Map.Entry<Character, Integer> itr : freq.entrySet())
    {
      denom *= fact(itr.getValue());
      cnt += itr.getValue();
    }

    // Return total number of
    // permutations of the given word
    return fact(cnt) / denom;
  }

  // Function to calculate number of permutations
  // such that no vowels come together
  static long no_vowels_together(String word)
  {

    // To store frequency of character
    HashMap<Character, Integer> freq = new HashMap<>();

    // Count frequency of all characters
    for(int i = 0; i < word.length(); i++)
    {
      char ch = Character.toLowerCase(word.charAt(i));
      if (freq.containsKey(ch))
      {
        freq.put(ch, freq.get(ch)+1);
      }
      else
      {
        freq.put(ch, 1);
      }
    }

    // Calculate total number of permutations
    long total = total_permutations(freq);

    // Calculate total number of permutations
    // such that all vowels come together
    long vwl_tgthr = all_vowels_together(freq);

    // Subtract vwl_tgthr from total
    // to get the result
    long res = total - vwl_tgthr;

    // Return the result
    return res;
  }

  // Driver code
  public static void main(String[] args) {
    String word = "allahabad";
    long ans = no_vowels_together(word);
    System.out.println(ans);

    word = "geeksforgeeks";
    ans = no_vowels_together(word);
    System.out.println(ans);

    word = "abcd";
    ans = no_vowels_together(word);
    System.out.println(ans);
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 code for above approach

# Function to check if a character is
# vowel or consonent
def isVowel(ch):
    if (ch == 'a' or ch == 'e' or
        ch == 'i' or ch == 'o' or ch == 'u') :
        return True
    else:
        return False

# Function to calculate factorial of a number
def fact(n):
    if (n < 2):
        return 1
    return n * fact(n - 1)

# Calculating no of ways for arranging vowels
def only_vowels(freq):

    denom = 1
    cnt_vwl = 0

    # Iterate the map and count the number of
    # vowels and calculate no of ways to arrange vowels
    for itr in freq:
        if (isVowel(itr)):
            denom *= fact(freq[itr])
            cnt_vwl += freq[itr]

    return fact(cnt_vwl) // denom

# calculating no of ways to arrange the given word
# such that vowels come together
def all_vowels_together(freq):

    # calculate no of ways to arrange vowels
    vow = only_vowels(freq)

    # to store denominator of fraction
    denom = 1

    # count of consonents
    cnt_cnst = 0

    for itr in freq:
        if (isVowel(itr) == False):
            denom *= fact(freq[itr])
            cnt_cnst += freq[itr]

    # calculate the number of ways to arrange
    # the word such that vowels come together
    ans = fact(cnt_cnst + 1) // denom

    return (ans * vow)

# To calculate total number of permutations
def total_permutations(freq):

    # To store length of the given word
    cnt = 0

    # denominator of fraction
    denom = 1

    for itr in freq:
        denom *= fact(freq[itr])
        cnt += freq[itr]

    # return total number of permutations
    # of the given word
    return fact(cnt) // denom

# Function to calculate number of permutations
# such that no vowels come together
def no_vowels_together(word):

    # to store frequency of character
    freq = dict()

    # count frequency of acharacters
    for i in word:
        ch = i.lower()
        freq[ch] = freq.get(ch, 0) + 1

    # calculate total number of permutations
    total = total_permutations(freq)

    # calculate total number of permutations
    # such that vowels come together
    vwl_tgthr = all_vowels_together(freq)

    # subtract vwl_tgthr from total
    # to get the result
    res = total - vwl_tgthr

    # return the result
    return res

# Driver code
word = "allahabad"
ans = no_vowels_together(word)
print(ans)

word = "geeksforgeeks"
ans = no_vowels_together(word)
print(ans)

word = "abcd"
ans = no_vowels_together(word)
print(ans)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# code for above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if a character
// is vowel or consonent
static bool isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
        return true;
    else
        return false;
}

// Function to calculate factorial of a number
static long fact(long n)
{
    if (n < 2)
    {
        return 1;
    }
    return n * fact(n - 1);
}

// Calculating no of ways for arranging vowels
static long only_vowels(Dictionary<char, int> freq)
{
    long denom = 1;
    long cnt_vwl = 0;

    // Iterate the map and count the number
    // of vowels and calculate no of ways
    // to arrange vowels
    foreach(KeyValuePair<char, int> itr in freq)
    {
        if (isVowel(itr.Key))
        {
            denom *= fact(itr.Value);
            cnt_vwl += itr.Value;
        }
    }

    return fact(cnt_vwl) / denom;
}

// Calculating no of ways to arrange
// the given word such that all vowels
// come together
static long all_vowels_together(Dictionary<char, int> freq)
{

    // Calculate no of ways to arrange vowels
    long vow = only_vowels(freq);

    // To store denominator of fraction
    long denom = 1;

    // Count of consonents
    long cnt_cnst = 0;

    foreach(KeyValuePair<char, int> itr in freq)
    {
        if (!isVowel(itr.Key))
        {
            denom *= fact(itr.Value);
            cnt_cnst += itr.Value;
        }
    }

    // Calculate the number of ways to
    // arrange the word such that
    // all vowels come together
    long ans = fact(cnt_cnst + 1) / denom;

    return (ans * vow);
}

// To calculate total number of permutations
static long total_permutations(Dictionary<char, int> freq)
{

    // To store length of the given word
    long cnt = 0;

    // Denominator of fraction
    long denom = 1;

    foreach(KeyValuePair<char, int> itr in freq)
    {
        denom *= fact(itr.Value);
        cnt += itr.Value;
    }

    // Return total number of
    // permutations of the given word
    return fact(cnt) / denom;
}

// Function to calculate number of permutations
// such that no vowels come together
static long no_vowels_together(string word)
{

    // To store frequency of character
    Dictionary<char,
               int> freq = new Dictionary<char,
                                          int>();

    // Count frequency of all characters
    for(int i = 0; i < word.Length; i++)
    {
        char ch = Char.ToLower(word[i]);
        if (freq.ContainsKey(ch))
        {
            freq[ch]++;
        }
        else
        {
            freq[ch] = 1;
        }
    }

    // Calculate total number of permutations
    long total = total_permutations(freq);

    // Calculate total number of permutations
    // such that all vowels come together
    long vwl_tgthr = all_vowels_together(freq);

    // Subtract vwl_tgthr from total
    // to get the result
    long res = total - vwl_tgthr;

    // Return the result
    return res;
}

// Driver Code
static void Main()
{
    string word = "allahabad";
    long ans = no_vowels_together(word);
    Console.WriteLine(ans);

    word = "geeksforgeeks";
    ans = no_vowels_together(word);
    Console.WriteLine(ans);

    word = "abcd";
    ans = no_vowels_together(word);
    Console.WriteLine(ans);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript code for above approach

// Function to check if a character
  // is vowel or consonent
function isVowel(ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
      return true;
    else
      return false;
}

 // Function to calculate factorial of a number
function fact(n)
{
    if (n < 2)
    {
      return 1;
    }
    return n * fact(n - 1);
}

// Calculating no of ways for arranging vowels
function only_vowels(freq)
{
    let denom = 1;
    let cnt_vwl = 0;

    // Iterate the map and count the number
    // of vowels and calculate no of ways
    // to arrange vowels
    for (let [key, value] of freq.entries())
    {
      if (isVowel(key))
      {
        denom *= fact(value);
        cnt_vwl += value;
      }
    }

    return Math.floor(fact(cnt_vwl) / denom);
}

// Calculating no of ways to arrange
  // the given word such that all vowels
  // come together
function all_vowels_together(freq)
{
    // Calculate no of ways to arrange vowels
    let vow = only_vowels(freq);

    // To store denominator of fraction
    let denom = 1;

    // Count of consonents
    let cnt_cnst = 0;

    for (let [key, value] of freq.entries())
    {
      if (!isVowel(key))
      {
        denom *= fact(value);
        cnt_cnst += value;
      }
    }

    // Calculate the number of ways to
    // arrange the word such that
    // all vowels come together
    let ans = Math.floor(fact(cnt_cnst + 1) / denom);

    return (ans * vow);
}

 // To calculate total number of permutations
function total_permutations(freq)
{
    // To store length of the given word
    let cnt = 0;

    // Denominator of fraction
    let denom = 1;      
    for (let [key, value] of freq.entries())
    {
      denom *= fact(value);
      cnt += value;
    }

    // Return total number of
    // permutations of the given word
    return Math.floor(fact(cnt) / denom);
}

// Function to calculate number of permutations
  // such that no vowels come together
function no_vowels_together(word)
{
    // To store frequency of character
    let freq = new Map();

    // Count frequency of all characters
    for(let i = 0; i < word.length; i++)
    {
      let ch = word[i].toLowerCase();
      if (freq.has(ch))
      {
        freq.set(ch, freq.get(ch)+1);
      }
      else
      {
        freq.set(ch, 1);
      }
    }

    // Calculate total number of permutations
    let total = total_permutations(freq);

    // Calculate total number of permutations
    // such that all vowels come together
    let vwl_tgthr = all_vowels_together(freq);

    // Subtract vwl_tgthr from total
    // to get the result
    let res = total - vwl_tgthr;

    // Return the result
    return res;
}

// Driver code
let word = "allahabad";
    let ans = no_vowels_together(word);
    document.write(ans+"<br>");

    word = "geeksforgeeks";
    ans = no_vowels_together(word);
    document.write(ans+"<br>");

    word = "abcd";
    ans = no_vowels_together(word);
    document.write(ans+"<br>");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
7200
32205600
0
```