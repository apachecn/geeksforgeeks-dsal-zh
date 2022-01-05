# 使用给定字符组成的给定字符串数组的字符串总长度

> 原文:[https://www . geeksforgeeks . org/给定字符串数组的总字符串长度-使用给定字符组合/](https://www.geeksforgeeks.org/total-length-of-string-from-given-array-of-strings-composed-using-given-characters/)

给定一个**字符列表**和一个**字符串数组**，找出字符串数组中所有可以使用给定字符组成的字符串的总长度。
**例:**

> **输入:**字符串= [“老鼠”、“我”、“蝙蝠”、“狮子”]，chars =“尤沙姆布”
> **输出:** 10
> **解释:**
> 使用字符“尤沙姆布”可以形成的字符串有“老鼠”和“我”以及“蝙蝠”。
> 鼠的长度为 5，“我”的长度为 2，“蝙蝠”的长度为 3
> 所有长度之和= 5 + 2 + 3 = 10。
> **输入:**字符串=[“hi”、“data”、“geeks forgeeks”]，chars =“tiadha”
> **输出:** 6
> **解释:**
> 使用字符“tiadha”可以构成的字符串有“hi”和“data”。其中“hi”的长度是 2，“data”的长度是 4，所有的总和是 2 + 4 = 6。

**方法:**
要解决上面提到的问题，我们必须遵循下面给出的步骤:

*   我们可以在形成字符串时使用给定字符串中的字符，即“字符”。我们还可以重用使用过的字符来形成下一个字符串
*   通过跟踪字符串中每个字符的[频率，维护一个以字符为关键字和值的](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)。
*   每次我们扫描字符串列表中的字符时，我们都会减少无序映射中的字符频率，但我们必须维护原始映射的副本，以便检查第二个字符串。
*   如果该键不在映射中，它会创建一个默认值为零的键，而不是引发错误。

**以下是上述方法的实施:**

## C++

```
// C++ implementation to find total length
// of string composed of given characters
// formed from given Array of strings

#include <bits/stdc++.h>
using namespace std;

// Function to count the total length
int countCharacters(
    vector<string>& strings,
    string chars)
{
    int res = 0;

    // Unordered_map for
    // keeping frequency of characters
    unordered_map<char, int> freq;

    // Calculate the frequency
    for (int i = 0; i < chars.length(); i++)
        freq[chars[i]] += 1;

    // Iterate in the N strings
    for (auto st : strings) {

        bool flag = true;

        // Iterates in the string
        for (auto c : st) {

            // Checks if given character of string
            // string appears in it or not
            if (!freq) {
                flag = false;
                break;
            }
        }

        // Adds the length of string
        // if all characters are present
        if (flag)
            res += st.length();
    }

    // Return the final result
    return res;
}

// Driver code
int main()
{
    vector<string> strings
        = { "hi", "data",
            "geeksforgeeks" };

    string chars = "tiadhae";

    cout << countCharacters(strings, chars);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find total length
// of string composed of given characters
// formed from given Array of strings
import java.util.*;
class GFG {

// Function to count the total length
static int countCharacters(List<String> strings,
                                String chars)
{
    int res = 0;

    // Map for
    // keeping frequency of characters
    Map<Character, Integer> freq = new HashMap<>();

    // Calculate the frequency
    for (int i = 0; i < chars.length(); i++)
    {
        freq.put(chars.charAt(i),
        freq.getOrDefault(chars.charAt(i), 0) + 1);
    }

    // Iterate in the N strings
    for (String st : strings)
    {
        boolean flag = true;

        // Iterates in the string
        for (char c : st.toCharArray())
        {

            // Checks if given character of string
            // string appears in it or not
            if (!freq.containsKey(c))
            {
                flag = false;
                break;
            }
        }

        // Adds the length of string
        // if all characters are present
        if (flag)
            res += st.length();
    }

    // Return the final result
    return res;
}

// Driver code
public static void main(String[] args)
{
    List<String> strings = Arrays.asList("hi", "data",
                                        "geeksforgeeks");

    String chars = "tiadhae";

    System.out.println(countCharacters(strings, chars));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find total length
# of string composed of given characters
# formed from given Array of strings

# Function to count the total length
def countCharacters(arr, chars):
    res = 0

    # Unordered_map for
    # keeping frequency of characters
    freq = dict()

    # Calculate the frequency
    for i in range(len(chars)):
        freq[chars[i]] = freq.get(chars[i], 0)+1

    # Iterate in the N strings
    for st in arr:

        flag = True

        # Iterates in the string
        for c in st:

            # Checks if given character of string
            # string appears in it or not
            if (c not in freq):
                flag = False
                break

        # Adds the length of string
        # if all characters are present
        if (flag):
            res += len(st)

    # Return the final result
    return res

# Driver code
if __name__ == '__main__':
    arr =["hi", "data", "geeksforgeeks"]

    chars = "tiadhae"

    print(countCharacters(arr, chars))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find total length
// of string composed of given characters
// formed from given Array of strings
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to count the total length
static int countCharacters(List<string> strings,
                                string chars)
{
    int res = 0;

    // Dictionary for keeping frequency
    // of characters
    Dictionary<char,
               int> freq = new Dictionary<char,
                                          int>();

    // Calculate the frequency
    for(int i = 0; i < chars.Length; i++)
    {
        if(freq.ContainsKey(chars[i]))
        {
            freq[chars[i]]++;
        }
        else
        {
            freq.Add(chars[i],
                     freq.GetValueOrDefault(
                         chars[i], 0) + 1);
        }
    }

    // Iterate in the N strings
    foreach(string st in strings)
    {
        bool flag = true;

        // Iterates in the string
        foreach (char c in st.ToCharArray())
        {

            // Checks if given character of string
            // string appears in it or not
            if (!freq.ContainsKey(c))
            {
                flag = false;
                break;
            }
        }

        // Adds the length of string
        // if all characters are present
        if (flag)
            res += st.Length;
    }

    // Return the final result
    return res;
}

// Driver code
public static void Main(string[] args)
{
    string []tmp = { "hi", "data",
                     "geeksforgeeks" };

    List<string> strings = tmp.ToList();

    string chars = "tiadhae";

    Console.Write(countCharacters(strings, chars));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find total length
// of string composed of given characters
// formed from given Array of strings

// Function to count the total length
function countCharacters(   strings,  chars)
{
    var res = 0;

    // Unordered_map for
    // keeping frequency of characters
    var freq = new Map(); 

    // Calculate the frequency
    for (var i = 0; i < chars.length; i++)
    {
        if(freq.has(chars[i]))
            freq.set(chars[i], freq.get(chars[i])+1)
        else
            freq.set(chars[i], 1)
    }

    // Iterate in the N strings
    strings.forEach(st => {

        var flag = true;

        // Iterates in the string
        st.split('').forEach(c => {

            // Checks if given character of string
            // string appears in it or not
            if (!freq.has(c)) {
                flag = false;
            }
        });

        // Adds the length of string
        // if all characters are present
        if (flag)
            res += st.length;
    });

    // Return the final result
    return res;
}

// Driver code
var strings
    = ["hi", "data",
        "geeksforgeeks"];
var chars = "tiadhae";
document.write( countCharacters(strings, chars));

// This code is contributed by noob2000.
</script>   
```

**Output:** 

```
6
```

***时间复杂度:** O(n * m)* ，其中 **n** 为 char 的长度， **m** 为字符串的长度。
***辅助空间复杂度:** O(1)* ，因为无序地图的大小只有 26。