# 一个单词的字符排列，使得所有元音都位于奇数位置

> 原文:[https://www . geeksforgeeks . org/单词中所有元音的字符排列都在奇数位置/](https://www.geeksforgeeks.org/arrangement-of-the-characters-of-a-word-such-that-all-vowels-are-at-odd-places/)

给定包含小写英文字母的元音和辅音的字符串“S”。任务是找出单词字符排列的方法，使元音只占据奇数位置。

**示例:**

> **输入:**极客
> T3】输出: 36
> ![3_P_2 \times 3_P_3 = 36   ](img/c5ffe5c04fe21a4b5e99b5a31611fb7d.png "Rendered by QuickLaTeX.com")
> **输入:**发布
> **输出:** 1440
> ![4_P_2 \times 5_P_5 = 720   ](img/4ca0006d3d21118e383f470004ab0094.png "Rendered by QuickLaTeX.com")

**进场:**

> 首先找出给定单词中奇数位和偶数位的总数。
> 偶数位总数=楼层(字长/2)
> 奇数位总数=字长–偶数位总数
> 我们来考虑一下字符串“contribute”，那么给定单词中有 10 个字母，有 5 个奇数位、5 个偶数位、4 个元音和 6 个辅音。
> 让我们将这些位置标记为:
> (1)(2)(3)(4)(5)(6)(7)(8)(9)(10)
> 现在，4 个元音可以放在五个位置中的任何一个，标记为 1、3、5、7、9。
> 排列元音的方式数= 5_P_4 = 5！= 120
> 同样，6 个辅音可以排列在剩下的 6 个位置。
> 这些排列的方式数= 6_P_6 = 6！= 720.
> 总路数= (120 x 720) = 86400

以下是上述方法的实现:

## C++

```
// C++ program to find the number of ways
// in which the characters of the word
// can be arranged such that the vowels
// occupy only the odd positions
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// factorial of a number
int fact(int n)
{
    int f = 1;
    for (int i = 2; i <= n; i++) {
        f = f * i;
    }

    return f;
}

// calculating nPr
int npr(int n, int r)
{
    return fact(n) / fact(n - r);
}

// Function to find the number of ways
// in which the characters of the word
// can be arranged such that the vowels
// occupy only the odd positions
int countPermutations(string str)
{
    // Get total even positions
    int even = floor(str.length() / 2);

    // Get total odd positions
    int odd = str.length() - even;

    int ways = 0;

    // Store frequency of each character of
    // the string
    int freq[26] = { 0 };
    for (int i = 0; i < str.length(); i++) {
        ++freq[str[i] - 'a'];
    }

    // Count total number of vowels
    int nvowels
        = freq[0] + freq[4]
          + freq[8] + freq[14]
          + freq[20];

    // Count total number of consonants
    int nconsonants
        = str.length() - nvowels;

    // Calculate the total number of ways
    ways = npr(odd, nvowels) * npr(nconsonants, nconsonants);

    return ways;
}

// Driver code
int main()
{
    string str = "geeks";

    cout << countPermutations(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of ways
// in which the characters of the word
// can be arranged such that the vowels
// occupy only the odd positions
class GFG{
// Function to return the
// factorial of a number
static int fact(int n)
{
    int f = 1;
    for (int i = 2; i <= n; i++) {
        f = f * i;
    }

    return f;
}

// calculating nPr
static int npr(int n, int r)
{
    return fact(n) / fact(n - r);
}

// Function to find the number of ways
// in which the characters of the word
// can be arranged such that the vowels
// occupy only the odd positions
static int countPermutations(String str)
{
    // Get total even positions
    int even = (int)Math.floor((double)(str.length() / 2));

    // Get total odd positions
    int odd = str.length() - even;

    int ways = 0;

    // Store frequency of each character of
    // the string
    int[] freq=new int[26];
    for (int i = 0; i < str.length(); i++) {
        freq[(int)(str.charAt(i)-'a')]++;
    }

    // Count total number of vowels
    int nvowels= freq[0] + freq[4]+ freq[8]
                + freq[14]+ freq[20];

    // Count total number of consonants
    int nconsonants= str.length() - nvowels;

    // Calculate the total number of ways
    ways = npr(odd, nvowels) * npr(nconsonants, nconsonants);

    return ways;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeks";

    System.out.println(countPermutations(str));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find the number
# of ways in which the characters
# of the word can be arranged such
# that the vowels occupy only the
# odd positions
import math

# Function to return the factorial
# of a number
def fact(n):
    f = 1;
    for i in range(2, n + 1):
        f = f * i;

    return f;

# calculating nPr
def npr(n, r):
    return fact(n) / fact(n - r);

# Function to find the number of
# ways in which the characters of
# the word can be arranged such
# that the vowels occupy only the
# odd positions
def countPermutations(str):

    # Get total even positions
    even = math.floor(len(str) / 2);

    # Get total odd positions
    odd = len(str) - even;

    ways = 0;

    # Store frequency of each
    # character of the string
    freq = [0] * 26;
    for i in range(len(str)):
        freq[ord(str[i]) - ord('a')] += 1;

    # Count total number of vowels
    nvowels = (freq[0] + freq[4] + freq[8] +
               freq[14] + freq[20]);

    # Count total number of consonants
    nconsonants = len(str) - nvowels;

    # Calculate the total number of ways
    ways = (npr(odd, nvowels) *
            npr(nconsonants, nconsonants));

    return int(ways);

# Driver code
str = "geeks";

print(countPermutations(str));

# This code is contributed by mits
```

## C#

```
// C# program to find the number of ways
// in which the characters of the word
// can be arranged such that the vowels
// occupy only the odd positions
using System;
class GFG{
// Function to return the
// factorial of a number
static int fact(int n)
{
    int f = 1;
    for (int i = 2; i <= n; i++) {
        f = f * i;
    }

    return f;
}

// calculating nPr
static int npr(int n, int r)
{
    return fact(n) / fact(n - r);
}

// Function to find the number of ways
// in which the characters of the word
// can be arranged such that the vowels
// occupy only the odd positions
static int countPermutations(String str)
{
    // Get total even positions
    int even = (int)Math.Floor((double)(str.Length / 2));

    // Get total odd positions
    int odd = str.Length - even;

    int ways = 0;

    // Store frequency of each character of
    // the string
    int[] freq=new int[26];
    for (int i = 0; i < str.Length; i++) {
        freq[(int)(str[i]-'a')]++;
    }

    // Count total number of vowels
    int nvowels= freq[0] + freq[4]+ freq[8]
                + freq[14]+ freq[20];

    // Count total number of consonants
    int nconsonants= str.Length - nvowels;

    // Calculate the total number of ways
    ways = npr(odd, nvowels) * npr(nconsonants, nconsonants);

    return ways;
}

// Driver code
static void Main()
{
    String str = "geeks";

    Console.WriteLine(countPermutations(str));
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number
// of ways in which the characters
// of the word can be arranged such
// that the vowels occupy only the
// odd positions

// Function to return the
// factorial of a number
function fact($n)
{
    $f = 1;
    for ($i = 2; $i <= $n; $i++)
    {
        $f = $f * $i;
    }

    return $f;
}

// calculating nPr
function npr($n, $r)
{
    return fact($n) / fact($n - $r);
}

// Function to find the number
// of $ways in which the characters
// of the word can be arranged such
// that the vowels occupy only the
// odd positions
function countPermutations($str)
{
    // Get total even positions
    $even = floor(strlen($str)/ 2);

    // Get total odd positions
    $odd = strlen($str) - $even;

    $ways = 0;

    // Store $frequency of each
    // character of the string
    $freq = array_fill(0, 26, 0);
    for ($i = 0; $i < strlen($str); $i++)
    {
        ++$freq[ord($str[$i]) - ord('a')];
    }

    // Count total number of vowels
    $nvowels= $freq[0] + $freq[4] +
              $freq[8] + $freq[14] +
              $freq[20];

    // Count total number of consonants
    $nconsonants= strlen($str) - $nvowels;

    // Calculate the total number of ways
    $ways = npr($odd, $nvowels) *
            npr($nconsonants, $nconsonants);

    return $ways;
}

// Driver code
$str = "geeks";

echo countPermutations($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find the number
// of ways in which the characters
// of the word can be arranged such
// that the vowels occupy only the
// odd positions

// Function to return the
// factorial of a number
function fact(n)
{
    let f = 1;
    for (let i = 2; i <= n; i++)
    {
        f = f * i;
    }

    return f;
}

// calculating nPr
function npr(n, r)
{
    return fact(n) / fact(n - r);
}

// Function to find the number
// of ways in which the characters
// of the word can be arranged such
// that the vowels occupy only the
// odd positions
function countPermutations(str)
{
    // Get total even positions
    let even = Math.floor(str.length/ 2);

    // Get total odd positions
    let odd = str.length - even;

    let ways = 0;

    // Store frequency of each
    // character of the string
    let freq = new Array(26).fill(0);
    for (let i = 0; i < str.length; i++)
    {
        ++freq[str.charCodeAt(i) - 'a'.charCodeAt(0)];
    }

    // Count total number of vowels
    let nvowels= freq[0] + freq[4] +
            freq[8] + freq[14] +
            freq[20];

    // Count total number of consonants
    let nconsonants= str.length - nvowels;

    // Calculate the total number of ways
    ways = npr(odd, nvowels) *
            npr(nconsonants, nconsonants);

    return ways;
}

// Driver code
let str = "geeks";

document.write(countPermutations(str));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
36
```