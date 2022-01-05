# 检查一个字符串是否由两个 K 长度不重叠的子字符串组成作为字谜

> 原文:[https://www . geesforgeks . org/check-if-a-string-compose-two-k-length-non-重叠-substrings-as-anagrams/](https://www.geeksforgeeks.org/check-if-a-string-consists-of-two-k-length-non-overlapping-substrings-as-anagrams/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**和一个整数 **K** ，任务是检查一个字符串是否有两个长度为 **K** 的非重叠子字符串作为字谜。

**示例:**

> **输入:**str = " gining "，K = 3
> **输出:** Yes
> **解释:**
> “gin”和“ing”是长度为 3 的两个不重叠的子串，是字谜。
> 因此，输出为是。
> 
> **输入:** str = "ginig "，K = 3
> **输出:** No
> **说明:**
> 在给定的字符串中，没有两个长度为 3 的不重叠的子串是字谜。请注意，子串“gin”和子串“nig”是字谜，但它们是重叠的，因此不被考虑。
> 因此，输出为否

**方法:**解决这个问题的思路是[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，使用[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)存储长度为 **K** 的子字符串，搜索给定字符串中存在的两个不重叠的子字符串。请遵循以下步骤:

*   初始化一个[无序集](https://www.geeksforgeeks.org/unorderd_set-stl-uses/) **集**来存储**长度为 K** 的子串。
*   [使用变量 **i** 迭代给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **字符串**的字符。
*   如果 str 中存在从索引**(I–1)**开始的长度为 K 的**字符串，则 [**从**集合****](https://www.geeksforgeeks.org/seterase-c-stl/) 中删除**长度为 **K** 的排序字符串。
*   如果在**字符串中存在以索引**(I–1)**结束的长度为 **K** 的字符串，**则 [**将排序后的长度为 **K** 的字符串插入**集合****](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) 。
*   如果在****集合**中找到从索引 **i** 开始的 **长度为 K** 的**排序子串，则**串**中存在两个不重叠的**长度为 K** 的子串作为[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。因此，打印**“是”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将排序后的长度为 **K** 的子串从索引 **i** 开始插入到**集合**中。****
*   **如果迭代整个字符串后没有找到一对子字符串，则打印**“否”。****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to check whether the string
// s has two non-overlapping substrings
// of length K as anagrams
void anagramPairs(string str, int K)
{
    // Stores the substrings of length K
    unordered_set<string> set;
    int l = str.length();

    // Iterate through every character
    for (int i = 0; i < l; i++) {

        // If there is a substring starting
        // at index i - 1 of length K then
        // erase that substring from set
        if (i > 0 && K - (i - 1) - 1 < l) {
            string s1 = str.substr(i - 1, K);

            // Sort the substring
            sort(s1.begin(), s1.end());

            // Remove from set
            set.erase(s1);
        }

        // If there is a substring of length
        // K ending at index i - 1
        if ((i - 1) - K + 1 >= 0) {

            string s1 = str.substr(
                (i - 1) - K + 1, K);

            // Sort the substring
            sort(s1.begin(), s1.end());

            // Insert substring into the Set
            set.insert(s1);
        }

        // If there is a substring of length
        // K starting from the i-th index
        if (K + i - 1 < l) {

            // Check if the sorted
            // substring is present in
            // the set or not
            string s1 = str.substr(i, K);

            sort(s1.begin(), s1.end());

            // If present in the Set
            if (set.count(s1)) {
                cout << "Yes";
                return;
            }

            // Insert the sorted
            // substring into the set
            set.insert(s1);
        }
    }

    // If not present in the Set
    cout << "No";
}

// Driver Code
int main()
{
    string str = "ginfing";
    int K = 3;

    // Function Call
    anagramPairs(str, K);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.util.*;

class GFG
{

// Function to check whether the String
// s has two non-overlapping subStrings
// of length K as anagrams
static void anagramPairs(String str, int K)
{

    // Stores the subStrings of length K
    HashSet<String> set = new HashSet<String>();
    int l = str.length();

    // Iterate through every character
    for (int i = 0; i < l; i++)
    {

        // If there is a subString starting
        // at index i - 1 of length K then
        // erase that subString from set
        if (i > 0 && K - (i - 1) - 1 < l)
        {
            String s1 = str.substring(i - 1, K);

            // Sort the subString
            s1 = sortString(s1);

            // Remove from set
            set.remove(s1);
        }

        // If there is a subString of length
        // K ending at index i - 1
        if ((i - 1) - K + 1 >= 0)
        {

            String s1 = str.substring(
                (i - 1) - K + 1, K);

            // Sort the subString
            s1 = sortString(s1);

            // Insert subString into the Set
            set.add(s1);
        }

        // If there is a subString of length
        // K starting from the i-th index
        if (K + i - 1 < l)
        {

            // Check if the sorted
            // subString is present in
            // the set or not
            String s1 = str.substring(i, i+K);

            s1 = sortString(s1);

            // If present in the Set
            if (set.contains(s1))
            {
                System.out.print("Yes");
                return;
            }

            // Insert the sorted
            // subString into the set
            set.add(s1);
        }
    }

    // If not present in the Set
    System.out.print("No");
}
static String sortString(String inputString)
{

    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Driver Code
public static void main(String[] args)
{
    String str = "ginfing";
    int K = 3;

    // Function Call
    anagramPairs(str, K);
}
}

// This code is contributed by Amit Katiyar
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to check whether the string
# s has two non-overlapping substrings
# of length K as anagrams
def anagramPairs(str, K):

    # Stores the substrings of length K
    sett = {}
    l = len(str)

    # Iterate through every character
    for i in range(l):

        # If there is a substring starting
        # at index i - 1 of length K then
        # erase that substring from sett
        if (i > 0 and K - (i - 1) - 1 < l):
            s1 = str[i - 1:i + K - 1]

            # Sort the substring
            s1 = sorted(s1)

            # Remove from sett
            del sett["".join(s1)]

        # If there is a substring of length
        # K ending at index i - 1
        if ((i - 1) - K + 1 >= 0):

            s1 = str[(i - 1) - K + 1:i]

            # Sort the substring
            s1 = sorted(s1)

            # Insert substring into the Set
            sett["".join(s1)] = 1

        # If there is a substring of length
        # K starting from the i-th index
        if (K + i - 1 < l):

            # Check if the sorted
            # substring is present in
            # the sett or not
            s1 = str[i : i + K]

            s1 = sorted(s1)

            # If present in the Set
            if "".join(s1) in sett:
                print("Yes")
                return

            #Insert the sorted
            # substring into the sett
            sett["".join(s1)] = 1

    # If not present in the Set
    print("No")

# Driver Code
if __name__ == '__main__':
    str = "ginfing"
    K = 3

    # Function Call
    anagramPairs(str, K)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to check whether the String
// s has two non-overlapping subStrings
// of length K as anagrams
static void anagramPairs(String str, int K)
{

    // Stores the subStrings of length K
    HashSet<String> set = new HashSet<String>();
    int l = str.Length;

    // Iterate through every character
    for (int i = 0; i < l; i++)
    {

        // If there is a subString starting
        // at index i - 1 of length K then
        // erase that subString from set
        if (i > 0 && K - (i - 1) - 1 < l)
        {
            String s1 = str.Substring(i - 1, K);

            // Sort the subString
            s1 = sortString(s1);

            // Remove from set
            set.Remove(s1);
        }

        // If there is a subString of length
        // K ending at index i - 1
        if ((i - 1) - K + 1 >= 0)
        {

            String s1 = str.Substring(
                (i - 1) - K + 1, K);

            // Sort the subString
            s1 = sortString(s1);

            // Insert subString into the Set
            set.Add(s1);
        }

        // If there is a subString of length
        // K starting from the i-th index
        if (K + i - 1 < l)
        {

            // Check if the sorted
            // subString is present in
            // the set or not
            String s1 = str.Substring(i, K);

            s1 = sortString(s1);

            // If present in the Set
            if (set.Contains(s1))
            {
                Console.Write("Yes");
                return;
            }

            // Insert the sorted
            // subString into the set
            set.Add(s1);
        }
    }

    // If not present in the Set
    Console.Write("No");
}
static String sortString(String inputString)
{

    // convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // sort tempArray
    Array.Sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "ginfing";
    int K = 3;

    // Function Call
    anagramPairs(str, K);
}
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to check whether the string
// s has two non-overlapping substrings
// of length K as anagrams
function anagramPairs(str, K) {
    // Stores the substrings of length K
    let set = new Set();
    let l = str.length;

    // Iterate through every character
    for (let i = 0; i < l; i++) {

        // If there is a substring starting
        // at index i - 1 of length K then
        // erase that substring from set
        if (i > 0 && K - (i - 1) - 1 < l) {
            let s1 = str.substr(i - 1, K);

            // Sort the substring
            s1 = s1.split("").sort().join("")

            // Remove from set
            set.delete(s1);
        }

        // If there is a substring of length
        // K ending at index i - 1
        if ((i - 1) - K + 1 >= 0) {

            let s1 = str.substr(
                (i - 1) - K + 1, K);

            // Sort the substring
            s1 = s1.split("").sort().join("")

            // Insert substring into the Set
            set.add(s1);
        }

        // If there is a substring of length
        // K starting from the i-th index
        if (K + i - 1 < l) {

            // Check if the sorted
            // substring is present in
            // the set or not
            let s1 = str.substr(i, K);
            s1 = s1.split("").sort().join("")

            // If present in the Set
            if (set.has(s1)) {
                document.write("Yes");
                return;
            }

            // Insert the sorted
            // substring into the set
            set.add(s1);
        }
    }

    // If not present in the Set
    document.write("No");
}

// Driver Code

let str = "ginfing";
let K = 3;

// Function Call
anagramPairs(str, K);

</script>
```

****Output:** 

```
Yes
```** 

*****时间复杂度:**O(N *(K+K * log K))*
***辅助空间:** O(N)***