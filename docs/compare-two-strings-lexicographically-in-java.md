# 在 Java 中按字典顺序比较两个字符串

> 原文:[https://www . geesforgeks . org/compare-two-string-in-Java 词典编纂/](https://www.geeksforgeeks.org/compare-two-strings-lexicographically-in-java/)

在本文中，我们将讨论如何在 Java 中按字典顺序比较两个字符串。

一种解决方案是使用 Java compareTo()方法。方法 compareTo()用于在 Java 中按字典顺序比较两个字符串。两个字符串的每个字符都被转换为 Unicode 值进行比较。

```
int compareTo(String str) :
```

它返回以下值:

1.  如果(string1 > string2)它返回一个正值。
2.  如果两个字符串在词典上相等
    (即 string1 == string2)，则返回 0。
3.  如果(string1 < string2 ),则返回负值。

```
// Java program to show how to compare Strings
// using library function
public class Test
{
    public static void main(String[] args)
    {
        String s1 = "Ram";
        String s2 = "Ram";
        String s3 = "Shyam";
        String s4 = "ABC";

        System.out.println(" Comparing strings with compareTo:");
        System.out.println(s1.compareTo(s2));
        System.out.println(s1.compareTo(s3));
        System.out.println(s1.compareTo(s4));
    }
}
```

**输出:**

```
Comparing strings with compareTo:
0
-1
17

```

参见[如何在 Java 中初始化和比较字符串？](https://www.geeksforgeeks.org/how-to-initialize-and-compare-strings-in-java/)了解更多详情。

**不使用库函数如何比较两个字符串？**

```
1\. Input two strings string 1 and string 2.
2\. for (int i = 0; i < str1.length() && 
        i < str2.length(); i ++) 
  (Loop through each character of both 
   strings comparing them until one 
   of the string terminates):
   a. If unicode value of both the characters 
      is same then continue;
   b. If unicode value of character of 
      string 1 and unicode value of string 2
      is different then return (str1[i]-str2[i])
3\. if length of string 1 is less than string2
       return str2[str1.length()]
   else 
       return str1[str2.length()]

```

下面是上述算法的实现。

```
// Java program to Compare two strings
// lexicographically
class Compare {

    // This method compares two strings
    // lexicographically without using
    // library functions
    public static int stringCompare(String str1,
                                    String str2)
    {
        for (int i = 0; i < str1.length() && 
                    i < str2.length(); i++) {
            if ((int)str1.charAt(i) == 
                (int)str2.charAt(i)) {
                continue;
            } 
            else {
                return (int)str1.charAt(i) - 
                    (int)str2.charAt(i);
            }
        }

        // Edge case for strings like
        // String 1="Geeky" and String 2="Geekyguy"
        if (str1.length() < str2.length()) {
            return (str1.length()-str2.length());
        } 
        else if (str1.length() > str2.length()) {
            return (str1.length()-str2.length());
        }

        // If none of the above conditions is true,
        // it implies both the strings are equal
        else {
            return 0;
        }
    }

    // Driver function to test the above program
    public static void main(String args[])
    {
        String string1 = new String("Geeks");
        String string2 = new String("Practice");
        String string3 = new String("Geeks");
        String string4 = new String("Geeksforgeeks");

        System.out.println(stringCompare(string1, 
                                        string2));
        System.out.println(stringCompare(string1, 
                                        string3));
        System.out.println(stringCompare(string2,
                                        string1));

        // To show for edge case
        // In these cases, the output is the difference of 
        // length of the string
        System.out.println(stringCompare(string1,
                                        string4));
        System.out.println(stringCompare(string4,
                                        string1));
    }
}
```

**输出:**

```
-9
0
9
-8
8

```

本文由 [**安基特·贾恩**](https://www.facebook.com/profile.php?id=100000412091676) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。