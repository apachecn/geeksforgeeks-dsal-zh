# Java 程序检查两个字符串是否互为字谜

> 原文:[https://www . geesforgeks . org/Java-program-to-check-two-string-is-anagram-of-other/](https://www.geeksforgeeks.org/java-program-to-check-whether-two-strings-are-anagram-of-each-other/)

写一个函数检查两个给定的字符串是否是彼此的[字谜](http://en.wikipedia.org/wiki/Anagram)。字符串的字谜是另一个包含相同字符的字符串，只有字符的顺序可以不同。例如，“abcd”和“dabc”是彼此的字谜。

![check-whether-two-strings-are-anagram-of-each-other](img/44eca765d93a8501e9332cab7ddb74ba.png)

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/anagram-1587115620/1)

**方法 1(使用排序):**

1.  对两个字符串进行排序
2.  比较排序后的字符串

下面是上述想法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether two strings
// are anagrams of each other
import java.io.*;
import java.util.Arrays;
import java.util.Collections;
class GFG
{
    /* Function to check whether two strings
       are anagram of each other */
    static boolean areAnagram(char[] str1,
                              char[] str2)
    {
        // Get lengths of both strings
        int n1 = str1.length;
        int n2 = str2.length;

        // If length of both strings is not
        // same, then they cannot be anagram
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

    // Driver Code
    public static void main(String args[])
    {
        char str1[] = {'t', 'e', 's', 't'};
        char str2[] = {'t', 't', 'e', 'w'};

        // Function Call
        if (areAnagram(str1, str2))
            System.out.println(
            "The two strings are" +
            " anagram of each other");
        else
            System.out.println(
            "The two strings are not" +
            " anagram of each other");
    }
}
// This code is contributed by Nikita Tiwari.
```

**输出:**

```
The two strings are not anagram of each other
```

**时间复杂度:** O(nLogn)

**方法 2(计数字符):**
该方法假设两个字符串中可能的字符集都很小。在下面的实现中，假设使用 8 位存储字符，并且可能有 256 个字符。

1.  为两个字符串创建大小为 256 的计数数组。将计数数组中的所有值初始化为 0。
2.  遍历两个字符串的每个字符，并增加相应计数数组中的字符数。
3.  比较计数数组。如果两个计数数组相同，则返回 true。

下面是上述想法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two strings
// are anagrams of each other
import java.io.*;
import java.util.*;
class GFG
{
    static int NO_OF_CHARS = 256;

    /* Function to check whether two strings
       are anagram of each other */
    static boolean areAnagram(char str1[],
                              char str2[])
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
        for (i = 0; i < str1.length &&
             i < str2.length; i++)
        {
            count1[str1[i]]++;
            count2[str2[i]]++;
        }

        // If both strings are of different length.
        // Removing this condition will make the
        // program fail for strings like "aaca"
        // and "aca"
        if (str1.length != str2.length)
            return false;

        // Compare count arrays
        for (i = 0; i < NO_OF_CHARS; i++)
            if (count1[i] != count2[i])
                return false;

        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        char str1[] =
        ("geeksforgeeks").toCharArray();
        char str2[] =
        ("forgeeksgeeks").toCharArray();

        // Function call
        if (areAnagram(str1, str2))
            System.out.println(
            "The two strings are" +
            "anagram of each other");
        else
            System.out.println(
            "The two strings are not" +
            " anagram of each other");
    }
}
// This code is contributed by Nikita Tiwari.
```

**输出:**

```
The two strings are anagram of each other
```

**方法 3(用一个数组计数字符):**
上面的实现可以进一步用一个计数数组代替两个。我们可以在 str1 中增加字符计数数组中的值，在 str2 中减少字符计数数组中的值。最后，如果所有计数值都是 0，那么这两个字符串就是彼此的字谜。感谢**高手**提出这个优化。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two strings
// are anagrams of each other
class GFG{

static int NO_OF_CHARS = 256;

// Function to check if two strings
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
    char str1[] =
    "geeksforgeeks".toCharArray();
    char str2[] =
    "forgeeksgeeks".toCharArray();

    // Function call
    if (areAnagram(str1, str2))
        System.out.print(
        "The two strings are " +
        "anagram of each other");
    else
        System.out.print(
        "The two strings are " +
        "not anagram of each other");
}
}
// This code is contributed by mark_85
```

**输出:**

```
The two strings are anagram of each other
```

**时间复杂度:** O(n)
详情请参考[查看两串是否互为字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)整篇文章！