# 计算正好有 k 个不同字符的子串数量

> 原文:[https://www . geesforgeks . org/count-count-number-of-substrings-with-k-distinct-characters/](https://www.geeksforgeeks.org/count-number-of-substrings-with-exactly-k-distinct-characters/)

给定一串小写字母，计算所有可能的子字符串(不一定是不同的)，这些子字符串正好有 k 个不同的字符。
**例:**

```
Input: abc, k = 2
Output: 2
Possible substrings are {"ab", "bc"}

Input: aba, k = 2
Output: 3
Possible substrings are {"ab", "ba", "aba"}

Input: aa, k = 1
Output: 3
Possible substrings are {"a", "a", "aa"}
```

**方法 1(蛮力)**

如果字符串的长度是 n，那么可以有 n*(n+1)/2 个可能的子字符串。一个简单的方法是生成所有的子串，并检查每个子串是否有 k 个唯一的字符。如果我们应用这种蛮力，将需要 O(n*n)来生成所有子字符串，并需要 O(n)来检查每个子字符串。因此，总的来说，它会变成 0(n * n * n)。

**方法二**

这个问题可以用 O(n*n)来解决。想法是维护一个哈希表，同时生成子字符串并使用该哈希表检查唯一字符的数量。
下面的实现假设输入字符串只包含从‘a’到‘z’的字符。
**实施**

## C++

```
// C++ program to count number of substrings with
// exactly k distinct characters in a given string
#include<bits/stdc++.h>
using namespace std;

// Function to count number of substrings
// with exactly k unique characters
int countkDist(string str, int k)
{
    int n = str.length();

    // Initialize result
    int res = 0;

    // To store count of characters from 'a' to 'z'
    int cnt[26];

    // Consider all substrings beginning with
    // str[i]
    for (int i = 0; i < n; i++)
    {
        int dist_count = 0;

        // Initializing array with 0
        memset(cnt, 0, sizeof(cnt));

        // Consider all substrings between str[i..j]
        for (int j=i; j<n; j++)
        {
            // If this is a new character for this
            // substring, increment dist_count.
            if (cnt[str[j] - 'a'] == 0)
                dist_count++;

            // Increment count of current character
            cnt[str[j] - 'a']++;

            // If distinct character count becomes k,
            // then increment result.
            if (dist_count == k)
                res++;
            if(dist_count > k) break;
        }
    }

    return res;
}

// Driver Program
int main()
{
    string str = "abcbaa";
    int k = 3;
    cout << "Total substrings with exactly "
         << k <<" distinct characters :"
         << countkDist(str, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to CountKSubStr number of substrings
// with exactly distinct characters in a given string
import java.util.Arrays;

public class CountKSubStr
{
    // Function to count number of substrings
    // with exactly k unique characters
    int countkDist(String str, int k)
    {
        // Initialize result
        int res = 0;

        int n = str.length();

        // To store count of characters from 'a' to 'z'
        int cnt[] = new int[26];

        // Consider all substrings beginning with
        // str[i]
        for (int i = 0; i < n; i++)
        {
            int dist_count = 0;

            // Initializing count array with 0
            Arrays.fill(cnt, 0);

            // Consider all substrings between str[i..j]
            for (int j=i; j<n; j++)
            {
                // If this is a new character for this
                // substring, increment dist_count.
                if (cnt[str.charAt(j) - 'a'] == 0)
                    dist_count++;

                // Increment count of current character
                cnt[str.charAt(j) - 'a']++;

                // If distinct character count becomes k,
                // then increment result.
                if (dist_count == k)
                    res++;
            }
        }

        return res;
    }

    // Driver Program
    public static void main(String[] args)
    {
        CountKSubStr ob = new CountKSubStr();
        String ch = "abcbaa";
        int k = 3;
        System.out.println("Total substrings with exactly " +
                           k +    " distinct characters : "
                           + ob.countkDist(ch, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count number of
# substrings with exactly k distinct
# characters in a given string

# Function to count number of substrings
# with exactly k unique characters
def countkDist(str1, k):
    n = len(str1)

    # Initialize result
    res = 0

    # To store count of characters from
    # 'a' to 'z'
    cnt = [0] * 27

    # Consider all substrings beginning
    # with str[i]
    for i in range(0, n):
        dist_count = 0

        # Initializing array with 0
        cnt = [0] * 27

        # Consider all substrings between str[i..j]
        for j in range(i, n):

            # If this is a new character for this
            # substring, increment dist_count.
            if(cnt[ord(str1[j]) - 97] == 0):
                dist_count += 1

            # Increment count of current character
            cnt[ord(str1[j]) - 97] += 1

            # If distinct character count becomes k,
            # then increment result.
            if(dist_count == k):
                res += 1
            if(dist_count > k):
                break

    return res    

# Driver Code
if __name__ == "__main__":
    str1 = "abcbaa"
    k = 3
    print("Total substrings with exactly", k,
           "distinct characters : ", end = "")
    print(countkDist(str1, k))

# This code is contributed by
# Sairahul Jella
```

## C#

```
// C# program to CountKSubStr number of substrings
// with exactly distinct characters in a given string

using System;
public class CountKSubStr
{
    // Function to count number of substrings
    // with exactly k unique characters
    int countkDist(string str, int k)
    {
        // Initialize result
        int res = 0;

        int n = str.Length;

        // To store count of characters from 'a' to 'z'
        int[] cnt = new int[26];

        // Consider all substrings beginning with
        // str[i]
        for (int i = 0; i < n; i++)
        {
            int dist_count = 0;

            // Initializing count array with 0
            Array.Clear(cnt, 0,cnt.Length);

            // Consider all substrings between str[i..j]
            for (int j=i; j<n; j++)
            {
                // If this is a new character for this
                // substring, increment dist_count.
                if (cnt[str[j] - 'a'] == 0)
                    dist_count++;

                // Increment count of current character
                cnt[str[j] - 'a']++;

                // If distinct character count becomes k,
                // then increment result.
                if (dist_count == k)
                    res++;
            }
        }

        return res;
    }

    // Driver Program
    public static void Main()
    {
        CountKSubStr ob = new CountKSubStr();
        string ch = "abcbaa";
        int k = 3;
        Console.Write("Total substrings with exactly " +
                           k +    " distinct characters : "
                           + ob.countkDist(ch, k));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to CountKSubStr number of substrings
// with exactly distinct characters in a given string

    // Function to count number of substrings
    // with exactly k unique characters
    function countkDist($str, $k)
    {
        // Initialize result
        $res = 0;

        $n = strlen($str);

        // To store count of characters from 'a' to 'z'
        $cnt = array();

        // Consider all substrings beginning with
        // str[i]
        for ($i = 0; $i < $n; $i++)
        {
            $dist_count = 0;

            // Initializing count array with 0
            $cnt = array_fill(0, 0, true);

            // Consider all substrings between str[i..j]
            for ($j = $i; $j < $n; $j++)
            {
                // If this is a new character for this
                // substring, increment dist_count.
                if ($cnt[ord($str[$j]) - ord('a')] == 0)
                    $dist_count++;

                // Increment count of current character
                $cnt[ord($str[$j]) - ord('a')]++;

                // If distinct character count becomes k,
                // then increment result.
                if ($dist_count == $k)
                    $res++;
            }
        }

        return $res;
    }

    // Driver code
    {
        $ch = "abcbaa";
        $k = 3;
        echo("Total substrings with exactly " .
                        $k . " distinct characters : "
                        . countkDist($ch, $k));
    }

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// javascript program to CountKSubStr number of substrings
// with exactly distinct characters in a given string

// Function to count number of substrings
// with exactly k unique characters
function countkDist(str , k)
{
    // Initialize result
    var res = 0;

    var n = str.length;

    // To store count of characters from 'a' to 'z'
    var cnt = Array.from({length: 26}, (_, i) => 0);

    // Consider all substrings beginning with
    // str[i]
    for (i = 0; i < n; i++)
    {
        var dist_count = 0;

       // Consider all substrings between str[i..j]
        for (j=i; j<n; j++)
        {
            // If this is a new character for this
            // substring, increment dist_count.
            if (cnt[str.charAt(j).charCodeAt(0) - 'a'.charCodeAt(0)] == 0)
                dist_count++;

            // Increment count of current character
            cnt[str.charAt(j).charCodeAt(0) - 'a'.charCodeAt(0)]++;

            // If distinct character count becomes k,
            // then increment result.
            if (dist_count == k)
                res++;
        }
    }

    return res;
}

// Driver Program
var ch = "abcbaa";
var k = 3;
document.write("Total substrings with exactly " +
                   k +    " distinct characters : "
                   + countkDist(ch, k));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
Total substrings with exactly 3 distinct characters : 8
```

**时间复杂度:** O(n*n)

**空间复杂度** : O(1)
说明:只使用了 26 大小的数组，可以认为是常数空间。

**练习(进一步优化):**
以上代码在每次外环迭代中重置计数数组“cnt[]”。对于大型字母表来说，这可能非常昂贵。我们能否修改上述程序，使 cnt[]不会每次都复位？
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。