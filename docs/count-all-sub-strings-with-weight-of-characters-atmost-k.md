# 统计所有字符权重为 K 的子串

> 原文:[https://www . geesforgeks . org/count-all-sub-string-with-weight-of-characters-Atmos-k/](https://www.geeksforgeeks.org/count-all-sub-strings-with-weight-of-characters-atmost-k/)

给定一个由小英文字母组成的字符串 **P** 和一个由英文字母表中所有字符的权重组成的字符串 **Q** ，使得对于所有的“I”，0 ≤ Q[i] ≤ 9。任务是在 **K** 找到唯一子串的总数和权重。
**示例:**

> **输入:** P = "ababab "，Q = "12345678912345678912345678 "，K = 5
> **输出:** 7
> **说明:**
> 单个字符权重之和≤ 5 的子串为:
> “a”、“ab”、“b”、“bc”、“c”、“d”、“e”
> **输入:**P = " acbacaa

**方法:**想法是使用一个[无序集](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)来存储唯一值。按照以下步骤计算答案:

*   使用[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples/)迭代所有子字符串，并保持到目前为止遇到的所有字符的权重总和。
*   如果字符的总和不大于 K，则将其插入散列表中。
*   最后，输出 hashmap 的大小。

以下是上述方法的实现:

## C++

```
// C++ program to find the count of
// all the sub-strings with weight of
// characters atmost K
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// all the substrings with weight
// of characters atmost K
int distinctSubstring(string& P, string& Q,
                      int K, int N)
{

    // Hashmap to store all substrings
    unordered_set<string> S;

    // Iterate over all substrings
    for (int i = 0; i < N; ++i) {

        // Maintain the sum of all characters
        // encountered so far
        int sum = 0;

        // Maintain the substring till the
        // current position
        string s;

        for (int j = i; j < N; ++j) {

            // Get the position of the
            // character in string Q
            int pos = P[j] - 'a';

            // Add weight to current sum
            sum += Q[pos] - '0';

            // Add current character to substring
            s += P[j];

            // If sum of characters is <=K
            // then insert  into the set
            if (sum <= K) {
                S.insert(s);
            }

            else {
                break;
            }
        }
    }

    // Finding the size of the set
    return S.size();
}

// Driver code
int main()
{
    string P = "abcde";
    string Q = "12345678912345678912345678";
    int K = 5;
    int N = P.length();

    cout << distinctSubstring(P, Q, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// all the sub-Strings with weight of
// characters atmost K
import java.util.*;

class GFG{

// Function to find the count of
// all the subStrings with weight
// of characters atmost K
static int distinctSubString(String P, String Q,
                      int K, int N)
{

    // Hashmap to store all subStrings
    HashSet<String> S = new HashSet<String>();

    // Iterate over all subStrings
    for (int i = 0; i < N; ++i) {

        // Maintain the sum of all characters
        // encountered so far
        int sum = 0;

        // Maintain the subString till the
        // current position
        String s = "";

        for (int j = i; j < N; ++j) {

            // Get the position of the
            // character in String Q
            int pos = P.charAt(j) - 'a';

            // Add weight to current sum
            sum += Q.charAt(pos) - '0';

            // Add current character to subString
            s += P.charAt(j);

            // If sum of characters is <=K
            // then insert  into the set
            if (sum <= K) {
                S.add(s);
            }

            else {
                break;
            }
        }
    }

    // Finding the size of the set
    return S.size();
}

// Driver code
public static void main(String[] args)
{
    String P = "abcde";
    String Q = "12345678912345678912345678";
    int K = 5;
    int N = P.length();

    System.out.print(distinctSubString(P, Q, K, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find the count of
# all the sub-strings with weight of
# characters atmost K

# Function to find the count of
# all the substrings with weight
# of characters atmost K
def distinctSubstring(P, Q, K, N):

    # Hashmap to store all substrings
    S = set()

    # Iterate over all substrings
    for i in range(0,N):

        # Maintain the sum of all characters
        # encountered so far
        sum = 0;

        # Maintain the substring till the
        # current position
        s = ''

        for j in range(i,N):

            # Get the position of the
            # character in string Q
            pos = ord(P[j]) - 97

            # Add weight to current sum
            sum = sum + ord(Q[pos]) - 48

            # Add current character to substring
            s += P[j]

            # If sum of characters is <=K
            # then insert  into the set
            if (sum <= K):
                S.add(s)
            else:
                break

    # Finding the size of the set
    return len(S)

# Driver code
P = "abcde"
Q = "12345678912345678912345678"
K = 5
N = len(P)

print(distinctSubstring(P, Q, K, N))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find the count of
// all the sub-Strings with weight of
// characters atmost K
using System;
using System.Collections.Generic;

class GFG{

// Function to find the count of
// all the subStrings with weight
// of characters atmost K
static int distinctSubString(String P, String Q,
                      int K, int N)
{

    // Hashmap to store all subStrings
    HashSet<String> S = new HashSet<String>();

    // Iterate over all subStrings
    for (int i = 0; i < N; ++i) {

        // c the sum of all characters
        // encountered so far
        int sum = 0;

        // Maintain the subString till the
        // current position
        String s = "";

        for (int j = i; j < N; ++j) {

            // Get the position of the
            // character in String Q
            int pos = P[j] - 'a';

            // Add weight to current sum
            sum += Q[pos] - '0';

            // Add current character to subString
            s += P[j];

            // If sum of characters is <=K
            // then insert  into the set
            if (sum <= K) {
                S.Add(s);
            }

            else {
                break;
            }
        }
    }

    // Finding the size of the set
    return S.Count;
}

// Driver code
public static void Main(String[] args)
{
    String P = "abcde";
    String Q = "12345678912345678912345678";
    int K = 5;
    int N = P.Length;

    Console.Write(distinctSubString(P, Q, K, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the count of
// all the sub-Strings with weight of
// characters atmost K

// Function to find the count of
// all the subStrings with weight
// of characters atmost K
function distinctSubString(P, Q, K, N)
{

    // Hashmap to store all subStrings
    let S = new Set();

    // Iterate over all subStrings
    for (let i = 0; i < N; ++i) {

        // Maintain the sum of all characters
        // encountered so far
        let sum = 0;

        // Maintain the subString till the
        // current position
        let s = "";

        for (let j = i; j < N; ++j) {

            // Get the position of the
            // character in String Q
            let pos = P[j].charCodeAt() - 'a'.charCodeAt();

            // Add weight to current sum
            sum += Q[pos].charCodeAt() - '0'.charCodeAt();

            // Add current character to subString
            s += P[j];

            // If sum of characters is <=K
            // then insert  into the set
            if (sum <= K) {
                S.add(s);
            }

            else {
                break;
            }
        }
    }

    // Finding the size of the set
    return S.size;
}

// Driver code

      let P = "abcde";
    let Q = "12345678912345678912345678";
    let K = 5;
    let N = P.length;

    document.write(distinctSubString(P, Q, K, N));

</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N <sup>2</sup> )