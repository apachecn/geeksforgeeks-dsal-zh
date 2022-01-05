# 检查两个给定的字符串是否彼此同构

> 原文:[https://www . geesforgeks . org/check-如果两个给定的字符串彼此同构/](https://www.geeksforgeeks.org/check-if-two-given-strings-are-isomorphic-to-each-other/)

如果 str1 的每个字符与 str2 的每个字符之间存在一对一的映射，则两个字符串 str1 和 str2 称为同构。并且“str1”中每个字符的所有出现都映射到“str2”中的相同字符。

示例:

```
Input:  str1 = "aab", str2 = "xxy"
Output: True
'a' is mapped to 'x' and 'b' is mapped to 'y'.

Input:  str1 = "aab", str2 = "xyz"
Output: False
One occurrence of 'a' in str1 has 'x' in str2 and 
other occurrence of 'a' has 'y'.
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/isomorphic-strings-1587115620/1)

一个**简单的解决方案**是考虑“str1”的每个字符，并检查它的所有出现是否映射到“str2”中的相同字符。这个解的时间复杂度是 O(n*n)。

一个**高效解**可以在 O(n)时间内解决这个问题。其思想是创建一个数组来存储已处理字符的映射。

```
1) If lengths of str1 and str2 are not same, return false.
2) Do following for every character in str1 and str2
   a) If this character is seen first time in str1, 
      then current of str2 must have not appeared before.
      (i) If current character of str2 is seen, return false.
          Mark current character of str2 as visited.
      (ii) Store mapping of current characters.
   b) Else check if previous occurrence of str1[i] mapped
      to same character.
```

以下是上述想法的实现:

## C++

```
// C++ program to check if two strings are isomorphic
#include <bits/stdc++.h>
using namespace std;
#define MAX_CHARS 256

// This function returns true if str1 and str2 are isomorphic
bool areIsomorphic(string str1, string str2)
{

    int m = str1.length(), n = str2.length();

    // Length of both strings must be same for one to one
    // corresponance
    if (m != n)
        return false;

    // To mark visited characters in str2
    bool marked[MAX_CHARS] = { false };

    // To store mapping of every character from str1 to
    // that of str2\. Initialize all entries of map as -1.
    int map[MAX_CHARS];
    memset(map, -1, sizeof(map));

    // Process all characters one by on
    for (int i = 0; i < n; i++) {
        // If current character of str1 is seen first
        // time in it.
        if (map[str1[i]] == -1) {
            // If current character of str2 is already
            // seen, one to one mapping not possible
            if (marked[str2[i]] == true)
                return false;

            // Mark current character of str2 as visited
            marked[str2[i]] = true;

            // Store mapping of current characters
            map[str1[i]] = str2[i];
        }

        // If this is not first appearance of current
        // character in str1, then check if previous
        // appearance mapped to same character of str2
        else if (map[str1[i]] != str2[i])
            return false;
    }

    return true;
}

// Driver program
int main()
{
    cout << areIsomorphic("aab", "xxy") << endl;
    cout << areIsomorphic("aab", "xyz") << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two strings are isomorphic
import java.io.*;
import java.util.*;
class Isomorphic {
    static int size = 256;

    // Function returns true if str1 and str2 are isomorphic
    static boolean areIsomorphic(String str1, String str2)
    {
        int m = str1.length();
        int n = str2.length();

        // Length of both strings must be same for one to
        // one corresponance
        if (m != n)
            return false;

        // To mark visited characters in str2
        Boolean[] marked = new Boolean[size];
        Arrays.fill(marked, Boolean.FALSE);

        // To store mapping of every character from str1 to
        // that of str2\. Initialize all entries of map as
        // -1.
        int[] map = new int[size];
        Arrays.fill(map, -1);

        // Process all characters one by on
        for (int i = 0; i < n; i++) {
            // If current character of str1 is seen first
            // time in it.
            if (map[str1.charAt(i)] == -1) {
                // If current character of str2 is already
                // seen, one to one mapping not possible
                if (marked[str2.charAt(i)] == true)
                    return false;

                // Mark current character of str2 as visited
                marked[str2.charAt(i)] = true;

                // Store mapping of current characters
                map[str1.charAt(i)] = str2.charAt(i);
            }

            // If this is not first appearance of current
            // character in str1, then check if previous
            // appearance mapped to same character of str2
            else if (map[str1.charAt(i)] != str2.charAt(i))
                return false;
        }

        return true;
    }
    // driver program
    public static void main(String[] args)
    {
        boolean res = areIsomorphic("aab", "xxy");
        System.out.println(res);

        res = areIsomorphic("aab", "xyz");
        System.out.println(res);
    }
}
```

## 计算机编程语言

```
# Python program to check if two strings are isomorphic
MAX_CHARS = 256

# This function returns true if str1 and str2 are isomorphic

def areIsomorphic(string1, string2):
    m = len(string1)
    n = len(string2)

    # Length of both strings must be same for one to one
    # corresponance
    if m != n:
        return False

    # To mark visited characters in str2
    marked = [False] * MAX_CHARS

    # To store mapping of every character from str1 to
    # that of str2\. Initialize all entries of map as -1
    map = [-1] * MAX_CHARS

    # Process all characters one by one
    for i in xrange(n):

        # if current character of str1 is seen first
        # time in it.
        if map[ord(string1[i])] == -1:

            # if current character of st2 is already
            # seen, one to one mapping not possible
            if marked[ord(string2[i])] == True:
                return False

            # Mark current character of str2 as visited
            marked[ord(string2[i])] = True

            # Store mapping of current characters
            map[ord(string1[i])] = string2[i]

        # If this is not first appearance of current
        # character in str1, then check if previous
        # appearance mapped to same character of str2
        elif map[ord(string1[i])] != string2[i]:
            return False

    return True

# Driver program
print areIsomorphic("aab", "xxy")
print areIsomorphic("aab", "xyz")
# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to check if two
// strings are isomorphic
using System;

class GFG {

    static int size = 256;

    // Function returns true if str1
    // and str2 are isomorphic
    static bool areIsomorphic(String str1, String str2)
    {

        int m = str1.Length;
        int n = str2.Length;

        // Length of both strings must be same
        // for one to one corresponance
        if (m != n)
            return false;

        // To mark visited characters in str2
        bool[] marked = new bool[size];

        for (int i = 0; i < size; i++)
            marked[i] = false;

        // To store mapping of every character
        // from str1 to that of str2 and
        // Initialize all entries of map as -1.
        int[] map = new int[size];

        for (int i = 0; i < size; i++)
            map[i] = -1;

        // Process all characters one by on
        for (int i = 0; i < n; i++) {

            // If current character of str1 is
            // seen first time in it.
            if (map[str1[i]] == -1) {

                // If current character of str2
                // is already seen, one to
                // one mapping not possible
                if (marked[str2[i]] == true)
                    return false;

                // Mark current character of
                // str2 as visited
                marked[str2[i]] = true;

                // Store mapping of current characters
                map[str1[i]] = str2[i];
            }

            // If this is not first appearance of current
            // character in str1, then check if previous
            // appearance mapped to same character of str2
            else if (map[str1[i]] != str2[i])
                return false;
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        bool res = areIsomorphic("aab", "xxy");
        Console.WriteLine(res);

        res = areIsomorphic("aab", "xyz");
        Console.WriteLine(res);
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>
    // Javascript program to check if two
    // strings are isomorphic

    let size = 256;

    // Function returns true if str1
    // and str2 are isomorphic
    function areIsomorphic(str1, str2)
    {

        let m = str1.length;
        let n = str2.length;

        // Length of both strings must be same
        // for one to one corresponance
        if(m != n)
            return false;

        // To mark visited characters in str2
        let marked = new Array(size);

        for(let i = 0; i < size; i++)
            marked[i]= false;

        // To store mapping of every character
        // from str1 to that of str2 and
        // Initialize all entries of map as -1.
        let map = new Array(size);
        map.fill(0);

        for(let i = 0; i < size; i++)
            map[i]= -1;

        // Process all characters one by on
        for (let i = 0; i < n; i++)
        {

            // If current character of str1 is
            // seen first time in it.
            if (map[str1[i].charCodeAt()] == -1)
            {

                // If current character of str2
                // is already seen, one to
                // one mapping not possible
                if (marked[str2[i].charCodeAt()] == true)
                    return false;

                // Mark current character of
                // str2 as visited
                marked[str2[i].charCodeAt()] = true;

                // Store mapping of current characters
                map[str1[i].charCodeAt()] = str2[i].charCodeAt();
            }

            // If this is not first appearance of current
            // character in str1, then check if previous
            // appearance mapped to same character of str2
            else if (map[str1[i].charCodeAt()] != str2[i].charCodeAt())
                return 0;
        }

        return 1;
    }

    let res = areIsomorphic("aab", "xxy");
    document.write(res + "</br>");

    res = areIsomorphic("aab", "xyz");
    document.write(res);

    // This code is contributed by decode2207.
</script>
```

**输出:**

```
1
0
```

**另一种方法:**

1.  在这种方法中，我们将使用两个数组来计数两个字符串中特定字符的出现次数，同时我们将比较两个数组，如果在循环的任何时刻两个字符串中当前字符的计数变得不同，我们将返回 false，否则在循环结束后，我们将返回 true。
2.  遵循下面给出的代码，你会明白一切。

```
Note: There is no need to create here array of 256 characters. We can reduce it to only 26 characters 
by storing count of ch-'a' (ch is the ith character of the string)in count array .This gives the same 
result as string consists of only small case characters.
```

下面是上述想法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define MAX_CHARS 26

// This function returns true if
// str1 and str2 are isomorphic
bool areIsomorphic(string str1, string str2)
{
    int n = str1.length(), m = str2.length();

    // Length of both strings must be
    // same for one to one
    // correspondence
    if (n != m)
        return false;

    // For counting the previous appearances of character in
    // both the strings
    int count[MAX_CHARS] = { 0 };
    int dcount[MAX_CHARS] = { 0 };

    // Process all characters one by one
    for (int i = 0; i < n; i++) {
        count[str1[i] - 'a']++;
        dcount[str2[i] - 'a']++;

        // For string to be isomorphic the previous counts
        // of appearances of
        // current character in both string must be same if
        // it is not same we return false.
        if (count[str1[i] - 'a'] != dcount[str2[i] - 'a'])
            return false;
    }
    return true;
}

// Driver Code
int main()
{
    cout << areIsomorphic("aab", "xxy") << endl;
    cout << areIsomorphic("aab", "xyz") << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    static final int CHAR = 26;

    // This function returns true if
    // str1 and str2 are isomorphic
    static boolean isoMorphic(String str1, String str2)
    {
        int n = str1.length();
        int m = str2.length();

        // Length of both strings must be
        // same for one to one
        // correspondence
        if (n != m)
            return false;

        // For counting the previous appearances
        // of character in both the strings
        int[] countChars1 = new int[CHAR];
        int[] countChars2 = new int[CHAR];

        // Process all characters one by one
        for (int i = 0; i < n; i++) {
            countChars1[str1.charAt(i) - 'a']++;
            countChars2[str2.charAt(i) - 'a']++;

            // For string to be isomorphic the
            // previous counts of appearances of
            // current character in both string
            // must be same if it is not same we
            // return false.
            if (countChars1[str1.charAt(i) - 'a']
                != countChars2[str2.charAt(i) - 'a']) {
                return false;
            }
        }
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        System.out.println(isoMorphic("aab", "xxy") ? 1
                                                    : 0);
        System.out.println(isoMorphic("aab", "xyz") ? 1
                                                    : 0);
    }
}

// This code is contributed by rohansharma1808
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static int CHAR = 26;

    // This function returns true if
    // str1 and str2 are isomorphic
    static bool isoMorphic(string str1, string str2)
    {
        int n = str1.Length;
        int m = str2.Length;

        // Length of both strings must be
        // same for one to one
        // correspondence
        if (n != m)
            return false;

        // For counting the previous appearances
        // of character in both the strings
        int[] countChars1 = new int[CHAR];
        int[] countChars2 = new int[CHAR];

        // Process all characters one by one
        for (int i = 0; i < n; i++) {
            countChars1[str1[i] - 'a']++;
            countChars2[str2[i] - 'a']++;

            // For string to be isomorphic the
            // previous counts of appearances of
            // current character in both string
            // must be same if it is not same we
            // return false.
            if (countChars1[str1[i] - 'a']
                != countChars2[str2[i] - 'a']) {
                return false;
            }
        }
        return true;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        Console.WriteLine(isoMorphic("aab", "xxy") ? 1 : 0);
        Console.WriteLine(isoMorphic("aab", "xyz") ? 1 : 0);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>    
    // Javascript program for the above approach

    let CHAR = 26;

    // This function returns true if
    // str1 and str2 are isomorphic
    function isoMorphic(str1, str2)
    {
        let n = str1.length;
        let m = str2.length;

        // Length of both strings must be
        // same for one to one
        // correspondence
        if (n != m)
            return false;

        // For counting the previous appearances
        // of character in both the strings
        let countChars1 = new Array(CHAR);
        countChars1.fill(0);
        let countChars2 = new Array(CHAR);
        countChars2.fill(0);

        // Process all characters one by one
        for(let i = 0; i < n; i++)
        {
            countChars1[str1[i].charCodeAt()-'a']++;
            countChars2[str2[i].charCodeAt()-'a']++;

            // For string to be isomorphic the
            // previous counts of appearances of
            // current character in both string
            // must be same if it is not same we
            // return false.
            if (countChars1[str1[i].charCodeAt()-'a'] !=
                countChars2[str2[i].charCodeAt()-'a'])
            {
                return false;
            }
        }
        return true;
    }

    document.write(isoMorphic("aab", "xxy") ? 1 + "</br>" : 0 + "</br>");
    document.write(isoMorphic("aab", "xyz") ? 1 : 0);

</script>
```

**Output**

```
1
0
```

**时间复杂度:** O(n)

**另一种方法:**

1)在这种方法中，对于第一个和第二个字符串中的相应字符，我们将只使用单个字典作为键值对。

2)如果键重复，我们检查该值是否与各自的索引匹配。

## C#

```
// C# program to check if two strings
// areIsIsomorphic

using System;
using System.Collections.Generic;

public class GFG {

    static bool areIsomorphic(char[] str1, char[] str2)
    {

        Dictionary<char, char> charCount
            = new Dictionary<char, char>();
        char c = 'a';
        for (int i = 0; i < str1.Length; i++) {
            if (charCount.ContainsKey(str1[i])
                && charCount.TryGetValue(str1[i], out c)) {
                if (c != str2[i])
                    return false;
            }
            else if (!charCount.ContainsValue(str2[i])) {
                charCount.Add(str1[i], str2[i]);
            }
            else {
                return false;
            }
        }
        return true;
    }

    /* Driver code*/
    public static void Main()
    {

        string str1 = "aac";
        string str2 = "xxy";

        // Function Call
        if (str1.Length == str2.Length
            && areIsomorphic(str1.ToCharArray(),
                             str2.ToCharArray()))
            Console.WriteLine(1);
        else
            Console.WriteLine(0);

        Console.ReadLine();
    }
}
```

**Output**

```
1
```

感谢 Gaurav 和 Utkarsh 提出上述方法。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息