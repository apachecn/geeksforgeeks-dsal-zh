# 可能的话重新排列字符形成回文

> 原文:[https://www . geesforgeks . org/重排-字符-形式-回文-可能/](https://www.geeksforgeeks.org/rearrange-characters-form-palindrome-possible/)

给定一个字符串，将该字符串转换为回文，无需任何修改，如添加字符、删除字符、替换字符等。

示例:

```
Input : "mdaam"
Output : "madam" or "amdma"

Input : "abb"
Output : "bab"

Input : "geeksforgeeks"
Output : "No Palindrome"
```

1.计算所有字符的出现次数。
2。计算奇数。如果这个计数大于 1 或等于 1，并且字符串的长度是偶数，那么显然回文不能由给定的字符串形成。
3。初始化两个空字符串前半部分和后半部分。
4。遍历地图。对于以计数为计数的每个字符，在前半部分的末尾和后半部分的开头附加 count/2 字符。
5。最后通过追加前半部分和后半部分返回结果

## C++

```
// C++ program to rearrange a string to
// make palindrome.
#include <bits/stdc++.h>
using namespace std;

string getPalindrome(string str)
{

    // Store counts of characters
    unordered_map<char, int> hmap;
    for (int i = 0; i < str.length(); i++)
        hmap[str[i]]++;

    /* find the number of odd elements.
       Takes O(n) */
    int oddCount = 0;
    char oddChar;
    for (auto x : hmap) {
        if (x.second % 2 != 0) {
            oddCount++;
            oddChar = x.first;
        }
    }

    /* odd_cnt = 1 only if the length of
       str is odd */
    if (oddCount > 1
        || oddCount == 1 && str.length() % 2 == 0)
        return "NO PALINDROME";

    /* Generate first halh of palindrome */
    string firstHalf = "", secondHalf = "";
    for (auto x : hmap) {

        // Build a string of floor(count/2)
        // occurrences of current character
        string s(x.second / 2, x.first);

        // Attach the built string to end of
        // and begin of second half
        firstHalf = firstHalf + s;
        secondHalf = s + secondHalf;
    }

    // Insert odd character if there
    // is any
    return (oddCount == 1)
               ? (firstHalf + oddChar + secondHalf)
               : (firstHalf + secondHalf);
}

int main()
{
    string s = "mdaam";
    cout << getPalindrome(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange a string to
// make palindrome
import java.util.HashMap;
import java.util.Map.Entry;

class GFG{

public static String getPalindrome(String str)
{

    // Store counts of characters
    HashMap<Character,
            Integer> counting = new HashMap<>();
    for(char ch : str.toCharArray())
    {
        if (counting.containsKey(ch))
        {
            counting.put(ch, counting.get(ch) + 1);
        }
        else
        {
            counting.put(ch, 1);
        }
    }

    /* Find the number of odd elements.
    Takes O(n) */
    int oddCount = 0;
    char oddChar = 0;

    for(Entry<Character,
              Integer> itr : counting.entrySet())
    {
        if (itr.getValue() % 2 != 0)
        {
            oddCount++;
            oddChar = itr.getKey();
        }
    }

    /* odd_cnt = 1 only if the length of
    str is odd */
    if (oddCount > 1 || oddCount == 1 &&
        str.length() % 2 == 0)
    {
        return "NO PALINDROME";
    }

    /* Generate first halh of palindrome */
    String firstHalf = "", lastHalf = "";
    for(Entry<Character, Integer> itr : counting.entrySet())
    {

        // Build a string of floor(count/2)
        // occurrences of current character
        String ss = "";
        for(int i = 0; i < itr.getValue() / 2; i++)
        {
            ss += itr.getKey();
        }

        // Attach the built string to end of
        // and begin of second half
        firstHalf = firstHalf + ss;
        lastHalf = ss + lastHalf;
    }

    // Insert odd character if there
    // is any
    return (oddCount == 1) ?
           (firstHalf + oddChar + lastHalf) :
           (firstHalf + lastHalf);
}

// Driver code
public static void main(String[] args)
{
    String str = "mdaam";
    System.out.println(getPalindrome(str));
}
}

// This code is contributed by Satyam Singh
```

## 蟒蛇 3

```
# Python3 program to rearrange a string to
# make palindrome.
from collections import defaultdict

def getPalindrome(st):

    # Store counts of characters
    hmap = defaultdict(int)
    for i in range(len(st)):
        hmap[st[i]] += 1

    # Find the number of odd elements.
    # Takes O(n)
    oddCount = 0

    for x in hmap:
        if (hmap[x] % 2 != 0):
            oddCount += 1
            oddChar = x

    # odd_cnt = 1 only if the length of
    # str is odd
    if (oddCount > 1 or oddCount == 1 and
            len(st) % 2 == 0):
        return "NO PALINDROME"

    # Generate first halh of palindrome
    firstHalf = ""
    secondHalf = ""

    for x in sorted(hmap.keys()):

        # Build a string of floor(count/2)
        # occurrences of current character
        s = (hmap[x] // 2) * x

        # Attach the built string to end of
        # and begin of second half
        firstHalf = firstHalf + s
        secondHalf = s + secondHalf

    # Insert odd character if there
    # is any
    if (oddCount == 1):
        return (firstHalf + oddChar + secondHalf)
    else:
        return (firstHalf + secondHalf)

# Driver code
if __name__ == "__main__":

    s = "mdaam"

    print(getPalindrome(s))

# This code is contributed by ukasp
```

**Output**

```
amdma
```