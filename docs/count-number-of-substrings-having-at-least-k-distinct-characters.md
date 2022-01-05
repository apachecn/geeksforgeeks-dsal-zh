# 统计至少有 K 个不同字符的子串数量

> 原文:[https://www . geesforgeks . org/count-number-of-substrings-至少有-k 个不同的字符/](https://www.geeksforgeeks.org/count-number-of-substrings-having-at-least-k-distinct-characters/)

给定一个由 **N** 个字符和一个正整数 **K** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是统计至少有 **K** 个不同字符的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量。

**示例:**

> **输入:** S = "abcca "，K = 3
> **输出:** 4
> **解释:**
> 至少包含 K(= 3)个不同字符的子串有:
> 
> 1.  **“ABC”:**不同字符数= 3。
> 2.  **“abcc”:**不同字符数= 3。
> 3.  **“abcca”:**不同字符数= 3。
> 4.  **“bcca”:**不同字符数= 3。
> 
> 因此，子字符串的总数是 4。
> 
> **输入:** S = "abcca "，K = 4
> T3】输出: 0

**天真方法:**解决给定问题最简单的方法是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有子串，并对那些[中至少有 **K** 个不同字符](https://www.geeksforgeeks.org/print-all-distinct-characters-of-a-string-in-order-3-methods/)的子串进行计数。检查所有子字符串后，打印获得的总计数作为结果。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(256)*

**高效方法:**上述方法也可以使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)和[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)的概念进行优化。按照以下步骤解决问题:

*   初始化一个变量，比如说 **ans** 为 **0** 来存储至少有 **K** 个不同字符的子串的计数。
*   初始化两个指针，**开始****结束**存储滑动窗口的起点和终点。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-pairs-in-c/) ，说 **M** 来存储窗口中字符的出现频率。
*   [迭代直到**结束**小于**N**T5】，执行以下步骤:](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)
    *   通过将 **M** 中 **S【结束】**的值增加 **1** 来包括窗口末尾的字符。
    *   [迭代直到 **M** 的大小变得小于**K**T5】，执行以下步骤:](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)
        *   通过将 **M** 中 **S【开始】**的值减 **1** 来删除窗口开始处的字符。
        *   如果其频率变为 **0** ，则[将其从地图](https://www.geeksforgeeks.org/map-erase-function-in-c-stl/) **M** 中删除。
        *   通过将**和**递增**(N–end+1)**，计算从**开始到 **N** 的所有子字符串。**
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of substrings
// having atleast k distinct characters
void atleastkDistinctChars(string s, int k)
{
    // Stores the size of the string
    int n = s.size();

    // Initialize a HashMap
    unordered_map<char, int> mp;

    // Stores the start and end
    // indices of sliding window
    int begin = 0, end = 0;

    // Stores the required result
    int ans = 0;

    // Iterate while the end
    // pointer is less than n
    while (end < n) {

        // Include the character at
        // the end of the window
        char c = s[end];
        mp++;

        // Increment end pointer by 1
        end++;

        // Iterate until count of distinct
        // characters becomes less than K
        while (mp.size() >= k) {

            // Remove the character from
            // the beginning of window
            char pre = s[begin];
            mp[pre]--;

            // If its frequency is 0,
            // remove it from the map
            if (mp[pre] == 0) {
                mp.erase(pre);
            }

            // Update the answer
            ans += s.length() - end + 1;
            begin++;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    string S = "abcca";
    int K = 3;
    atleastkDistinctChars(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count number of substrings
// having atleast k distinct characters
static void atleastkDistinctChars(String s, int k)
{

    // Stores the size of the string
    int n = s.length();

    // Initialize a HashMap
    Map<Character, Integer> mp = new HashMap<>();

    // Stores the start and end
    // indices of sliding window
    int begin = 0, end = 0;

    // Stores the required result
    int ans = 0;

    // Iterate while the end
    // pointer is less than n
    while (end < n) {

        // Include the character at
        // the end of the window
        char c = s.charAt(end);
        mp.put(c,mp.getOrDefault(c,0)+1);

        // Increment end pointer by 1
        end++;

        // Iterate until count of distinct
        // characters becomes less than K
        while (mp.size() >= k) {

            // Remove the character from
            // the beginning of window
            char pre = s.charAt(begin);
            mp.put(pre,mp.getOrDefault(pre,0)-1);

            // If its frequency is 0,
            // remove it from the map
            if (mp.get(pre)==0){
                mp.remove(pre);
            }

            // Update the answer
            ans += s.length() - end + 1;
            begin++;
        }
    }

    // Print the result
    System.out.println(ans);
}

  // Driver code
public static void main (String[] args) 
{

      // Given inputs
    String S = "abcca";
    int K = 3;
    atleastkDistinctChars(S, K);

    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from collections import defaultdict

# Function to count number of substrings
# having atleast k distinct characters
def atleastkDistinctChars(s, k):

    # Stores the size of the string
    n = len(s)

    # Initialize a HashMap
    mp = defaultdict(int)

    # Stores the start and end
    # indices of sliding window
    begin = 0
    end = 0

    # Stores the required result
    ans = 0

    # Iterate while the end
    # pointer is less than n
    while (end < n):

        # Include the character at
        # the end of the window
        c = s[end]
        mp += 1

        # Increment end pointer by 1
        end += 1

        # Iterate until count of distinct
        # characters becomes less than K
        while (len(mp) >= k):

            # Remove the character from
            # the beginning of window
            pre = s[begin]
            mp[pre] -= 1

            # If its frequency is 0,
            # remove it from the map
            if (mp[pre] == 0):
                del mp[pre]

            # Update the answer
            ans += len(s) - end + 1
            begin += 1

    # Print the result
    print(ans)

# Driver Code
if __name__ == "__main__":

    S = "abcca"
    K = 3
    atleastkDistinctChars(S, K)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count number of substrings
// having atleast k distinct characters
static void atleastkDistinctChars(string s, int k)
{

    // Stores the size of the string
    int n = s.Length;

    // Initialize a HashMap
    Dictionary<char,
               int> mp = new Dictionary<char,
                                        int>();

    // Stores the start and end
    // indices of sliding window
    int begin = 0, end = 0;

    // Stores the required result
    int ans = 0;

    // Iterate while the end
    // pointer is less than n
    while (end < n) 
    {

        // Include the character at
        // the end of the window
        char c = s[end];
        if (mp.ContainsKey(c))
            mp++;
        else
            mp.Add(c, 1);

        // Increment end pointer by 1
        end++;

        // Iterate until count of distinct
        // characters becomes less than K
        while (mp.Count >= k)
        {

            // Remove the character from
            // the beginning of window
            char pre = s[begin];
            mp[pre]--;

            // If its frequency is 0,
            // remove it from the map
            if (mp[pre] == 0) 
            {
                mp.Remove(pre);
            }

            // Update the answer
            ans += s.Length - end + 1;
            begin++;
        }
    }

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    string S = "abcca";
    int K = 3;

    atleastkDistinctChars(S, K);
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    // Function to count number of substrings
// having atleast k distinct characters
    function atleastkDistinctChars(s,k)
    {
        // Stores the size of the string
    let n = s.length;

    // Initialize a HashMap
    let mp = new Map();

    // Stores the start and end
    // indices of sliding window
    let begin = 0, end = 0;

    // Stores the required result
    let ans = 0;

    // Iterate while the end
    // pointer is less than n
    while (end < n)
    {

        // Include the character at
        // the end of the window
        let c = s[end];
        if (mp.has(c))
            mp.set(c,mp.get(c)+1);
        else
            mp.set(c, 1);

        // Increment end pointer by 1
        end++;

        // Iterate until count of distinct
        // characters becomes less than K
        while (mp.size >= k)
        {

            // Remove the character from
            // the beginning of window
            let pre = s[begin];
            mp.set(pre,mp.get(pre)-1);

            // If its frequency is 0,
            // remove it from the map
            if (mp.get(pre) == 0)
            {
                mp.delete(pre);
            }

            // Update the answer
            ans += s.length - end + 1;
            begin++;
        }
    }

    // Print the result
    document.write(ans);
    }

    // Driver Code
    let S = "abcca";
    let K = 3;
    atleastkDistinctChars(S, K);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(256)