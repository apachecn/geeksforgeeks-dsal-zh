# 生成一个大小为 N 的字符串，其大小为 M 的每个子串都有正好 K 个不同的字符

> 原文:[https://www . geeksforgeeks . org/generate-a-string-of-size-n-其每个大小为 m-的子串具有-k 个完全不同的字符/](https://www.geeksforgeeks.org/generate-a-string-of-size-n-whose-each-substring-of-size-m-has-exactly-k-distinct-characters/)

给定 3 个正整数 **N** 、 **M** 和 **K** 。任务是构建一个由小写字母组成的长度为 **N** 的字符串，这样长度为 **M** 的每个子串都恰好具有 **K** 个不同的字母。
**示例:**

> **输入:** N = 5，M = 2，K = 2
> **输出:** abade
> **解释:**
> 大小为 2 的每个子串“ab”、“ba”、“ad”、“de”都有 2 个不同的字母。
> **输入:** N = 7，M = 5，K = 3
> **输出:**abcaab
> **解释:**
> 大小为 5 的每个子串“tleel”、“leelt”、“eelte”都有 3 个不同的字母。

**方法:**在一个大小为 N 的字符串中，每个大小为 M 的子串必须包含正好 K 个不同的字母-

*   构造一个有 K 个不同字母的字符串，从“a”到“z”直到 M 的大小，然后把剩下的字母放在“a”这样的位置..
*   因为我们已经生成了一个大小为 M、K 值不同的字符串。现在，继续重复，直到我们达到 n 的字符串大小

以下是上述方法的实现:

## C++

```
// C++ program to generate a string of size N
// whose each substring of size M
// has exactly K distinct characters

#include <bits/stdc++.h>
using namespace std;

// Function to generate the string
string generateString(int N, int M, int K)
{

    // Declare empty string
    string s = "";

    // counter for M
    int cnt1 = 0;

    // counter for K
    int cnt2 = 0;

    // Loop to generate string size of N
    for (int i = 0; i < N; i++) {
        cnt1++;
        cnt2++;

        // Generating K distinct
        // letters one by one
        if (cnt1 <= M) {
            if (cnt2 <= K) {
                s = s + char(96 + cnt1);
            }

            // After generating b distinct letters,
            // append rest a-b letters as 'a'
            else {
                s = s + 'a';
            }
        }

        // Reset the counter value
        // and repeat the process
        else {
            cnt1 = 1;
            cnt2 = 1;
            s = s + 'a';
        }
    }

    // return final result string
    return s;
}

// Driver code
int main()
{
    int N = 7, M = 5, K = 3;

    cout << generateString(N, M, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate a String of size N
// whose each subString of size M
// has exactly K distinct characters
import java.util.*;
class GFG{

// Function to generate the String
static String generateString(int N, int M, int K)
{

    // Declare empty String
    String s = "";

    // counter for M
    int cnt1 = 0;

    // counter for K
    int cnt2 = 0;

    // Loop to generate String size of N
    for (int i = 0; i < N; i++)
    {
        cnt1++;
        cnt2++;

        // Generating K distinct
        // letters one by one
        if (cnt1 <= M)
        {
            if (cnt2 <= K)
            {
                s = s + (char)(96 + cnt1);
            }

            // After generating b distinct letters,
            // append rest a-b letters as 'a'
            else
            {
                s = s + 'a';
            }
        }

        // Reset the counter value
        // and repeat the process
        else
        {
            cnt1 = 1;
            cnt2 = 1;
            s = s + 'a';
        }
    }

    // return final result String
    return s;
}

// Driver code
public static void main(String[] args)
{
    int N = 7, M = 5, K = 3;

    System.out.println(generateString(N, M, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to generate a string of size N
# whose each substring of size M
# has exactly K distinct characters
# Function to generate the string
def generateString(N, M, K):

    # Declare empty string
    s = ""

    # counter for M
    cnt1 = 0

    # counter for K
    cnt2 = 0

    # Loop to generate string size of N
    for i in range (N):
        cnt1 += 1
        cnt2 += 1

        # Generating K distinct
        # letters one by one
        if (cnt1 <= M):
            if (cnt2 <= K):
                s = s + chr(96 + cnt1)

            # After generating b distinct letters,
            # append rest a-b letters as 'a'
            else:
                s = s + 'a'

        # Reset the counter value
        # and repeat the process
        else:
            cnt1 = 1
            cnt2 = 1
            s = s + 'a'

    # return final result string
    return s

# Driver code
if __name__ == "__main__": 
    N = 7
    M = 5
    K = 3
    print (generateString(N, M, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to generate a String of
// size N whose each subString of size
// M has exactly K distinct characters
using System;

class GFG{

// Function to generate the String
static String generateString(int N, int M, int K)
{

    // Declare empty String
    String s = "";

    // Counter for M
    int cnt1 = 0;

    // Counter for K
    int cnt2 = 0;

    // Loop to generate String size of N
    for(int i = 0; i < N; i++)
    {
       cnt1++;
       cnt2++;

       // Generating K distinct
       // letters one by one
       if (cnt1 <= M)
       {
           if (cnt2 <= K)
           {
               s = s + (char)(96 + cnt1);
           }

           // After generating b distinct letters,
           // append rest a-b letters as 'a'
           else
           {
               s = s + 'a';
           }
       }

       // Reset the counter value
       // and repeat the process
       else
       {
           cnt1 = 1;
           cnt2 = 1;
           s = s + 'a';
       }
    }

    // Return readonly result String
    return s;
}

// Driver code
public static void Main(String[] args)
{
    int N = 7, M = 5, K = 3;

    Console.WriteLine(generateString(N, M, K));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to generate
// a String of size N
// whose each subString of size M
// has exactly K distinct characters

    // Function to generate the String
    function generateString(N,M,K)
    {
        // Declare empty string
    let s = "";

    // counter for M
    let cnt1 = 0;

    // counter for K
    let cnt2 = 0;

    // Loop to generate string size of N
    for (let i = 0; i < N; i++) {
        cnt1++;
        cnt2++;

        // Generating K distinct
        // letters one by one
        if (cnt1 <= M) {
            if (cnt2 <= K) {
                s = s + String.fromCharCode(96 + cnt1);
            }

            // After generating b distinct letters,
            // append rest a-b letters as 'a'
            else {
                s = s + 'a';
            }
        }

        // Reset the counter value
        // and repeat the process
        else {
            cnt1 = 1;
            cnt2 = 1;
            s = s + 'a';
        }
    }

    // return final result string
    return s;
    }

    // Driver code
    let N = 7, M = 5, K = 3;
    document.write( generateString(N, M, K))

    // This code is contributed
    // by avanitrachhadiya2155

</script>
```

**Output:** 

```
abcaaab
```

***时间复杂度:**O(N)*
T5**空间复杂度:** O(1)