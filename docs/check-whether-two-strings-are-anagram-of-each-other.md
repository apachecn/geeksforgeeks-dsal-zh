# 检查两个字符串是否是彼此的字谜

> 原文:[https://www . geeksforgeeks . org/check-two-string-is-anagram-of-other/](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)

写一个函数检查两个给定的字符串是否是彼此的[字谜](http://en.wikipedia.org/wiki/Anagram)。字符串的字谜是另一个包含相同字符的字符串，只有字符的顺序可以不同。例如，“abcd”和“dabc”是彼此的字谜。

![check-whether-two-strings-are-anagram-of-each-other](img/44eca765d93a8501e9332cab7ddb74ba.png)

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/anagram-1587115620/1)

**方法 1(使用排序)**

1.  对两个字符串进行排序
2.  比较排序后的字符串

下面是上述想法的实现:

## C++

```
// C++ program to check whether two strings are anagrams
// of each other
#include <bits/stdc++.h>
using namespace std;

/* function to check whether two strings are anagram of
each other */
bool areAnagram(string str1, string str2)
{
    // Get lengths of both strings
    int n1 = str1.length();
    int n2 = str2.length();

    // If length of both strings is not same, then they
    // cannot be anagram
    if (n1 != n2)
        return false;

    // Sort both the strings
    sort(str1.begin(), str1.end());
    sort(str2.begin(), str2.end());

    // Compare sorted strings
    for (int i = 0; i < n1; i++)
        if (str1[i] != str2[i])
            return false;

    return true;
}

// Driver code
int main()
{
    string str1 = "test";
    string str2 = "ttew";

    // Function Call
    if (areAnagram(str1, str2))
        cout << "The two strings are anagram of each other";
    else
        cout << "The two strings are not anagram of each "
                "other";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check whether two strings
// are anagrams of each other
import java.io.*;
import java.util.Arrays;
import java.util.Collections;

class GFG {

    /* function to check whether two strings are
    anagram of each other */
    static boolean areAnagram(char[] str1, char[] str2)
    {
        // Get lengths of both strings
        int n1 = str1.length;
        int n2 = str2.length;

        // If length of both strings is not same,
        // then they cannot be anagram
        if (n1 != n2)
            return false;

        // Sort both strings
        Arrays.sort(str1);
        Arrays.sort(str2);

        // Compare sorted strings
        for (int i = 0; i < n1; i++)
            if (str1[i] != str2[i])
                return false;

        return true;
    }

    /* Driver Code*/
    public static void main(String args[])
    {
        char str1[] = { 't', 'e', 's', 't' };
        char str2[] = { 't', 't', 'e', 'w' };

        // Function Call
        if (areAnagram(str1, str2))
            System.out.println("The two strings are"
                               + " anagram of each other");
        else
            System.out.println("The two strings are not"
                               + " anagram of each other");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to check whether two strings are
# anagrams of each other

# function to check whether two strings are anagram
# of each other

def areAnagram(str1, str2):
    # Get lengths of both strings
    n1 = len(str1)
    n2 = len(str2)

    # If length of both strings is not same, then
    # they cannot be anagram
    if n1 != n2:
        return 0

    # Sort both strings
    str1 = sorted(str1)
    str2 = sorted(str2)

    # Compare sorted strings
    for i in range(0, n1):
        if str1[i] != str2[i]:
            return 0

    return 1

# Driver code
str1 = "test"
str2 = "ttew"

# Function Call
if areAnagram(str1, str2):
    print("The two strings are anagram of each other")
else:
    print("The two strings are not anagram of each other")

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to check whether two
// strings are anagrams of each other
using System;
using System.Collections;
class GFG {

    /* function to check whether two
strings are anagram of each other */
    public static bool areAnagram(ArrayList str1,
                                  ArrayList str2)
    {
        // Get lengths of both strings
        int n1 = str1.Count;
        int n2 = str2.Count;

        // If length of both strings is not
        // same, then they cannot be anagram
        if (n1 != n2) {
            return false;
        }

        // Sort both strings
        str1.Sort();
        str2.Sort();

        // Compare sorted strings
        for (int i = 0; i < n1; i++) {
            if (str1[i] != str2[i]) {
                return false;
            }
        }

        return true;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // create and initialize new ArrayList
        ArrayList str1 = new ArrayList();
        str1.Add('t');
        str1.Add('e');
        str1.Add('s');
        str1.Add('t');
        // create and initialize new ArrayList
        ArrayList str2 = new ArrayList();
        str2.Add('t');
        str2.Add('t');
        str2.Add('e');
        str2.Add('w');

        // Function call
        if (areAnagram(str1, str2)) {
            Console.WriteLine("The two strings are"
                              + " anagram of each other");
        }
        else {
            Console.WriteLine("The two strings are not"
                              + " anagram of each other");
        }
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to check whether two strings
// are anagrams of each other

    /* function to check whether two strings are
    anagram of each other */
    function areAnagram(str1,str2)
    {
        // Get lengths of both strings
        let n1 = str1.length;
        let n2 = str2.length;

        // If length of both strings is not same,
        // then they cannot be anagram
        if (n1 != n2)
            return false;

        // Sort both strings
        str1.sort();
        str2.sort()

        // Compare sorted strings
        for (let i = 0; i < n1; i++)
            if (str1[i] != str2[i])
                return false;

        return true;
    }

    /* Driver Code*/
    let str1=['t', 'e', 's', 't' ];
    let str2=['t', 't', 'e', 'w' ];

    // Function Call
        if (areAnagram(str1, str2))
            document.write("The two strings are"
                               + " anagram of each other<br>");
        else
            document.write("The two strings are not"
                               + " anagram of each other<br>");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
The two strings are not anagram of each other
```

**时间复杂度:** O(nLogn)

**方法 2(计数字符)**
该方法假设两个字符串中可能的字符集都很小。在下面的实现中，假设使用 8 位存储字符，并且可能有 256 个字符。

1.  为两个字符串创建大小为 256 的计数数组。将计数数组中的所有值初始化为 0。
2.  遍历两个字符串的每个字符，并增加相应计数数组中的字符数。
3.  比较计数数组。如果两个计数数组相同，则返回 true。

下面是上述想法的实现:

## C++

```
// C++ program to check if two strings
// are anagrams of each other
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

/* function to check whether two strings are anagram of
each other */
bool areAnagram(char* str1, char* str2)
{
    // Create 2 count arrays and initialize all values as 0
    int count1[NO_OF_CHARS] = { 0 };
    int count2[NO_OF_CHARS] = { 0 };
    int i;

    // For each character in input strings, increment count
    // in the corresponding count array
    for (i = 0; str1[i] && str2[i]; i++) {
        count1[str1[i]]++;
        count2[str2[i]]++;
    }

    // If both strings are of different length. Removing
    // this condition will make the program fail for strings
    // like "aaca" and "aca"
    if (str1[i] || str2[i])
        return false;

    // Compare count arrays
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count1[i] != count2[i])
            return false;

    return true;
}

/* Driver code*/
int main()
{
    char str1[] = "geeksforgeeks";
    char str2[] = "forgeeksgeeks";

    // Function Call
    if (areAnagram(str1, str2))
        cout << "The two strings are anagram of each other";
    else
        cout << "The two strings are not anagram of each "
                "other";

    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// C program to check if two strings
// are anagrams of each other
#include <stdio.h>
#define NO_OF_CHARS 256

/* function to check whether two strings are anagram of
   each other */
bool areAnagram(char* str1, char* str2)
{
    // Create 2 count arrays and initialize all values as 0
    int count1[NO_OF_CHARS] = { 0 };
    int count2[NO_OF_CHARS] = { 0 };
    int i;

    // For each character in input strings, increment count
    // in the corresponding count array
    for (i = 0; str1[i] && str2[i]; i++) {
        count1[str1[i]]++;
        count2[str2[i]]++;
    }

    // If both strings are of different length. Removing
    // this condition will make the program fail for strings
    // like "aaca" and "aca"
    if (str1[i] || str2[i])
        return false;

    // Compare count arrays
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count1[i] != count2[i])
            return false;

    return true;
}

/* Driver code*/
int main()
{
    char str1[] = "geeksforgeeks";
    char str2[] = "forgeeksgeeks";

    // Function Call
    if (areAnagram(str1, str2))
        printf("The two strings are anagram of each other");
    else
        printf("The two strings are not anagram of each "
               "other");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if two strings
// are anagrams of each other
import java.io.*;
import java.util.*;

class GFG {

    static int NO_OF_CHARS = 256;

    /* function to check whether two strings
    are anagram of each other */
    static boolean areAnagram(char str1[], char str2[])
    {
        // Create 2 count arrays and initialize
        // all values as 0
        int count1[] = new int[NO_OF_CHARS];
        Arrays.fill(count1, 0);
        int count2[] = new int[NO_OF_CHARS];
        Arrays.fill(count2, 0);
        int i;

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (i = 0; i < str1.length && i < str2.length;
             i++) {
            count1[str1[i]]++;
            count2[str2[i]]++;
        }

        // If both strings are of different length.
        // Removing this condition will make the program
        // fail for strings like "aaca" and "aca"
        if (str1.length != str2.length)
            return false;

        // Compare count arrays
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }

    /* Driver code*/
    public static void main(String args[])
    {
        char str1[] = ("geeksforgeeks").toCharArray();
        char str2[] = ("forgeeksgeeks").toCharArray();

        // Function call
        if (areAnagram(str1, str2))
            System.out.println("The two strings are"
                               + "anagram of each other");
        else
            System.out.println("The two strings are not"
                               + " anagram of each other");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to check if two strings are anagrams of
# each other
NO_OF_CHARS = 256

# Function to check whether two strings are anagram of
# each other

def areAnagram(str1, str2):

    # Create two count arrays and initialize all values as 0
    count1 = [0] * NO_OF_CHARS
    count2 = [0] * NO_OF_CHARS

    # For each character in input strings, increment count
    # in the corresponding count array
    for i in str1:
        count1[ord(i)] += 1

    for i in str2:
        count2[ord(i)] += 1

    # If both strings are of different length. Removing this
    # condition will make the program fail for strings like
    # "aaca" and "aca"
    if len(str1) != len(str2):
        return 0

    # Compare count arrays
    for i in xrange(NO_OF_CHARS):
        if count1[i] != count2[i]:
            return 0

    return 1

# Driver code
str1 = "geeksforgeeks"
str2 = "forgeeksgeeks"

# Function call
if areAnagram(str1, str2):
    print "The two strings are anagram of each other"
else:
    print "The two strings are not anagram of each other"

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to check if two strings
// are anagrams of each other

using System;

public class GFG {

    static int NO_OF_CHARS = 256;

    /* function to check whether two strings
    are anagram of each other */
    static bool areAnagram(char[] str1, char[] str2)
    {
        // Create 2 count arrays and initialize
        // all values as 0
        int[] count1 = new int[NO_OF_CHARS];
        int[] count2 = new int[NO_OF_CHARS];
        int i;

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (i = 0; i < str1.Length && i < str2.Length;
             i++) {
            count1[str1[i]]++;
            count2[str2[i]]++;
        }

        // If both strings are of different length.
        // Removing this condition will make the program
        // fail for strings like "aaca" and "aca"
        if (str1.Length != str2.Length)
            return false;

        // Compare count arrays
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }

    /* Driver code*/
    public static void Main()
    {
        char[] str1 = ("geeksforgeeks").ToCharArray();
        char[] str2 = ("forgeeksgeeks").ToCharArray();

        // Function Call
        if (areAnagram(str1, str2))
            Console.WriteLine("The two strings are"
                              + "anagram of each other");
        else
            Console.WriteLine("The two strings are not"
                              + " anagram of each other");
    }
}

// This code contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JAVAscript program to check if two strings
// are anagrams of each other

let NO_OF_CHARS = 256;

/* function to check whether two strings
    are anagram of each other */
function areAnagram(str1, str2)
{

    // Create 2 count arrays and initialize
        // all values as 0
        let count1 = new Array(NO_OF_CHARS);
        let count2 = new Array(NO_OF_CHARS);
        for(let i = 0; i < NO_OF_CHARS; i++)
        {
            count1[i] = 0;
            count2[i] = 0;
        }

        let i;

        // For each character in input strings,
        // increment count in the corresponding
        // count array
        for (i = 0; i < str1.length && i < str2.length;
             i++) {
            count1[str1[i].charCodeAt(0)]++;
            count2[str1[i].charCodeAt(0)]++;
        }

        // If both strings are of different length.
        // Removing this condition will make the program
        // fail for strings like "aaca" and "aca"
        if (str1.length != str2.length)
            return false;

        // Compare count arrays
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
}

/* Driver code*/
let str1 = ("geeksforgeeks").split("");
        let str2 = ("forgeeksgeeks").split("");

        // Function call
        if (areAnagram(str1, str2))
            document.write("The two strings are"
                               + "anagram of each other<br>");
        else
            document.write("The two strings are not"
                               + " anagram of each other<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
The two strings are anagram of each other
```

**方法 3(用一个数组计数字符)**
上面的实现可以进一步用一个计数数组代替两个。我们可以在 str1 中增加字符计数数组中的值，在 str2 中减少字符计数数组中的值。最后，如果所有计数值都是 0，那么这两个字符串就是彼此的字谜。感谢**高手**提出这个优化。

## C++

```
// C++ program to check if two strings
// are anagrams of each other
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

bool areAnagram(char* str1, char* str2)
{
    // Create a count array and initialize all values as 0
    int count[NO_OF_CHARS] = { 0 };
    int i;

    // For each character in input strings, increment count
    // in the corresponding count array
    for (i = 0; str1[i] && str2[i]; i++) {
        count[str1[i]]++;
        count[str2[i]]--;
    }

    // If both strings are of different length. Removing
    // this condition will make the program fail for strings
    // like "aaca" and "aca"
    if (str1[i] || str2[i])
        return false;

    // See if there is any non-zero value in count array
    for (i = 0; i < NO_OF_CHARS; i++)
        if (count[i])
            return false;
    return true;
}

// Driver code
int main()
{
    char str1[] = "geeksforgeeks";
    char str2[] = "forgeeksgeeks";

    // Function call
    if (areAnagram(str1, str2))
        cout << "The two strings are anagram of each other";
    else
        cout << "The two strings are not anagram of each "
                "other";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two strings
// are anagrams of each other
class GFG{

static int NO_OF_CHARS = 256;

// function to check if two strings
// are anagrams of each other
static boolean areAnagram(char[] str1,
                          char[] str2)
{

    // Create a count array and initialize
    // all values as 0
    int[] count = new int[NO_OF_CHARS];
    int i;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for(i = 0; i < str1.length; i++)
    {
        count[str1[i] - 'a']++;
        count[str2[i] - 'a']--;
    }

    // If both strings are of different
    // length. Removing this condition
    // will make the program fail for
    // strings like "aaca" and "aca"
    if (str1.length != str2.length)
        return false;

    // See if there is any non-zero
    // value in count array
    for(i = 0; i < NO_OF_CHARS; i++)
        if (count[i] != 0)
        {
            return false;
        }
    return true;
}

// Driver code
public static void main(String[] args)
{
    char str1[] = "geeksforgeeks".toCharArray();
    char str2[] = "forgeeksgeeks".toCharArray();

    // Function call
    if (areAnagram(str1, str2))
        System.out.print("The two strings are " +
                         "anagram of each other");
    else
        System.out.print("The two strings are " +
                         "not anagram of each other");
}
}

// This code is contributed by mark_85
```

## 蟒蛇 3

```
# Python program to check if two strings
# are anagrams of each other

NO_OF_CHARS = 256

# function to check if two strings
# are anagrams of each other
def areAnagram(str1,str2):

    # Create a count array and initialize
    # all values as 0
    count=[0 for i in range(NO_OF_CHARS)]
    i=0

    # For each character in input strings,
    # increment count in the corresponding
    # count array
    for i in range(len(str1)):
        count[ord(str1[i]) - ord('a')] += 1;
        count[ord(str2[i]) - ord('a')] -= 1;

    # If both strings are of different
    # length. Removing this condition
    # will make the program fail for
    # strings like "aaca" and "aca"   
    if(len(str1) != len(str2)):
        return False;

    # See if there is any non-zero
    # value in count array
    for i in range(NO_OF_CHARS):
        if (count[i] != 0):
            return False

    return True

# Driver code
str1="geeksforgeeks"
str2="forgeeksgeeks"

# Function call
if (areAnagram(str1, str2)):
    print("The two strings are anagram of each other")
else:
    print("The two strings are not anagram of each other")

# This code is contributed by patel2127
```

## C#

```
// C# program to check if two strings
// are anagrams of each other
using System;

class GFG{

static int NO_OF_CHARS = 256;

// function to check if two strings
// are anagrams of each other
static bool areAnagram(char[] str1,
                       char[] str2)
{

    // Create a count array and initialize
    // all values as 0
    int[] count = new int[NO_OF_CHARS];
    int i;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for(i = 0; i < str1.Length; i++)
    {
        count[str1[i] - 'a']++;
        count[str2[i] - 'a']--;
    }

    // If both strings are of different
    // Length. Removing this condition
    // will make the program fail for
    // strings like "aaca" and "aca"
    if (str1.Length != str2.Length)
        return false;

    // See if there is any non-zero
    // value in count array
    for(i = 0; i < NO_OF_CHARS; i++)
        if (count[i] != 0)
        {
            return false;
        }

    return true;
}

// Driver code
public static void Main(String []args)
{
    char []str1 = "geeksforgeeks".ToCharArray();
    char []str2 = "forgeeksgeeks".ToCharArray();

    // Function call
    if (areAnagram(str1, str2))
       Console.Write("The two strings are " +
                     "anagram of each other");
    else
       Console.Write("The two strings are " +
                     "not anagram of each other");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program to check if two strings
// are anagrams of each other
let NO_OF_CHARS = 256;

// function to check if two strings
// are anagrams of each other
function areAnagram(str1, str2)
{

    // Create a count array and initialize
    // all values as 0
    let count = new Array(NO_OF_CHARS);
    for(let i = 0; i < NO_OF_CHARS; i++)
    {
        count[i] = 0;
    }
    let i;

    // For each character in input strings,
    // increment count in the corresponding
    // count array
    for(i = 0; i < str1.length; i++)
    {
        count[str1[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        count[str2[i].charCodeAt(0) - 'a'.charCodeAt(0)]--;
    }

    // If both strings are of different
    // length. Removing this condition
    // will make the program fail for
    // strings like "aaca" and "aca"
    if (str1.length != str2.length)
        return false;

    // See if there is any non-zero
    // value in count array
    for(i = 0; i < NO_OF_CHARS; i++)
        if (count[i] != 0)
        {
            return false;
        }
    return true;
}

// Driver code
let str1 = "geeksforgeeks".split("");
let str2 = "forgeeksgeeks".split("");

// Function call
if (areAnagram(str1, str2))
    document.write("The two strings are " +
                 "anagram of each other");
else
    document.write("The two strings are " +
                 "not anagram of each other");

// This code is contributed by unknown2108.
</script>
```

**Output:** 

```
The two strings are anagram of each other
```

**时间复杂度:** O(n)

**方法 4(将所有字符放入 HashMap)**

在上面的实现中，我们使用额外的空间来创建 256 个字符的数组，但是我们可以使用 HashMap 来优化它，在 HashMap 中我们可以存储字符和字符计数。想法是将一个字符串的所有字符放在 HashMap 中，并在遍历其他字符串时减少它们。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;

class GFG {
    public static boolean isAnagram(String a, String b)
    {
        // Check if length of both strings is same or not
        if (a.length() != b.length()) {
            return false;
        }
        // Create a HashMap containing Character as Key and
        // Integer as Value. We will be storing character as
        // Key and count of character as Value.
        HashMap<Character, Integer> map = new HashMap<>();
        // Loop over all character of String a and put in
        // HashMap.
        for (int i = 0; i < a.length(); i++) {
            // Check if HashMap already contain current
            // character or not
            if (map.containsKey(a.charAt(i))) {
                // If contains increase count by 1 for that
                // character
                map.put(a.charAt(i),
                        map.get(a.charAt(i)) + 1);
            }
            else {
                // else put that character in map and set
                // count to 1 as character is encountered
                // first time
                map.put(a.charAt(i), 1);
            }
        }
        // Now loop over String b
        for (int i = 0; i < b.length(); i++) {
            // Check if current character already exists in
            // HashMap/map
            if (map.containsKey(b.charAt(i))) {
                // If contains reduce count of that
                // character by 1 to indicate that current
                // character has been already counted as
                // idea here is to check if in last count of
                // all characters in last is zero which
                // means all characters in String a are
                // present in String b.
                map.put(b.charAt(i),
                        map.get(b.charAt(i)) - 1);
            }
        }
        // Extract all keys of HashMap/map
        Set<Character> keys = map.keySet();
        // Loop over all keys and check if all keys are 0.
        // If so it means it is anagram.
        for (Character key : keys) {
            if (map.get(key) != 0) {
                return false;
            }
        }
        // Returning True as all keys are zero
        return true;
    }
    public static void main(String[] args)
    {
        String str1 = "geeksforgeeks";
        String str2 = "forgeeksgeeks";

        // Function call
        if (isAnagram(str1, str2))
            System.out.print("The two strings are "
                             + "anagram of each other");
        else
            System.out.print("The two strings are "
                             + "not anagram of each other");
    }
}
```

**输出:**

```
The two strings are anagram of each other
```

**时间复杂度:** O(n)

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。