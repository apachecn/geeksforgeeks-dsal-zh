# 当重复恰好 K 次时给出 S 的排列的字符串

> 原文:[https://www . geeksforgeeks . org/string-当重复-精确-k 次-给出-s-置换/](https://www.geeksforgeeks.org/string-which-when-repeated-exactly-k-times-gives-a-permutation-of-s/)

给定一个整数 **K** 和一个小写英文字符的字符串 **str** ，任务是找到一个字符串 **s** ，这样当 **s** 被精确地重复 **K** 次时，它给出一个 **S** 的排列。如果没有这样的字符串，打印 **-1** 。
**举例:**

> **输入:** str = "aabb "，k = 2
> **输出:**ab
> 【ab】重复 2 次给出“abab”，是“AABB”
> **的排列输入:** str = "aabb "，k = 3
> **输出:** -1

**方法:**一种有效的方法是统计给定字符串的每个字符的频率。如果任何字符的频率不能被 **k** 整除，那么解决方法是不可能的，打印 **-1** 。否则，将每个字符**(频率/ k)** 次添加到结果字符串中，并最终打印生成的字符串。
以下是上述方法的实施:

## C++

```
// C++ program to find a string which when repeated
// exactly k times gives a permutation
// of the given string
#include <bits/stdc++.h>
using namespace std;

// Function to return a string which when repeated
// exactly k times gives a permutation of s
string K_String(string s, int k)
{
    // size of string
    int n = s.size();

    // to frequency of each character
    int fre[26] = { 0 };

    // get frequency of each character
    for (int i = 0; i < n; i++)
        fre[s[i] - 'a']++;

    // to store final answer
    string str = "";

    for (int i = 0; i < 26; i++) {

        // check if frequency is divisible by k
        if (fre[i] % k == 0) {
            int x = fre[i] / k;

            // add to answer
            while (x--) {
                str += (char)(i + 'a');
            }
        }

        // if frequency is not divisible by k
        else {
            return "-1";
        }
    }

    return str;
}

// Driver code
int main()
{
    string s = "aabb";
    int k = 2;

    // function call
    cout << K_String(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a string which when repeated
// exactly k times gives a permutation
// of the given string
class GfG {

// Function to return a string which when repeated
// exactly k times gives a permutation of s
static String K_String(String s, int k)
{
    // size of string
    int n = s.length();

    // to frequency of each character
    int fre[] = new int[26];

    // get frequency of each character
    for (int i = 0; i < n; i++)
        fre[s.charAt(i) - 'a']++;

    // to store final answer
    String str = "";

    for (int i = 0; i < 26; i++) {

        // check if frequency is divisible by k
        if (fre[i] % k == 0) {
            int x = fre[i] / k;

            // add to answer
            while (x != 0) {
                str += (char)(i + 'a');
                x--;
            }
        }

        // if frequency is not divisible by k
        else {
            return "-1";
        }
    }

    return str;
}

// Driver code
public static void main(String[] args)
{
    String s = "aabb";
    int k = 2;

    // function call
    System.out.println(K_String(s, k));

}
}
```

## 蟒蛇 3

```
# Python 3 program to find a string
# which when repeated exactly k times
# gives a permutation of the given string

# Function to return a string which
# when repeated exactly k times gives
# a permutation of s
def K_String(s, k):

    # size of string
    n = len(s)

    # to frequency of each character
    fre = [0] * 26

    # get frequency of each character
    for i in range(n):
        fre[ord(s[i]) - ord('a')] += 1

    # to store final answer
    str = ""

    for i in range( 26) :

        # check if frequency is divisible by k
        if (fre[i] % k == 0) :
            x = fre[i] // k

            # add to answer
            while (x) :
                str += chr(i + ord('a'))
                x -= 1

        # if frequency is not divisible by k
        else :
            return "-1"

    return str

# Driver code
if __name__ == "__main__":

    s = "aabb"
    k = 2

    # function call
    print( K_String(s, k))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find a string which
// when repeated exactly k times gives
// a permutation of the given string
using System;

class GFG
{

// Function to return a string which
// when repeated exactly k times gives
// a permutation of s
static String K_String(String s, int k)
{
    // size of string
    int n = s.Length ;

    // to frequency of each character
    int []fre = new int[26];

    // get frequency of each character
    for (int i = 0; i < n; i++)
        fre[s[i] - 'a']++;

    // to store final answer
    String str = "";

    for (int i = 0; i < 26; i++)
    {

        // check if frequency is
        // divisible by k
        if (fre[i] % k == 0)
        {
            int x = fre[i] / k;

            // add to answer
            while (x != 0)
            {
                str += (char)(i + 'a');
                x--;
            }
        }

        // if frequency is not divisible by k
        else
        {
            return "-1";
        }
    }

    return str;
}

// Driver code
public static void Main(String []args)
{
    String s = "aabb";
    int k = 2;

    // function call
    Console.WriteLine(K_String(s, k));
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a string which
// when repeated exactly k times gives
// a permutation of the given string

// Function to return a string which
// when repeated exactly k times gives
// a permutation of s
function K_String($s, $k)
{
    // size of string
    $n = strlen($s);

    // to frequency of each character
    $fre = $array = array_fill(0, 26, 0);

    // get frequency of each character
    for ($i = 0; $i < $n; $i++)
        $fre[ord($s[$i]) - ord('a')]++;

    // to store final answer
    $str = "";

    for ($i = 0; $i < 26; $i++)
    {

        // check if frequency is divisible by k
        if ($fre[$i] % $k == 0)
        {
            $x = $fre[$i] / $k;

            // add to answer
            while ($x--)
            {
                $str .= chr($i + ord('a'));
            }
        }

        // if frequency is not divisible by k
        else
        {
            return "-1";
        }
    }
    return $str;
}

// Driver code
$s = "aabb";
$k = 2;

// function call
echo K_String($s, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript program to find a string which when repeated
// exactly k times gives a permutation
// of the given string

    // Function to return a string which when repeated
    // exactly k times gives a permutation of s
    function K_String(s,k)
    {
        // size of string
    let n = s.length;

    // to frequency of each character
    let fre = new Array(26);
    for(let i=0;i<fre.length;i++)
    {
        fre[i]=0;
    }

    // get frequency of each character
    for (let i = 0; i < n; i++)
        fre[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // to store final answer
    let str = "";

    for (let i = 0; i < 26; i++) {

        // check if frequency is divisible by k
        if (fre[i] % k == 0) {
            let x = Math.floor(fre[i] / k);

            // add to answer
            while (x != 0) {
                str += String.fromCharCode(i + 'a'.charCodeAt(0));
                x--;
            }
        }

        // if frequency is not divisible by k
        else {
            return "-1";
        }
    }

    return str;
    }

    // Driver code
    let s = "aabb";
    let k = 2;
     // function call
    document.write(K_String(s, k));

    //This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
ab
```