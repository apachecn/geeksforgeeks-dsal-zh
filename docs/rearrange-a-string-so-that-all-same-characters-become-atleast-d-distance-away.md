# 重新排列一个字符串，使所有相同的字符至少相距 d 距离

> 原文:[https://www . geeksforgeeks . org/relay-a-string-so-all-相同的字符-变成-至少-d-distance-away/](https://www.geeksforgeeks.org/rearrange-a-string-so-that-all-same-characters-become-atleast-d-distance-away/)

给定一个字符串和一个正整数 d，重新排列给定字符串中的字符，使相同的字符彼此之间的距离至少为 d。

请注意，可能有许多可能的重新排列，输出应该是可能的重新排列之一。如果不可能有这样的安排，也应该报告。

预期的时间复杂度是 O(n)，其中 n 是输入字符串的长度。

示例:

```
Input:  "aaaabbbcc", d = 2
Output: "ababacabc" 

Input:  "aacbbc", d = 3
Output: "abcabc" 

Input: "geeksforgeeks", d = 3
Output: egkesfegkeors

Input:  "aaa",  d = 2
Output: Cannot be rearranged 
```

我们已经讨论过[如何将相同的字符精确地放在距离](https://www.geeksforgeeks.org/rearrange-a-string-so-that-all-same-characters-become-at-least-d-distance-away/)d 的地方。这是一个扩展版本，相同的字符应该移动至少-d 的距离。

这个想法是使用额外的空间来存储所有字符的频率，并维护一个数组，用于在正确的距离插入值。以下是完整的算法–

1.  假设给定的字符串是字符串，字符串的大小是 n，字母的大小假定为 256(一个常数)。
2.  我们扫描输入字符串并将所有字符的频率存储在一个数组 freq 中。
3.  我们创建一个数组 dist[]用于在正确的距离插入值。dist[j]将存储当前位置和我们可以使用字符“j”的下一个位置之间的最小距离。
    如果 dist[j] < = 0，可以在当前位置插入字符‘j’。
4.  循环运行 n 次
    *   搜索具有最大频率和距离[j] <= 0 的下一个符合条件的字符。
    *   如果我们找到这样的字符，我们将该字符放在输出数组中的下一个可用位置，降低其频率，并将其距离重置为 d。如果我们没有找到任何字符，字符串将无法重新排列，我们返回 false。
    *   当我们在输出字符串中前进时，我们将 dist[]中所有字符的距离减 1。

下面是上述算法的实现。

## C++

```
// C++ program to rearrange a string so that all same
// characters become atleast d distance away
#include <bits/stdc++.h>
#define MAX_CHAR 256
using namespace std;

// The function returns next eligible character
// with maximum frequency (Greedy!!) and
// zero or negative distance
int nextChar(int freq[], int dist[])
{
    int max = INT_MIN;
    for (int i = 0; i < MAX_CHAR; i++)
        if (dist[i] <= 0 && freq[i] > 0 &&
        (max == INT_MIN || freq[i] > freq[max]))
                max = i;

    return max;
}

// The main function that rearranges input string 'str'
// such that two same characters become atleast d
// distance away
int rearrange(char str[], char out[], int d)
{
    // Find length of input string
    int n = strlen(str);

    // Create an array to store all characters and their
    // frequencies in str[]
    int freq[MAX_CHAR] = { 0 };

    // Traverse the input string and store frequencies
    // of all characters in freq[] array.
    for (int i = 0; i < n; i++)
        freq[str[i]]++;

    // Create an array for inserting the values at
    // correct distance dist[j] stores the least distance
    // between current position and the next position we
    // can use character 'j'
    int dist[MAX_CHAR] = { 0 };

    for (int i = 0; i < n; i++)
    {
        // find next eligible character
        int j = nextChar(freq, dist);

        // return 0 if string cannot be rearranged
        if (j == INT_MIN)
            return 0;

        // Put character j at next position
        out[i] = j;

        // decrease its frequency
        freq[j]--;

        // set distance as d
        dist[j] = d;

        // decrease distance of all characters by 1
        for (int i = 0; i < MAX_CHAR; i++)
            dist[i]--;
    }

    // null terminate output string
    out[n] = '\0';

    // return success
    return 1;
}

// Driver code
int main()
{
    char str[] = "aaaabbbcc";
    int n = strlen(str);

    // To store output
    char out[n];

    if (rearrange(str, out, 2))
        cout << out;
    else
        cout << "Cannot be rearranged";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange a string so that all same
// characters become atleast d distance away
import java.util.*;

class GFG
{

static int MAX_CHAR = 256;

// The function returns next eligible character
// with maximum frequency (Greedy!!) and
// zero or negative distance
static int nextChar(int freq[], int dist[])
{
    int max = Integer.MIN_VALUE;
    for (int i = 0; i < MAX_CHAR; i++)
        if (dist[i] <= 0 && freq[i] > 0 &&
        (max == Integer.MIN_VALUE || freq[i] > freq[max]))
                max = i;

    return max;
}

// The main function that rearranges input string 'str'
// such that two same characters become atleast d
// distance away
static int rearrange(char str[], char out[], int d)
{
    // Find length of input string
    int n = str.length;

    // Create an array to store all characters and their
    // frequencies in str[]
    int []freq = new int[MAX_CHAR];

    // Traverse the input string and store frequencies
    // of all characters in freq[] array.
    for (int i = 0; i < n; i++)
        freq[str[i]]++;

    // Create an array for inserting the values at
    // correct distance dist[j] stores the least distance
    // between current position and the next position we
    // can use character 'j'
    int []dist = new int[MAX_CHAR];

    for (int i = 0; i < n; i++)
    {
        // find next eligible character
        int j = nextChar(freq, dist);

        // return 0 if string cannot be rearranged
        if (j == Integer.MIN_VALUE)
            return 0;

        // Put character j at next position
        out[i] = (char) j;

        // decrease its frequency
        freq[j]--;

        // set distance as d
        dist[j] = d;

        // decrease distance of all characters by 1
        for (int k = 0; k < MAX_CHAR; k++)
            dist[k]--;
    }

    // null terminate output string
        Arrays.copyOfRange(out, 0, n);
    // out[n] = '\0';

    // return success
    return 1;
}

// Driver code
public static void main(String[] args)
{
    char str[] = "aaaabbbcc".toCharArray();
    int n = str.length;

    // To store output
    char []out = new char[n];

    if (rearrange(str, out, 2)==1)
            System.out.println(String.valueOf(out));
    else
            System.out.println("Cannot be rearranged");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to rearrange a string so that all
# same characters become at least d distance away
MAX_CHAR = 256

# The function returns next eligible character
# with maximum frequency (Greedy!!)
# and zero or negative distance
def nextChar(freq, dist):

    Max = float('-inf')
    for i in range(0, MAX_CHAR):
        if (dist[i] <= 0 and freq[i] > 0 and
        (Max == float('-inf') or freq[i] > freq[Max])):
                Max = i

    return Max

# The main function that rearranges input
# string 'str' such that two same characters
# become atleast d distance away
def rearrange(string, out, d):

    # Find length of input string
    n = len(string)

    # Create an array to store all characters
    # and their frequencies in str[]
    freq = [0] * MAX_CHAR

    # Traverse the input string and store frequencies
    # of all characters in freq[] array.
    for i in range(0, n):
        freq[ord(string[i])] += 1

    # Create an array for inserting the values at
    # correct distance dist[j] stores the least
    # distance between current position and the
    # we next position can use character 'j'
    dist = [0] * MAX_CHAR

    for i in range(0, n):

        # find next eligible character
        j = nextChar(freq, dist)

        # return 0 if string cannot be rearranged
        if j == float('-inf'):
            return 0

        # Put character j at next position
        out[i] = chr(j)

        # decrease its frequency
        freq[j] -= 1

        # set distance as d
        dist[j] = d

        # decrease distance of all characters by 1
        for i in range(0, MAX_CHAR):
            dist[i] -= 1

    # return success
    return 1

# Driver code
if __name__ == "__main__":

    string = "aaaabbbcc"
    n = len(string)

    # To store output
    out = [None] * n

    if rearrange(string, out, 2):
        print(''.join(out))
    else:
        print("Cannot be rearranged")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to rearrange a string so that all same
// characters become atleast d distance away
using System;

class GFG
{

static int MAX_CHAR = 256;

// The function returns next eligible character
// with maximum frequency (Greedy!!) and
// zero or negative distance
static int nextChar(int []freq, int []dist)
{
    int max = int.MinValue;
    for (int i = 0; i < MAX_CHAR; i++)
        if (dist[i] <= 0 && freq[i] > 0 &&
        (max == int.MinValue || freq[i] > freq[max]))
                max = i;

    return max;
}

// The main function that rearranges input string 'str'
// such that two same characters become atleast d
// distance away
static int rearrange(char []str, char []ouT, int d)
{
    // Find length of input string
    int n = str.Length;

    // Create an array to store all characters and their
    // frequencies in str[]
    int []freq = new int[MAX_CHAR];

    // Traverse the input string and store frequencies
    // of all characters in freq[] array.
    for (int i = 0; i < n; i++)
        freq[str[i]]++;

    // Create an array for inserting the values at
    // correct distance dist[j] stores the least distance
    // between current position and the next position we
    // can use character 'j'
    int []dist = new int[MAX_CHAR];

    for (int i = 0; i < n; i++)
    {
        // find next eligible character
        int j = nextChar(freq, dist);

        // return 0 if string cannot be rearranged
        if (j == int.MinValue)
            return 0;

        // Put character j at next position
        ouT[i] = (char) j;

        // decrease its frequency
        freq[j]--;

        // set distance as d
        dist[j] = d;

        // decrease distance of all characters by 1
        for (int k = 0; k < MAX_CHAR; k++)
            dist[k]--;
    }

    // null terminate output string
        Array.Copy(ouT,ouT, n);
    // out[n] = '\0';

    // return success
    return 1;
}

// Driver code
public static void Main(String[] args)
{
    char []str = "aaaabbbcc".ToCharArray();
    int n = str.Length;

    // To store output
    char []ouT = new char[n];

    if (rearrange(str, ouT, 2)==1)
            Console.WriteLine(String.Join("",ouT));
    else
            Console.WriteLine("Cannot be rearranged");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to rearrange a
// string so that all same characters
// become atleast d distance away
let MAX_CHAR = 256;

// The function returns next eligible
// character with maximum frequency
// (Greedy!!) and zero or negative distance
function nextChar(freq, dist)
{
    let max = Number.MIN_VALUE;
    for(let i = 0; i < MAX_CHAR; i++)
        if (dist[i] <= 0 && freq[i] > 0 &&
           (max == Number.MIN_VALUE ||
            freq[i] > freq[max]))
            max = i;

    return max;
}

// The main function that rearranges input
// string 'str' such that two same characters
// become atleast d distance away
function rearrange(str, out, d)
{

    // Find length of input string
    let n = str.length;

    // Create an array to store all characters
    // and their frequencies in str[]
    let freq = new Array(MAX_CHAR);
      for(let i = 0; i < freq.length; i++)
    {
        freq[i] = 0;
    }

    // Traverse the input string and store
    // frequencies of all characters in
    // freq[] array.
    for(let i = 0; i < n; i++)
        freq[str[i].charCodeAt(0)]++;

    // Create an array for inserting the
    // values at correct distance dist[j]
    // stores the least distance between
    // current position and the next position
    // we can use character 'j'
    let dist = new Array(MAX_CHAR);
      for(let i = 0; i < dist.length; i++)
    {
        dist[i] = 0;
    }
    for(let i = 0; i < n; i++)
    {

        // Find next eligible character
        let j = nextChar(freq, dist);

        // return 0 if string cannot
        // be rearranged
        if (j == Number.MIN_VALUE)
            return 0;

        // Put character j at next position
        out[i] = String.fromCharCode (j);

        // Decrease its frequency
        freq[j]--;

        // Set distance as d
        dist[j] = d;

        // Decrease distance of all
        // characters by 1
        for(let k = 0; k < MAX_CHAR; k++)
            dist[k]--;
    }

    // Null terminate output string
    // Arrays.copyOfRange(out, 0, n);
    // out[n] = '\0';

    // Return success
    return 1;
}

// Driver code
let str= "aaaabbbcc".split("");
let n = str.length;

// To store output
let out = new Array(n);

if (rearrange(str, out, 2) == 1)
    document.write(out.join(""));
else
    document.write("Cannot be rearranged");

// This code is contributed by rag2127

</script>
```

**输出:**

```
ababacabc
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息