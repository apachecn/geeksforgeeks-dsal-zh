# 从字符串中删除偶数频率字符

> 原文:[https://www . geesforgeks . org/从字符串中删除偶数频率字符/](https://www.geeksforgeeks.org/remove-even-frequency-characters-from-the-string/)

给定一个字符串“str”，任务是从该字符串中删除所有具有偶数频率的字符。

**示例:**

```
Input: str = "aabbbddeeecc"
Output: bbbeee
The characters a, d, c have even frequencies
So, they are removed from the string.

Input: str = "zzzxxweeerr"
Output: zzzweee
```

**进场:**

*   创建一个映射并将字符串中每个字符的频率存储到同一个映射中。
*   然后，遍历字符串，并在地图的帮助下找出哪些字符具有偶数频率。
*   忽略所有具有偶数频率的字符，并将其余字符存储在新字符串中。
*   最后，显示新字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that removes the
// characters which have even
// frequencies in the string
void solve(string s)
{
    // create a map to store the
    // frequency of each character
    unordered_map<char, int> m;
    for (int i = 0; i < s.length(); i++) {
        m[s[i]]++;
    }

    // to store the new string
    string new_string = "";

    // remove the characters which
    // have even frequencies
    for (int i = 0; i < s.length(); i++) {

        // if the character has
        // even frequency then skip
        if (m[s[i]] % 2 == 0)
            continue;

        // else concatenate the
        // character to the new string
        new_string += s[i];
    }

    // display the modified string
    cout << new_string << endl;
}

// Driver code
int main()
{
    string s = "aabbbddeeecc";

    // remove the characters which
    // have even frequencies
    solve(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Function that removes the
    // characters which have even
    // frequencies in the string
    static void solve(String s)
    {
        // create a map to store the
        // frequency of each character
        HashMap<Character, Integer> m = new HashMap<>();

        for (int i = 0; i < s.length(); i++)
        {
            if(m.containsKey(s.charAt(i)))
                        m.put(s.charAt(i),
                        m.get(s.charAt(i)) + 1);
            else
                m.put(s.charAt(i), 1);
        }

        // to store the new string
        String new_string = "";

        // remove the characters which
        // have even frequencies
        for (int i = 0; i < s.length(); i++)
        {

            // if the character has
            // even frequency then skip
            if (m.get(s.charAt(i)) % 2 == 0)
                continue;

            // else concatenate the
            // character to the new string
            new_string = new_string + s.charAt(i);
        }

        // display the modified string
        System.out.println(new_string);
    }

    // Driver code
    public static void main(String []args)
    {
        String s = "aabbbddeeecc";

        // remove the characters which
        // have even frequencies
        solve(s);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function that removes the
# characters which have even
# frequencies in the string
def solve(s):

    # create a map to store the
    # frequency of each character
    m = dict()
    for i in range(len(s)):
        if s[i] in m:
            m[s[i]] = m[s[i]]+1
        else:
            m[s[i]] = 1

    # to store the new string
    new_string = ""

    # remove the characters which
    # have even frequencies
    for i in range(len(s)):

        # if the character has
        # even frequency then skip
        if m[s[i]]%2 == 0:
            continue

        # else concatenate the
        # character to the new string
        new_string = new_string+s[i]

    # display the modified string
    print(new_string)

#Driver code
if __name__=='__main__':
    s = "aabbbddeeecc"

# remove the characters which
# have even frequencies
    solve(s)

# this code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    // Function that removes the
    // characters which have even
    // frequencies in the string
    static void solve(String s)
    {
        // create a map to store the
        // frequency of each character
        Dictionary<char, int> m = new Dictionary<char, int>();

        for (int i = 0; i < s.Length; i++)
        {
            if(m.ContainsKey(s[i]))
            {
                var val = m[s[i]];
                m.Remove(s[i]);
                m.Add(s[i], val + 1);

            }        
            else
                m.Add(s[i], 1);
        }

        // to store the new string
        String new_string = "";

        // remove the characters which
        // have even frequencies
        for (int i = 0; i < s.Length; i++)
        {

            // if the character has
            // even frequency then skip
            if (m[s[i]] % 2 == 0)
                continue;

            // else concatenate the
            // character to the new string
            new_string = new_string + s[i];
        }

        // display the modified string
        Console.WriteLine(new_string);
    }

    // Driver code
    public static void Main(String []args)
    {
        String s = "aabbbddeeecc";

        // remove the characters which
        // have even frequencies
        solve(s);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

     // Function that removes the
    // characters which have even
    // frequencies in the string
    function solve(s)
    {
        // create a map to store the
        // frequency of each character
        let m = new Map();

        for (let i = 0; i < s.length; i++)
        {
            if(m.has(s[i]))
                        m.set(s[i],
                        m.get(s[i]) + 1);
            else
                m.set(s[i], 1);
        }

        // to store the new string
        let new_string = "";

        // remove the characters which
        // have even frequencies
        for (let i = 0; i < s.length; i++)
        {

            // if the character has
            // even frequency then skip
            if (m.get(s[i]) % 2 == 0)
                continue;

            // else concatenate the
            // character to the new string
            new_string = new_string + s[i];
        }

        // display the modified string
        document.write(new_string);
    }

// Driver Code

        let s = "aabbbddeeecc";

        // remove the characters which
        // have even frequencies
        solve(s);

</script>   
```

**Output:** 

```
bbbeee
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

#### 方法 2:使用内置的 Python 函数

*   使用 [**【计数器()**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能计算所有字符的频率。
*   然后，遍历字符串，并在地图的帮助下找出哪些字符具有偶数频率。
*   忽略所有具有偶数频率的字符，并将其余字符存储在新字符串中。
*   最后，显示新字符串。

下面是实现:

## 蟒蛇 3

```
# Python3 implementation of
# above approach
from collections import Counter

# Function that removes the
# characters which have even
# frequencies in the string
def removeEven(s):

    # Calculate the frequency using Counter function
    # to store the new string
    m = Counter(s)
    new_string = ""

    # Remove the characters which
    # have even frequencies
    for i in range(len(s)):
        if(m[s[i]] % 2 != 0):

            # Concatenate the character to the new string
            new_string = new_string+s[i]

    # display the modified string
    print(new_string)

# Driver code
if __name__ == '__main__':
    s = "aabbbddeeecc"

# remove the characters which
# have even frequencies
    removeEven(s)

# this code is contributed by vikkycirus
```

**输出:**

```
bbbeee
```

**时间复杂度:** O(N)

**辅助空间:** O(N)