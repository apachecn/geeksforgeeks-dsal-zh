# 给定字符的所有出现一起出现的字符串的排列数

> 原文:[https://www . geeksforgeeks . org/给定字符的所有出现一起出现的字符串排列数/](https://www.geeksforgeeks.org/number-of-permutations-of-a-string-in-which-all-the-occurrences-of-a-given-character-occurs-together/)

给定一个字符串“s”和一个字符“c”，任务是找到该字符串的置换数，其中字符“c”的所有出现都将在一起(一个接一个)。
**例:**

> **输入:** Str = "AKA" ch = 'A'
> **输出:**2
> AKA 所有唯一的排列是:AKA、AAK 和 KAA
> “A”连续出现只有两次。因此，答案是 2
> **输入:**str = " mississic " ch = ' S '
> **输出:** 840

**天真的方法:**

*   生成给定字符串的所有排列。
*   对于每个排列，检查字符的所有出现是否一起出现。
*   计算上一步的排列数就是答案。

**有效方法:**让字符串的长度为“l”，字符串中字符的频率为“n”。

*   存储字符串中每个字符的频率。
*   如果字符串中不存在该字符，则输出将为“0”。
*   将所有出现的字符视为一个组合的单个字符。
*   因此，“l”将变成“l–occ+1”，其中“OCC”是给定字符的总出现次数，“l”是字符串的新长度。
*   返回**((l 的阶乘)/(除给定字符外每个字符出现次数的阶乘乘积))**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return factorial
// of the number passed as argument
long long int fact(int n)
{
    long long result = 1;
    for (int i = 1; i <= n; i++)
        result *= i;
    return result;
}

// Function to get the total permutations
// which satisfy the given condition
int getResult(string str, char ch)
{
    // Create has to store count
    // of each character
    int has[26] = { 0 };

    // Store character occurrences
    for (int i = 0; i < str.length(); i++)
        has[str[i] - 'A']++;

    // Count number of times
    // Particular character comes
    int particular = has[ch - 'A'];

    // If particular character isn't
    // present in the string then return 0
    if (particular == 0)
        return 0;

    // Remove count of particular character
    has[ch - 'A'] = 0;

    // Total length
    // of the string
    int total = str.length();

    // Assume all occurrences of
    // particular character as a
    // single character.
    total = total - particular + 1;

    // Compute factorial of the length
    long long int result = fact(total);

    // Divide by the factorials of
    // the no. of occurrences of all
    // the characters.
    for (int i = 0; i < 26; i++) {
        if (has[i] > 1) {
            result = result / fact(has[i]);
        }
    }

    // return the result
    return result;
}

// Driver Code
int main()
{
    string str = "MISSISSIPPI";

    // Assuming the string and the character
    // are all in uppercase
    cout << getResult(str, 'S') << endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// Java implementation of above approach
import java.util.*;
class solution
{

// Function to return factorial
// of the number passed as argument
 static int fact(int n)
{
     int result = 1;
    for (int i = 1; i <= n; i++)
        result *= i;
    return result;
}

// Function to get the total permutations
// which satisfy the given condition
static int getResult(String str, char ch)
{
    // Create has to store count
    // of each character
    int has[] = new int[26];

    for(int i=0;i<26;i++)
    has[i]=0;

    // Store character occurrences
    for (int i = 0; i < str.length(); i++)
        has[str.charAt(i) - 'A']++;

    // Count number of times
    // Particular character comes
    int particular = has[ch - 'A'];

    // If particular character isn't
    // present in the string then return 0
    if (particular == 0)
        return 0;

    // Remove count of particular character
    has[ch - 'A'] = 0;

    // Total length
    // of the string
    int total = str.length();

    // Assume all occurrences of
    // particular character as a
    // single character.
    total = total - particular + 1;

    // Compute factorial of the length
     int result = fact(total);

    // Divide by the factorials of
    // the no. of occurrences of all
    // the characters.
    for (int i = 0; i < 26; i++) {
        if (has[i] > 1) {
            result = result / fact(has[i]);
        }
    }

    // return the result
    return result;
}

// Driver Code
public static void main(String args[])
{
    String str = "MISSISSIPPI";

    // Assuming the string and the character
    // are all in uppercase
    System.out.println( getResult(str, 'S') );

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach

# Function to return factorial
# of the number passed as argument
def fact(n) :

    result = 1

    for i in range(1, n + 1) :
        result *= i

    return result

# Function to get the total permutations
# which satisfy the given condition
def getResult(string, ch):

    # Create has to store count
    # of each character
    has = [0] * 26

    # Store character occurrences
    for i in range(len(string)) :
        has[ord(string[i]) - ord('A')] += 1

    # Count number of times
    # Particular character comes
    particular = has[ord(ch) - ord('A')]

    # If particular character isn't
    # present in the string then return 0
    if particular == 0 :
        return 0

    # Remove count of particular character
    has[ord(ch) - ord('A')] = 0

    # Total length
    # of the string
    total = len(string)

    # Assume all occurrences of
    # particular character as a
    # single character.
    total = total - particular + 1

    # Compute factorial of the length
    result = fact(total)

    # Divide by the factorials of
    # the no. of occurrences of all
    # the characters.
    for i in range(26) :

        if has[i] > 1 :
            result /= fact(has[i])

    # return the result
    return result

# Driver code
if __name__ == "__main__" :

    string = "MISSISSIPPI"

    # Assuming the string and the character
    # are all in uppercase
    print(getResult(string,'S'))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to return factorial
// of the number passed as argument
static int fact(int n)
{
    int result = 1;
    for (int i = 1; i <= n; i++)
        result *= i;
    return result;
}

// Function to get the total permutations
// which satisfy the given condition
static int getResult(string str, char ch)
{
    // Create has to store count
    // of each character
    int []has = new int[26];

    for(int i = 0; i < 26; i++)
    has[i] = 0;

    // Store character occurrences
    for (int i = 0; i < str.Length; i++)
        has[str[i] - 'A']++;

    // Count number of times
    // Particular character comes
    int particular = has[ch - 'A'];

    // If particular character
    // isn't present in the string
    // then return 0
    if (particular == 0)
        return 0;

    // Remove count of particular character
    has[ch - 'A'] = 0;

    // Total length of the string
    int total = str.Length;

    // Assume all occurrences of
    // particular character as a
    // single character.
    total = total - particular + 1;

    // Compute factorial of the length
    int result = fact(total);

    // Divide by the factorials of
    // the no. of occurrences of all
    // the characters.
    for (int i = 0; i < 26; i++)
    {
        if (has[i] > 1)
        {
            result = result / fact(has[i]);
        }
    }

    // return the result
    return result;
}

// Driver Code
public static void Main()
{
    string str = "MISSISSIPPI";

    // Assuming the string and the
    // character are all in uppercase
    Console.WriteLine(getResult(str, 'S') );
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return factorial of
// the number passed as argument
function fact($n)
{
    $result = 1;
    for ($i = 1; $i <= $n; $i++)
        $result *= $i;
    return $result;
}

// Function to get the total permutations
// which satisfy the given condition
function getResult($str, $ch)
{
    // Create has to store count
    // of each character
    $has = array_fill(0, 26, NULL);

    // Store character occurrences
    for ($i = 0; $i < strlen($str); $i++)
        $has[ord($str[$i]) - ord('A')]++;

    // Count number of times
    // Particular character comes
    $particular = $has[ord($ch) - ord('A')];

    // If particular character isn't
    // present in the string then return 0
    if ($particular == 0)
        return 0;

    // Remove count of particular character
    $has[ord($ch) - ord('A')] = 0;

    // Total length
    // of the string
    $total = strlen($str);

    // Assume all occurrences of
    // particular character as a
    // single character.
    $total = $total - $particular + 1;

    // Compute factorial of the length
    $result = fact($total);

    // Divide by the factorials of
    // the no. of occurrences of all
    // the characters.
    for ($i = 0; $i < 26; $i++)
    {
        if ($has[$i] > 1)
        {
            $result = $result / fact($has[$i]);
        }
    }

    // return the result
    return $result;
}

// Driver Code
$str = "MISSISSIPPI";

// Assuming the string and the character
// are all in uppercase
echo getResult($str, 'S')."\n" ;

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

// Function to return factorial of
// the number passed as argument
function fact(n)
{
    let result = 1;
    for (let i = 1; i <= n; i++)
        result *= i;
    return result;
}

// Function to get the total permutations
// which satisfy the given condition
function getResult(str, ch)
{
    // Create has to store count
    // of each character
    let has = new Array(26).fill(null);

    // Store character occurrences
    for (let i = 0; i < str.length; i++)
        has[str.charCodeAt(i) - 'A'.charCodeAt(0)]++;

    // Count number of times
    // Particular character comes
    particular = has[ch.charCodeAt(0) - 'A'.charCodeAt(0)];

    // If particular character isn't
    // present in the string then return 0
    if (particular == 0)
        return 0;

    // Remove count of particular character
    has[ch.charCodeAt(0) - 'A'.charCodeAt(0)] = 0;

    // Total length
    // of the string
    let total = str.length;

    // Assume all occurrences of
    // particular character as a
    // single character.
    total = total - particular + 1;

    // Compute factorial of the length
    let result = fact(total);

    // Divide by the factorials of
    // the no. of occurrences of all
    // the characters.
    for (let i = 0; i < 26; i++)
    {
        if (has[i] > 1)
        {
            result = result / fact(has[i]);
        }
    }

    // return the result
    return result;
}

// Driver Code
let str = "MISSISSIPPI";

// Assuming the string and the character
// are all in uppercase
document.write(getResult(str, 'S') + "<br>");

// This code is contributed by gfgking
</script>
```

**Output:** 

```
840
```