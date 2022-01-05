# 一个字符串中的字符在另一个字符串中出现的频率之和

> 原文:[https://www . geeksforgeeks . org/字符串出现在另一个字符串中的字符频率总和/](https://www.geeksforgeeks.org/sum-of-frequencies-of-characters-of-a-string-present-in-another-string/)

给定两个长度分别为 **M** 和 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S1** 和 **S2** ，任务是计算字符串**S1** 的字符在字符串 **S2** 中的[频率之和。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)

**示例:**

> **输入:**S1 =“pPKf”，S2 =“KKKttsdppfP”
> T3】输出: 7
> **说明:**
> 字符‘p’在字符串 S2 中出现两次。
> 字符“P”在字符串 S2 中出现一次。
> 字符“K”在字符串 S2 中出现三次。
> 字符“f”在字符串 S2 中出现一次。
> 因此，字符串 S1 的字符在字符串 S2 中总共出现 7 次。
> 
> **输入:** S1 =【极客 FOR】，S2 =【极客 forgeeks】
> T3】输出: 7

**天真方法:**最简单的方法是[迭代字符串的每个字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S1** ，计算其在字符串中的出现频率 **S2** 。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用[哈希](https://www.geeksforgeeks.org/hashing-set-1-introduction/)进行优化。按照以下步骤解决问题:

*   初始化一个整数**计数**来存储所需的总和。
*   [将字符串 **S1** 的所有字符插入一个集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)中，比如 **bset** 。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S2】**的字符，检查当前字符是否存在于集合中，**设置**。如果发现为真，则增加**计数**1。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find sum of frequencies
// of characters of S1 present in S2
void countTotalFrequencies(string S1, string S2)
{

  // Insert all characters of
  // string S1 in the set
  set<char> bset;
  for(auto x:S1)
    bset.insert(x);
  int count = 0;

  // Traverse the string S2
  for (auto x: S2)
  {

    // Check if X is present
    // in bset or not
    if (bset.find(x) != bset.end())

      // Increment count by 1
      count += 1;
  }

  // Finally, print the count
  cout << count << endl;

}

// Driver Code
int main()
{

  // Given strings
  string S1 = "geEksFOR";
  string S2 = "GeEksforgeEKS";

  countTotalFrequencies(S1, S2);

}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashSet;

class GFG{

// Function to find sum of frequencies
// of characters of S1 present in S2
static void countTotalFrequencies(String S1, String S2)
{

    // Insert all characters of
    // string S1 in the set
    HashSet<Character> bset = new HashSet<Character>();
    char[] S1arr = S1.toCharArray();
    char[] S2arr = S2.toCharArray();

    for(char x : S1arr)
        bset.add(x);

    int count = 0;

    // Traverse the string S2
    for(char x : S2arr)
    {

        // Check if X is present
        // in bset or not
        if (bset.contains(x))

            // Increment count by 1
            count += 1;
    }

    // Finally, print the count
    System.out.print(count);
}

// Driver code
public static void main(String[] args)
{

    // Given strings
    String S1 = "geEksFOR";
    String S2 = "GeEksforgeEKS";

    countTotalFrequencies(S1, S2);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find sum of frequencies
# of characters of S1 present in S2
def countTotalFrequencies(S1, S2):

    # Insert all characters of
    # string S1 in the set
    bset = set(S1)
    count = 0

    # Traverse the string S2
    for x in S2:

        # Check if X is present
        # in bset or not
        if x in bset:

            # Increment count by 1
            count += 1

    # Finally, print the count
    print(count)

# Driver Code

# Given strings
S1 = "geEksFOR"
S2 = "GeEksforgeEKS"

countTotalFrequencies(S1, S2)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

// Function to find sum of frequencies
// of characters of S1 present in S2
static void countTotalFrequencies(string S1,
                                  string S2)
{

    // Insert all characters of
    // string S1 in the set
    HashSet<char> bset = new HashSet<char>();

    foreach(char x in S1)
        bset.Add(x);

    int count = 0;

    // Traverse the string S2
    foreach(char x in S2)
    {

        // Check if X is present
        // in bset or not
        if (bset.Contains(x))

            // Increment count by 1
            count += 1;
    }

    // Finally, print the count
    Console.Write(count);
}

// Driver code
static void Main()
{

    // Given strings
    string S1 = "geEksFOR";
    string S2 = "GeEksforgeEKS";

    countTotalFrequencies(S1, S2);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find sum of frequencies
// of characters of S1 present in S2
function countTotalFrequencies(S1, S2)
{

    // Insert all characters of
    // string S1 in the set
    var bset = new Set();
    for(var i = 0; i < S1.length; i++)
    {
        bset.add(S1[i]);
    }

    var count = 0;

    // Traverse the string S2
    for(var i = 0; i < S2.length; i++)
    {

        // Check if X is present
        // in bset or not
        if (bset.has(S2[i]))

            // Increment count by 1
            count += 1;
    }

    // Finally, print the count
    document.write(count);
}

// Driver Code

// Given strings
var S1 = "geEksFOR";
var S2 = "GeEksforgeEKS";

countTotalFrequencies(S1, S2);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)