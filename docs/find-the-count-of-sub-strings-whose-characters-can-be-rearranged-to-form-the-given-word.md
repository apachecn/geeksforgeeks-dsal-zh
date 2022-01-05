# 找出字符可以重新排列形成给定单词的子串的个数

> 原文:[https://www . geeksforgeeks . org/find-子字符串的计数-其字符可以重新排列以形成给定的单词/](https://www.geeksforgeeks.org/find-the-count-of-sub-strings-whose-characters-can-be-rearranged-to-form-the-given-word/)

给定一个字符串 **str** ，任务是找到所有长度为 4 的子字符串的计数，这些子字符串的字符可以重新排列以形成单词**“拍手”**。
**例:**

> **输入:**str = " clapc "
> T3】输出:2
> “clap”和“lapc”是所需的子串
> **输入:** str = "abcd"
> **输出:** 0

**方法:**对于每一个长度为 4 的子串，从单词**【拍拍】**开始计算字符出现的次数。如果每个字符在子字符串中都恰好出现一次，则增加**计数**。最后打印**计数**。
以下是上述方法的实施:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count of
// required occurrence
int countOcc(string s)
{

    // To store the count of occurrences
    int cnt = 0;

    // Check first four characters from ith position
    for (int i = 0; i < s.length() - 3; i++)
    {

        // Variables for counting the required characters
        int c = 0, l = 0, a = 0, p = 0;

        // Check the four contiguous characters which
        // can be reordered to form 'clap'
        for (int j = i; j < i + 4; j++)
        {
            switch (s[j])
            {
                case 'c':
                    c++;
                    break;
                case 'l':
                    l++;
                    break;
                case 'a':
                    a++;
                    break;
                case 'p':
                    p++;
                    break;
            }
        }

        // If all four contiguous characters are present
        // then increment cnt variable
        if (c == 1 && l == 1 && a == 1 && p == 1)
            cnt++;
    }

    return cnt;
}

// Driver code
int main()
{
    string s = "clapc";
    transform(s.begin(), s.end(), s.begin(), ::tolower);
    cout << (countOcc(s));
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count of
    // required occurrence
    static int countOcc(String s)
    {

        // To store the count of occurrences
        int cnt = 0;

        // Check first four characters from ith position
        for (int i = 0; i < s.length() - 3; i++) {

            // Variables for counting the required characters
            int c = 0, l = 0, a = 0, p = 0;

            // Check the four contiguous characters which
            // can be reordered to form 'clap'
            for (int j = i; j < i + 4; j++) {
                switch (s.charAt(j)) {
                case 'c':
                    c++;
                    break;
                case 'l':
                    l++;
                    break;
                case 'a':
                    a++;
                    break;
                case 'p':
                    p++;
                    break;
                }
            }

            // If all four contiguous characters are present
            // then increment cnt variable
            if (c == 1 && l == 1 && a == 1 && p == 1)
                cnt++;
        }

        return cnt;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "clapc";
        System.out.print(countOcc(s.toLowerCase()));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# required occurrence
def countOcc(s):

    # To store the count of occurrences
    cnt = 0

    # Check first four characters from ith position
    for i in range(0, len(s) - 3):

        # Variables for counting the required characters
        c, l, a, p = 0, 0, 0, 0

        # Check the four contiguous characters
        # which can be reordered to form 'clap'
        for j in range(i, i + 4):

            if s[j] == 'c':
                c += 1

            elif s[j] == 'l':
                l += 1

            elif s[j] == 'a':
                a += 1

            elif s[j] == 'p':
                p += 1

        # If all four contiguous characters are
        # present then increment cnt variable
        if c == 1 and l == 1 and a == 1 and p == 1:
            cnt += 1

    return cnt

# Driver code
if __name__ == "__main__":

    s = "clapc"
    print(countOcc(s.lower()))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// required occurrence
static int countOcc(string s)
{

    // To store the count of occurrences
    int cnt = 0;

    // Check first four characters
    // from ith position
    for (int i = 0; i < s.Length - 3; i++)
    {

        // Variables for counting the
        // required characters
        int c = 0, l = 0, a = 0, p = 0;

        // Check the four contiguous characters
        // which can be reordered to form 'clap'
        for (int j = i; j < i + 4; j++)
        {
            switch (s[j])
            {
                case 'c':
                    c++;
                    break;
                case 'l':
                    l++;
                    break;
                case 'a':
                    a++;
                    break;
                case 'p':
                    p++;
                    break;
            }
        }

        // If all four contiguous characters are
        // present then increment cnt variable
        if (c == 1 && l == 1 && a == 1 && p == 1)
            cnt++;
    }

    return cnt;
}

// Driver code
public static void Main()
{
    string s = "clapc";
    Console.Write(countOcc(s.ToLower()));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// required occurrence
function countOcc($s)
{

    // To store the count of occurrences
    $cnt = 0;

    // Check first four characters
    // from ith position
    for ($i = 0; $i < strlen($s) - 3; $i++)
    {

        // Variables for counting the
        // required characters
        $c = 0; $l = 0; $a = 0; $p = 0;

        // Check the four contiguous characters 
        // which can be reordered to form 'clap'
        for ($j = $i; $j < $i + 4; $j++)
        {
            switch ($s[$j])
            {
            case 'c':
                $c++;
                break;
            case 'l':
                $l++;
                break;
            case 'a':
                $a++;
                break;
            case 'p':
                $p++;
                break;
            }
        }

        // If all four contiguous characters are present
        // then increment cnt variable
        if ($c == 1 && $l == 1 &&
            $a == 1 && $p == 1)
            $cnt++;
    }

    return $cnt;
}

// Driver code
$s = "clapc";

echo countOcc(strtolower($s));

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// required occurrence
function countOcc(s)
{

    // To store the count of occurrences
    var cnt = 0;

    // Check first four characters from ith position
    for (var i = 0; i < s.length - 3; i++)
    {

        // Variables for counting the required characters
        var c = 0, l = 0, a = 0, p = 0;

        // Check the four contiguous characters which
        // can be reordered to form 'clap'
        for (var j = i; j < i + 4; j++)
        {
            switch (s[j])
            {
                case 'c':
                    c++;
                    break;
                case 'l':
                    l++;
                    break;
                case 'a':
                    a++;
                    break;
                case 'p':
                    p++;
                    break;
            }
        }

        // If all four contiguous characters are present
        // then increment cnt variable
        if (c == 1 && l == 1 && a == 1 && p == 1)
            cnt++;
    }

    return cnt;
}

// Driver code
var s = "clapc";
s = s.toLowerCase();
document.write(countOcc(s));

</script>
```

**Output:** 

```
2
```