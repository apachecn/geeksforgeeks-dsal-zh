# 从出现正好 K 次的字符串中删除字符

> 原文:[https://www . geesforgeks . org/remove-characters-from-from-a-string-出现-恰好-k-times/](https://www.geeksforgeeks.org/remove-characters-from-a-string-that-appears-exactly-k-times/)

给定一串长度为 **N** 的小写字母 **str** ，任务是通过删除字符串中出现次数正好为 **K** 的字符来减少它。
**举例:**

> **输入:**str = " geesforgeks "，K = 2
> **输出:** eeforee
> **输入:**str = " geesforgeks "，K = 4
> **输出:**gksforgeks

**进场:**

*   创建大小为 **26** 的[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，其中**第 0 个**索引代表**【a】****第 1 个**索引代表**【b】**以此类推。
*   将哈希表初始化为零。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并增加哈希表中每个字符( **s[i]** )的频率
*   现在，再次遍历字符串，并在新字符串中添加频率为 K 的字符。

以下是上述方法的实现:

## C++

```
// C++ program to remove characters from
// a String that appears exactly K times

#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// Function to reduce the string by
// removing the characters which
// appears exactly k times
string removeChars(char arr[], int k)
{
    // Hash table initialised to 0
    int hash[MAX_CHAR] = { 0 };

    // Increment the frequency
    // of the character
    int n = strlen(arr);
    for (int i = 0; i < n; ++i)
        hash[arr[i] - 'a']++;

    // To store answer
    string ans = "";

    // Next index in reduced string
    int index = 0;
    for (int i = 0; i < n; ++i) {

        // Append the characters which
        // appears exactly k times
        if (hash[arr[i] - 'a'] != k) {
            ans += arr[i];
        }
    }

    return ans;
}

// Driver code
int main()
{
    char str[] = "geeksforgeeks";
    int k = 2;

    // Function call
    cout << removeChars(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove characters from
// a String that appears exactly K times
import java.util.*;

class GFG{

static int MAX_CHAR = 26;

// Function to reduce the String by
// removing the characters which
// appears exactly k times
static String removeChars(char arr[], int k)
{
    // Hash table initialised to 0
    int []hash = new int[MAX_CHAR];

    // Increment the frequency
    // of the character
    int n = arr.length;
    for (int i = 0; i < n; ++i)
        hash[arr[i] - 'a']++;

    // To store answer
    String ans = "";

    for (int i = 0; i < n; ++i) {

        // Append the characters which
        // appears exactly k times
        if (hash[arr[i] - 'a'] != k) {
            ans += arr[i];
        }
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    char str[] = "geeksforgeeks".toCharArray();
    int k = 2;

    // Function call
    System.out.print(removeChars(str, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to remove characters from
# a String that appears exactly K times

MAX_CHAR = 26

# Function to reduce the string by
# removing the characters which
# appears exactly k times
def removeChars(arr, k):

    # Hash table initialised to 0
    hash = [0]*MAX_CHAR

    # Increment the frequency
    # of the character
    n = len(arr)
    for i in range( n):
        hash[ord(arr[i]) - ord('a')] += 1

    # To store answer
    ans = ""

    # Next index in reduced string
    index = 0
    for i in range(n):

        # Append the characters which
        # appears exactly k times
        if (hash[ord(arr[i]) - ord('a')] != k):
            ans += arr[i]

    return ans

# Driver code
if __name__ =="__main__":
    str = "geeksforgeeks"
    k = 2

    # Function call
    print(removeChars(str, k))

# This code is contributed by chitranayal
```

## C#

```
// C# program to remove characters from
// a String that appears exactly K times
using System;

class GFG{

static int MAX_CHAR = 26;

// Function to reduce the String by
// removing the characters which
// appears exactly k times
static String removeChars(char []arr, int k)
{
    // Hash table initialised to 0
    int []hash = new int[MAX_CHAR];

    // Increment the frequency
    // of the character
    int n = arr.Length;
    for (int i = 0; i < n; ++i)
        hash[arr[i] - 'a']++;

    // To store answer
    String ans = "";

    for (int i = 0; i < n; ++i) {

        // Append the characters which
        // appears exactly k times
        if (hash[arr[i] - 'a'] != k) {
            ans += arr[i];
        }
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    char []str = "geeksforgeeks".ToCharArray();
    int k = 2;

    // Function call
    Console.Write(removeChars(str, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to remove characters from
// a String that appears exactly K times

let MAX_CHAR = 26;

// Function to reduce the String by
// removing the characters which
// appears exactly k times
function removeChars(arr, k)
{
    // Hash table initialised to 0
    let hash =  Array.from({length: MAX_CHAR}, (_, i) => 0);

    // Increment the frequency
    // of the character
    let n = arr.length;
    for (let i = 0; i < n; ++i)
        hash[arr[i].charCodeAt() - 'a'.charCodeAt()]++;

    // To store answer
    let ans = "";

    for (let i = 0; i < n; ++i) {

        // Append the characters which
        // appears exactly k times
        if (hash[arr[i].charCodeAt() - 'a'.charCodeAt()] != k) {
            ans += arr[i];
        }
    }

    return ans;
}

// Driver code

      let str = "geeksforgeeks".split('');
    let k = 2;

    // Function call
    document.write(removeChars(str, k));

</script>
```

**Output:** 

```
eeforee
```

***时间复杂度:**O(N)*T4】