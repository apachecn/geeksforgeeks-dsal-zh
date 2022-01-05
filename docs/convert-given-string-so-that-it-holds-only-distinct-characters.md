# 转换给定的字符串，使其只包含不同的字符

> 原文:[https://www . geeksforgeeks . org/convert-given-string-so-it-hold-only-distinct-characters/](https://www.geeksforgeeks.org/convert-given-string-so-that-it-holds-only-distinct-characters/)

给定一个由小写英文字母组成的字符串 **str** ，任务是转换该字符串，使其只包含不同的字符。字符串的任何字符都可以被任何其他小写字符替换(替换次数必须最少)。打印修改后的字符串。
**例:**

> **输入:**str = " geeksforgeks "
> **输出:**abcdforgieks
> **输入:**str = " bbcagagkkk "
> **输出:**dbefaghik

**方法:**如果字符串的长度 **> 26** 那么字符串不可能有所有不同的字符。
否则，计算字符串中每个字符的出现次数，对于出现多次的字符，用字符串中尚未出现的字符替换它们。最后打印修改后的字符串。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    // Function to return the index of the character
    // that has 0 occurrence starting from index i
    int nextZero(int i, int occurrences[])
    {
        while (i < 26)
        {

            // If current character has 0 occurrence
            if (occurrences[i] == 0)
                return i;
            i++;
        }

        // If no character has 0 occurrence
        return -1;
    }

    // Function to return the modified string
    // which consists of distinct characters
    string getModifiedString(string str)
    {

        int n = str.length();

        // String cannot consist of
        // all distinct characters
        if (n > 26)
            return "-1";

        string ch = str;

        int i, occurrences[26] = {0};

        // Count the occurrences for
        // each of the character
        for (i = 0; i < n; i++)
            occurrences[ch[i] - 'a']++;

        // Index for the first character
        // that hasn't appeared in the string
        int index = nextZero(0, occurrences);
        for (i = 0; i < n; i++)
        {

            // If current character appeared more
            // than once then it has to be replaced
            // with some character that
            // hasn't occurred yet
            if (occurrences[ch[i] - 'a'] > 1)
            {

                // Decrement current character's occurrence by 1
                occurrences[ch[i] - 'a']--;

                // Replace the character
                ch[i] = (char)('a' + index);

                // Update the new character's occurrence
                // This step can also be skipped as
                // we'll never encounter this character
                // in the string because it has
                //  been added just now
                occurrences[index] = 1;

                // Find the next character that hasn't occurred yet
                index = nextZero(index + 1, occurrences);
            }
        }
    cout << ch << endl;
    }

    // Driver code
    int main()
    {
        string str = "geeksforgeeks";
        getModifiedString(str);
    }

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the index of the character
    // that has 0 occurrence starting from index i
    static int nextZero(int i, int occurrences[])
    {
        while (i < occurrences.length) {

            // If current character has 0 occurrence
            if (occurrences[i] == 0)
                return i;
            i++;
        }

        // If no character has 0 occurrence
        return -1;
    }

    // Function to return the modified string
    // which consists of distinct characters
    static String getModifiedString(String str)
    {

        int n = str.length();

        // String cannot consist of all distinct characters
        if (n > 26)
            return "-1";

        char ch[] = str.toCharArray();

        int i, occurrences[] = new int[26];

        // Count the occurrences for each of the character
        for (i = 0; i < n; i++)
            occurrences[ch[i] - 'a']++;

        // Index for the first character
        // that hasn't appeared in the string
        int index = nextZero(0, occurrences);
        for (i = 0; i < n; i++) {

            // If current character appeared more than once then
            // it has to be replaced with some character
            // that hasn't occurred yet
            if (occurrences[ch[i] - 'a'] > 1) {

                // Decrement current character's occurrence by 1
                occurrences[ch[i] - 'a']--;

                // Replace the character
                ch[i] = (char)('a' + index);

                // Update the new character's occurrence
                // This step can also be skipped as we'll never encounter
                // this character in the string because
                // it has been added just now
                occurrences[index] = 1;

                // Find the next character that hasn't occurred yet
                index = nextZero(index + 1, occurrences);
            }
        }

        // Return the modified string
        return String.valueOf(ch);
    }

    // Driver code
    public static void main(String arr[])
    {
        String str = "geeksforgeeks";
        System.out.print(getModifiedString(str));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the index of the character
# that has 0 occurrence starting from index i
def nextZero(i, occurrences):
    while i < 26:

        # If current character has 0 occurrence
        if occurrences[i] == 0:
            return i
        i += 1

    # If no character has 0 occurrence
    return -1

# Function to return the modified string
# which consists of distinct characters
def getModifiedString(str):
    n = len(str)

    # String cannot consist of
    # all distinct characters
    if n > 26:
        return "-1"

    ch = str
    ch = list(ch)
    occurrences = [0] * 26

    # Count the occurrences for
    # each of the character
    for i in range(n):
        occurrences[ord(ch[i]) - ord('a')] += 1

    # Index for the first character
    # that hasn't appeared in the string
    index = nextZero(0, occurrences)

    for i in range(n):

        # If current character appeared more
        # than once then it has to be replaced
        # with some character that
        # hasn't occurred yet
        if occurrences[ord(ch[i]) - ord('a')] > 1:

            # Decrement current character's occurrence by 1
            occurrences[ord(ch[i]) - ord('a')] -= 1

            # Replace the character
            ch[i] = chr(ord('a') + index)

            # Update the new character's occurrence
            # This step can also be skipped as
            # we'll never encounter this character
            # in the string because it has
            # been added just now
            occurrences[index] = 1

            # Find the next character
            # that hasn't occurred yet
            index = nextZero(index + 1, occurrences)

    ch = ''.join(ch)
    print(ch)

# Driver code
if __name__ == "__main__":
    str = "geeksforgeeks"
    getModifiedString(str)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the index of the character
    // that has 0 occurrence starting from index i
    static int nextZero(int i, int []occurrences)
    {
        while (i < occurrences.Length)
        {

            // If current character has 0 occurrence
            if (occurrences[i] == 0)
                return i;
            i++;
        }

        // If no character has 0 occurrence
        return -1;
    }

    // Function to return the modified string
    // which consists of distinct characters
    static string getModifiedString(string str)
    {

        int n = str.Length ;

        // String cannot consist of all distinct characters
        if (n > 26)
            return "-1";

        char []ch = str.ToCharArray();
        int []occurrences = new int[26];
        int i ;

        // Count the occurrences for each of the character
        for (i = 0; i < n; i++)
            occurrences[ch[i] - 'a']++;

        // Index for the first character
        // that hasn't appeared in the string
        int index = nextZero(0, occurrences);
        for (i = 0; i < n; i++)
        {

            // If current character appeared more than 
            // once then it has to be replaced with some 
            // character that hasn't occurred yet
            if (occurrences[ch[i] - 'a'] > 1)
            {

                // Decrement current character's occurrence by 1
                occurrences[ch[i] - 'a']--;

                // Replace the character
                ch[i] = (char)('a' + index);

                // Update the new character's occurrence
                // This step can also be skipped
                // as we'll never encounter
                // this character in the string because
                // it has been added just now
                occurrences[index] = 1;

                // Find the next character that hasn't occurred yet
                index = nextZero(index + 1, occurrences);
            }
        }

        string s = new string(ch) ;

        // Return the modified string
        return s ;
    }

    // Driver code
    public static void Main()
    {
        string str = "geeksforgeeks";
        Console.WriteLine(getModifiedString(str));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the index of the character
    // that has 0 occurrence starting from index i
    function nextZero(i, occurrences)
    {
        while (i < occurrences.length)
        {

            // If current character has 0 occurrence
            if (occurrences[i] == 0)
                return i;
            i++;
        }

        // If no character has 0 occurrence
        return -1;
    }

    // Function to return the modified string
    // which consists of distinct characters
    function getModifiedString(str)
    {

        let n = str.length ;

        // String cannot consist of all distinct characters
        if (n > 26)
            return "-1";

        let ch = str.split('');
        let occurrences = new Array(26);
        occurrences.fill(0);
        let i ;

        // Count the occurrences for each of the character
        for (i = 0; i < n; i++)
            occurrences[ch[i].charCodeAt() - 'a'.charCodeAt()]++;

        // Index for the first character
        // that hasn't appeared in the string
        let index = nextZero(0, occurrences);
        for (i = 0; i < n; i++)
        {

            // If current character appeared more than 
            // once then it has to be replaced with some 
            // character that hasn't occurred yet
            if (occurrences[ch[i].charCodeAt() - 'a'.charCodeAt()] > 1)
            {

                // Decrement current character's occurrence by 1
                occurrences[ch[i].charCodeAt() - 'a'.charCodeAt()]--;

                // Replace the character
                ch[i] = String.fromCharCode('a'.charCodeAt() + index);

                // Update the new character's occurrence
                // This step can also be skipped
                // as we'll never encounter
                // this character in the string because
                // it has been added just now
                occurrences[index] = 1;

                // Find the next character that hasn't occurred yet
                index = nextZero(index + 1, occurrences);
            }
        }

        let s = ch.join("");

        // Return the modified string
        return s ;
    }

    let str = "geeksforgeeks";
      document.write(getModifiedString(str));

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
abcdhforgieks
```