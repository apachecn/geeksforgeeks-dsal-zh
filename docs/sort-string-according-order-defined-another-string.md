# 根据另一个字符串定义的顺序对一个字符串进行排序

> 原文:[https://www . geeksforgeeks . org/sort-string-accorder-defined-other-string/](https://www.geeksforgeeks.org/sort-string-according-order-defined-another-string/)

给定两个字符串(小写字母)、一个模式和一个字符串。任务是根据模式定义的顺序对字符串进行排序。可以假设模式包含字符串的所有字符，并且模式中的所有字符只出现一次。
**例:**

```
Input  : pat = "bca", str = "abc"
Output : str = "bca"

Input  : pat = "bxyzca", str = "abcabcabc"
Output : str = "bbbcccaaa"

Input  : pat = "wcyuogmlrdfphitxjakqvzbnes", str = "jcdokai"
Output : str = "codijak"
```

**方法 1:**
想法是首先统计字符串中所有字符的出现次数，并将这些计数存储在计数数组中。然后从左到右遍历模式，对于每个字符 pat[i]，查看它在计数数组中出现的次数，并将该字符多次复制到 str 中。
以下是上述思路的实现。

**实施:**

## C++

```
// C++ program to sort a string according to the
// order defined by a pattern string
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// Sort str according to the order defined by pattern.
void sortByPattern(string& str, string pat)
{
    // Create a count array store count of characters in str.
    int count[MAX_CHAR] = { 0 };

    // Count number of occurrences of each character
    // in str.
    for (int i = 0; i < str.length(); i++)
        count[str[i] - 'a']++;

    // Traverse the pattern and print every characters
    // same number of times as it appears in str. This
    // loop takes O(m + n) time where m is length of
    // pattern and n is length of str.
    int index = 0;
    for (int i = 0; i < pat.length(); i++)
        for (int j = 0; j < count[pat[i] - 'a']; j++)
            str[index++] = pat[i];
}

// Driver code
int main()
{
    string pat = "bca";
    string str = "abc";
    sortByPattern(str, pat);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort a string according to the
// order defined by a pattern string

class GFG {

    static int MAX_CHAR = 26;

    // Sort str according to the order defined by pattern.
    static void sortByPattern(char[] str, char[] pat)
    {
        // Create a count array stor
        // count of characters in str.
        int count[] = new int[MAX_CHAR];

        // Count number of occurrences of
        // each character in str.
        for (int i = 0; i < str.length; i++) {
            count[str[i] - 'a']++;
        }

        // Traverse the pattern and print every characters
        // same number of times as it appears in str. This
        // loop takes O(m + n) time where m is length of
        // pattern and n is length of str.
        int index = 0;
        for (int i = 0; i < pat.length; i++) {
            for (int j = 0; j < count[pat[i] - 'a']; j++) {
                str[index++] = pat[i];
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        char[] pat = "bca".toCharArray();
        char[] str = "abc".toCharArray();
        sortByPattern(str, pat);
        System.out.println(String.valueOf(str));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to sort a string according to
# the order defined by a pattern string
MAX_CHAR = 26

# Sort str according to the order defined by pattern.
def sortByPattern(str, pat):

    global MAX_CHAR

    # Create a count array store count
    # of characters in str.
    count = [0] * MAX_CHAR

    # Count number of occurrences of
    # each character in str.
    for i in range (0, len(str)):
        count[ord(str[i]) - 97] += 1

    # Traverse the pattern and print every characters
    # same number of times as it appears in str. This
    # loop takes O(m + n) time where m is length of
    # pattern and n is length of str.
    index = 0;
    str = ""

    for i in range (0, len(pat)):
        j = 0
        while(j < count[ord(pat[i]) - ord('a')]):
            str += pat[i]
            j = j + 1
            index += 1

    return str

# Driver code
pat = "bca"
str = "abc"
print(sortByPattern(str, pat))

# This code is contributed by ihritik
```

## C#

```
// C# program to sort a string according to the
// order defined by a pattern string
using System;

class GFG {

    static int MAX_CHAR = 26;

    // Sort str according to the order defined by pattern.
    static void sortByPattern(char[] str, char[] pat)
    {
        // Create a count array stor
        // count of characters in str.
        int[] count = new int[MAX_CHAR];

        // Count number of occurrences of
        // each character in str.
        for (int i = 0; i < str.Length; i++) {
            count[str[i] - 'a']++;
        }

        // Traverse the pattern and print every characters
        // same number of times as it appears in str. This
        // loop takes O(m + n) time where m is length of
        // pattern and n is length of str.
        int index = 0;
        for (int i = 0; i < pat.Length; i++) {
            for (int j = 0; j < count[pat[i] - 'a']; j++) {
                str[index++] = pat[i];
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        char[] pat = "bca".ToCharArray();
        char[] str = "abc".ToCharArray();
        sortByPattern(str, pat);
        Console.WriteLine(String.Join("", str));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to sort a string according to the
// order defined by a pattern string
let MAX_CHAR = 26;

// Sort str according to the order defined by pattern.
function sortByPattern(str,pat)
{
    // Create a count array stor
        // count of characters in str.
        let count = new Array(MAX_CHAR);
        for(let i = 0; i < MAX_CHAR; i++)
        {
            count[i] = 0;
        }

        // Count number of occurrences of
        // each character in str.
        for (let i = 0; i < str.length; i++) {
            count[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        // Traverse the pattern and print every characters
        // same number of times as it appears in str. This
        // loop takes O(m + n) time where m is length of
        // pattern and n is length of str.
        let index = 0;
        for (let i = 0; i < pat.length; i++) {
            for (let j = 0; j < count[pat[i].charCodeAt(0) - 'a'.charCodeAt(0)]; j++) {
                str[index++] = pat[i];
            }
        }
}

// Driver code
let pat = "bca".split("");
let str = "abc".split("");
sortByPattern(str, pat);
document.write((str).join(""));

// This code is contributed by rag2127
</script>
```

**Output**

```
bca
```

**时间复杂度:** O(m + n)，其中 m 为模式长度，n 为 str 长度。

**方法 2:** 使用 STL

我们可以将比较器传递给 C++中的 sort()函数，并根据模式对字符串进行排序。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Declaring a vector globally that stores which character
// is occuring first
vector<int> position(26, -1);

//Comparator function
bool cmp(char& char1, char& char2)
{
    return position[char1 - 'a'] < position[char2 - 'a'];
}

int main()
{

    // Pattern
    string pat = "wcyuogmlrdfphitxjakqvzbnes";

    for (int i = 0; i < pat.length(); i++) {
        if (position[pat[i] - 'a'] == -1)
            position[pat[i] - 'a'] = i;
    }

    // String to be sorted
    string str = "jcdokai";

    // Passing a comparator to sort function
    sort(str.begin(), str.end(), cmp);
    cout << str;
}
```

**Output**

```
codijak
```

**练习**:在上面的解决方案中，假设模式有 str 的所有字符。考虑一个修改版本，其中模式可能没有所有字符，任务是将所有剩余的字符(在字符串中，但不在模式中)放在最后。剩下的字符需要按字母顺序排序。提示:在第二个循环中，当增加索引并将字符放入字符串中时，我们也可以减少当时的计数。最后，我们遍历计数数组，将剩余的字符按字母顺序排序。

本文由 [**桑杰·哈达**](https://www.linkedin.com/in/sanjay-khadda-65b298120) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。