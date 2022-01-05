# 频率为 K 的给定字符串中每个不同字符的最大索引

> 原文:[https://www . geeksforgeeks . org/给定频率字符串中每个不同字符的最大索引-k/](https://www.geeksforgeeks.org/largest-index-for-each-distinct-character-in-given-string-with-frequency-k/)

给定一个字符串 **S** 由小写英文字母和一个整数 **K** 组成，任务是为 S 中的每个不同字符找到与该字符完全相同的最大索引 **K** 次。如果不存在这样的字符，请打印-1。按照字典顺序打印结果。
**注:**考虑 s 中基于 0 的索引。

**示例:**

> **输入:**S =【cbaabacbcd】，K = 2
> **输出:** { {a 4}、{b 7}、{c 8} }
> **说明:**
> 对于‘a’，拥有 2 a 的最大指数为“cbaab”。
> 对于“b”，拥有 2 个 b 的最大指数是“cbaabaac”。
> 对于‘c’，有 2 个 c 的最大指数是“cbaabaacb”。
> 对于“d”，没有我们有 2 d 的索引
> 
> **输入:** P = "acbacbacbaba "，K = 3
> **输出:** { {a 8}、{b 9}、{c 11} }

**方法:**想法是首先[找到字符串 S](https://www.geeksforgeeks.org/print-all-distinct-characters-of-a-string-in-order-3-methods/) 中所有不同的字符。然后，对于每个小写英文字符，检查它是否存在于 S 中，并从 S 开始运行 for 循环，并保持该字符的计数直到现在。当计数等于 K 时，相应地更新索引答案。最后，在向量结果中附加这个字符及其对应的索引。
以下是上述办法的实施情况。

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to find largest index for each
// distinct character occuring exactly K times.
void maxSubstring(string& S, int K, int N)
{

    // finding all characters present in S
    int freq[26];
    memset(freq, 0, sizeof freq);

    // Finding all distinct characters in S
    for (int i = 0; i < N; ++i) {
        freq[S[i] - 'a'] = 1;
    }

    // vector to store result for each character
    vector<pair<char, int> > answer;

    // loop through each lower case English character
    for (int i = 0; i < 26; ++i) {

        // if current character is absent in s
        if (freq[i] == 0)
            continue;

        // getting current character
        char ch = i + 97;

        // finding count of character ch in S
        int count = 0;

        // to store max Index encountred so far
        int index = -1;

        for (int j = 0; j < N; ++j) {
            if (S[j] == ch)
                count++;

            if (count == K)
                index = j;
        }

        answer.push_back({ ch, index });
    }

    int flag = 0;

    // printing required result
    for (int i = 0; i < (int)answer.size(); ++i) {

        if (answer[i].second > -1) {
            flag = 1;
            cout << answer[i].first << " "
                << answer[i].second << endl;
        }
    }

    // If no such character exists, print -1
    if (flag == 0)
        cout << "-1" << endl;
}

// Driver code
int main()
{
    string S = "cbaabaacbcd";
    int K = 2;
    int N = S.length();

    maxSubstring(S, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG{
    static class pair
    {     char first;
        int  second;
        public pair(char first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
}

// Function to find largest
//  index for each distinct
// character occuring exactly K times.
static void maxSubString(char [] S,
                         int K, int N)
{
    // finding all characters present in S
    int []freq = new int[26];   

    // Finding all distinct characters in S
    for (int i = 0; i < N; ++i)
    {
        freq[S[i] - 'a'] = 1;
    }

    // vector to store result for each character
    Vector<pair> answer = new Vector<pair>();

    // loop through each lower case English character
    for (int i = 0; i < 26; ++i)
    {
        // if current character is absent in s
        if (freq[i] == 0)
            continue;

        // getting current character
        char ch = (char) (i + 97);

        // finding count of character ch in S
        int count = 0;

        // to store max Index encountred so far
        int index = -1;

        for (int j = 0; j < N; ++j)
        {
            if (S[j] == ch)
                count++;
            if (count == K)
                index = j;
        }
        answer.add(new pair(ch, index ));
    }

    int flag = 0;

    // printing required result
    for (int i = 0; i < (int)answer.size(); ++i)
    {
        if (answer.get(i).second > -1)
        {
            flag = 1;
            System.out.print(answer.get(i).first + " " +
                             answer.get(i).second + "\n");
        }
    }

    // If no such character exists, print -1
    if (flag == 0)
        System.out.print("-1" + "\n");
}

// Driver code
public static void main(String[] args)
{
    String S = "cbaabaacbcd";
    int K = 2;
    int N = S.length();
    maxSubString(S.toCharArray(), K, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to find largest index for each
# distinct character occuring exactly K times.
def maxSubstring(S, K, N):

    # Finding all characters present in S
    freq = [0 for i in range(26)]

    # Finding all distinct characters in S
    for i in range(N):
        freq[ord(S[i]) - 97] = 1

    # To store result for each character
    answer = []

    # Loop through each lower
    # case English character
    for i in range(26):

        # If current character is absent in s
        if (freq[i] == 0):
            continue

        # Getting current character
        ch = chr(i + 97)

        # Finding count of character ch in S
        count = 0

        # To store max Index encountred so far
        index = -1

        for j in range(N):
            if (S[j] == ch):
                count += 1

            if (count == K):
                index = j

        answer.append([ch, index])

    flag = 0

    # Printing required result
    for i in range(len(answer)):
        if (answer[i][1] > -1):
            flag = 1
            print(answer[i][0],
                  answer[i][1])

    # If no such character exists,
    # print -1
    if (flag == 0):
        print("-1")

# Driver code
if __name__ == '__main__':

    S = "cbaabaacbcd"
    K = 2
    N = len(S)

    maxSubstring(S, K, N)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

class pair
{    
    public char first;
    public int second;

    public pair(char first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find largest
// index for each distinct
// character occuring exactly K times.
static void maxSubString(char [] S,
                         int K, int N)
{

    // Finding all characters present in S
    int []freq = new int[26];

    // Finding all distinct characters in S
    for(int i = 0; i < N; ++i)
    {
        freq[S[i] - 'a'] = 1;
    }

    // To store result for each character
    List<pair> answer = new List<pair>();

    // Loop through each lower case
    // English character
    for(int i = 0; i < 26; ++i)
    {

        // If current character is absent in s
        if (freq[i] == 0)
            continue;

        // Getting current character
        char ch = (char)(i + 97);

        // Finding count of character ch in S
        int count = 0;

        // To store max Index encountred so far
        int index = -1;

        for(int j = 0; j < N; ++j)
        {
            if (S[j] == ch)
                count++;
            if (count == K)
                index = j;
        }
        answer.Add(new pair(ch, index));
    }

    int flag = 0;

    // Printing required result
    for(int i = 0; i < (int)answer.Count; ++i)
    {
        if (answer[i].second > -1)
        {
            flag = 1;
            Console.Write(answer[i].first + " " +
                          answer[i].second + "\n");
        }
    }

    // If no such character exists, print -1
    if (flag == 0)
        Console.Write("-1" + "\n");
}

// Driver code
public static void Main(String[] args)
{
    String S = "cbaabaacbcd";
    int K = 2;
    int N = S.Length;

    maxSubString(S.ToCharArray(), K, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to find largest
      // index for each distinct
      // character occuring exactly K times.
      function maxSubString(S, K, N) {
        // Finding all characters present in S
        var freq = new Array(26).fill(0);

        // Finding all distinct characters in S
        for (var i = 0; i < N; ++i) {
          freq[S[i].charCodeAt(0) - "a".charCodeAt(0)] = 1;
        }

        // To store result for each character
        var answer = [];

        // Loop through each lower case
        // English character
        for (var i = 0; i < 26; ++i) {
          // If current character is absent in s
          if (freq[i] === 0)
              continue;

          // Getting current character
          var ch = String.fromCharCode(i + 97);

          // Finding count of character ch in S
          var count = 0;

          // To store max Index encountred so far
          var index = -1;

          for (var j = 0; j < N; ++j) {
            if (S[j] === ch) count++;
            if (count === K) index = j;
          }
          answer.push([ch, index]);
        }

        var flag = 0;

        // Printing required result
        for (var i = 0; i < answer.length; ++i) {
          if (answer[i][1] > -1) {
            flag = 1;
            document.write(answer[i][0] + " " + answer[i][1] + "<br>");
          }
        }

        // If no such character exists, print -1
        if (flag === 0)
            document.write("-1" + "<br>");
      }

      // Driver code
      var S = "cbaabaacbcd";
      var K = 2;
      var N = S.length;

      maxSubString(S.split(""), K, N);
</script>
```

**Output:** 

```
a 4
b 7
c 8
```

***时间复杂度:** O(26 * N)*