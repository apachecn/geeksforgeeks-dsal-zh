# 计算给定句子中每个单词的字符的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序-计数-字符-单词-给定-句子/](https://www.geeksforgeeks.org/java-program-count-characters-word-given-sentence/)

写一个 Java 程序来计算给定句子中每个单词的字符数？
示例:

```
Input : geeks for geeks
Output :
geeks->5
for->3
geeks->5
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
class CountCharacterInEachWords {
    static void count(String str)
    {
        // Create an char array of given String
        char[] ch = str.toCharArray();
        for (int i = 0; i < ch.length; i++) {

            // Declare an String with empty initialization
            String s = "";

            // When the character is not space
            while (i < ch.length && ch[i] != ' ') {

                // concat with the declared String
                s = s + ch[i];
                i++;
            }

            if (s.length() > 0)
                System.out.println(s + "->" + s.length());           
        }
    }
    public static void main(String[] args)
    {
        String str = "geeks for geeks";
        count(str);
    }
}
```

输出:

```
geeks->5
for->3
geeks->5
```