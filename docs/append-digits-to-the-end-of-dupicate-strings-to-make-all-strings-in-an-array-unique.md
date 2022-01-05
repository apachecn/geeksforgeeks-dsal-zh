# 将数字附加到重复字符串的末尾，使数组中的所有字符串唯一

> 原文:[https://www . geeksforgeeks . org/将数字附加到重复字符串的末尾，使数组中的所有字符串唯一/](https://www.geeksforgeeks.org/append-digits-to-the-end-of-dupicate-strings-to-make-all-strings-in-an-array-unique/)

给定一个由 **N** 个字符串组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过附加 ay 号替换重复的字符串来修改数组，这样数组中的所有字符串都是唯一的。

**示例:**

> **输入:**S = {“aa”、“bb”、“cc”、“bb”、“aa”、“aa”、“aa”}
> **输出:**{“aa”、“bb”、“cc”、“bb1”、“aa1”、“aa2”、“aa3”}
> **解释:**
> 第二次出现“bb”的输出为“bb1”
> 第二次出现“aa”的输出为“aa1”
> 第三次出现“aa”的输出为“aa2”【T11
> 
> **输入:**S = {“aa”、“bb”、“cc”、“aa”}
> **输出:**{“aa”、“bb”、“cc”、“aa1”}

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、[将**arr【】**中每个字符串](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)的频率存储在 [Hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中。存储频率时，如果字符串没有以前出现过的频率，则保持字符串不变。否则，在末尾追加其频率。最后，打印数组 **arr[]** 中存在的所有唯一字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace duplicate strings
// by alphanumeric strings to make all
// strings in the array unique
void replaceDuplicates(
    vector<string>& names)
{
    // Store the frequency of strings
    unordered_map<string, int> hash;

    // Iterate over the array
    for (int i = 0;
         i < names.size(); i++) {

        // For the first occurrence,
        // update the frequency count
        if (hash.count(names[i]) == 0)
            hash[names[i]]++;

        // Otherwise
        else {

            int count = hash[names[i]]++;

            // Append frequency count
            // to end of the string
            names[i] += to_string(count);
        }
    }

    // Print the modified array
    for (int i = 0;
         i < names.size(); i++) {
        cout << names[i] << " ";
    }
}

// Driver Code
int main()
{
    vector<string> str
        = { "aa", "bb", "cc", "bb",
            "aa", "aa", "aa" };

    // Function Call
    replaceDuplicates(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to replace duplicate strings
// by alphanumeric strings to make all
// strings in the array unique
static void replaceDuplicates(String[] names)
{

    // Store the frequency of strings
    HashMap<String, Integer> hash = new HashMap<>();

    // Iterate over the array
    for(int i = 0; i < names.length; i++)
    {

        // For the first occurrence,
        // update the frequency count
        if (!hash.containsKey(names[i]))
            hash.put(names[i], 1);

        // Otherwise
        else
        {
            int count = hash.get(names[i]);
            hash.put(names[i], hash.get(names[i]) + 1);

            // Append frequency count
            // to end of the string
            names[i] += Integer.toString(count);
        }
    }

    // Print the modified array
    for(int i = 0; i < names.length; i++)
    {
        System.out.print(names[i] + ' ');
    }
}

// Driver Code
public static void main(String[] args)
{
    String[] str = { "aa", "bb", "cc",
                     "bb", "aa", "aa", "aa" };

    // Function Call
    replaceDuplicates(str);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to replace duplicate strings
# by alphanumeric strings to make all
# strings in the array unique
def replaceDuplicates(names):

    # Store the frequency of strings
    hash = {}

    # Iterate over the array
    for i in range(0, len(names)):

        # For the first occurrence,
        # update the frequency count
        if names[i] not in hash:
            hash[names[i]] = 1

        # Otherwise
        else:
            count = hash[names[i]]
            hash[names[i]] += 1

            # Append frequency count
            # to end of the string
            names[i] += str(count)

    # Print the modified array
    for i in range(0, len(names)):
        print(names[i], end = ' ')

# Driver Code
if __name__ == '__main__':

    str1 = [ "aa", "bb", "cc",
             "bb", "aa", "aa", "aa" ]

    # Function Call
    replaceDuplicates(str1)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to replace duplicate strings
// by alphanumeric strings to make all
// strings in the array unique
static void replaceDuplicates(string[] names)
{

    // Store the frequency of strings
    Dictionary<string,
               int> hash = new Dictionary<string,
                                          int>();

    // Iterate over the array
    for(int i = 0; i < names.Length; i++)
    {

        // For the first occurrence,
        // update the frequency count
        if (!hash.ContainsKey(names[i]))
            hash[names[i]] = 1;

        // Otherwise
        else
        {
            int count = hash[names[i]];
            hash[names[i]] += 1;

            // Append frequency count
            // to end of the string
            names[i] += count.ToString();
        }
    }

    // Print the modified array
    for(int i = 0; i < names.Length; i++)
    {
        Console.Write(names[i] + ' ');
    }
}

// Driver Code
public static void Main()
{
    string[] str = { "aa", "bb", "cc",
                     "bb", "aa", "aa", "aa" };

    // Function Call
    replaceDuplicates(str);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to replace duplicate strings
// by alphanumeric strings to make all
// strings in the array unique
function replaceDuplicates( names)
{
    // Store the frequency of strings
    var hash = new Map();

    // Iterate over the array
    for (var i = 0;
         i < names.length; i++) {

        // For the first occurrence,
        // update the frequency count
        if (!hash.has(names[i]))
            hash.set(names[i],1);

        // Otherwise
        else {

            var count = hash.get(names[i]);
            hash.set(names[i],hash.get(names[i])+1);
            // Append frequency count
            // to end of the string
            names[i] += count.toString();
        }
    }

    // Print the modified array
    for (var i = 0;
         i < names.length; i++) {
        document.write( names[i] + " ");
    }
}

// Driver Code
var str
    = [ "aa", "bb", "cc", "bb",
        "aa", "aa", "aa" ];
// Function Call
replaceDuplicates(str);

</script>
```

**Output:** 

```
aa bb cc bb1 aa1 aa2 aa3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)