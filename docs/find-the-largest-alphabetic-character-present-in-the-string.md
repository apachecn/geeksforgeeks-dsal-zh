# 找到字符串中最大的字母字符

> 原文:[https://www . geesforgeks . org/find-字符串中最大的字母字符/](https://www.geeksforgeeks.org/find-the-largest-alphabetic-character-present-in-the-string/)

给定一个**字符串**，我们的任务是**找到最大的字母字符**，它的大写和小写都出现在字符串中。应该返回大写字符。如果没有这样的字符，则返回-1，否则打印该字符的大写字母。

**示例:**

> **输入:** str = "admeDCAB"
> **输出:** D
> **解释:**
> 字母 D 的大小写字母都存在于字符串中，也是最大的字母字符，因此我们的输出是 D。
> 
> **输入:** str = "dAeB"
> **输出:** -1
> **解释:**
> 虽然字符串中最大的字符是 d，但大写版本不存在，因此输出为-1。

**幼稚方法:**为了解决上述问题，幼稚方法是检查字符串中每个字符是否存在大写或小写字符，也就是说**对于字母 A，字符串中应该存在“A”和“A”。如果存在这样的字母，那么将跟踪该字符，并且仅当当前字符大于先前选择的字符时才更新。这种方法在最坏的情况下需要 O(n <sup>2</sup> )时间，可以进一步优化。**

**高效方法:**为了优化上述方法，我们使用了英语字母表中有 26 个字符的事实，我们可以通过维护大小为 26 的数组来跟踪小写和大写字符。当遍历给定字符串时，如果当前字符同时以大写和小写字母出现，我们将在两个数组中标记**为真。标记了各个数组中的所有字符后，我们将运行一个从 25 到 0 的循环，并检查两个数组中是否都标记了“真”。如果是，那么我们打印该字符的大写字母，否则返回-1。**

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find the Largest Alphabetic
// Character present in the string of both
// uppercase and lowercase English characters

public class Main {

    // Function to find the Largest Alphabetic Character
    public static String largestCharacter(String str)
    {
        // Array for keeping track of both uppercase
        // and lowercase english alphabets
        boolean[] uppercase = new boolean[26];
        boolean[] lowercase = new boolean[26];

        char[] arr = str.toCharArray();

        for (char c : arr) {

            if (Character.isLowerCase(c))
                lowercase = true;

            if (Character.isUpperCase(c))
                uppercase = true;
        }

        // Iterate from right side of array
        // to get the largest index character
        for (int i = 25; i >= 0; i--) {

            // Check for the character if both its
            // uppercase and lowercase exist or not
            if (uppercase[i] && lowercase[i])
                return (char)(i + 'A') + "";
        }

        // Return -1 if no such character whose
        // uppercase and lowercase present in
        // string str
        return "-1";
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "admeDCAB";

        System.out.println(largestCharacter(str));
    }
}
```

## 蟒蛇 3

```
# Java program to Find the Largest Alphabetic
# Character present in the string of both
# uppercase and lowercase English characters

# Function to find the Largest Alphabetic Character
def largestCharacter(str):

    # Array for keeping track of both uppercase
    # and lowercase english alphabets
    uppercase = [False] * 26
    lowercase = [False] * 26

    arr = list(str)
    for c in arr:
        if (c.islower()):
            lowercase[ord(c) - ord('a')] = True
        if (c.isupper()):
            uppercase[ord(c) - ord('A')] = True

    # Iterate from right side of array
    # to get the largest index character
    for i in range(25,-1,-1):

        # Check for the character if both its
        # uppercase and lowercase exist or not
        if (uppercase[i] and lowercase[i]):
            return chr(i + ord('A')) + ""
    # Return -1 if no such character whose
    # uppercase and lowercase present in
    # string str
    return "-1"

# Driver code

str = "admeDCAB"
print(largestCharacter(str))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to Find the Largest Alphabetic
// char present in the string of both
// uppercase and lowercase English characters
using System;

class GFG{

// Function to find the Largest Alphabetic char
public static String largestchar(String str)
{

    // Array for keeping track of both uppercase
    // and lowercase english alphabets
    bool[] uppercase = new bool[26];
    bool[] lowercase = new bool[26];

    char[] arr = str.ToCharArray();

    foreach(char c in arr)
    {
        if (char.IsLower(c))
            lowercase = true;

        if (char.IsUpper(c))
             uppercase = true;
    }

    // Iterate from right side of array
    // to get the largest index character
    for(int i = 25; i >= 0; i--)
    {

        // Check for the character if both its
        // uppercase and lowercase exist or not
        if (uppercase[i] && lowercase[i])
            return (char)(i + 'A') + "";
    }

    // Return -1 if no such character whose
    // uppercase and lowercase present in
    // string str
    return "-1";
}

// Driver code
public static void Main(String[] args)
{
    String str = "admeDCAB";

    Console.WriteLine(largestchar(str));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

    // JavaScript program to Find the Largest Alphabetic
    // Character present in the string of both
    // uppercase and lowercase English characters

    // Function to find the Largest Alphabetic Character
    function largestCharacter(str)
    {
        // Array for keeping track of both uppercase
        // and lowercase english alphabets
        let uppercase = new Array(26);
        uppercase.fill(false);
        let lowercase = new Array(26);
        lowercase.fill(false);

        let arr = str.split('');

        for (let c = 0; c < arr.length; c++) {

            if (arr == arr.toLowerCase())
                lowercase[arr.charCodeAt() - 97] = true;

            if (arr == arr.toUpperCase())
                uppercase[arr.charCodeAt() - 65] = true;
        }

        // Iterate from right side of array
        // to get the largest index character
        for (let i = 25; i >= 0; i--) {

            // Check for the character if both its
            // uppercase and lowercase exist or not
            if (uppercase[i] && lowercase[i])
                return String.fromCharCode(i +
                'A'.charCodeAt()) + "";
        }

        // Return -1 if no such character whose
        // uppercase and lowercase present in
        // string str
        return "-1";
    }

    let str = "admeDCAB";

    document.write(largestCharacter(str));

</script>
```

**输出:**

```
D
```

**时间复杂度:** O(n)，其中 n 为字符串长度。
**空间复杂度:** O(52)