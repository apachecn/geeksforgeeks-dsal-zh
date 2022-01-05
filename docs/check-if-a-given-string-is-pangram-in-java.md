# 检查给定的字符串是否是 Java 中的 Pangram

> 原文:[https://www . geesforgeks . org/check-if-a-给定字符串是-pangram-in-java/](https://www.geeksforgeeks.org/check-if-a-given-string-is-pangram-in-java/)

给定字符串 **str** ，任务是编写 [Java 程序](https://www.geeksforgeeks.org/java/)检查给定字符串是否是庞加莱。

> 如果字符串包含字母的所有字符，忽略字母的大小写，则它是 pangram 字符串。

**示例:**

> **输入:** *字符串**= "**Abcdefghijklmnopqrstuvwxyz "*
> **输出:**是
> **解释:**给定字符串包含从 a 到 z 的所有字母(忽略大小写)。
> 
> **输入:**str**=**“geeks forgeeks”
> **输出:** No
> **解释:**给定的字符串不包含从 a 到 z 的所有字母(忽略大小写)。

**方法 1–使用频率阵列:**

1.  [将字符串的每个字母转换为小写或大写](https://www.geeksforgeeks.org/convert-alternate-characters-string-upper-case/)。
2.  创建一个频率数组来标记从 **a** 到 **z** 的每个字母的频率。
3.  然后，遍历频率数组，如果给定字符串中没有任何字母，则打印*否*，否则打印*是*。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    static int size = 26;

    // Function to check if ch is a letter
    static boolean isLetter(char ch)
    {
        if (!Character.isLetter(ch))
            return false;

        return true;
    }

    // Function to check if a string
    // contains all the letters from
    // a to z
    static boolean allLetter(String str,
                             int len)
    {
        // Convert the given string
        // into lowercase
        str = str.toLowerCase();

        // Create a frequency array to
        // mark the present letters
        boolean[] present = new boolean[size];

        // Traverse for each character
        // of the string
        for (int i = 0; i < len; i++) {

            // If the current character
            // is a letter
            if (isLetter(str.charAt(i))) {

                // Mark current letter as present
                int letter = str.charAt(i) - 'a';
                present[letter] = true;
            }
        }

        // Traverse for every letter
        // from a to z
        for (int i = 0; i < size; i++) {

            // If the current character
            // is not present in string
            // then return false,
            // otherwise return true
            if (!present[i])
                return false;
        }
        return true;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given string str
        String str = "Abcdefghijklmnopqrstuvwxyz";
        int len = str.length();

        // Function Call
        if (allLetter(str, len))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(26)*

**方法 2–使用遍历:**想法是将给定的字符串转换为小写字母，然后迭代从 **a** 到 **z** 本身的每个字符，并检查给定的字符串是否包含从 a 到 z 的所有字母。如果所有字母都存在，则打印*是*，否则打印*否*。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to check if a string
    // contains all the letters from
    // a to z (ignoring case)
    public static void
    allLetter(String str)
    {
        // Converting the given string
        // into lowercase
        str = str.toLowerCase();

        boolean allLetterPresent = true;

        // Loop over each character itself
        for (char ch = 'a'; ch <= 'z'; ch++) {

            // Check if the string does not
            // contains all the letters
            if (!str.contains(String.valueOf(ch))) {
                allLetterPresent = false;
                break;
            }
        }

        // Check if all letter present then
        // print "Yes", else print "No"
        if (allLetterPresent)
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given string str
        String str = "Abcdefghijklmnopqrstuvwxyz12";

        // Function call
        allLetter(str);
    }
}
```

**Output:** 

```
Yes
```

***时间复杂度:** O(26*N)*
***辅助空间:** O(1)*