# 最大长度前缀，以使每个字符的频率最多为最小频率的字符数

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)

给定字符串 **S** ，任务是找到具有最大可能长度的字符串 **S** 的前缀，以使前缀中每个字符的频率最多为 S 中的字符数 以最小的频率。

**示例**：

> **输入**：S ='aabcdaab'
> **输出**：aabcd
> **说明**：
> 给定字符串中字符的频率–
> {a：4，b：2，c：1，d：1}
> 最小频率为 1，最小频率的计数为 2。
> 因此前缀中每个字符的频率最多为 2。
> 
> **输入**：S ='aaabc'
> **输出**：aa
> **说明**：
> 给定字符串中字符的频率–
> {a：3，b：1，c：1}。
> 最小频率为 1，最小频率计数为 2。
> 因此前缀中每个字符的频率最多为 2。

**方法**：

*   初始化[哈希图](https://www.geeksforgeeks.org/hashing-data-structure/)以存储字符的频率。

*   遍历字符串，并增加哈希图中字符的频率。

*   查找字符串中出现的最小字符，以及出现频率最小的此类字符的计数。

*   初始化另一个哈希图，以存储可能的前缀字符串的字符的频率。

*   最后，从头开始遍历字符串，并增加字符计数，直到任何字符的频率不大于最小频率的计数。

下面是上述方法的实现：

## Python3

```py

# Python3 implementation to find the

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)
# prefix of the string such that 

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)
# occurrence of each character is

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)
# atmost the count of minimum 

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)
# frequency in the string

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)

# Function to find the maximum

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)
# possible prefix of the string

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)
def MaxPrefix(string):

    # Hash map to store the frequency
    # of the characters in the string
    Dict = {}
    maxprefix = 0

    # Iterate over the string to find
    # the occurence of each Character
    for i in string:
        Dict[i] = Dict.get(i, 0) + 1

    # Minimum frequency of the Characters
    minfrequency = min(Dict.values())
    countminFrequency = 0

    # Loop to find the count of minimum
    # frequency in the hash-map
    for x in Dict:
        if (Dict[x] == minfrequency):
            countminFrequency += 1

    mapper = {}
    indi = 0

    # Loop to find the maximum possible 
    # length of the prefix in the string    
    for i in string:
        mapper[i] = mapper.get(i, 0) + 1

        # Condition to check if the frequency
        # is greater than minimum possible freq
        if (mapper[i] > countminFrequency):
            break
        indi += 1

    # maxprefix string and its length.
    print(string[:indi])

# Driver code 

> 原文：[https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/](https://www.geeksforgeeks.org/maximum-length-prefix-such-that-frequency-of-each-character-is-atmost-number-of-characters-with-minimum-frequency/)
if __name__ == '__main__': 

    # String is initialize.
    str = 'aabcdaab'
    # str is passed in MaxPrefix function.
    MaxPrefix(str)

```

## C#

```cs

// C# implementation to find the
// prefix of the s such that 
// occurrence of each character is
// atmost the count of minimum 
// frequency in the s
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to find the maximum
// possible prefix of the s
static void MaxPrefix(string s)
{    

    // Hash map to store the frequency
    // of the characters in the s
    Dictionary<char,
               int> Dict = new Dictionary<char,
                                          int>();

    // Iterate over the s to find
    // the occurence of each Character
    foreach(char i in s)
    {
        if (Dict.ContainsKey(i))
        {
            Dict[i]++;
        }
        else
        {
            Dict[i] = 1;
        }
    }

    int minfrequency = Int32.MaxValue;

    // Minimum frequency of the Characters
    foreach(int x in Dict.Values.ToList())
    {
        minfrequency = Math.Min(minfrequency, x);    
    }

    int countminFrequency = 0;

    // Loop to find the count of minimum
    // frequency in the hash-map
    foreach(char x in Dict.Keys.ToList())
    {
        if (Dict[x] == minfrequency)
            countminFrequency += 1;
    }

    Dictionary<char,
               int> mapper = new Dictionary<char,
                                            int>(); 
    int indi = 0;

    // Loop to find the maximum possible 
    // length of the prefix in the s
    foreach(char i in s)
    {
        if (mapper.ContainsKey(i))
        {
            mapper[i]++;
        }
        else
        {
            mapper[i] = 1;
        }

        // Condition to check if the frequency
        // is greater than minimum possible freq
        if (mapper[i] > countminFrequency)
            break;

        indi += 1;
    }

    // maxprefix s and its length.
    Console.Write(s.Substring(0, indi));
}

// Driver Code
public static void Main(string[] args)
{

    // s is initialize.
    string str = "aabcdaab";

    // str is passed in 
    // MaxPrefix function.
    MaxPrefix(str);
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
aabcd

```

**效果分析**：

*   **时间复杂度**：在上述方法中，有一个循环来查找字符串中每个字符的频率，在最坏的情况下需要 O（N）时间。 因此，该方法的时间复杂度将为 **O（N）**。

*   **空间复杂度**：在上述方法中，有多余的空间用于存储字符的频率。 因此，上述方法的空间复杂度将为 **O（N）**

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



