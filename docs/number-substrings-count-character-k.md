# 每个字符计数为 k 的子串数量

> 原文:[https://www . geesforgeks . org/number-substrings-count-character-k/](https://www.geeksforgeeks.org/number-substrings-count-character-k/)

给定一个字符串和一个整数 k，求所有不同字符恰好出现 k 次的子字符串数。

**例:**

```
Input : s = "aabbcc"
        k = 2 
Output : 6
The substrings are aa, bb, cc,
aabb, bbcc and aabbcc.

Input : s = "aabccc"
        k = 2
Output : 3
There are three substrings aa, 
cc and cc
```

这个想法是遍历所有子字符串。我们确定一个起始点，遍历所有以该点为起点的子串，不断增加所有字符的频率。如果所有频率都变成 k，我们就增加结果。如果任何频率的计数超过 k，我们就中断并改变起点。

## c++

```
// C++ program to count number of substrings
// with counts of distinct characters as k.
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// Returns true if all values
// in freq[] are either 0 or k.
bool check(int freq[], int k)
{
    for (int i = 0; i < MAX_CHAR; i++)
        if (freq[i] && freq[i] != k)
            return false;
    return true;
}

// Returns count of substrings where frequency
// of every present character is k
int substrings(string s, int k)
{
    int res = 0;  // Initialize result

    // Pick a starting point
    for (int i = 0; s[i]; i++) {

        // Initialize all frequencies as 0
        // for this starting point
        int freq[MAX_CHAR] = { 0 };

        // One by one pick ending points
        for (int j = i; s[j]; j++) {

            // Increment frequency of current char
            int index = s[j] - 'a';
            freq[index]++;

            // If frequency becomes more than
            // k, we can't have more substrings
            // starting with i
            if (freq[index] > k)
                break;

            // If frequency becomes k, then check
            // other frequencies as well.
            else if (freq[index] == k &&
                  check(freq, k) == true)
                res++;
        }
    }
    return res;
}

// Driver code
int main()
{
    string s = "aabbcc";
    int k = 2;
    cout << substrings(s, k) << endl;

    s = "aabbc";
    k = 2;
    cout << substrings(s, k) << endl;
}
```

## Java

```
// Java program to count number of substrings
// with counts of distinct characters as k.
class GFG
{

static int MAX_CHAR = 26;

// Returns true if all values
// in freq[] are either 0 or k.
static boolean check(int freq[], int k)
{
    for (int i = 0; i < MAX_CHAR; i++)
        if (freq[i] !=0 && freq[i] != k)
            return false;
    return true;
}

// Returns count of substrings where frequency
// of every present character is k
static int substrings(String s, int k)
{
    int res = 0; // Initialize result

    // Pick a starting point
    for (int i = 0; i< s.length(); i++)
    {

        // Initialize all frequencies as 0
        // for this starting point
        int freq[] = new int[MAX_CHAR];

        // One by one pick ending points
        for (int j = i; j<s.length(); j++)
        {

            // Increment frequency of current char
            int index = s.charAt(j) - 'a';
            freq[index]++;

            // If frequency becomes more than
            // k, we can't have more substrings
            // starting with i
            if (freq[index] > k)
                break;

            // If frequency becomes k, then check
            // other frequencies as well.
            else if (freq[index] == k &&
                check(freq, k) == true)
                res++;
        }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    String s = "aabbcc";
    int k = 2;
    System.out.println(substrings(s, k));

    s = "aabbc";
    k = 2;
    System.out.println(substrings(s, k));
}
}

// This code has been contributed by 29AjayKumar
```

## python 3

T2

## c#

T21

```
// C# program to count number of substrings
// with counts of distinct characters as k.
using System;

class GFG
{

static int MAX_CHAR = 26;

// Returns true if all values
// in freq[] are either 0 or k.
static bool check(int []freq, int k)
{
    for (int i = 0; i < MAX_CHAR; i++)
        if (freq[i] != 0 && freq[i] != k)
            return false;
    return true;
}

// Returns count of substrings where frequency
// of every present character is k
static int substrings(String s, int k)
{
    int res = 0; // Initialize result

    // Pick a starting point
    for (int i = 0; i < s.Length; i++)
    {

        // Initialize all frequencies as 0
        // for this starting point
        int []freq = new int[MAX_CHAR];

        // One by one pick ending points
        for (int j = i; j < s.Length; j++)
        {

            // Increment frequency of current char
            int index = s[j] - 'a';
            freq[index]++;

            // If frequency becomes more than
            // k, we can't have more substrings
            // starting with i
            if (freq[index] > k)
                break;

            // If frequency becomes k, then check
            // other frequencies as well.
            else if (freq[index] == k &&
                check(freq, k) == true)
                res++;
        }
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    String s = "aabbcc";
    int k = 2;
    Console.WriteLine(substrings(s, k));

    s = "aabbc";
    k = 2;
    Console.WriteLine(substrings(s, k));
}
}

/* This code contributed by PrinciRaj1992 */
```

## PHP

T4

## Javascript

```
<script>

// Javascript program to count number of
// substrings with counts of distinct
// characters as k.
let MAX_CHAR = 26;

// Returns true if all values
// in freq[] are either 0 or k.
function check(freq,k)
{
    for(let i = 0; i < MAX_CHAR; i++)
        if (freq[i] != 0 && freq[i] != k)
            return false;

    return true;
}

// Returns count of substrings where frequency
// of every present character is k
function substrings(s, k)
{

    // Initialize result
    let res = 0;

    // Pick a starting point
    for(let i = 0; i< s.length; i++)
    {

        // Initialize all frequencies as 0
        // for this starting point
        let freq = new Array(MAX_CHAR);
        for(let i = 0; i < freq.length ;i++)
        {
            freq[i] = 0;
        }

        // One by one pick ending points
        for(let j = i; j < s.length; j++)
        {

            // Increment frequency of current char
            let index = s[j].charCodeAt(0) -
                         'a'.charCodeAt(0);
            freq[index]++;

            // If frequency becomes more than
            // k, we can't have more substrings
            // starting with i
            if (freq[index] > k)
                break;

            // If frequency becomes k, then check
            // other frequencies as well.
            else if (freq[index] == k &&
                check(freq, k) == true)
                res++;
        }
    }
    return res;
}

// Driver code
let s = "aabbcc";
let k = 2;
document.write(substrings(s, k) + "<br>");

s = "aabbc";
k = 2;
document.write(substrings(s, k) + "<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

T31**输出**

```
6
3
```