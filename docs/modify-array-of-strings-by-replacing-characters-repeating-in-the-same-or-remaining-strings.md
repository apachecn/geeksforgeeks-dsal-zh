# 通过替换在相同或剩余字符串中重复的字符来修改字符串数组

> 原文:[https://www . geeksforgeeks . org/通过替换相同或剩余字符串中的重复字符来修改字符串数组/](https://www.geeksforgeeks.org/modify-array-of-strings-by-replacing-characters-repeating-in-the-same-or-remaining-strings/)

给定仅由小写和大写字符组成的字符串数组 **arr[]** ，任务是通过从相同字符串或任何其他字符串中重复的字符串中移除字符来修改数组。打印修改后的数组。

**示例:**

> **输入:** arr[] = {“极客”、“For”、“极客”}
> **输出:**{“Geks”、“For”}
> **解释:**
> 在 arr 中【0【、**‘e’**在字符串中出现两次。从第一个字符串中删除单个**‘e’**会将“极客”修改为“Geks”。
> 在 arr[1]中，所有字符都是不重复的。因此，字符串保持不变。
> 在 arr[2]中，字符串与 arr[0]相同。因此，需要删除完整的字符串。
> 
> **输入:** arr[] = {“极客”、“For”、“极客”、“Post”}
> **输出:** {“极客”、“For”、“Pt”}

**方法:**按照步骤解决问题:

*   当[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)时，初始化一个[无序集](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)来存储字符串的字符。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并对每个字符串执行以下操作:
    *   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
    *   [如果当前角色已经出现在集合](https://www.geeksforgeeks.org/set-find-function-in-c-stl/)中，跳过它。否则，将其追加到输出字符串中。
    *   将新生成的字符串推入已初始化的列表以存储输出。
*   打印作为答案获得的字符串列表。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to remove duplicate
// characters across the strings
void removeDuplicateCharacters(vector<string> arr)
{
    // Stores distinct characters
    unordered_set<char> cset;

    // Size of the array
    int n = arr.size();

    // Stores the list of
    // modified strings
    vector<string> out;

    // Traverse the array
    for (auto str : arr) {

        // Stores the modified string
        string out_curr = "";

        // Iterate over the characters
        // of the modified string
        for (auto ch : str) {

            // If character is already present
            if (cset.find(ch) != cset.end())
                continue;

            out_curr += ch;

            // Insert character into the Set
            cset.insert(ch);
        }

        if (out_curr.size())
            out.push_back(out_curr);
    }

    // Print the list of modified strings
    for (int i = 0; i < out.size(); i++) {

        // Print each string
        cout << out[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array of strings
    vector<string> arr
        = { "Geeks", "For", "Geeks", "Post" };

    // Function Call to modify the
    // given array of strings
    removeDuplicateCharacters(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to remove duplicate
// characters across the strings
static void removeDuplicateCharacters(String arr[])
{

    // Stores distinct characters
    HashSet<Character> cset = new HashSet<>();

    // Size of the array
    int n = arr.length;

    // Stores the list of
    // modified strings
    ArrayList<String> out = new ArrayList<>();

    // Traverse the array
    for(String str : arr)
    {

        // Stores the modified string
        String out_curr = "";

        // Iterate over the characters
        // of the modified string
        for(char ch : str.toCharArray())
        {

            // If character is already present
            if (cset.contains(ch))
                continue;

            out_curr += ch;

            // Insert character into the Set
            cset.add(ch);
        }

        if (out_curr.length() != 0)
            out.add(out_curr);
    }

    // Print the list of modified strings
    for(int i = 0; i < out.size(); i++)
    {

        // Print each string
        System.out.print(out.get(i) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array of strings
    String arr[] = { "Geeks", "For", "Geeks", "Post" };

    // Function Call to modify the
    // given array of strings
    removeDuplicateCharacters(arr);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to remove duplicate
# characters across the strings
def removeDuplicateCharacters(arr):

    # Stores distinct characters
    cset = set([])

    # Size of the array
    n = len(arr)

    # Stores the list of
    # modified strings
    out = []

    # Traverse the array
    for st in arr:

        # Stores the modified string
        out_curr = ""

        # Iterate over the characters
        # of the modified string
        for ch in st:

            # If character is already present
            if (ch in cset):
                continue

            out_curr += ch

            # Insert character into the Set
            cset.add(ch)

        if (len(out_curr)):
            out.append(out_curr)

    # Print the list of modified strings
    for i in range(len(out)):

        # Print each string
        print(out[i], end = " ")

# Driver Code
if __name__ == "__main__":

    # Given array of strings
    arr = ["Geeks", "For", "Geeks", "Post"]

    # Function Call to modify the
    # given array of strings
    removeDuplicateCharacters(arr)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to remove duplicate
// characters across the strings
static void removeDuplicateCharacters(string[] arr)
{

    // Stores distinct characters
    HashSet<int> cset = new HashSet<int>();

    // Size of the array
    int n = arr.Length;

    // Stores the list of
    // modified strings
    List<string> Out = new List<string>();

    // Traverse the array
    foreach(string str in arr)
    {

        // Stores the modified string
        string out_curr = "";

        // Iterate over the characters
        // of the modified string
        foreach(char ch in str.ToCharArray())
        {

            // If character is already present
            if (cset.Contains(ch))
                continue;

            out_curr += ch;

            // Insert character into the Set
            cset.Add(ch);
        }

        if (out_curr.Length != 0)
            Out.Add(out_curr);
    }

    // Print the list of modified strings
    for(int i = 0; i < Out.Count; i++)
    {

        // Print each string
        Console.Write(Out[i] + " ");
    }
}

    static public void Main (){

        // Given array of strings
    string[] arr = { "Geeks", "For",
                     "Geeks", "Post" };

    // Function Call to modify the
    // given array of strings
    removeDuplicateCharacters(arr);
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to remove duplicate
// characters across the strings
function removeDuplicateCharacters(arr)
{
    // Stores distinct characters
    var cset = new Set();

    // Size of the array
    var n = arr.length;

    // Stores the list of
    // modified strings
    var out = [];

    // Traverse the array
    arr.forEach(str => {

        // Stores the modified string
        var out_curr = "";

        // Iterate over the characters
        // of the modified string
        str.split('').forEach(ch => {

            // If character is already present
            if (!cset.has(ch))
            {

            out_curr += ch;

            // Insert character into the Set
            cset.add(ch);
            }
        });

        if (out_curr.size!=0)
            out.push(out_curr);
    });

    // Print the list of modified strings
    for (var i = 0; i < out.length; i++) {

        // Print each string
        document.write( out[i] + " ");
    }
}

// Driver Code
// Given array of strings
var arr
    = ["Geeks", "For", "Geeks", "Post"];
// Function Call to modify the
// given array of strings
removeDuplicateCharacters(arr);

</script>
```

**Output:** 

```
Geks For Pt
```

***时间复杂度:** O(N * M)其中 **M** 是数组中最长字符串的长度。*
***辅助空间:** O(N)*