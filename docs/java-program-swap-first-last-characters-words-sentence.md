# Java 程序交换一个句子中单词的第一个和最后一个字符

> 原文:[https://www . geesforgeks . org/Java-program-swap-first-last-characters-words-句子/](https://www.geeksforgeeks.org/java-program-swap-first-last-characters-words-sentence/)

编写一个 Java 程序来交换句子中单词的第一个和最后一个字符，就像例子中提到的那样？

示例:

```
Input : geeks for geeks
Output :seekg rof seekg

```

**方法:**如示例中所述，我们必须替换单词的第一个和最后一个字符，并保持其余字母不变。

*   First, we will use the toCharArray () method to create a Char array of a given string.
*   Now we use the for loop to iterate over the char array.
*   In the for loop, we declare a variable whose value depends on I.
*   Whenever we find an alphabet, we increase the value of I, and whenever we reach a space, we will exchange between the first and last characters of the word in front of the space.

```
class SwapFirstLastCharacters {
    static String count(String str)
    {
        // Create an equivalent char array
        // of given string
        char[] ch = str.toCharArray();
        for (int i = 0; i < ch.length; i++) {

            // k stores index of first character
            // and i is going to store index of last 
            // character. 
            int k = i;
            while (i < ch.length && ch[i] != ' ') 
                i++;

            // Swapping
            char temp = ch[k];
            ch[k] = ch[i - 1];
            ch[i - 1] = temp;

            // We assume that there is only one space
            // between two words.
        }
        return new String(ch);
    }
    public static void main(String[] args)
    {
        String str = "geeks for geeks";
        System.out.println(count(str));
    }
}
```

输出:

```
seekg rof seekg

```