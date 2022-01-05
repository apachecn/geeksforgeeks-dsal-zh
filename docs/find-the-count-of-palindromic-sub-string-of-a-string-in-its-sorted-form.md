# 以字符串的排序形式找到字符串的回文子串的计数

> 原文:[https://www . geeksforgeeks . org/find-the-count-of-回文-sub-string-of-a-string-in-it-sorted-form/](https://www.geeksforgeeks.org/find-the-count-of-palindromic-sub-string-of-a-string-in-its-sorted-form/)

给定一个由小写英文字母组成的字符串 *str* ，任务是找出以排序形式出现的回文子字符串的总数 *str* 。
**例:**

> **输入:** str = "acbbd"
> **输出:** 6
> 其排序形式的所有回文子串(“abbcd”)都是“a”、“b”、“b”、“bb”、“c”和“d”。
> **输入:**str = " abbdbd "
> **输出:** 16

**天真的方法:**一种方法是对给定的字符串进行排序，然后计算存在的回文子字符串的总数。为了找到回文子串的数目[,可以使用这个](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string-set-2/)方法，它具有 O(n^2).的时间复杂度
**优化方法:**一种有效的方法是统计每个字符的频率，然后对于每个频率回文总数将为 *(n*(n+1))/2* ，因为排序后的字符串的所有回文子字符串将由相同的字符组成。
例如，字符串*“aabbbcd”*的回文子串将为*“a”、“aa”、……、“bbb”、“c”、……*等。这种方法的时间复杂度为 0(n)。

*   创建一个哈希表，用于存储字符串*字符串*中每个字符的频率。
*   遍历哈希表，对于每个非零频率，将*(哈希[i] *(哈希[i]+1)) / 2* 添加到*和*中。
*   最后打印*和*。

以下是上述方法的实现:

## C++

```
// CPP program to find the count of palindromic sub-string
// of a string in it's ascending form
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// function to return count of palindromic sub-string
int countPalindrome(string str)
{
    int n = str.size();
    int sum = 0;

    // calculate frequency
    int hashTable[MAX_CHAR];
    for (int i = 0; i < n; i++)
        hashTable[str[i] - 'a']++;

    // calculate count of palindromic sub-string
    for (int i = 0; i < 26; i++) {
        if (hashTable[i])
            sum += (hashTable[i] * (hashTable[i] + 1) / 2);
    }

    // return result
    return sum;
}

// driver program
int main()
{
    string str = "ananananddd";

    cout << countPalindrome(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of palindromic sub-string
// of a string in it's ascending form

class GFG {

    final static int MAX_CHAR = 26;

// function to return count of palindromic sub-string
    static int countPalindrome(String str) {
        int n = str.length();
        int sum = 0;

        // calculate frequency
        int hashTable[] = new int[MAX_CHAR];
        for (int i = 0; i < n; i++) {
            hashTable[str.charAt(i) - 'a']++;
        }

        // calculate count of palindromic sub-string
        for (int i = 0; i < 26; i++) {
            if (hashTable[i] != 0) {
                sum += (hashTable[i] * (hashTable[i] + 1) / 2);
            }
        }

        // return result
        return sum;
    }

// driver program
    public static void main(String[] args) {
        String str = "ananananddd";

        System.out.println(countPalindrome(str));

    }
}
```

## 蟒蛇 3

```
# Python3 program to find the count of
# palindromic sub-string of a string
# in it's ascending form
MAX_CHAR = 26

# function to return count of
# palindromic sub-string
def countPalindrome(str):

    n = len (str)
    sum = 0

    # calculate frequency
    hashTable = [0] * MAX_CHAR
    for i in range(n):
        hashTable[ord(str[i]) -
                  ord('a')] += 1

    # calculate count of palindromic
    # sub-string
    for i in range(26) :
        if (hashTable[i]):
            sum += (hashTable[i] *
                   (hashTable[i] + 1) // 2)

    # return result
    return sum

# Driver Code
if __name__ == "__main__":

    str = "ananananddd"

    print (countPalindrome(str))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the count of palindromic sub-string
// of a string in it's ascending form
using System;

public class GFG{

    readonly static int MAX_CHAR = 26;

// function to return count of palindromic sub-string
    static int countPalindrome(String str) {
        int n = str.Length;
        int sum = 0;

        // calculate frequency
        int []hashTable = new int[MAX_CHAR];
        for (int i = 0; i < n; i++) {
            hashTable[str[i] - 'a']++;
        }

        // calculate count of palindromic sub-string
        for (int i = 0; i < 26; i++) {
            if (hashTable[i] != 0) {
                sum += (hashTable[i] * (hashTable[i] + 1) / 2);
            }
        }

        // return result
        return sum;
    }

// driver program
    public static void Main() {
        String str = "ananananddd";

        Console.Write(countPalindrome(str));

    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the count of
// palindromic sub-string of a string
// in it's ascending form
$MAX_CHAR = 26;

// function to return count of
// palindromic sub-string
function countPalindrome($str)
{
    global $MAX_CHAR;
    $n = strlen($str);
    $sum = 0;

    // calculate frequency
    $hashTable = array_fill(0, $MAX_CHAR, 0);
    for ($i = 0; $i < $n; $i++)
        $hashTable[ord($str[$i]) - ord('a')]++;

    // calculate count of palindromic sub-string
    for ($i = 0; $i < 26; $i++)
    {
        if ($hashTable[$i])
            $sum += (int)($hashTable[$i] *
                         ($hashTable[$i] + 1) / 2);
    }

    // return result
    return $sum;
}

// Driver Code
$str = "ananananddd";

echo countPalindrome($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the count of palindromic sub-string
// of a string in it's ascending form

var MAX_CHAR = 26;

// function to return count of palindromic sub-string
function countPalindrome(str)
{
    var n = str.length;
    var sum = 0;

    // calculate frequency
    var hashTable = Array(MAX_CHAR).fill(0);
    for (var i = 0; i < n; i++)
        hashTable[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // calculate count of palindromic sub-string
    for (var i = 0; i < 26; i++) {
        if (hashTable[i])
            sum += (hashTable[i] * (hashTable[i] + 1) / 2);
    }

    // return result
    return sum;
}

// driver program
var str = "ananananddd";
document.write( countPalindrome(str));

</script>
```

**Output:** 

```
26
```