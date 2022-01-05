# 从字符串中删除奇数频率字符

> 原文:[https://www . geeksforgeeks . org/从字符串中删除奇数频率字符/](https://www.geeksforgeeks.org/remove-odd-frequency-characters-from-the-string/)

给定大小为 **N** 的字符串 **str** ，任务是从字符串中移除所有具有奇数频率的字符。

**示例:**

> **输入:**str = " geeks forgeks "
> **输出:**geeks
> 字符 f、o、r 具有奇数频率
> 因此，它们被从字符串中移除。
> 
> **输入:**【str = " zzzxxweeerr】
> **输出:** xxrr

**进场:**

*   创建一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)并将字符串中每个字符的[频率存储到同一个映射中。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   然后，遍历字符串，并在地图的帮助下找出哪些字符具有奇数频率。
*   忽略所有具有奇数频率的字符，并将其余字符存储在新字符串中。
*   最后，显示新字符串。

下面是上述方法的实现:

## C++

```
// C++ program to remove the characters
// having odd frequencies in the string
#include <bits/stdc++.h>
using namespace std;

// Function to remove the characters which
// have odd frequencies in the string
string removeOddFrequencyCharacters(string s)
{
    // Create a map to store the
    // frequency of each character
    unordered_map<char, int> m;
    for (int i = 0; i < s.length(); i++) {
        m[s[i]]++;
    }

    // To store the new string
    string new_string = "";

    // Remove the characters which
    // have odd frequencies
    for (int i = 0; i < s.length(); i++) {

        // If the character has
        // odd frequency then skip
        if (m[s[i]] & 1)
            continue;

        // Else concatenate the
        // character to the new string
        new_string += s[i];
    }

    // Return the modified string
    return new_string;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    // Remove the characters which
    // have odd frequencies
    str = removeOddFrequencyCharacters(str);
    cout << str << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove the characters
// having odd frequencies in the string
import java.util.*;

class GFG
{

    // Function to remove the characters which
    // have odd frequencies in the string
    static String removeOddFrequencyCharacters(String s)
    {
        // Create a map to store the
        // frequency of each character
        HashMap<Character, Integer> m = new HashMap<Character,Integer>();
        for (int i = 0; i < s.length(); i++) {
            char p = s.charAt(i);
            Integer count = m.get(p);
            if( count == null)
            {
                count=0;
                m.put(p,1);
            }
            else
                m.put(p,count + 1);
        }

        // To store the new string
        String new_string = "";

        // Remove the characters which
        // have odd frequencies
        for (int i = 0; i < s.length(); i++) {

            // If the character has
            // odd frequency then skip
            if ((m.get(s.charAt(i))& 1)==1)
                continue;

            // Else concatenate the
            // character to the new string
            new_string += s.charAt(i);
        }

        // Return the modified string
        return new_string;
    }

    // Driver code
    public static void main(String []args)
    {
        String str = "geeksforgeeks";

        // Remove the characters which
        // have odd frequencies
        str = removeOddFrequencyCharacters(str);
        System.out.print(str);
    }
}

// This is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to remove the characters
# having odd frequencies in the string

# Function to remove the characters which
# have odd frequencies in the string
def removeOddFrequencyCharacters(s):

    # Create a map to store the
    # frequency of each character
    m = dict()
    for i in s:
        m[i] = m.get(i, 0) + 1

    # To store the new string
    new_s = ""

    # Remove the characters which
    # have odd frequencies
    for i in s:

        # If the character has
        # odd frequency then skip
        if (m[i] & 1):
            continue

        # Else concatenate the
        # character to the new string
        new_s += i

    # Return the modified string
    return new_s

# Driver code
if __name__ == '__main__':
    str = "geeksforgeeks"

    # Remove the characters which
    # have odd frequencies
    str = removeOddFrequencyCharacters(str)
    print(str)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to remove the characters
// having odd frequencies in the string
using System;
using System.Collections.Generic;

class GFG{

// Function to remove the characters which
// have odd frequencies in the string
static string removeOddFrequencyCharacters(string s)
{

    // Create a map to store the
    // frequency of each character
    Dictionary<char,
               int> m = new Dictionary<char,
                                       int>();

    for(int i = 0; i < s.Length; i++)
    {
        char p = s[i];

        if (m.ContainsKey(p))
        {
            m[p]++;
        }
        else
        {
            m[p] = 1;
        }
    }

    // To store the new string
    string new_string = "";

    // Remove the characters which
    // have odd frequencies
    for(int i = 0; i < s.Length; i++)
    {

        // If the character has
        // odd frequency then skip
        if ((m[s[i]] & 1) == 1)
            continue;

        // Else concatenate the
        // character to the new string
        new_string += s[i];
    }

    // Return the modified string
    return new_string;
}

// Driver code
public static void Main(string []args)
{
    string str = "geeksforgeeks";

    // Remove the characters which
    // have odd frequencies
    str = removeOddFrequencyCharacters(str);

    Console.Write(str);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to remove the characters
// having odd frequencies in the string

    // Function to remove the characters which
    // have odd frequencies in the string
    function removeOddFrequencyCharacters(s)
    {
        // Create a map to store the
        // frequency of each character
        let m = new Map();
        for (let i = 0; i < s.length; i++) {
            let p = s[i];
            let count = m.get(p);
            if( count == null)
            {
                count=0;
                m.set(p,1);
            }
            else
                m.set(p,count + 1);
        }

        // To store the new string
        let new_string = "";

        // Remove the characters which
        // have odd frequencies
        for (let i = 0; i < s.length; i++) {

            // If the character has
            // odd frequency then skip
            if ((m.get(s[i])& 1)==1)
                continue;

            // Else concatenate the
            // character to the new string
            new_string += s[i];
        }

        // Return the modified string
        return new_string;
    }

// Driver code

      let str = "geeksforgeeks";

        // Remove the characters which
        // have odd frequencies
        str = removeOddFrequencyCharacters(str);
        document.write(str);

</script>
```

**Output:** 

```
geeksgeeks
```