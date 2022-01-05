# 给定字符串中“GFG”子序列的计数

> 原文:[https://www . geesforgeks . org/count-gfg-subseques-given-string/](https://www.geeksforgeeks.org/count-gfg-subsequences-given-string/)

给定一串长度为 **n** 的大写字母。任务是找到给定字符串中“GFG”子序列的计数。
**例:**

```
Input : str[] = "GFGFG"
Output : 4
GFGFG, GFGFG, GFGFG, GFGFG

Input : str[] = "ABCFGFPG"
Output : 1
```

要找到给定字符串中“GFG”子序列的数量，请观察每个“F”，如果我们知道它前后的“G”的数量。那么那个‘F’的“GFG”子序列的数目等于那个‘F’前后的‘G’的数目的乘积。
所以，想法是维护一个数组，arr[]，其中 arr[i]存储索引 I 之前的‘G’的数字，如果字符串的第 I 个字符是‘F’，如果第 I 个字符是‘G’，则存储索引 I 之前的‘F’的数字。
此外，每当我们遇到“G”时，我们都会计算并在结果中存储“GFG”子序列的数量。
以下是本办法的实施情况:

## C++

```
// CPP Program to find the "GFG" subsequence in
// the given string
#include <bits/stdc++.h>
using namespace std;
#define MAX 100

// Print the count of "GFG" subsequence in the string
void countSubsequence(char s[], int n)
{
    int cntG = 0, cntF = 0, result = 0, C=0;

    // Traversing the given string
    for (int i = 0; i < n; i++) {
        switch (s[i]) {

        // If the character is 'G', increment
        // the count of 'G', increase the result
        // and update the array.
        case 'G':
            cntG++;
            result+=C;
            break;

        // If the character is 'F', increment
        // the count of 'F' and update the array.
        case 'F':
            cntF++;
            C+=cntG;
            break;

        // Ignore other character.
        default:
            continue;
        }
    }

    cout << result << endl;
}

// Driven Program
int main()
{
    char s[] = "GFGFG";
    int n = strlen(s);
    countSubsequence(s, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the "GFG" subsequence
// in the given string

public class GFG {

    static int max = 100;

    // Print the count of "GFG" subsequence
    // in the string
    static void countSubsequence(String s, int n)
    {
        int cntG = 0, cntF = 0, result = 0, C=0;

        // Traversing the given string
        for (int i = 0; i < n; i++) {
            switch (s.charAt(i)) {

            // If the character is 'G',
            // increment the count of 'G',
            // increase the result and
            // update the array.
            case 'G':
                cntG++;
                result+=C;
                break;

            // If the character is 'F',
            // increment the count of 'F'
            // and update the array.
            case 'F':
                cntF++;
                C+=cntG;
                break;

            // Ignore other character.
            default:
                continue;
            }
        }

        System.out.println(result);
    }

    // Driver code   
    public static void main(String args[]) {
        String s= "GFGFG";
        int n = s.length();
        countSubsequence(s, n);
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python 3 Program to find the "GFG"
# subsequence in the given string
MAX = 100

# Print the count of "GFG" subsequence
# in the string
def countSubsequence(s, n):
    cntG = 0
    cntF = 0
    result = 0
    C=0

    # Traversing the given string
    for i in range(n):
        if (s[i] == 'G'):

            # If the character is 'G', increment
            # the count of 'G', increase the result
            # and update the array.
            cntG += 1
            result += C
            continue

        # If the character is 'F', increment
        # the count of 'F' and update the array.
        if (s[i] == 'F'):
            cntF += 1
            C += cntG
            continue

        # Ignore other character.
        else:
            continue

    print(result)

# Driver Code
if __name__ == '__main__':
    s = "GFGFG"
    n = len(s)
    countSubsequence(s, n)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# Program to find the "GFG" subsequence
// in the given string
using System;

class GFG {

    // Print the count of "GFG" subsequence
    // in the string
    static void countSubsequence(string s,
                                     int n)
    {
        int cntG = 0, cntF = 0, result = 0, C=0;

        // Traversing the given string
        for (int i = 0; i < n; i++) {
            switch (s[i]) {

            // If the character is 'G',
            // increment the count of 'G',
            // increase the result and
            // update the array.
            case 'G':
                cntG++;
                result += C;
                break;

            // If the character is 'F',
            // increment the count of 'F'
            // and update the array.
            case 'F':
                cntF++;
                C+=cntG;
                break;

            // Ignore other character.
            default:
                continue;
            }
        }

        Console.WriteLine(result);
    }

    // Driver code
    public static void Main()
    {
        string s= "GFGFG";
        int n = s.Length;
        countSubsequence(s, n);
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>

// Javascript Program to find the "GFG" subsequence in
// the given string
var MAX = 100;

// Print the count of "GFG" subsequence in the string
function countSubsequence( s, n)
{
    var cntG = 0, cntF = 0, result = 0, C=0;

    // Traversing the given string
    for (var i = 0; i < n; i++) {
        switch (s[i]) {

        // If the character is 'G', increment
        // the count of 'G', increase the result
        // and update the array.
        case 'G':
            cntG++;
            result+=C;
            break;

        // If the character is 'F', increment
        // the count of 'F' and update the array.
        case 'F':
            cntF++;
            C+=cntG;
            break;

        // Ignore other character.
        default:
            continue;
        }
    }

    document.write( result );
}

// Driven Program
var s = "GFGFG";
var n = (s.length);
countSubsequence(s, n);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
4
```