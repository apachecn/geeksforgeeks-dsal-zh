# 在字符串中打印偶数长度单词的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序到打印-偶数长度字符串中的单词/](https://www.geeksforgeeks.org/java-program-to-print-even-length-words-in-a-string/)

给定一个字符串 **str** ，编写一个 Java 程序，打印给定字符串中所有长度为偶数的单词。

**例:**

```
Input: s = "This is a java language"
Output: This
        is
        java
        language 

Input: s = "i am GFG"
Output: am

```

**进场:**

*   Take strings
*   With the help of [split () method in string class, the string is broken into words. It is a rope used to break sentences. So here **""(space)** is passed as a parameter. As a result, the words of the string are split into string arrays

    ```
    String[] words = str.split(" ");

    ```](https://www.geeksforgeeks.org/split-string-java-examples/) 
*   Returns, with the help of [foreach loop](https://www.geeksforgeeks.org/for-each-loop-in-java/) in Java, traversing every word in the returned string array.

    ```
    for(String word : words)
    { }

    ```

*   Use the [string.length ()](https://www.geeksforgeeks.org/how-to-determine-length-or-size-of-a-string-in-java/) function to calculate the length of each word.

    ```
    int lengthOfWord = word.length();

    ```

*   If the length is even, then print this word.

下面是上述方法的实现:

```
// Java program to print
// even length words in a string

class GfG {
    public static void printWords(String s)
    {

        // Splits Str into all possible tokens
        for (String word : s.split(" "))

            // if length is even
            if (word.length() % 2 == 0)

                // Print the word
                System.out.println(word);
    }

    // Driver Code
    public static void main(String[] args)
    {

        String s = "i am Geeks for Geeks and a Geek";
        printWords(s);
    }
}
```

**输出:**

```
am
Geek

```