# 转换为 k 长度子串的重复字符串

> 原文:[https://www . geesforgeks . org/convert-string-repeat-substring-k-length/](https://www.geeksforgeeks.org/convert-string-repetition-substring-k-length/)

给定一个字符串，查找是否有可能将其转换为由 k 个字符组成的子串的重复字符串。为了转换，我们可以用 k 个字符替换一个长度为 k 的子串。

**示例:**

```
Input: str = "bdac",  k = 2
Output: True
We can either replace "bd" with "ac" or 
"ac" with "bd".

Input: str = "abcbedabcabc",  k = 3
Output: True
Replace "bed" with "abc" so that the 
whole string becomes repetition of "abc".

Input: str = "bcacc", k = 3
Output: False
k doesn't divide string length i.e. 5%3 != 0

Input: str = "bcacbcac", k = 2
Output: False

Input: str = "bcdbcdabcedcbcd", k = 3
Output: False
```

这可以用于压缩。如果我们有一个字符串，除了一个子字符串之外，整个字符串都是重复的，那么我们可以使用这个算法来压缩这个字符串。

一个观察是，字符串的长度必须是 k 的倍数，因为我们只能替换一个子字符串。
这个想法是声明一个映射 **mp** ，它将长度为 k 的字符串映射为一个表示其计数的整数。因此，如果在映射容器中只有两个不同的长度为 k 的子串，并且其中一个子串的计数为 1，那么答案是正确的。否则，回答是假的。

## C++

```
// C++ program to check if a string can be converted to
// a string that has repeated substrings of length k.
#include<bits/stdc++.h>
using namespace std;

// Returns true if str can be converted to a string
// with k repeated substrings after replacing k
// characters.
bool checkString(string str, long k)
{
    // Length of string must be a multiple of k
    int n = str.length();
    if (n%k != 0)
        return false;

    // Map to store strings of length k and their counts
    unordered_map<string, int> mp;
    for (int i=0; i<n; i+=k)
        mp[str.substr(i, k)]++;

    // If string is already a repetition of k substrings,
    // return true.
    if (mp.size() == 1)
        return true;

    // If number of distinct substrings is not 2, then
    // not possible to replace a string.
    if (mp.size() != 2)
        return false;

    // One of the two distinct must appear exactly once.
    // Either the first entry appears once, or it appears
    // n/k-1 times to make other substring appear once.
    if ((mp.begin()->second == (n/k - 1)) ||
                    mp.begin()->second == 1)
       return true;

    return false;
}

// Driver code
int main()
{
    checkString("abababcd", 2)? cout << "Yes" :
                                cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string
// can be converted to a string that has
// repeated substrings of length k.
import java.util.HashMap;
import java.util.Iterator;

class GFG
{

    // Returns true if str can be converted
    // to a string with k repeated substrings
    // after replacing k characters.
    static boolean checkString(String str, int k)
    {

        // Length of string must be
        // a multiple of k
        int n = str.length();
        if (n % k != 0)
            return false;

        // Map to store strings of
        // length k and their counts
        HashMap<String, Integer> mp = new HashMap<>();
        try
        {
            for (int i = 0; i < n; i += k)
                mp.put(str.substring(i, k),
                mp.get(str.substring(i, k)) == null ? 1 :
                mp.get(str.substring(i, k)) + 1);
        } catch (Exception e) {    }

        // If string is already a repetition
        // of k substrings, return true.
        if (mp.size() == 1)
            return true;

        // If number of distinct substrings is not 2,
        // then not possible to replace a string.
        if (mp.size() != 2)
            return false;

        HashMap.Entry<String,
                Integer> entry = mp.entrySet().iterator().next();

        // One of the two distinct must appear
        // exactly once. Either the first entry
        // appears once, or it appears n/k-1 times
        // to make other substring appear once.
        if (entry.getValue() == (n / k - 1) ||
            entry.getValue() == 1)
            return true;

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        if (checkString("abababcd", 2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to check if a can be converted to
# a that has repeated subs of length k.

# Returns True if S can be converted to a
# with k repeated subs after replacing k
# characters.
def check( S, k):

    # Length of must be a multiple of k
    n = len(S)

    if (n % k != 0):
        return False

    # Map to store s of length k and their counts
    mp =  {}
    for i in range(0, n, k):
        mp[S[i:k]] = mp.get(S[i:k], 0) + 1

    # If is already a repetition of k subs,
    # return True.
    if (len(mp) == 1):
        return True

    # If number of distinct subs is not 2, then
    # not possible to replace a .
    if (len(mp) != 2):
        return False

    # One of the two distinct must appear exactly once.
    # Either the first entry appears once, or it appears
    # n/k-1 times to make other sub appear once.
    for i in mp:
        if i == (n//k - 1) or mp[i] == 1:
            return True

    return False

# Driver code

if check("abababcd", 2):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to check if a string
// can be converted to a string that has
// repeated substrings of length k.
using System;
using System.Collections.Generic;

class GFG
{

    // Returns true if str can be converted
    // to a string with k repeated substrings
    // after replacing k characters.
    static bool checkString(String str, int k)
    {

        // Length of string must be
        // a multiple of k
        int n = str.Length;
        if (n % k != 0)
            return false;

        // Map to store strings of
        // length k and their counts
        Dictionary<String,
                   int> mp = new Dictionary<String,
                                            int>();

        for (int i = 0; i < n; i += k)
        {
            if(!mp.ContainsKey(str.Substring(i, k)))
                mp.Add(str.Substring(i, k), 1);
            else
                mp[str.Substring(i, k)] = mp[str.Substring(i, k)] + 1;
        }

        // If string is already a repetition
        // of k substrings, return true.
        if (mp.Count == 1)
            return true;

        // If number of distinct substrings is not 2,
        // then not possible to replace a string.
        if (mp.Count != 2)
            return false;

        foreach(KeyValuePair<String, int> entry in mp)
        {

            // One of the two distinct must appear
            // exactly once. Either the first entry
            // appears once, or it appears n/k-1 times
            // to make other substring appear once.
            if (entry.Value == (n / k - 1) ||
                entry.Value == 1)
                return true;
        }
        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        if (checkString("abababcd", 2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to check if a string
// can be converted to a string that has
// repeated substrings of length k.

    // Returns true if str can be converted
    // to a string with k repeated substrings
    // after replacing k characters.
    function checkString(str,k)
    {
        // Length of string must be
        // a multiple of k
        let n = str.length;
        if (n % k != 0)
            return false;

        // Map to store strings of
        // length k and their counts
        let mp = new Map();
        for (let i = 0; i < n; i += k)        
        {
            if(mp.has(str.substring(i, i+k)))
                mp.set(str.substring(i, i+k),mp.get(str.substring(i, i+k)) + 1);
            else
                mp.set(str.substring(i, i+k),1);
        }    

        // If string is already a repetition
        // of k substrings, return true.
        if (mp.size == 1)
            return true;

        // If number of distinct substrings is not 2,
        // then not possible to replace a string.
        if (mp.size != 2)
        {   
            return false;
          }

        // One of the two distinct must appear
        // exactly once. Either the first entry
        // appears once, or it appears n/k-1 times
        // to make other substring appear once.
        for (let [key, value] of mp.entries())
        {

            if(value == (Math.floor(n/k) - 1) || value == 1)
                return true;
        }

        return false;
    }

    // Driver code
    if (checkString("abababcd", 2))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
Yes
```

本文由**希曼舒·古普塔(巴格里)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。