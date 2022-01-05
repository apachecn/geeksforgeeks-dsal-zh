# 用 Java 打印字符串的所有排列

> 原文:[https://www . geeksforgeeks . org/print-all-排列成串的 java/](https://www.geeksforgeeks.org/print-all-permutations-of-a-string-in-java/)

给定一个字符串 **str** ，任务是打印 **str** 的所有排列。一个**排列**是一组物体的全部或部分的排列，关于排列的顺序。例如，单词“bat”和“tab”代表相似的三个字母单词的两种不同排列(或排列)。

**示例:**

> **输入:**str = " CD "
> T3】输出: cd dc
> 
> **输入:**str = " abb "
> T3】输出:【abb bab bba bab bba

**方法:**编写一个递归函数，打印给定字符串的每个排列。当传递的字符串为空时，将出现终止条件。

下面是上述方法的实现:

```
// Java program to print all the permutations
// of the given string
public class GFG {

    // Function to print all the permutations of str
    static void printPermutn(String str, String ans)
    {

        // If string is empty
        if (str.length() == 0) {
            System.out.print(ans + " ");
            return;
        }

        for (int i = 0; i < str.length(); i++) {

            // ith character of str
            char ch = str.charAt(i);

            // Rest of the string after excluding 
            // the ith character
            String ros = str.substring(0, i) + 
                         str.substring(i + 1);

            // Recurvise call
            printPermutn(ros, ans + ch);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abb";
        printPermutn(s, "");
    }
}
```

**Output:**

```
abb abb bab bba bab bba

```

**当排列需要不同时。**

**示例:**

> **输入:**str = " abb "
> T3】输出: abb bab bba
> 
> **输入:**【str = " geek】
> **输出:**【geek geke egke eegk eekg ekeg kge kege keeg】

**方法:**写一个递归函数，打印不同的排列。创建一个大小为' 26 '的布尔数组，用于表示正在使用的字符。如果这个字符没有被使用，那么递归调用就会发生。否则，不要打任何电话。当传递的字符串为空时，将出现终止条件。

下面是上述方法的实现:

```
// Java program to print all the permutations
// of the given string
public class GFG {

    // Function to print all the distinct
    // permutations of str
    static void printDistinctPermutn(String str, 
                                     String ans)
    {

        // If string is empty
        if (str.length() == 0) {

            // print ans
            System.out.print(ans + " ");
            return;
        }

        // Make a boolean array of size '26' which
        // stores false by default and make true 
        // at the position which alphabet is being
        // used
        boolean alpha[] = new boolean[26];

        for (int i = 0; i < str.length(); i++) {

            // ith character of str
            char ch = str.charAt(i);

            // Rest of the string after excluding 
            // the ith character
            String ros = str.substring(0, i) + 
                         str.substring(i + 1);

            // If the character has not been used 
            // then recursive call will take place. 
            // Otherwise, there will be no recursive
            // call
            if (alpha[ch - 'a'] == false)
                printDistinctPermutn(ros, ans + ch);
            alpha[ch - 'a'] = true;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geek";
        printDistinctPermutn(s, "");
    }
}
```

**Output:**

```
geek geke gkee egek egke eegk eekg ekge ekeg kgee kege keeg

```