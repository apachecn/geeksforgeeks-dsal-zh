# 最大字符数大于相邻字符数的字符串的排列

> 原文:[https://www . geeksforgeeks . org/最大字符数大于其相邻字符数的字符串排列/](https://www.geeksforgeeks.org/permutation-of-a-string-with-maximum-number-of-characters-greater-than-its-adjacent-characters/)

给定一个字符串，任务是打印在字符串的任何排列中大于其左右字符的最大字符数。
**例:**

> **输入:** str = "abc"
> **输出:** 1
> 每个字符串中字符数最大的字符串排列为:
> ABC–0
> ACB–1 此处为 a<c>b
> BAC–0
> BCA–1 此处为 b<c>a
> cab–0
> CBA–0
> T13】输入: str = "极客

**观察:**

*   如果字符串的长度小于 3，那么答案将是 0，因为满足给定条件的置换是不可能的。
*   如果给定字符串的长度大于或等于 3，那么假设在结果字符串中，每隔一个字符是最大字符，也就是说，在任意两个连续的最大字符之间正好有一个字符(否则我们可以删除除最低字符之外的所有字符，并将它们添加到字符串的末尾)。
*   为简单起见，假设这个数字是奇数。然后，理想情况下，该字符串可以在偶数位置具有最大的字符，即最多(n-1)/2，其中 n 是给定字符串的长度，而剩余的字符在奇数位置。
*   首先按升序排列所有字符，将前半个字符放在奇数位置，然后用剩余的字符填充剩余的偶数位置。
    这样，偶数位置的所有字符都将是那些左右位置的字符较小的字符，如果没有出现频率过高的较小字符，则从奇数位置开始放置一个字符，以相同的字符继续到偶数位置，最终到达我们开始放置该字符的奇数位置旁边的位置。这里，如果字符串中某个较小字符的频率太高，那么最大字符的计数将总是小于(n-1)/2。

**进场:**

1.  计算给定字符串中每个字符的频率。
2.  检查频率最高的字符。
3.  如果最大频率元素是给定字符串中最小的元素，则将标志标记为 0，否则将标志值标记为 1。
4.  答案将是**((n–1)/2，n–max _ freq–flag)**的最小值。

以下是上述方法的实现:

## C++

```
// C++ program to find maximum count
// of such characters which are greater
// its left and right character in
// any permutation of the string
#include <bits/stdc++.h>
using namespace std;

// function to find maximum maximal character in the string
int solve(int freq[])
{
    // to store sum of all frequency
    int n = 0;

    // to store maximum frequency
    int max_freq = 0;

    // frequency of the smallest element
    int first;

    // to check if the smallest
    // element have maximum frequency or not
    int flag = 0;

    // Iterate in the string and count frequency
    for (int i = 0; i < 26; i++) {
        n += freq[i];

        // to store frequency of smallest element
        if (freq[i] != 0 && flag == 0) {
            first = freq[i];
            flag = 1;
        }

        // to store maximum frequency
        if (max_freq < freq[i])
            max_freq = freq[i];
    }

    // if sum of frequency of all element if 0
    if (n == 0)
        return 0;

    // if frequency of smallest character
    // if largest frequency
    if (first != max_freq)
        flag = 1;
    else
        flag = 0;

    return min((n - 1) / 2, n - max_freq - flag);
}

// Function that counts the frequency of
// each element
void solve(string s)
{
    // array to store the frequency of each character
    int freq[26];

    // initialize frequency of all character with 0
    memset(freq, 0, sizeof(freq));

    // loop to calculate frequency of
    // each character in the given string
    for (int i = 0; i < s.length(); i++) {
        freq[s[i] - 'a']++;
    }

    cout << solve(freq);
}

// Driver Code
int main()
{
    string s = "geeks";

    solve(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum count
// of such characters which are greater
// its left and right character in
// any permutation of the string only three characters 

class GFG {

// function to find maximum maximal character in the string
    static int solve(int freq[]) {
        // to store sum of all frequency
        int n = 0;

        // to store maximum frequency
        int max_freq = 0;

        // frequency of the smallest element
        int first = 0;

        // to check if the smallest
        // element have maximum frequency or not
        int flag = 0;

        // Iterate in the string and count frequency
        for (int i = 0; i < 26; i++) {
            n += freq[i];

            // to store frequency of smallest element
            if (freq[i] != 0 && flag == 0) {
                first = freq[i];
                flag = 1;
            }

            // to store maximum frequency
            if (max_freq < freq[i]) {
                max_freq = freq[i];
            }
        }

        // if sum of frequency of all element if 0
        if (n == 0) {
            return 0;
        }

        // if frequency of smallest character
        // if largest frequency
        if (first != max_freq) {
            flag = 1;
        } else {
            flag = 0;
        }

        return Math.min((n - 1) / 2, n - max_freq - flag);
    }

// Function that counts the frequency of
// each element
    static void solve(String s) {
        // array to store the frequency of each character
        int freq[] = new int[26];

        // loop to calculate frequency of
        // each character in the given string
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;
        }

        System.out.println(solve(freq));
    }

// Driver Code
    public static void main(String[] args) {
        String s = "geeks";

        solve(s);

    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find maximum
# count of such characters which
# are greater its left and right
# character in any permutation
# of the string

# function to find maximum maximal
# character in the string
def Solve_1(freq):

    # to store sum of all frequency
    n = 0

    # to store maximum frequency
    max_freq = 0

    # to check if the smallest
    # element have maximum
    # frequency or not
    flag = 0

    # Iterate in the string
    # and count frequency
    for i in range(26) :
        n += freq[i]

        # to store frequency of
        # smallest element
        if (freq[i] != 0 and flag == 0) :
            first = freq[i]
            flag = 1

        # to store maximum frequency
        if (max_freq < freq[i]):
            max_freq = freq[i]

    # if sum of frequency of
    # all element if 0
    if (n == 0):
        return 0

    # if frequency of smallest character
    # if largest frequency
    if (first != max_freq):
        flag = 1
    else:
        flag = 0

    return min((n - 1) // 2, n - max_freq - flag)

# Function that counts the
# frequency of each element
def solve(s):

    # array to store the frequency
    # of each character initialize
    # frequency of all character with 0
    freq = [0] * 26

    # loop to calculate frequency of
    # each character in the given string
    for i in range(len(s)):

        freq[ord(s[i]) - ord('a')] += 1

    print(Solve_1(freq))

# Driver Code
if __name__ == "__main__":
    s = "geeks"
    solve(s)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find maximum count
// of such characters which are greater
// its left and right character in
// any permutation of the string only three characters
using System;
public class GFG{
//JAVA program to find maximum count
// of such characters which are greater
// its left and right character in
// any permutation of the string only three characters 

// function to find maximum maximal character in the string
    static int solve(int []freq) {
        // to store sum of all frequency
        int n = 0;

        // to store maximum frequency
        int max_freq = 0;

        // frequency of the smallest element
        int first = 0;

        // to check if the smallest
        // element have maximum frequency or not
        int flag = 0;

        // Iterate in the string and count frequency
        for (int i = 0; i < 26; i++) {
            n += freq[i];

            // to store frequency of smallest element
            if (freq[i] != 0 && flag == 0) {
                first = freq[i];
                flag = 1;
            }

            // to store maximum frequency
            if (max_freq < freq[i]) {
                max_freq = freq[i];
            }
        }

        // if sum of frequency of all element if 0
        if (n == 0) {
            return 0;
        }

        // if frequency of smallest character
        // if largest frequency
        if (first != max_freq) {
            flag = 1;
        } else {
            flag = 0;
        }

        return Math.Min((n - 1) / 2, n - max_freq - flag);
    }

// Function that counts the frequency of
// each element
    static void solve(String s) {
        // array to store the frequency of each character
        int []freq = new int[26];

        // loop to calculate frequency of
        // each character in the given string
        for (int i = 0; i < s.Length; i++) {
            freq[s[i] - 'a']++;
        }

        Console.Write(solve(freq));
    }

// Driver Code
    public static void Main() {
        String s = "geeks";

        solve(s);

    }
}
// This code is contributed by Rajput-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum count of such
// characters which are greater its left and
// right character in any permutation
// of the string

// function to find maximum maximal
// character in the string
function Solve_1($freq)
{
    // to store sum of all frequency
    $n = 0;

    // to store maximum frequency
    $max_freq = 0;

    // to check if the smallest element
    // have maximum frequency or not
    $flag = 0;

    // Iterate in the string
    // and count frequency
    for($i = 0; $i < 26; $i++)
    {
        $n += $freq[$i];

        // to store frequency of
        // smallest element
        if ($freq[$i] != 0 and $flag == 0)
        {
            $first = $freq[$i];
            $flag = 1;
        }

        // to store maximum frequency
        if ($max_freq < $freq[$i])
            $max_freq = $freq[$i];
    }

    // if sum of frequency of
    // all element if 0
    if ($n == 0)
        return 0;

    // if frequency of smallest character
    // if largest frequency
    if ($first != $max_freq)
        $flag = 1;
    else
        $flag = 0;

    return min(($n - 1) / 2,
                $n - $max_freq - $flag);
}

// Function that counts the
// frequency of each element
function solve($s)
{
    // array to store the frequency
    // of each character initialize
    // frequency of all character with 0
    $freq = array_fill(0, 26, 0);

    // loop to calculate frequency of
    // each character in the given string
    for($i = 0; $i < strlen($s); $i++)

        $freq[ord($s[$i]) - ord('a')] += 1;

    print(Solve_1($freq));
}

// Driver Code
$s = "geeks";
solve($s);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find maximum count
// of such characters which are greater
// its left and right character in
// any permutation of the string only three characters 

    // function to find maximum maximal character in the string
    function solve1(freq)
    {
        // to store sum of all frequency
        let n = 0;

        // to store maximum frequency
        let max_freq = 0;

        // frequency of the smallest element
        let first = 0;

        // to check if the smallest
        // element have maximum frequency or not
        let flag = 0;

        // Iterate in the string and count frequency
        for (let i = 0; i < 26; i++) {
            n += freq[i];

            // to store frequency of smallest element
            if (freq[i] != 0 && flag == 0) {
                first = freq[i];
                flag = 1;
            }

            // to store maximum frequency
            if (max_freq < freq[i]) {
                max_freq = freq[i];
            }
        }

        // if sum of frequency of all element if 0
        if (n == 0) {
            return 0;
        }

        // if frequency of smallest character
        // if largest frequency
        if (first != max_freq) {
            flag = 1;
        } else {
            flag = 0;
        }

        return Math.min(Math.floor((n - 1) / 2), n - max_freq - flag);
    }

    // Function that counts the frequency of
    // each element
    function solve(s)
    {
        // array to store the frequency of each character
        let freq = new Array(26);
        for(let i=0;i<26;i++)
        {
            freq[i]=0;
        }

        // loop to calculate frequency of
        // each character in the given string
        for (let i = 0; i < s.length; i++) {

            freq[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        document.write(solve1(freq));
    }

    // Driver Code
    let s = "geeks";

    solve(s);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```