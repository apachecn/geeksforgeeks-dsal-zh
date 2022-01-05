# 第一个字符串中最常见的单词，但第二个字符串中不存在

> 原文:[https://www . geeksforgeeks . org/最常出现的第一字符串中的单词第二字符串中不存在的单词/](https://www.geeksforgeeks.org/most-frequent-word-in-first-string-which-is-not-present-in-second-string/)

给定两个字符串“S1”和“S2”，任务是从“S1”返回“S2”中不存在的最频繁(使用次数最多)的单词。如果可能有一个以上的单词，那么按字典顺序打印其中最小的一个。
**例:**

> **输入:** S1 =“极客对于极客来说是最好学习的地方”，S2 =“不好的地方”
> **输出:**极客
> “极客”是 S1 出现频率最高的词，在 S2 也不存在。
> 极客的频率为 2
> **输入:** S1 =“快棕狐跳过懒狗”，S2 =“棕狐跳过”
> **输出:**狗
> 所有单词都有频率 1。
> 字典上最小的单词是“狗”

**方法:**思考过程必须从创建一个映射来存储键值对(string，int)开始。接下来开始从第一个字符串中提取单词，同时更新映射和计数。对于第一个数组中出现的第二个数组中的每个字，重置计数。最后，遍历地图，找到出现频率最高的词，得到字典最小的词。
**算法:**

1.  遍历字符串 S2，创建一个地图，并将其中的所有单词插入到地图中。
2.  遍历字符串 S1，检查该单词是否出现在上一步创建的地图中。
3.  如果这个单词满足条件，那么更新答案，如果同一个单词的出现频率到目前为止是最大的。
4.  如果单词的出现频率等于先前选择的单词，那么根据两个字符串中字典序最小的一个更新答案。

以下是上述方法的实现:

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return frequent
// word from S1 that isn't
// present in S2
string smallestFreq(string S1, string S2)
{

    map<string, int> banned;

    // create map of banned words
    for (int i = 0; i < S2.length(); ++i) {

        string s = "";
        while (i < S2.length() && S2[i] != ' ')
            s += S2[i++];

        banned[s]++;
    }

    map<string, int> result;
    string ans;
    int freq = 0;

    // find smallest and most frequent word
    for (int i = 0; i < S1.length(); ++i) {

        string s = "";
        while (i < S1.length() && S1[i] != ' ')
            s += S1[i++];

        // check if word is not banned
        if (banned[s] == 0) {
            result[s]++;
            if (result[s] > freq
                || (result[s] == freq && s < ans)) {
                ans = s;
                freq = result[s];
            }
        }
    }

    // return answer
    return ans;
}

// Driver program
int main()
{
    string S1 = "geeks for geeks is best place to learn";
    string S2 = "bad place";

    cout << smallestFreq(S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.HashMap;

class GFG
{

    // Function to return frequent
    // word from S1 that isn't
    // present in S2
    static String smallestFreq(String S1,
                               String S2)
    {
        HashMap<String,
                Integer> banned = new HashMap<>();

        // create map of banned words
        for (int i = 0; i < S2.length(); i++)
        {
            String s = "";
            while (i < S2.length() &&
                       S2.charAt(i) != ' ')
                s += S2.charAt(i++);

            banned.put(s, banned.get(s) == null ?
                      1 : banned.get(s) + 1);
        }

        HashMap<String,
                Integer> result = new HashMap<>();
        String ans = "";
        int freq = 0;

        // find smallest and most frequent word
        for (int i = 0; i < S1.length(); i++)
        {
            String s = "";
            while (i < S1.length() &&
                       S1.charAt(i) != ' ')
                s += S1.charAt(i++);

            // check if word is not banned
            if (banned.get(s) == null)
            {
                result.put(s, result.get(s) == null ? 1 :
                              result.get(s) + 1);
                if (result.get(s) > freq ||
                   (result.get(s) == freq &&
                    s.compareTo(ans) < 0))
                {
                    ans = s;
                    freq = result.get(s);
                }
            }
        }

        // return answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S1 = "geeks for geeks is best place to learn";
        String S2 = "bad place";
        System.out.println(smallestFreq(S1, S2));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of above approach
from collections import defaultdict

# Function to return frequent
# word from S1 that isn't
# present in S2
def smallestFreq(S1, S2):

    banned = defaultdict(lambda:0)

    i = 0

    # create map of banned words
    while i < len(S2):

        s = ""
        while i < len(S2) and S2[i] != ' ':
            s += S2[i]
            i += 1

        i += 1
        banned[s] += 1

    result = defaultdict(lambda:0)
    ans = ""
    freq = 0
    i = 0

    # find smallest and most frequent word
    while i < len(S1):

        s = ""
        while i < len(S1) and S1[i] != ' ':
            s += S1[i]
            i += 1

        i += 1

        # check if word is not banned
        if banned[s] == 0:
            result[s] += 1

            if (result[s] > freq or
               (result[s] == freq and s < ans)):
                ans = s
                freq = result[s]

    # return answer
    return ans

# Driver Code
if __name__ == "__main__":

    S1 = "geeks for geeks is best place to learn"
    S2 = "bad place"

    print(smallestFreq(S1, S2))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return frequent
    // word from S1 that isn't
    // present in S2
    static String smallestFreq(String S1,
                               String S2)
    {
        Dictionary<String,
                   int> banned = new Dictionary<String,
                                                int>();

        // create map of banned words
        for (int i = 0; i < S2.Length; i++)
        {
            String s = "";
            while (i < S2.Length &&
                    S2[i] != ' ')
                s += S2[i++];

            if(banned.ContainsKey(s))
            {
                var val = banned[s];
                banned.Remove(s);
                banned.Add(s, val + 1);
            }
            else
            {
                banned.Add(s, 1);
            }
        }

        Dictionary<String,
                   int> result = new Dictionary<String,
                                                int>();
        String ans = "";
        int freq = 0;

        // find smallest and most frequent word
        for (int i = 0; i < S1.Length; i++)
        {
            String s = "";
            while (i < S1.Length &&
                    S1[i] != ' ')
                s += S1[i++];

            // check if word is not banned
            if (!banned.ContainsKey(s))
            {
                if(result.ContainsKey(s))
                {
                    var val = result[s];
                    result.Remove(s);
                    result.Add(s, val + 1);
                }
                else
                {
                    result.Add(s, 1);
                }
                if (result[s] > freq ||
                   (result[s] == freq &&
                    s.CompareTo(ans) < 0))
                {
                    ans = s;
                    freq = result[s];
                }
            }
        }

        // return answer
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String S1 = "geeks for geeks is best place to learn";
        String S2 = "bad place";
        Console.WriteLine(smallestFreq(S1, S2));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

 // Function to return frequent
    // word from S1 that isn't
    // present in S2
function smallestFreq(S1,S2)
{
    let banned = new Map();

        // create map of banned words
        for (let i = 0; i < S2.length; i++)
        {
            let s = "";
            while (i < S2.length &&
                       S2[i] != ' ')
                s += S2[i++];

            banned.set(s, banned[s] == null ?
                      1 : banned.get(s) + 1);
        }

        let result = new Map();
        let ans = "";
        let freq = 0;

        // find smallest and most frequent word
        for (let i = 0; i < S1.length; i++)
        {
            let s = "";
            while (i < S1.length &&
                       S1[i] != ' ')
                s += S1[i++];

            // check if word is not banned
            if (banned.get(s) == null)
            {
                result.set(s, result.get(s) == null ? 1 :
                              result.get(s) + 1);
                if (result.get(s) > freq ||
                   (result.get(s) == freq &&
                    s < (ans) ))
                {
                    ans = s;
                    freq = result.get(s);
                }
            }
        }

        // return answer
        return ans;
}

// Driver Code
let S1 = "geeks for geeks is best place to learn";
let S2 = "bad place";
document.write(smallestFreq(S1, S2));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
geeks
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为字符串的长度。
    需要对字符串进行一次遍历。
*   **空间复杂度:** O(n)。
    一个字符串最多可以有 n 个单词。映射需要 O(n)个空间来存储字符串。