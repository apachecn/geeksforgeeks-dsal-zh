# 计算一个字符串中最大长度的回文

> 原文:[https://www . geesforgeks . org/count-maximum-length-回文-string/](https://www.geeksforgeeks.org/count-maximum-length-palindromes-string/)

给定一个字符串，计算有多少个最大长度的回文。(它不必是子字符串)

**示例:**

```
Input : str = "ababa"
Output: 2
Explanation : 
palindromes of maximum of lengths are  :
 "ababa", "baaab" 

Input : str = "ababab"
Output: 4
Explanation : 
palindromes of maximum of lengths are  :
 "ababa", "baaab", "abbba", "babab"
```

**趋近**一个回文可以表示为**“str+t+reverse(str)”**。

**注意**:**“t”**对于偶数长度回文串为空
计算“str”可以用多少种方式构成，然后乘以“t”(省略的单个字符数)。
设 c <sub>i</sub> 为字符串中某个字符出现的次数。考虑以下情况:
1。如果 c <sub>i</sub> 是偶数。那么每个最大回文的一半将包含精确的字母 f <sub>i</sub> = c <sub>i</sub> / 2。
2。如果 c <sub>i</sub> 是奇数。那么每个最大回文的一半将包含精确的字母 f<sub>I</sub>=(c<sub>I</sub>–1)/2。
设 k 为奇数 c 的个数 <sub>i</sub> 。如果 k=0，最大回文长度为偶数；否则它将是奇数，将有 k 个可能的中间字母，也就是说，我们可以将这个字母设置在回文的中间。
n 个物体与 n 个 <sub>1</sub> 同类型物体、n 个 <sub>2</sub> 同类型物体、n3 个同类型物体的排列数为 **n！/ (n1！* n2！* n3！)**。
所以这里我们的字符总数为 f<sub>a</sub>+f<sub>b</sub>+f<sub>a</sub>+……。+f <sub>y</sub> +f <sub>z</sub> 。所以排列的个数是**(f<sub>a</sub>+f<sub>b</sub>+f<sub>a</sub>+……。+f <sub>y</sub> +f <sub>z</sub> )！/ f <sub>a</sub> ！f <sub>b</sub> ！…f <sub>y</sub> ！f <sub>z</sub> ！。**
现在如果 K 不是 0，很明显答案是 K *(f<sub>a</sub>+f<sub>b</sub>+f<sub>a</sub>+……。+f <sub>y</sub> +f <sub>z</sub> +)！/ f <sub>a</sub> ！f <sub>b</sub> ！…f <sub>y</sub> ！f <sub>z</sub> ！

下面是上面的实现。

## C++

```
// C++ implementation for counting
// maximum length palindromes
#include <bits/stdc++.h>
using namespace std;

// factorial of a number
int fact(int n)
{
    int ans = 1;
    for (int i = 1; i <= n; i++)   
        ans = ans * i;
    return (ans);
}

// function to count maximum length palindromes.
int numberOfPossiblePalindrome(string str, int n)
{  
    // Count number of occurrence
    // of a charterer in the string
    unordered_map<char, int> mp;
    for (int i = 0; i < n; i++)
        mp[str[i]]++;

    int k = 0;  // Count of singles
    int num = 0;  // numerator of result
    int den = 1;  // denominator of result
    int fi; 
    for (auto it = mp.begin(); it != mp.end(); ++it)
    {
        // if frequency is even
        // fi = ci / 2
        if (it->second % 2 == 0)
            fi = it->second / 2;

        // if frequency is odd
        // fi = ci - 1 / 2.
        else
        {
            fi = (it->second - 1) / 2;
            k++;
        }

        // sum of all frequencies
        num = num + fi;

        // product of factorial of
        // every frequency
        den = den * fact(fi);
    }

    // if all character are unique
    // so there will be no palindrome,
    // so if num != 0 then only we are
    // finding the factorial
    if (num != 0)
        num = fact(num);

    int ans = num / den;

    if (k != 0)
    {
        // k are the single
        // elements that can be
        // placed in middle
        ans = ans * k;
    }

    return (ans);
}

// Driver program
int main()
{
    char str[] = "ababab";
    int n = strlen(str);
    cout << numberOfPossiblePalindrome(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for counting
// maximum length palindromes
import java.util.*;

class GFG
{

// factorial of a number
static int fact(int n)
{
    int ans = 1;
    for (int i = 1; i <= n; i++)
        ans = ans * i;
    return (ans);
}

// function to count maximum length palindromes.
static int numberOfPossiblePalindrome(String str, int n)
{
    // Count number of occurrence
    // of a charterer in the string
    Map<Character,Integer> mp = new HashMap<>();
    for (int i = 0; i < n; i++)
        mp.put( str.charAt(i),mp.get( str.charAt(i))==null?
                1:mp.get( str.charAt(i))+1);

    int k = 0; // Count of singles
    int num = 0; // numerator of result
    int den = 1; // denominator of result
    int fi;
    for (Map.Entry<Character,Integer> it : mp.entrySet())
    {
        // if frequency is even
        // fi = ci / 2
        if (it.getValue() % 2 == 0)
            fi = it.getValue() / 2;

        // if frequency is odd
        // fi = ci - 1 / 2.
        else
        {
            fi = (it.getValue() - 1) / 2;
            k++;
        }

        // sum of all frequencies
        num = num + fi;

        // product of factorial of
        // every frequency
        den = den * fact(fi);
    }

    // if all character are unique
    // so there will be no palindrome,
    // so if num != 0 then only we are
    // finding the factorial
    if (num != 0)
        num = fact(num);

    int ans = num / den;

    if (k != 0)
    {
        // k are the single
        // elements that can be
        // placed in middle
        ans = ans * k;
    }

    return (ans);
}

// Driver code
public static void main(String[] args)
{
    String str = "ababab";
    int n = str.length();
    System.out.println(numberOfPossiblePalindrome(str, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation for counting
# maximum length palindromes
import math as mt

# factorial of a number
def fact(n):
    ans = 1
    for i in range(1, n + 1):
        ans = ans * i
    return (ans)

# function to count maximum length palindromes.
def numberOfPossiblePalindrome(string, n):

    # Count number of occurrence
    # of a charterer in the string
    mp = dict()
    for i in range(n):
        if string[i] in mp.keys():
            mp[string[i]] += 1
        else:
            mp[string[i]] = 1

    k = 0 # Count of singles
    num = 0 # numerator of result
    den = 1 # denominator of result
    fi = 0
    for it in mp:

        # if frequency is even
        # fi = ci / 2
        if (mp[it] % 2 == 0):
            fi = mp[it] // 2

        # if frequency is odd
        # fi = ci - 1 / 2.
        else:

            fi = (mp[it] - 1) // 2
            k += 1

        # sum of all frequencies
        num = num + fi

        # product of factorial of
        # every frequency
        den = den * fact(fi)

    # if all character are unique
    # so there will be no palindrome,
    # so if num != 0 then only we are
    # finding the factorial
    if (num != 0):
        num = fact(num)

    ans = num //den

    if (k != 0):

        # k are the single
        # elements that can be
        # placed in middle
        ans = ans * k

    return (ans)

# Driver Code
string = "ababab"
n = len(string)
print(numberOfPossiblePalindrome(string, n))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation for counting
// maximum length palindromes
using System;
using System.Collections.Generic;

class GFG
{

// factorial of a number
static int fact(int n)
{
    int ans = 1;
    for (int i = 1; i <= n; i++)
        ans = ans * i;
    return (ans);
}

// function to count maximum length palindromes.
static int numberOfPossiblePalindrome(String str, int n)
{
    // Count number of occurrence
    // of a charterer in the string
    Dictionary<char,int> mp = new Dictionary<char,int>();
    for (int i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(str[i]))
        {
            var val = mp[str[i]];
            mp.Remove(str[i]);
            mp.Add(str[i], val + 1);
        }
        else
        {
            mp.Add(str[i], 1);
        }
    }

    int k = 0; // Count of singles
    int num = 0; // numerator of result
    int den = 1; // denominator of result
    int fi;
    foreach(KeyValuePair<char, int> it in mp)
    {
        // if frequency is even
        // fi = ci / 2
        if (it.Value % 2 == 0)
            fi = it.Value / 2;

        // if frequency is odd
        // fi = ci - 1 / 2.
        else
        {
            fi = (it.Value - 1) / 2;
            k++;
        }

        // sum of all frequencies
        num = num + fi;

        // product of factorial of
        // every frequency
        den = den * fact(fi);
    }

    // if all character are unique
    // so there will be no palindrome,
    // so if num != 0 then only we are
    // finding the factorial
    if (num != 0)
        num = fact(num);

    int ans = num / den;

    if (k != 0)
    {
        // k are the single
        // elements that can be
        // placed in middle
        ans = ans * k;
    }

    return (ans);
}

// Driver code
public static void Main(String[] args)
{
    String str = "ababab";
    int n = str.Length;
    Console.WriteLine(numberOfPossiblePalindrome(str, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation for counting
// maximum length palindromes

    // factorial of a number
    function fact(n)
    {
        let ans = 1;
    for (let i = 1; i <= n; i++)
        ans = ans * i;
    return (ans);
    }

// function to count maximum length palindromes.
function numberOfPossiblePalindrome(str,n)
{
    // Count number of occurrence
    // of a charterer in the string
    let mp = new Map();
    for (let i = 0; i < n; i++)
        mp.set( str[i],mp.get( str[i])==null?
                1:mp.get( str[i])+1);

    let k = 0; // Count of singles
    let num = 0; // numerator of result
    let den = 1; // denominator of result
    let fi;
    for (let [key, value] of mp.entries())
    {
        // if frequency is even
        // fi = ci / 2
        if (value % 2 == 0)
            fi = value / 2;

        // if frequency is odd
        // fi = ci - 1 / 2.
        else
        {
            fi = (value - 1) / 2;
            k++;
        }

        // sum of all frequencies
        num = num + fi;

        // product of factorial of
        // every frequency
        den = den * fact(fi);
    }

    // if all character are unique
    // so there will be no palindrome,
    // so if num != 0 then only we are
    // finding the factorial
    if (num != 0)
        num = fact(num);

    let ans = Math.floor(num / den);

    if (k != 0)
    {
        // k are the single
        // elements that can be
        // placed in middle
        ans = ans * k;
    }

    return (ans);
}

// Driver code
let str = "ababab";
let n = str.length;
document.write(numberOfPossiblePalindrome(str, n));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n)