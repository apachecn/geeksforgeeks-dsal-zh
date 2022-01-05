# 计算字符串中子序列的最大出现次数，以使子序列中的索引位于 A.P.

> 原文:[https://www . geesforgeks . org/count-字符串中子序列最大出现次数-这样子序列中的索引就是在-a-p 中/](https://www.geeksforgeeks.org/count-maximum-occurrence-of-subsequence-in-string-such-that-indices-in-subsequence-is-in-a-p/)

给定一个字符串 **S** ，任务是计算给定字符串中子序列的最大出现次数，使得子序列的字符索引为[算术级数](https://www.geeksforgeeks.org/arithmetic-progression/)。

**示例:**

> **输入:** S = "xxxyy"
> **输出:** 6
> **解释:**
> 有一个子序列“xy”，其中子序列的每个字符的索引都在 A.P.
> 构成子序列“xy”的不同字符的索引–
> {(1，4)，(1，5)，(2，4)，(2，5)，(3，4)，(3，4)，(3，5)}
> 
> **输入:** S = "pop"
> **输出:** 2
> **解释:**
> 有一个子序列“p”，其中子序列的每个字符的索引都在 A.P.
> 组成子序列“p”的不同字符的索引–
> {(1)、(2)}

**处理方法:**问题中的关键观察是，如果一个字符串中有两个字符的集合出现次数大于任何单个字符的出现次数，那么这些字符将形成该字符串中出现字符最多的子序列，即算术级数，因为每两个整数总会形成一个算术级数。下面是步骤的说明:

*   迭代字符串并计算字符串中字符的出现频率。那就是考虑长度为 1 的子序列。
*   迭代字符串，选择字符串中每两个可能的字符，并增加字符串子序列的频率。
*   最后，从长度 1 和 2 中找出子序列的最大频率。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
#include <bits/stdc++.h>

using namespace std;

// Function to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
int maximumOccurrence(string s)
{
    int n = s.length();

    // Frequencies of subsequence
    map<string, int> freq;

    // Loop to find the frequencies
    // of subsequence of length 1
    for (int i = 0; i < n; i++) {
        string temp = "";
        temp += s[i];
        freq[temp]++;
    }

    // Loop to find the frequencies
    // subsequence of length 2
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            string temp = "";
            temp += s[i];
            temp += s[j];
            freq[temp]++;
        }
    }

    int answer = INT_MIN;

    // Finding maximum frequency
    for (auto it : freq)
        answer = max(answer, it.second);
    return answer;
}

// Driver Code
int main()
{
    string s = "xxxyy";

    cout << maximumOccurrence(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
import java.util.*;

class GFG
{
    // Function to find the
    // maximum occurrence of the subsequence
    // such that the indices of characters
    // are in arithmetic progression
    static int maximumOccurrence(String s)
    {
        int n = s.length();

        // Frequencies of subsequence
        HashMap<String, Integer> freq = new HashMap<String,Integer>();
        int i, j;

        // Loop to find the frequencies
        // of subsequence of length 1
        for ( i = 0; i < n; i++) {
            String temp = "";
            temp += s.charAt(i);
            if (freq.containsKey(temp)){
                freq.put(temp,freq.get(temp)+1);
            }
            else{
                freq.put(temp, 1);
            }
        }

        // Loop to find the frequencies
        // subsequence of length 2
        for (i = 0; i < n; i++) {
            for (j = i + 1; j < n; j++) {
                String temp = "";
                temp += s.charAt(i);
                temp += s.charAt(j);
                if(freq.containsKey(temp))
                    freq.put(temp,freq.get(temp)+1);
                else
                    freq.put(temp,1);
            }
        }
        int answer = Integer.MIN_VALUE;

        // Finding maximum frequency
        for (int it : freq.values())
            answer = Math.max(answer, it);
        return answer;
    }

    // Driver Code
    public static void main(String []args)
    {
        String s = "xxxyy";

        System.out.print(maximumOccurrence(s));
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum occurrence of the subsequence
# such that the indices of characters
# are in arithmetic progression

# Function to find the
# maximum occurrence of the subsequence
# such that the indices of characters
# are in arithmetic progression
def maximumOccurrence(s):
    n = len(s)

    # Frequencies of subsequence
    freq = {}

    # Loop to find the frequencies
    # of subsequence of length 1
    for i in s:
        temp = ""
        temp += i
        freq[temp] = freq.get(temp, 0) + 1

    # Loop to find the frequencies
    # subsequence of length 2
    for i in range(n):
        for j in range(i + 1, n):
            temp = ""
            temp += s[i]
            temp += s[j]
            freq[temp] = freq.get(temp, 0) + 1

    answer = -10**9

    # Finding maximum frequency
    for it in freq:
        answer = max(answer, freq[it])
    return answer

# Driver Code
if __name__ == '__main__':
    s = "xxxyy"

    print(maximumOccurrence(s))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
using System;
using System.Collections.Generic;
class GFG
{
// Function to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
static int maximumOccurrence(string s)
{
  int n = s.Length;

  // Frequencies of subsequence
  Dictionary<string,
             int> freq = new Dictionary<string,
                                        int>();
  int i, j;

  // Loop to find the frequencies
  // of subsequence of length 1
  for ( i = 0; i < n; i++)
  {
    string temp = "";
    temp += s[i];
    if (freq.ContainsKey(temp))
    {
      freq[temp]++;
    }
    else
    {
      freq[temp] = 1;
    }
  }

  // Loop to find the frequencies
  // subsequence of length 2
  for (i = 0; i < n; i++)
  {
    for (j = i + 1; j < n; j++)
    {
      string temp = "";
      temp += s[i];
      temp += s[j];
      if(freq.ContainsKey(temp))
        freq[temp]++;
      else
        freq[temp] = 1;
    }
  }
  int answer =int.MinValue;

  // Finding maximum frequency
  foreach(KeyValuePair<string,
                       int> it in freq)
    answer = Math.Max(answer, it.Value);
  return answer;
}

// Driver Code
public static void Main(string []args)
{
  string s = "xxxyy";
  Console.Write(maximumOccurrence(s));
}
}

// This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression

// Function to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
function maximumOccurrence(s)
{
    var n = s.length;

    // Frequencies of subsequence
    var freq = new Map();

    // Loop to find the frequencies
    // of subsequence of length 1
    for (var i = 0; i < n; i++) {
        var temp = "";
        temp += s[i];
        if(freq.has(temp))
                freq.set(temp, freq.get(temp)+1)
            else
                freq.set(temp, 1)
    }

    // Loop to find the frequencies
    // subsequence of length 2
    for (var i = 0; i < n; i++) {
        for (var j = i + 1; j < n; j++) {
            var temp = "";
            temp += s[i];
            temp += s[j];

            if(freq.has(temp))
                freq.set(temp, freq.get(temp)+1)
            else
                freq.set(temp, 1)
        }
    }

    var answer = -1000000000;

    // Finding maximum frequency
    freq.forEach((value, key) => {
        answer = Math.max(answer, value);
    });
    return answer;
}

// Driver Code
var s = "xxxyy";
document.write( maximumOccurrence(s));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N <sup>2</sup> )

**有效方法:**想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)范例来计算字符串中长度为 1 和 2 的子序列的频率。下面是步骤的说明:

*   计算频率数组中字符串字符的频率。
*   对于长度为 2 的字符串的子序列，DP 状态将为

```
dp[i][j] = Total number of times ith
  character occured before jth character.
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression

#include <bits/stdc++.h>

using namespace std;

// Function to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
int maximumOccurrence(string s)
{
    int n = s.length();

    // Frequency for characters
    int freq[26] = { 0 };
    int dp[26][26] = { 0 };

    // Loop to count the occurrence
    // of ith character before jth
    // character in the given string
    for (int i = 0; i < n; i++) {
        int c = (s[i] - 'a');

        for (int j = 0; j < 26; j++)
            dp[j] += freq[j];

        // Increase the frequency
        // of s[i] or c of string
        freq++;
    }

    int answer = INT_MIN;

    // Maximum occurrence of subsequence
    // of length 1 in given string
    for (int i = 0; i < 26; i++)
        answer = max(answer, freq[i]);

    // Maximum occurrence of subsequence
    // of length 2 in given string
    for (int i = 0; i < 26; i++) {
        for (int j = 0; j < 26; j++) {
            answer = max(answer, dp[i][j]);
        }
    }

    return answer;
}

// Driver Code
int main()
{
    string s = "xxxyy";

    cout << maximumOccurrence(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression

class GFG{

// Function to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
static int maximumOccurrence(String s)
{
    int n = s.length();

    // Frequency for characters
    int freq[] = new int[26];
    int dp[][] = new int[26][26];

    // Loop to count the occurrence
    // of ith character before jth
    // character in the given String
    for (int i = 0; i < n; i++) {
        int c = (s.charAt(i) - 'a');

        for (int j = 0; j < 26; j++)
            dp[j] += freq[j];

        // Increase the frequency
        // of s[i] or c of String
        freq++;
    }

    int answer = Integer.MIN_VALUE;

    // Maximum occurrence of subsequence
    // of length 1 in given String
    for (int i = 0; i < 26; i++)
        answer = Math.max(answer, freq[i]);

    // Maximum occurrence of subsequence
    // of length 2 in given String
    for (int i = 0; i < 26; i++) {
        for (int j = 0; j < 26; j++) {
            answer = Math.max(answer, dp[i][j]);
        }
    }

    return answer;
}

// Driver Code
public static void main(String[] args)
{
    String s = "xxxyy";

    System.out.print(maximumOccurrence(s));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum occurrence of the subsequence
# such that the indices of characters
# are in arithmetic progression
import sys

# Function to find the maximum occurrence
# of the subsequence such that the
# indices of characters are in
# arithmetic progression
def maximumOccurrence(s):

    n = len(s)

    # Frequency for characters
    freq = [0] * (26)

    dp = [[0 for i in range(26)]
             for j in range(26)]

    # Loop to count the occurrence
    # of ith character before jth
    # character in the given String
    for i in range(n):
        c = (ord(s[i]) - ord('a'))

        for j in range(26):
            dp[j] += freq[j]

        # Increase the frequency
        # of s[i] or c of String
        freq += 1

    answer = -sys.maxsize

    # Maximum occurrence of subsequence
    # of length 1 in given String
    for i in range(26):
        answer = max(answer, freq[i])

    # Maximum occurrence of subsequence
    # of length 2 in given String
    for i in range(26):
        for j in range(26):
            answer = max(answer, dp[i][j])

    return answer

# Driver Code
if __name__ == '__main__':

    s = "xxxyy"

    print(maximumOccurrence(s))

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
using System;
class GFG{

// Function to find the maximum
// occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
static int maximumOccurrence(string s)
{
    int n = s.Length;

    // Frequency for characters
    int []freq = new int[26];
    int [,]dp = new int[26, 26];

    // Loop to count the occurrence
    // of ith character before jth
    // character in the given String
    for(int i = 0; i < n; i++)
    {
       int x = (s[i] - 'a');

       for(int j = 0; j < 26; j++)
          dp[x, j] += freq[j];

       // Increase the frequency
       // of s[i] or c of String
       freq[x]++;
    }

    int answer = int.MinValue;

    // Maximum occurrence of subsequence
    // of length 1 in given String
    for(int i = 0; i < 26; i++)
       answer = Math.Max(answer, freq[i]);

    // Maximum occurrence of subsequence
    // of length 2 in given String
    for(int i = 0; i < 26; i++)
    {
       for(int j = 0; j < 26; j++)
       {
          answer = Math.Max(answer, dp[i, j]);
       }
    }
    return answer;
}

// Driver Code
public static void Main(string[] args)
{
    string s = "xxxyy";

    Console.Write(maximumOccurrence(s));
}
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// javascript implementation to find the
// maximum occurrence of the subsequence
// such that the indices of characters
// are in arithmetic progression
    // Function to find the
    // maximum occurrence of the subsequence
    // such that the indices of characters
    // are in arithmetic progression
    function maximumOccurrence(s) {
        var n = s.length;

        // Frequency for characters
        var freq = Array(26).fill(0);
        var dp = Array(26).fill().map(()=>Array(26).fill(0));

        // Loop to count the occurrence
        // of ith character before jth
        // character in the given String
        for (var i = 0; i < n; i++) {
            var c = (s.charCodeAt(i) - 'a'.charCodeAt(0));

            for (var j = 0; j < 26; j++)
                dp[j] += freq[j];

            // Increase the frequency
            // of s[i] or c of String
            freq++;
        }

        var answer = Number.MIN_VALUE;

        // Maximum occurrence of subsequence
        // of length 1 in given String
        for (var i = 0; i < 26; i++)
            answer = Math.max(answer, freq[i]);

        // Maximum occurrence of subsequence
        // of length 2 in given String
        for (var i = 0; i < 26; i++) {
            for (var j = 0; j < 26; j++) {
                answer = Math.max(answer, dp[i][j]);
            }
        }

        return answer;
    }

    // Driver Code

        var s = "xxxyy";

        document.write(maximumOccurrence(s));

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(26 * N)