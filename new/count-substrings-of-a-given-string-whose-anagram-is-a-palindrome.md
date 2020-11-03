# 计算给定字符串（其异序词是回文）的子字符串

> 原文：[https://www.geeksforgeeks.org/count-substrings-of-a-given-string-whose-anagram-is-a-palindrome/](https://www.geeksforgeeks.org/count-substrings-of-a-given-string-whose-anagram-is-a-palindrome/)

给定长度为 **N** 的仅包含小写字母的字符串 **S** ，任务是打印给定的[字符串，其异序词是回文](https://www.geeksforgeeks.org/check-anagram-string-palindrome-not/)。

**示例**：

> **输入**：`S = "aaaa"`
>
> **输出**：10
>
> **说明**：
> 可能的子字符串为`{"a", "a", "a", "a", "aa", "aa", "aa", "aaa", "aaa", "aaaa"}`。 由于所有子字符串都具有回文字母，所以所需答案为 10。
> 
> **输入**：`S = "abc"`
>
> **输出**：3

**朴素的方法**：的想法是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有子字符串，并为每个子字符串检查其[异序词](http://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)是否是回文。 不断增加发现上述条件成立的子字符串的数量。 最后，打印所有这些子字符串的计数。

**时间复杂度**：`O(N ^ 3)`

**辅助空间**：`O(n)`

[**位掩码**](https://www.geeksforgeeks.org/bit-tricks-competitive-programming/) **方法**：想法是生成 **26 位**数字的掩码，因为 **26** 字符。 另外，请注意，如果某个字符串的异序词是回文，则其字符的频率必须最多为偶数。

[请按照以下步骤解决问题](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/)：

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，并在每个索引处初始化变量`X = 0`。

*   从每个索引`i`，在索引范围`[i， N – 1]`上遍历字符串，并对每个字符`S[j]`，计算`X`和`2 ^ (S[j] – 'a')`的[按位异或](http://www.geeksforgeeks.org/calculate-xor-1-n/)，其中第 0 位表示`a`的频率是否为奇数， 第 1 位表示`b`的频率是否奇数，依此类推。

*   然后，检查`X & (X - 1)`是否等于 **0**。 如果发现是真的，则将**计数**递增 **1**。

> **解释**：假设`X = 0b0001000`，`X – 1`将表示为`0b0000111`。因此，`X & (X - 1) = 0`

*   完成上述步骤后，请打印获得的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print count of substrings
// whose anagrams are palindromic
void countSubstring(string s)
{
    // Stores the answer
    int res = 0;

    // Iterate over the string
    for (int i = 0;
         i < s.length(); i++) {

        int x = 0;

        for (int j = i;
             j < s.length(); j++) {

            // Set the current character
            int temp = 1 << s[j] - 'a';

            // Parity update
            x ^= temp;
            if ((x & (x - 1)) == 0)
                res++;
        }
    }

    // Print the final count
    cout << res;
}

// Driver Code
int main()
{
    string str = "aaa";

    // Function Call
    countSubstring(str);

    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
class GFG{

// Function to print count of subStrings
// whose anagrams are palindromic
static void countSubString(String s)
{
  // Stores the answer
  int res = 0;

  // Iterate over the String
  for (int i = 0; i < s.length(); i++) 
  {
    int x = 0;
    for (int j = i; j < s.length(); j++) 
    {
      // Set the current character
      int temp = 1 << s.charAt(j) - 'a';

      // Parity update
      x ^= temp;
      if ((x & (x - 1)) == 0)
        res++;
    }
  }

  // Print the final count
  System.out.print(res);
}

// Driver Code
public static void main(String[] args)
{
  String str = "aaa";

  // Function Call
  countSubString(str);
}
}

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program for
# the above approach

# Function to prcount of subStrings
# whose anagrams are palindromic
def countSubString(s):

    # Stores the answer
    res = 0;

    # Iterate over the String
    for i in range(len(s)):
        x = 0;
        for j in range(i, len(s)):

            # Set the current character
            temp = 1 << ord(s[j]) - ord('a');

            # Parity update
            x ^= temp;
            if ((x & (x - 1)) == 0):
                res += 1;

    # Print final count
    print(res);

# Driver Code
if __name__ == '__main__':
    str = "aaa";

    # Function Call
    countSubString(str);

# This code is contributed by 29AjayKumar

```

## C#

```cs

// C# program for 
// the above approach
using System;
class GFG{

// Function to print count of subStrings
// whose anagrams are palindromic
static void countSubString(String s)
{
  // Stores the answer
  int res = 0;

  // Iterate over the String
  for (int i = 0; i < s.Length; i++) 
  {
    int x = 0;

    for (int j = i; j < s.Length; j++) 
    {
      // Set the current character
      int temp = 1 << s[j] - 'a';

      // Parity update
      x ^= temp;
      if ((x & (x - 1)) == 0)
        res++;
    }
  }

  // Print the readonly count
  Console.Write(res);
}

// Driver Code
public static void Main(String[] args)
{
  String str = "aaa";

  // Function Call
  countSubString(str);
}
}

// This code is contributed by shikhasingrajput

```

**Output**

```
6
```

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`

**高效方法**：为了优化上述[位掩码技术](https://www.geeksforgeeks.org/bit-tricks-competitive-programming/)，其想法是使用[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。 请按照以下步骤解决问题：

1.  初始化映射以存储模板的频率。 初始化变量`X = 0`。

2.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，对于第`i`个索引，计算`X`和`2 ^ (S[j] – 'a')`的[按位异或](http://www.geeksforgeeks.org/calculate-xor-1-n/)并通过添加`X`映射中的当前值的频率来更新**答案**，因为如果 0 至`j`中的任何子字符串具有与`X`相同的掩码，这是 **0** 至`i`的子串的掩码， 那么子字符串`S[j + 1, i]`将具有偶数频率，其中`j < i`。

3.  还要加上掩码`X xor 2 ^ k`的频率，其中`0 ≤ k < 26`。 之后，将`X`的频率增加 **1** 的频率。

4.  对给定字符串的每个索引重复上述步骤。

5.  遍历给定的字符串后，打印所需的**答案**。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the count of substrings
// whose anagrams are palindromic
void countSubstring(string s)
{
    // Store the answer
    int answer = 0;

    // Map to store the freq of masks
    unordered_map<int, int> m;

    // Set frequency for mask
    // 00...00 to 1
    m[0] = 1;

    // Store mask in x from 0 to i
    int x = 0;
    for (int j = 0; j < s.length(); j++) {
        x ^= 1 << (s[j] - 'a');

        // Update answer
        answer += m[x];
        for (int i = 0; i < 26; ++i) {
            answer += m[x ^ (1 << i)];
        }

        // Update frequency
        m[x] += 1;
    }

    // Print the answer
    cout << answer;
}

// Driver Code
int main()
{
    string str = "abab";

    // Function Call
    countSubstring(str);
    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
import java.util.*;
class GFG {

// Function to get the count of subStrings
// whose anagrams are palindromic
static void countSubString(String s) 
{
  // Store the answer
  int answer = 0;

  // Map to store the freq of masks
  HashMap<Integer, 
          Integer> m = new HashMap<Integer, 
                                   Integer>();

  // Set frequency for mask
  // 00...00 to 1
  m.put(0, 1);

  // Store mask in x from 0 to i
  int x = 0;
  for (int j = 0; j < s.length(); j++) 
  {
    x ^= 1 << (s.charAt(j) - 'a');

    // Update answer
    answer += m.containsKey(x) ? m.get(x) : 0;
    for (int i = 0; i < 26; ++i) 
    {
      answer += m.containsKey(x ^ (1 << i)) ?
                m.get(x ^ (1 << i)) : 0;
    }

    // Update frequency
    if (m.containsKey(x))
      m.put(x, m.get(x) + 1);
    else
      m.put(x, 1);
  }

  // Print the answer
  System.out.print(answer);
}

// Driver Code
public static void main(String[] args) 
{
  String str = "abab";

  // Function Call
  countSubString(str);
}
}

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program for the above approach 
from collections import defaultdict

# Function to get the count of substrings
# whose anagrams are palindromic
def countSubstring(s):

    # Store the answer
    answer = 0

    # Map to store the freq of masks
    m = defaultdict(lambda : 0)

    # Set frequency for mask
    # 00...00 to 1
    m[0] = 1

    # Store mask in x from 0 to i
    x = 0

    for j in range(len(s)):
        x ^= 1 << (ord(s[j]) - ord('a'))

        # Update answer
        answer += m[x]
        for i in range(26):
            answer += m[x ^ (1 << i)]

        # Update frequency
        m[x] += 1

    # Print the answer 
    print(answer)

# Driver Code
str = "abab"

# Function call
countSubstring(str)

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# program for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to get the count of 
// subStrings whose anagrams 
// are palindromic
static void countSubString(String s) 
{
  // Store the answer
  int answer = 0;

  // Map to store the freq of masks
  Dictionary<int, 
             int> m = new Dictionary<int, 
                                     int>();

  // Set frequency for mask
  // 00...00 to 1
  m.Add(0, 1);

  // Store mask in x from 0 to i
  int x = 0;
  for (int j = 0; j < s.Length; j++) 
  {
    x ^= 1 << (s[j] - 'a');

    // Update answer
    answer += m.ContainsKey(x) ? m[x] : 0;
    for (int i = 0; i < 26; ++i) 
    {
      answer += m.ContainsKey(x ^ (1 << i)) ?
                m[x ^ (1 << i)] : 0;
    }

    // Update frequency
    if (m.ContainsKey(x))
      m[x] = m[x] + 1;
    else
      m.Add(x, 1);
  }

  // Print the answer
  Console.Write(answer);
}

// Driver Code
public static void Main(String[] args) 
{
  String str = "abab";

  // Function Call
  countSubString(str);
}
}

// This code is contributed by shikhasingrajput

```

**Output**

```
7
```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



