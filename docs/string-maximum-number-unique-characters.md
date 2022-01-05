# 唯一字符数最大的字符串

> 原文:[https://www . geesforgeks . org/string-最大数量-唯一-字符/](https://www.geeksforgeeks.org/string-maximum-number-unique-characters/)

给定一个字符串列表，找到其中最大的字符串。最大字符串是唯一字符数最多的字符串。

**示例:**

```
Input : "AN KOW", "LO JO", "ZEW DO RO" 
Output : "ZEW DO RO" 
Explanation : 
"ZEW DO RO" has maximum distinct letters.

Input : "ROMEO", "EMINEM", "RADO"
Output : "ROMEO" 
Explanation : In case of tie, we can print
any of the strings.
```

我们对字符串进行迭代，并获取一个布尔数组来检查字母的存在。此外，记录最大唯一字母数。返回包含最大数量不同字符的字符串。

## C++

```
// C++ code to find
// the largest string
#include <bits/stdc++.h>
using namespace std;

// Function to find string
// with maximum number of
// unique characters.
void LargestString(string *na)
{
    int N = sizeof(na) /
            sizeof(na[0]);
    int c[N];

    // Index of string with
    // maximum unique characters
    int m = 1;

    // iterate through
    // all strings
    for (int j = 0; j < N; j++)
    {
        // array indicating any
        // alphabet included or
        // not included
        bool character[26];

        // count number of unique
        // alphabets in each string
        for (int k = 0; k < na[j].size(); k++)
        {
            int x = (int)(na[j][k] - 'A');
            if (na[j][k] != ' ' &&
                character[x] == false)
            {
                c[j]++;
                character[x] = true;
            }
        }

        // keep track of maximum
        // number of alphabets
        if (c[j] > c[m])
            m = j;
    }
    // print result
    cout << na[m] << endl;
}

// Driver code
int main()
{
    string na[] = {"BOB", "A AB C JOHNSON",
                   "ANJALI","ASKRIT",
                   "ARMAN MALLIK"};

    LargestString(na);
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the largest string
import java.lang.*;
import java.io.*;
import java.util.Arrays;

class Geek {

    // Function to find string with maximum
    // number of unique characters.
    public static void LargestString(String na[])
    {
        int N = na.length;
        int c[] = new int[N];

        // Index of string with maximum unique
        // characters
        int m = 0;

        // iterate through all strings
        for (int j = 0; j < N; j++)
        {
            // array indicating any alphabet
            // included or not included
            boolean character[] = new boolean[26];

            // count number of unique alphabets in each string
            for (int k = 0; k < na[j].length(); k++)
            {
                int x = na[j].charAt(k) - 'A';
                if ((na[j].charAt(k) != ' ') &&
                        (character[x] == false))
                {
                    c[j]++;
                    character[x] = true;
                }
            }

            // keep track of maximum number of alphabets
            if (c[j] > c[m])
                m = j;
        }

        // print result
        System.out.println(na[m]);
    }

    // Driver code
    public static void main(String[] args)
    {
        String na[] = {"BOB", "A AB C JOHNSON","ANJALI",
                       "ASKRIT", "ARMAN MALLIK"};

        LargestString(na);
    }
}
```

## 蟒蛇 3

```
# Python3 code to find the largest string

# Function to find string with maximum
# number of unique characters.
def LargestString(na):
    N = len(na)
    c = [0] * N

    # Index of string with
    # maximum unique characters
    m = 0

    # Iterate through all strings
    for j in range(N):

        # Array indicating any alphabet
        # included or not included
        character = [False] * 26

        # count number of unique
        # alphabets in each string
        for k in range(len(na[j])):
            x = ord(na[j][k]) - ord('A')

            if ((na[j][k] != ' ') and (character[x] == False)):
                c[j] += 1
                character[x] = True

            # keep track of maximum
            # number of alphabets
            if (c[j] > c[m]):
                m = j

    # print result
    print(na[m])

# Driver code
na = ["BOB", "A AB C JOHNSON","ANJALI",
                "ASKRIT", "ARMAN MALLIK"]
LargestString(na)

# This article is Contributed by Sharad Bhardwaj.
```

## C#

```
// C# code to find the largest string
using System;

class GFG {

    // Function to find string with maximum
    // number of unique characters.
    public static void LargestString(string []na)
    {
        int N = na.Length;
        int []c = new int[N];

        // Index of string with maximum unique
        // characters
        int m = 0;

        // iterate through all strings
        for (int j = 0; j < N; j++)
        {
            // array indicating any alphabet
            // included or not included
            bool []character = new bool[26];

            // count number of unique alphabets
            // in each string
            for (int k = 0; k < na[j].Length; k++)
            {
                int x = na[j][k] - 'A';

                if ((na[j][k] != ' ') &&
                        (character[x] == false))
                {
                    c[j]++;
                    character[x] = true;
                }
            }

            // keep track of maximum number of
            // alphabets
            if (c[j] > c[m])
                m = j;
        }

        // print result
        Console.Write(na[m]);
    }

    // Driver code
    public static void Main()
    {
        string []na = {"BOB", "A AB C JOHNSON",
           "ANJALI", "ASKRIT", "ARMAN MALLIK"};

        LargestString(na);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find the largest string

// Function to find string with maximum
// number of unique characters
function LargestString($na)
{
    $N = sizeof($na);
    $c = array_fill(0, $N, 0);

    // Index of string with maximum unique
    // characters
    $m = 0;

    // iterate through all strings
    for ($j = 0; $j < $N; $j++)
    {
        // array indicating any alphabet
        // included or not included
        $character = array_fill(0, 26,
                                false);

        // count number of unique
        // alphabets in each string
        for ($k = 0; $k < strlen($na[$j]);
                                    $k++)
        {
            $x = ord($na[$j][$k]) - 65;
            if (($na[$j][$k] != ' ') &&
                ($character[$x] == false))
            {
                $c[$j]++;
                $character[$x] = true;
            }
        }

        // keep track of maximum
        // number of alphabets
        if ($c[$j] > $c[$m])
            $m = $j;
    }

    // print result
    echo $na[$m]."\n";
}

// Driver code
$na = array("BOB", "A AB C JOHNSON",
            "ASKRIT", "ARMAN MALLIK",
                           "ANJALI");
LargestString($na);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// C# code to find the largest string

// Function to find string with maximum
// number of unique characters.
function LargestString(na)
{
    let N = na.length;
    let c = new Array(N);

    // Index of string with maximum unique
    // characters
    let m = 1;

    // iterate through all strings
    for (let j = 0; j < N; j++)
    {
        // array indicating any alphabet
        // included or not included
        let character = new Array(26,0);

        // count number of unique alphabets
        // in each string
        for (let k = 0; k < na[j].length; k++)
        {
            let x = na[j][k].charCodeAt(0)-65;

            if ((na[j][k] != ' ') &&
                    (character[x] == 0))
            {
                c[j]++;
                character[x] = 1;
            }
        }

        // keep track of maximum number of
        // alphabets
        if (c[j] > c[m])
            m = j;
    }

    // prlet result
    document.write(na[m]);
}

// Driver code

let na =["BOB", "A AB C JOHNSON","ANJALI", "ASKRIT", "ARMAN MALLIK"];

LargestString(na);

</script>
```

**输出:**

```
A AB C JOHNSON
```