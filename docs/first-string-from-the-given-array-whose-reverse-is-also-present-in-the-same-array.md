# 给定数组中的第一个字符串，其反向也出现在同一数组中

> 原文:[https://www . geesforgeks . org/给定数组中的第一个字符串-其反向也存在于同一个数组中/](https://www.geeksforgeeks.org/first-string-from-the-given-array-whose-reverse-is-also-present-in-the-same-array/)

给定一个字符串数组 **str[]** ，任务是从给定数组中找到第一个字符串，该字符串的逆序也出现在同一数组中。如果没有这样的字符串，则打印 **-1** 。
**例:**

> **输入:** str[] = {“极客”、“for”、“skeg”}
> **输出:**极客
> “极客”是数组中第一个反向也出现在数组中的字符串，即“skeg”。
> **输入:** str[] = {“有”、“你”、“正在”}
> **输出:** -1

**方法:**逐元素遍历数组，对于每个字符串，检查数组中当前字符串之后是否有出现与其相反的字符串。如果是，则打印当前字符串，否则最后打印-1。
以下是上述办法的实施情况:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    // Function that returns true if s1
    // is equal to reverse of s2
    bool isReverseEqual(string s1, string s2)
    {

        // If both the strings differ in length
        if (s1.length() != s2.length())
            return false;

        int len = s1.length();
        for (int i = 0; i < len; i++)

            // In case of any character mismatch
            if (s1[i] != s2[len - i - 1])
                return false;

        return true;
    }

    // Function to return the first word whose
    // reverse is also present in the array
    string getWord(string str[], int n)
    {

        // Check every string
        for (int i = 0; i < n - 1; i++)

            // Pair with every other string
            // appearing after the current string
            for (int j = i + 1; j < n; j++)

                // If first string is equal to the
                // reverse of the second string
                if (isReverseEqual(str[i], str[j]))
                    return str[i];

        // No such string exists
        return "-1";
    }

    // Driver code
    int main()
    {
        string str[] = { "geeks", "for", "skeeg" };

        cout<<(getWord(str, 3));
    }

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true if s1
    // is equal to reverse of s2
    static boolean isReverseEqual(String s1, String s2)
    {

        // If both the strings differ in length
        if (s1.length() != s2.length())
            return false;

        int len = s1.length();
        for (int i = 0; i < len; i++)

            // In case of any character mismatch
            if (s1.charAt(i) != s2.charAt(len - i - 1))
                return false;

        return true;
    }

    // Function to return the first word whose
    // reverse is also present in the array
    static String getWord(String str[], int n)
    {

        // Check every string
        for (int i = 0; i < n - 1; i++)

            // Pair with every other string
            // appearing after the current string
            for (int j = i + 1; j < n; j++)

                // If first string is equal to the
                // reverse of the second string
                if (isReverseEqual(str[i], str[j]))
                    return str[i];

        // No such string exists
        return "-1";
    }

    // Driver code
    public static void main(String[] args)
    {
        String str[] = { "geeks", "for", "skeeg" };
        int n = str.length;

        System.out.print(getWord(str, n));
    }
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function that returns true if s1
# is equal to reverse of s2
def isReverseEqual(s1, s2):

    # If both the strings differ in length
    if len(s1) != len(s2):
        return False

    l = len(s1)

    for i in range(l):

        # In case of any character mismatch
        if s1[i] != s2[l-i-1]:
            return False
    return True

# Function to return the first word whose
# reverse is also present in the array
def getWord(str, n):

    # Check every string
    for i in range(n-1):

        # Pair with every other string
        # appearing after the current string
        for j in range(i+1, n):

            # If first string is equal to the
            # reverse of the second string
            if (isReverseEqual(str[i], str[j])):
                return str[i]

    # No such string exists
    return "-1"

# Driver code
if __name__ == "__main__":
    str = ["geeks", "for", "skeeg"]
    print(getWord(str, 3))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if s1
    // is equal to reverse of s2
    static bool isReverseEqual(String s1, String s2)
    {

        // If both the strings differ in length
        if (s1.Length != s2.Length)
            return false;

        int len = s1.Length;
        for (int i = 0; i < len; i++)

            // In case of any character mismatch
            if (s1[i] != s2[len - i - 1])
                return false;

        return true;
    }

    // Function to return the first word whose
    // reverse is also present in the array
    static String getWord(String []str, int n)
    {

        // Check every string
        for (int i = 0; i < n - 1; i++)

            // Pair with every other string
            // appearing after the current string
            for (int j = i + 1; j < n; j++)

                // If first string is equal to the
                // reverse of the second string
                if (isReverseEqual(str[i], str[j]))
                    return str[i];

        // No such string exists
        return "-1";
    }

    // Driver code
    public static void Main(String[] args)
    {
        String []str = { "geeks", "for", "skeeg" };
        int n = str.Length;

        Console.Write(getWord(str, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if s1
// is equal to reverse of s2
function isReverseEqual($s1, $s2)
{

    // If both the strings differ in length
    if (strlen($s1) != strlen($s2))
        return false;

    $len = strlen($s1);
    for ($i = 0; $i < $len; $i++)

        // In case of any character mismatch
        if ($s1[$i] != $s2[$len - $i - 1])
            return false;

    return true;
}

// Function to return the first word whose
// reverse is also present in the array
function getWord($str, $n)
{

    // Check every string
    for ($i = 0; $i < $n - 1; $i++)

        // Pair with every other string
        // appearing after the current string
        for ($j = $i + 1; $j < $n; $j++)

            // If first string is equal to the
            // reverse of the second string
            if (isReverseEqual($str[$i], $str[$j]))
                return $str[$i];

    // No such string exists
    return "-1";
}

// Driver code
$str = array( "geeks", "for", "skeeg" );
$n = count($str);

print(getWord($str, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

    // Function that returns true if s1
    // is equal to reverse of s2
    function isReverseEqual(s1, s2)
    {

        // If both the strings differ in length
        if (s1.length != s2.length)
            return false;

        let len = s1.length;
        for (let i = 0; i < len; i++)

            // In case of any character mismatch
            if (s1[i] != s2[len - i - 1])
                return false;

        return true;
    }

    // Function to return the first word whose
    // reverse is also present in the array
    function getWord(str, n)
    {

        // Check every string
        for (let i = 0; i < n - 1; i++)

            // Pair with every other string
            // appearing after the current string
            for (let j = i + 1; j < n; j++)

                // If first string is equal to the
                // reverse of the second string
                if (isReverseEqual(str[i], str[j]))
                    return str[i];

        // No such string exists
        return "-1";
    }

    // Driver code

        let str = [ "geeks", "for", "skeeg" ];

        document.write(getWord(str, 3));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
geeks
```

**高效进场:** O(n)进场。这种方法需要一个 Hashmap 来存储遍历的单词。当我们遍历时，如果在地图中找到当前单词的反义词，那么反义词就是第一个出现的答案。如果在遍历结束时没有找到，返回-1。
以下是上述办法的实施情况:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Method that returns first occurrence of revered word.
string getReversed(string words[], int length)
{

  // Hashmap to store word as we traverse
  map<string,bool> reversedWordMap;
  for(int i = 0; i < length; i++)
  {

    string reversedString = words[i];
    reverse(reversedString.begin(),reversedString.end());

    // check if reversed word exists in map.
    if (reversedWordMap.find(reversedString) !=
        reversedWordMap.end() and reversedWordMap[reversedString])
      return reversedString;
    else

      // else put the word in map
      reversedWordMap[words[i]] = true;
  }
  return "-1";
}

// Driver code
int main()
{
    string words[] = {"some", "geeks", "emos", "for", "skeeg"};
    int length = sizeof(words) / sizeof(words[0]);
    cout << getReversed(words, length);
    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;
import java.util.Map;

public class ReverseExist {

    // Driver Code
    public static void main(String[] args) {
        String[] words = {"some", "geeks", "emos", "for", "skeeg"};
        System.out.println(getReversed(words, words.length));
    }

    // Method that returns first occurrence of revered word.
    private static String getReversed(String[] words, int length) {

        // Hashmap to store word as we traverse
        Map<String, Boolean> reversedWordMap = new HashMap<>();

        for (String word : words) {
            StringBuilder reverse = new StringBuilder(word);
            String reversed = reverse.reverse().toString();

            // check if reversed word exists in map.
            Boolean exists = reversedWordMap.get(reversed);
            if (exists != null && exists.booleanValue()) {
                return reversed;
            } else {
                // else put the word in map
                reversedWordMap.put(word, true);
            }

        }
        return "-1";
    }
}
// Contributed by srika21m
```

## 蟒蛇 3

```
# Method that returns first occurrence of revered word.
def getReversed(words, length):

  # Hashmap to store word as we traverse
  reversedWordMap = {}
  for word in words:
    reversedString = word[::-1]

    # check if reversed word exists in map.
    if (reversedString in reversedWordMap and reversedWordMap[reversedString]):
      return reversedString
    else:

      # else put the word in map
      reversedWordMap[word] = True
  return "-1"

# Driver Code
if __name__ == "__main__":
  words = ["some", "geeks", "emos", "for", "skeeg"]
  print(getReversed(words, len(words)))

  # This code is contributed by chitranayal
```

## C#

```
using System;
using System.Collections.Generic;
class GFG
{

    // Method that returns first occurrence of revered word.
    static string getReversed(string[] words, int length)
    {

      // Hashmap to store word as we traverse
      Dictionary<string, bool> reversedWordMap =
        new Dictionary<string, bool>();
      for(int i = 0; i < length; i++)
      {

        char[] reversedString = words[i].ToCharArray();
        Array.Reverse(reversedString);

        // check if reversed word exists in map.
        if (reversedWordMap.ContainsKey(new string(reversedString)) &&
            reversedWordMap[new string(reversedString)])
          return new string(reversedString);
        else

          // else put the word in map
          reversedWordMap[words[i]] = true;
      }
      return "-1";
    }

  // Driver code
  static void Main()
  {
    string[] words = {"some", "geeks", "emos", "for", "skeeg"};
    int length = words.Length;
    Console.Write(getReversed(words, length));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Method that returns first occurrence of revered word.
function  getReversed(words,length)
{
    // Hashmap to store word as we traverse
        let reversedWordMap = new Map();

        for (let word=0;word<words.length;word++) {
            let reverse = words[word].split("");
            let reversed = reverse.reverse().join("");

            if (reversedWordMap.has(reversed) &&
            reversedWordMap.get(reversed))
                  return reversed;
            else

                  // else put the word in map
                  reversedWordMap.set(words[word] , true);

        }
        return "-1";
}

// Driver code
let words=["some", "geeks", "emos", "for", "skeeg"];
document.write(getReversed(words, words.length));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
some
```