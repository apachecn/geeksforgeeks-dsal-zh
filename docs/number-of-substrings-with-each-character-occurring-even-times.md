# 每个字符出现偶数次的子串数量

> 原文:[https://www . geeksforgeeks . org/每个字符出现偶数次的子字符串数量/](https://www.geeksforgeeks.org/number-of-substrings-with-each-character-occurring-even-times/)

给定一个由小写字母 **N** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是计算每个字符出现频率为偶数的子字符串的数量。

**示例:**

> **输入:**S = " ABBA "
> T3】输出: 4
> **解释:**
> 每个字符出现频率为偶数的子串为{“ABBA”、“aa”、“bb”、“bbaa”}。
> 因此，计数为 4。
> 
> **输入:** S =【极客暴走族】
> T3】输出: 2

**天真方法:**解决给定问题的最简单方法是[生成给定字符串的所有可能的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) ，并对每个字符具有偶数频率的子串进行计数。检查所有子字符串后，打印获得的总计数。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
public class GFG
{

    // Function to count substrings having
    // even frequency of each character
    static int subString(String s, int n)
    {

        // Stores the total
        // count of substrings
        int count = 0;

        // Traverse the range [0, N]:
        for (int i = 0; i < n; i++) {

            // Traverse the range [i + 1, N]
            for (int len = i + 1; len <= n; len++) {

                // Stores the substring over
                // the range of indices [i, len]
                String test_str = s.substring(i, len);

                // Stores the frequency of characters
                HashMap<Character, Integer> res
                    = new HashMap<>();

                // Count frequency of each character
                for (char keys : test_str.toCharArray()) {
                    res.put(keys,
                            res.getOrDefault(keys, 0) + 1);
                }

                int flag = 0;

                // Traverse the dictionary
                for (char keys : res.keySet()) {

                    // If any of the keys
                    // have odd count
                    if (res.get(keys) % 2 != 0) {

                        flag = 1;
                        break;
                    }
                }

                // Otherwise
                if (flag == 0)
                    count += 1;
            }
        }

        // Return count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "abbaa";
        int N = S.length();
        System.out.println(subString(S, N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count substrings having
# even frequency of each character
def subString(s, n):

    # Stores the total
    # count of substrings
    count = 0

    # Traverse the range [0, N]:
    for i in range(n):

        # Traverse the range [i + 1, N]
        for len in range(i + 1, n + 1):

            # Stores the substring over
            # the range of indices [i, len]
            test_str = (s[i: len])

            # Stores the frequency of characters
            res = {}

            # Count frequency of each character
            for keys in test_str:
                res[keys] = res.get(keys, 0) + 1

            flag = 0

            # Traverse the dictionary
            for keys in res:

                # If any of the keys
                # have odd count
                if res[keys] % 2 != 0:

                    flag = 1
                    break

            # Otherwise
            if flag == 0:
                count += 1

    # Return count
    return count

# Driver Code

S = "abbaa"
N = len(S)
print(subString(S, N))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

    // Function to count substrings having
    // even frequency of each character
    static int subString(string s, int n)
    {

        // Stores the total
        // count of substrings
        int count = 0;

        // Traverse the range [0, N]:
        for (int i = 0; i < n; i++) {

            // Traverse the range [i + 1, N]
            for (int len = i + 1; len <= n; len++) {

                // Stores the substring over
                // the range of indices [i, len]
                string test_str = s.Substring(i, len-i);

                // Stores the frequency of characters
                Dictionary<char,int> res
                    = new Dictionary<char,int>();

                // Count frequency of each character
                foreach (char keys in test_str.ToCharArray()) {

                    if(!res.ContainsKey(keys))
                        res.Add(keys,0);

                    res[keys]++;
                }

                int flag = 0;

                // Traverse the dictionary
                foreach (KeyValuePair<char,int> keys in res) {

                    // If any of the keys
                    // have odd count
                    if (keys.Value % 2 != 0) {

                        flag = 1;
                        break;
                    }
                }

                // Otherwise
                if (flag == 0)
                    count += 1;
            }
        }

        // Return count
        return count;
    }

    // Driver Code

    static public void Main (){

        string S = "abbaa";
        int N = S.Length;
        Console.WriteLine(subString(S, N));

    }
}

// This code is contributed by rag2127.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
// Function to count substrings having
// even frequency of each character
function subString(s, n)
{

    // Stores the total
    // count of substrings
    var count = 0;

    // Traverse the range [0, N]:
    for(var i = 0; i < n; i++)
    {

        // Traverse the range [i + 1, N]
        for(var len = i + 1; len <= n; len++)
        {

            // Stores the substring over
            // the range of indices [i, len]
            var test_str = s.substring(i, len);

            // Stores the frequency of characters
            var res = {};

            // Count frequency of each character

            var temp = test_str.split("");

            for(const keys of temp)
            {
                res[keys] = (res[keys] ? res[keys] : 0) + 1;
            }

            var flag = 0;

            // Traverse the dictionary
            for(const [key, value] of Object.entries(res))
            {

                // If any of the keys
                // have odd count
                if (res[key] % 2 != 0)
                {
                    flag = 1;
                    break;
                }
            }

            // Otherwise
            if (flag == 0) count += 1;
        }
    }

    // Return count
    return count;
}

// Driver Code
var S = "abbaa";
var N = S.length;

document.write(subString(S, N));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
4
```

**时间复杂度:***O(N<sup>2</sup>* 26)*
**辅助空间:** O(N)

**高效方法:**上述方法可以通过使用 [**位屏蔽**](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/) 和[**字典**](https://www.geeksforgeeks.org/python-dictionary/) 的概念进行优化。按照以下步骤解决问题:

*   初始化一个[字典](https://www.geeksforgeeks.org/python-dictionary/)，比如说**散列**来存储一个字符的计数。
*   初始化两个变量，比如说**计数**为 **0** 和**预**为 **0** 来存储每个字符计数为偶数的子串的总数，并存储子串中包含的字符掩码。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并执行以下步骤:
    *   翻转变量**前**中的**(S[I]–‘a’)<sup>第</sup>** 位。
    *   将**计数**增加**散列【预】**和**散列**中**预**的计数。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C ++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count substrings having
// even frequency of each character
int subString(string s, int n)
{

    // Stores the count of a character
    map<int, int> hash;
    hash[0] = 1;

    // Stores bitmask
    int pre = 0;

    // Stores the count of substrings
    // with even count of each character
    int count = 0;

    // Traverse the string S
    for (int i = 0; i < n; i++) {

        // Flip the ord(i)-97 bits in pre
        pre ^= (1 << int(s[i]) - 97);

        // Increment the count by hash[pre]
        count += hash[pre];

        // Increment count of pre in hash
        hash[pre] = hash[pre] + 1;
    }

    // Return the total count obtained
    return count;
}

// Driver Code
int main()
{
    string S = "abbaa";
    int N = S.length();
    cout << (subString(S, N));
}

// THIS CODE IS CONTRIBUTED BY UKASP.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to count substrings having
// even frequency of each character
static int subString(String s, int n)
{

    // Stores the count of a character
    Map<Integer, Integer> hash = new HashMap<>();
    hash.put(0, 1);

    // Stores bitmask
    int pre = 0;

    // Stores the count of substrings
    // with even count of each character
    int count = 0;

    // Traverse the string S
    for(int i = 0; i < n; i++)
    {

        // Flip the ord(i)-97 bits in pre
        pre ^= (1 << (int)(s.charAt(i) - 97));

        // Increment the count by hash[pre]
        count += hash.getOrDefault(pre, 0);

        // Increment count of pre in hash
        hash.put(pre, hash.getOrDefault(pre, 0) + 1);
    }

    // Return the total count obtained
    return count;
}

// Driver code
public static void main(String[] args)
{
    String S = "abbaa";
    int N = S.length();

    System.out.print(subString(S, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count substrings having
# even frequency of each character
def subString(s, n):

    # Stores the count of a character
    hash = {0: 1}

    # Stores bitmask
    pre = 0

    # Stores the count of substrings
    # with even count of each character
    count = 0

    # Traverse the string S
    for i in s:

        # Flip the ord(i)-97 bits in pre
        pre ^= (1 << ord(i) - 97)

        # Increment the count by hash[pre]
        count += hash.get(pre, 0)

        # Increment count of pre in hash
        hash[pre] = hash.get(pre, 0) + 1

    # Return the total count obtained
    return count

# Driver Code

S = "abbaa"
N = len(S)
print(subString(S, N))
```

## C#

```
// C# program for the above approach
using System.IO;
using System;
using System.Collections.Generic;

class GFG{

// Function to count substrings having
// even frequency of each character
static int subString(string s, int n)
{

    // Stores the count of a character
    Dictionary<int,
               int> hash = new Dictionary<int,
                                          int>();

    hash[0] = 1;

    // Stores bitmask
    int pre = 0;

    // Stores the count of substrings
    // with even count of each character
    int count = 0;

    // Traverse the string S
    for(int i = 0; i < n; i++)
    {

        // Flip the ord(i)-97 bits in pre
        pre ^= (1 << (int)(s[i]) - 97);

        // Increment the count by hash[pre]
        if (hash.ContainsKey(pre))
            count += hash[pre];
        else
            count += 0;

        // Increment count of pre in hash
        if (hash.ContainsKey(pre))
            hash[pre] = hash[pre] + 1;
        else
            hash.Add(pre, 1);
    }

    // Return the total count obtained
    return count;
}

// Driver code
static void Main()
{
    String S = "abbaa";
    int N = S.Length;

    Console.WriteLine(subString(S, N));
}
}

// This code is contributed by sk944795
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count substrings having
// even frequency of each character
function subString(s,n)
{
    // Stores the count of a character
    let hash = new Map();
    hash.set(0, 1);

    // Stores bitmask
    let pre = 0;

    // Stores the count of substrings
    // with even count of each character
    let count = 0;

    // Traverse the string S
    for(let i = 0; i < n; i++)
    {

        // Flip the ord(i)-97 bits in pre
        pre ^= (1 << s[i].charCodeAt(0) - 97);

        if(!hash.has(pre))
            hash.set(pre,0);

        // Increment the count by hash[pre]
        count += (hash.get(pre));

        // Increment count of pre in hash
        hash.set(pre, hash.get(pre)==null? 0 : hash.get(pre)+1);
    }

    // Return the total count obtained
    return count;
}

// Driver code
let S = "abbaa";
let N = S.length;

document.write(subString(S, N));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)