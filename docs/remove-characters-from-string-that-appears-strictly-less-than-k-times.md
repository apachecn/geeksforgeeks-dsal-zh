# 从出现次数严格小于 K 次的字符串中删除字符

> 原文:[https://www . geeksforgeeks . org/从出现的字符串中删除字符-严格来说-小于 k 倍/](https://www.geeksforgeeks.org/remove-characters-from-string-that-appears-strictly-less-than-k-times/)

给定一个由小写字母和数字 K 组成的字符串，任务是通过删除字符串中出现次数严格小于 K 次的字符来减少它。
**例**:

```
Input : str = "geeksforgeeks", K = 2
Output : geeksgeeks

Input : str = "geeksforgeeks", K = 3
Output : eeee
```

**进场:**

*   创建一个包含 26 个索引的哈希表，其中第 0 个索引代表“a”，第 1 个索引代表“b”等等，以存储输入字符串中每个字符的频率。将此哈希表初始化为零。
*   遍历字符串并增加哈希表中每个字符的频率。即 hash[str[i]-'a']++。
*   现在创建一个新的空字符串，再次遍历输入字符串，只追加新字符串中那些在哈希表中出现频率大于或等于 k 的字符，跳过那些出现次数少于 k 次的字符。

下面是上述方法的实现:

## C++

```
// C++ program to reduce the string by
// removing the characters which
// appears less than k times

#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// Function to reduce the string by
// removing the characters which
// appears less than k times
string removeChars(string str, int k)
{
    // Hash table initialised to 0
    int hash[MAX_CHAR] = { 0 };

    // Increment the frequency of the character
    int n = str.length();
    for (int i = 0; i < n; ++i)
        hash[str[i] - 'a']++;

    // create a new empty string
    string res = "";
    for (int i = 0; i < n; ++i) {

        // Append the characters which
        // appears more than equal to k times
        if (hash[str[i] - 'a'] >= k) {
            res += str[i];
        }
    }

    return res;
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";
    int k = 2;

    cout << removeChars(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reduce the string by
// removing the characters which
// appears less than k times
class GFG {

    final static int MAX_CHAR = 26;

// Function to reduce the string by
// removing the characters which
// appears less than k times
    static String removeChars(String str, int k) {
        // Hash table initialised to 0
        int hash[] = new int[MAX_CHAR];

        // Increment the frequency of the character
        int n = str.length();
        for (int i = 0; i < n; ++i) {
            hash[str.charAt(i) - 'a']++;
        }

        // create a new empty string
        String res = "";
        for (int i = 0; i < n; ++i) {

            // Append the characters which
            // appears more than equal to k times
            if (hash[str.charAt(i) - 'a'] >= k) {
                res += str.charAt(i);
            }
        }

        return res;
    }

// Driver Code
    static public void main(String[] args) {
        String str = "geeksforgeeks";
        int k = 2;

        System.out.println(removeChars(str, k));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to reduce the string
# by removing the characters which
# appears less than k times
MAX_CHAR = 26

# Function to reduce the string by
# removing the characters which
# appears less than k times
def removeChars(str, k):

    # Hash table initialised to 0
    hash = [0] * (MAX_CHAR)

    # Increment the frequency of
    # the character
    n = len(str)
    for i in range(n):
        hash[ord(str[i]) - ord('a')] += 1

    # create a new empty string
    res = ""
    for i in range(n):

        # Append the characters which
        # appears more than equal to k times
        if (hash[ord(str[i]) - ord('a')] >= k) :
            res += str[i]

    return res

# Driver Code
if __name__ == "__main__":

    str = "geeksforgeeks"
    k = 2

    print(removeChars(str, k))

# This code is contributed by ita_c
```

## C#

```
// C# program to reduce the string by
// removing the characters which
// appears less than k times
using System;
class GFG
{

    readonly static int MAX_CHAR = 26;

    // Function to reduce the string by
    // removing the characters which
    // appears less than k times
    static String removeChars(String str, int k) 
    {
        // Hash table initialised to 0
        int []hash = new int[MAX_CHAR];

        // Increment the frequency of the character
        int n = str.Length;
        for (int i = 0; i < n; ++i)
        {
            hash[str[i] - 'a']++;
        }

        // create a new empty string
        String res = "";
        for (int i = 0; i < n; ++i)
        {

            // Append the characters which
            // appears more than equal to k times
            if (hash[str[i] - 'a'] >= k)
            {
                res += str[i];
            }
        }

        return res;
    }

    // Driver Code
    static public void Main()
    {
        String str = "geeksforgeeks";
        int k = 2;

        Console.WriteLine(removeChars(str, k));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to reduce the string by
// removing the characters which
// appears less than k times

let MAX_CHAR = 26;

// Function to reduce the string by
// removing the characters which
// appears less than k times
function removeChars(str,k)
{
    // Hash table initialised to 0
        let hash = new Array(MAX_CHAR);
         for(let i=0;i<MAX_CHAR;i++)
            hash[i]=0;
        // Increment the frequency of the character
        let n = str.length;
        for (let i = 0; i < n; ++i) {
            hash[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        // create a new empty string
        let res = "";
        for (let i = 0; i < n; ++i) {

            // Append the characters which
            // appears more than equal to k times
            if (hash[str[i].charCodeAt(0) - 'a'.charCodeAt(0)] >= k) {
                res += str[i];
            }
        }

        return res;
}

// Driver Code
let str = "geeksforgeeks";
let k = 2;

document.write(removeChars(str, k));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
geeksgeeks
```