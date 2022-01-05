# 删除最少数量的字符，使两个字符串成为字谜

> 原文:[https://www . geesforgeks . org/remove-最小字符数-两个字符串-变成字谜/](https://www.geeksforgeeks.org/remove-minimum-number-characters-two-strings-become-anagram/)

给定两个小写字符串，任务是使它们成为[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。唯一允许的操作是从任何字符串中删除一个字符。找到要删除的最小字符数以使两个字符串都成为字谜？
如果两个字符串以任何顺序包含相同的数据集，那么字符串被称为**字谜**。

**示例:**

```
Input : str1 = "bcadeh" str2 = "hea"
Output: 3
We need to remove b, c and d from str1.

Input : str1 = "cddgk" str2 = "gcd"
Output: 2

Input : str1 = "bca" str2 = "acb"
Output: 0
```

其思想是为字符串和每个字符的存储频率创建字符计数数组。现在迭代两个字符串的计数数组和任意字符的频率差**ABS(count 1[str 1[I]-' a ']–count 2[str 2[I]-' a '])**在两个字符串中是要在任一字符串中删除的字符数。

## C++

```
// C++ program to find minimum number of characters
// to be removed to make two strings anagram.
#include<bits/stdc++.h>
using namespace std;
const int CHARS = 26;

// function to calculate minimum numbers of characters
// to be removed to make two strings anagram
int remAnagram(string str1, string str2)
{
    // make hash array for both string and calculate
    // frequency of each character
    int count1[CHARS] = {0}, count2[CHARS] = {0};

    // count frequency of each character in first string
    for (int i=0; str1[i]!='\0'; i++)
        count1[str1[i]-'a']++;

    // count frequency of each character in second string
    for (int i=0; str2[i]!='\0'; i++)
        count2[str2[i]-'a']++;

    // traverse count arrays to find number of characters
    // to be removed
    int result = 0;
    for (int i=0; i<26; i++)
        result += abs(count1[i] - count2[i]);
    return result;
}

// Driver program to run the case
int main()
{
    string str1 = "bcadeh", str2 = "hea";
    cout << remAnagram(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of
// characters to be removed to make two
// strings anagram.
import java.util.*;

class GFG {

    // function to calculate minimum numbers
    // of characters to be removed to make
    // two strings anagram
    static int remAnagram(String str1, String str2)
    {
        // make hash array for both string
        // and calculate frequency of each
        // character
        int count1[] = new int[26];
        int count2[] = new int[26];

        // count frequency of each character
        // in first string
        for (int i = 0; i < str1.length() ; i++)
            count1[str1.charAt(i) -'a']++;

        // count frequency of each character
        // in second string
        for (int i = 0; i < str2.length() ; i++)
            count2[str2.charAt(i) -'a']++;

        // traverse count arrays to find
        // number of characters to be removed
        int result = 0;
        for (int i = 0; i < 26; i++)
            result += Math.abs(count1[i] -
                               count2[i]);
        return result;
    }

    // Driver program to run the case
    public static void main(String[] args)
    {
        String str1 = "bcadeh", str2 = "hea";
        System.out.println(remAnagram(str1, str2));
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program to find minimum
# number of characters
# to be removed to make two
# strings anagram.

CHARS = 26

# function to calculate minimum
# numbers of characters
# to be removed to make two
# strings anagram
def remAnagram(str1, str2):

    # make hash array for both string
    # and calculate
    # frequency of each character
    count1 = [0]*CHARS
    count2 = [0]*CHARS

    # count frequency of each character
    # in first string
    i = 0
    while i < len(str1):
        count1[ord(str1[i])-ord('a')] += 1
        i += 1

    # count frequency of each character
    # in second string
    i =0
    while i < len(str2):
        count2[ord(str2[i])-ord('a')] += 1
        i += 1

    # traverse count arrays to find
    # number of characters
    # to be removed
    result = 0
    for i in range(26):
        result += abs(count1[i] - count2[i])
    return result

# Driver program to run the case
if __name__ == "__main__":
    str1 = "bcadeh"
    str2 = "hea"
    print(remAnagram(str1, str2))

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to find minimum
// number of characters to be
// removed to make two strings
// anagram.
using System;

class GFG
{

    // function to calculate
    // minimum numbers of
    // characters to be removed
    // to make two strings anagram
    static int remAnagram(string str1,
                          string str2)
    {
        // make hash array for both
        // string and calculate frequency
        // of each character
        int []count1 = new int[26];
        int []count2 = new int[26];

        // count frequency of each
        // character in first string
        for (int i = 0; i < str1.Length ; i++)
            count1[str1[i] -'a']++;

        // count frequency of each 
        // character in second string
        for (int i = 0; i < str2.Length ; i++)
            count2[str2[i] -'a']++;

        // traverse count arrays to
        // find number of characters
        // to be removed
        int result = 0;
        for (int i = 0; i < 26; i++)
            result += Math.Abs(count1[i] -
                               count2[i]);
        return result;
    }

    // Driver Code
    public static void Main()
    {
        string str1 = "bcadeh",
               str2 = "hea";
        Console.Write(remAnagram(str1, str2));
    }
}

// This code is contributed
// by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number of
// characters to be removed to make two
// strings anagram.

// function to calculate minimum numbers
// of characters to be removed to make
// two strings anagram
function remAnagram($str1, $str2)
{
    // make hash array for both string
    // and calculate frequency of each
    // character
    $count1 = array(26);
    $count2 = array(26);

    // count frequency of each character
    // in first string
    for ($i = 0; $i < strlen($str1) ; $i++)
        $count1[$str1[$i] - 'a']++;

    // count frequency of each character
    // in second string
    for ($i = 0; $i < strlen($str2) ; $i++)
        $count2[$str2[$i] -'a']++;

    // traverse count arrays to find
    // number of characters to be removed
    $result = 0;
    for ($i = 0; $i < 26; $i++)
        $result += abs($count1[$i] -
                       $count2[$i]);
    return $result;
}

// Driver Code
{
    $str1 = "bcadeh"; $str2 = "hea";
    echo(remAnagram($str1, $str2));
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript program to find minimum number of
// characters to be removed to make two
// strings anagram.

// function to calculate minimum numbers
// of characters to be removed to make
// two strings anagram
function remAnagram(str1, str2)
{
    // make hash array for both string
    // and calculate frequency of each
    // character
    var count1 = Array.from({length: 26}, (_, i) => 0);
    var count2 = Array.from({length: 26}, (_, i) => 0);

    // count frequency of each character
    // in first string
    for (i = 0; i < str1.length ; i++)
        count1[str1.charAt(i).charCodeAt(0) -'a'.charCodeAt(0)]++;

    // count frequency of each character
    // in second string
    for (i = 0; i < str2.length ; i++)
        count2[str2.charAt(i).charCodeAt(0) -'a'.charCodeAt(0)]++;

    // traverse count arrays to find
    // number of characters to be removed
    var result = 0;
    for (i = 0; i < 26; i++)
        result += Math.abs(count1[i] -
                           count2[i]);
    return result;
}

// Driver program to run the case
var str1 = "bcadeh", str2 = "hea";
document.write(remAnagram(str1, str2));

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
3
```

**时间复杂度:**O(n)
T3】辅助空间: O(ALPHABET-SIZE)

上述解决方案可以优化为使用单计数阵列。

## C++

```
// C++ implementation to count number of deletions
// required from two strings to create an anagram
#include <bits/stdc++.h>
using namespace std;
const int CHARS = 26;

int countDeletions(string str1, string str2)
{
    int arr[CHARS] = {0};
    for (int i = 0; i < str1.length(); i++)
        arr[str1[i] - 'a']++;

    for (int i = 0; i < str2.length(); i++)
        arr[str2[i] - 'a']--;

    long long int ans = 0;
    for(int i = 0; i < CHARS; i++)
        ans +=abs(arr[i]);
    return ans;
}

int main() {
    string str1 = "bcadeh", str2 = "hea";
    cout << countDeletions(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count number of deletions
// required from two strings to create an anagram

class GFG {

    final static int CHARS = 26;

    static int countDeletions(String str1, String str2) {
        int arr[] = new int[CHARS];
        for (int i = 0; i < str1.length(); i++) {
            arr[str1.charAt(i) - 'a']++;
        }

        for (int i = 0; i < str2.length(); i++) {
            arr[str2.charAt(i) - 'a']--;
        }

        int ans = 0;
        for (int i = 0; i < CHARS; i++) {
            ans += Math.abs(arr[i]);
        }
        return ans;
    }

    static public void main(String[] args) {
        String str1 = "bcadeh", str2 = "hea";
        System.out.println(countDeletions(str1, str2));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find minimum
# number of characters to be
# removed to make two strings
# anagram.

# function to calculate minimum
# numbers of characters to be
# removed to make two strings anagram
def makeAnagram(a, b):
    buffer = [0] * 26
    for char in a:
        buffer[ord(char) - ord('a')] += 1
    for char in b:
        buffer[ord(char) - ord('a')] -= 1
    return sum(map(abs, buffer))

# Driver Code
if __name__ == "__main__" :

    str1 = "bcadeh"
    str2 = "hea"
    print(makeAnagram(str1, str2))

# This code is contributed
# by Raghib Ahsan
```

## C#

```

// C# implementation to count number of deletions
// required from two strings to create an anagram
using System;
public class GFG {

    readonly static int CHARS = 26;

    static int countDeletions(String str1, String str2) {
        int []arr = new int[CHARS];
        for (int i = 0; i < str1.Length; i++) {
            arr[str1[i]- 'a']++;
        }

        for (int i = 0; i < str2.Length; i++) {
            arr[str2[i] - 'a']--;
        }

        int ans = 0;
        for (int i = 0; i < CHARS; i++) {
            ans += Math.Abs(arr[i]);
        }
        return ans;
    }

    static public void Main() {
        String str1 = "bcadeh", str2 = "hea";
        Console.WriteLine(countDeletions(str1, str2));
    }
}
  //This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count number of deletions
// required from two strings to create an anagram

function countDeletions($str1, $str2)
{
    $CHARS = 26;
    $arr = array();
    for ($i = 0; $i < strlen($str1); $i++)
    {
        $arr[ord($str1[$i]) - ord('a')]++;
    }

    for ($i = 0; $i < strlen($str2); $i++)
    {
        $arr[ord($str2[$i]) - ord('a')]--;
    }

    $ans = 0;
    for ($i = 0; $i < $CHARS; $i++)
    {
        $ans += abs($arr[$i]);
    }
    return $ans;
}

// Driver Code
$str1 = "bcadeh"; $str2 = "hea";
echo(countDeletions($str1, $str2));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript implementation to count
// number of deletions required from
// two strings to create an anagram
CHARS = 26;

function countDeletions(str1, str2)
{
    var arr = Array.from({length: CHARS}, (_, i) => 0);

    for(i = 0; i < str1.length; i++)
    {
        arr[str1.charAt(i).charCodeAt(0) -
                       'a'.charCodeAt(0)]++;
    }

    for(i = 0; i < str2.length; i++)
    {
        arr[str2.charAt(i).charCodeAt(0) -
                       'a'.charCodeAt(0)]--;
    }

    var ans = 0;
    for(i = 0; i < CHARS; i++)
    {
        ans += Math.abs(arr[i]);
    }
    return ans;
}

// Driver code
str1 = "bcadeh", str2 = "hea";

document.write(countDeletions(str1, str2));

// This code is contributed by Rajput-Ji

</script>
```

**输出:**

```
3
```

感谢 [vishal9619](https://auth.geeksforgeeks.org/user/vishal9619/articles) 提出这个优化方案。
本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。