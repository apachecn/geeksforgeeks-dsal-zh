# Java 中的字符串类|集合 1

> 原文:[https://www.geeksforgeeks.org/string-class-in-java/](https://www.geeksforgeeks.org/string-class-in-java/)

字符串是一个字符序列。在 java 中，String 的对象是不可变的，这意味着一个常量，一旦创建就不能更改。

**创建字符串**

在 Java 中有两种方法可以创建字符串:

*   ***弦字面***T0】
*   **使用*新增*关键词**T0】

**施工人员**

1.  **字符串(字节[]字节 _ arr)**–通过解码*字节数组*来构建新字符串。它使用平台的默认字符集进行解码。
    **例:**

    ```
    byte[] b_arr = {71, 101, 101, 107, 115};
    String s_byte =new String(b_arr); //Geeks

    ```

2.  **字符串(字节[]字节 _arr，字符集 char _ set)**–通过解码*字节数组*来构建新字符串。它使用 *char_set* 进行解码。
    **例:**

    ```
    byte[] b_arr = {71, 101, 101, 107, 115};
    Charset cs = Charset.defaultCharset();
    String s_byte_char = new String(b_arr, cs); //Geeks

    ```

3.  **字符串(字节[]字节 _arr，字符串 char _ set _ name)**–通过解码*字节数组*来构建新字符串。它使用 *char_set_name* 进行解码。
    它看起来类似于上面的构造，它们出现在类似的函数之前，但是它以*字符串(包含 char_set_name)* 为参数，而上面的构造函数以 *CharSet 为参数。*
    **例:**

    ```
    byte[] b_arr = {71, 101, 101, 107, 115};
    String s = new String(b_arr, "US-ASCII"); //Geeks

    ```

4.  **字符串(byte[] byte_arr，int start_index，int length)**–根据 *start_index(起始位置)*和 *length(起始位置的字符数)从*字节数组*构建新字符串。*
    **例:**

    ```
    byte[] b_arr = {71, 101, 101, 107, 115};
    String s = new String(b_arr, 1, 3); // eek

    ```

5.  **字符串(byte[] byte_arr，int start_index，int length，Charset char _ set)**–根据 *start_index(起始位置)*和 *length(起始位置的字符数)*从*字节数组*构建新字符串。使用 *char_set* 进行解码。
    **例:**

    ```
    byte[] b_arr = {71, 101, 101, 107, 115};
    Charset cs = Charset.defaultCharset();
    String s = new String(b_arr, 1, 3, cs); // eek

    ```

6.  **字符串(byte[] byte_arr，int start_index，int length，String char _ set _ name)**–根据 *start_index(起始位置)*和 *length(起始位置的字符数)*从*字节数组*构建新字符串。使用 *char_set_name* 进行解码。
    **例:**

    ```
    byte[] b_arr = {71, 101, 101, 107, 115};
    String s = new String(b_arr, 1, 4, "US-ASCII"); // eeks

    ```

7.  **字符串(char[]char _ arr)**–从给定的*字符数组*
    **中分配一个新字符串示例:**

    ```
    char char_arr[] = {'G', 'e', 'e', 'k', 's'};
    String s = new String(char_arr); //Geeks

    ```

8.  **字符串(char[] char_array，int start_index，int count)**–从给定的*字符数组*中分配一个字符串，但从 *start_index* 中选择*计数*字符。
    **例:**

    ```
    char char_arr[] = {'G', 'e', 'e', 'k', 's'};
    String s = new String(char_arr , 1, 3); //eek

    ```

9.  **字符串(int[] uni_code_points，int offset，int count)**–从 *uni_code_array* 中分配字符串，但从 *start_index* 中选择*计数*字符。
    **例:**

    ```
    int[] uni_code = {71, 101, 101, 107, 115};
    String s = new String(uni_code, 1, 3); //eek

    ```

10.  **字符串(StringBuffer s _ buffer)**–从 *s_buffer*
    **中的字符串分配新字符串示例:**

    ```
    StringBuffer s_buffer = new StringBuffer("Geeks");
    String s = new String(s_buffer); //Geeks

    ```

11.  **字符串(StringBuilder s _ builder)**–从 *s_builder*
    **中的字符串分配新字符串示例:**

    ```
    StringBuilder s_builder = new StringBuilder("Geeks");
    String s = new String(s_builder); //Geeks

    ```

**串法**

1.  **int length():** 返回字符串中的字符数。

    ```
    "GeeksforGeeks".length();  // returns 13
    ```

2.  **[Char charAt(int I)](https://www.geeksforgeeks.org/java-string-charat-method-example/):**返回 i <sup>th</sup> 索引处的字符。

    ```
    "GeeksforGeeks".charAt(3); // returns  ‘k’
    ```

3.  **[字符串子串(int i)](https://www.geeksforgeeks.org/substring-in-java/) :** 从 i <sup>第</sup>个索引字符返回子串到结尾。

    ```
    "GeeksforGeeks".substring(3); // returns “ksforGeeks”
    ```

4.  **[字符串子串(int i，int j)](https://www.geeksforgeeks.org/substring-in-java/) :** 返回从 I 到 j-1 索引的子串。

    ```
     "GeeksforGeeks".substring(2, 5); // returns “eks”
    ```

5.  **[字符串连接符(String str)](https://www.geeksforgeeks.org/java-string-concat-examples/) :** 将指定的字符串连接到该字符串的末尾。

    ```
     String s1 = ”Geeks”;
     String s2 = ”forGeeks”;
     String output = s1.concat(s2); // returns “GeeksforGeeks”

    ```

6.  **[int indexOf(字符串)](https://www.geeksforgeeks.org/java-string-indexof/) :** 返回指定字符串第一次出现的字符串内的索引。

    ```
     String s = ”Learn Share Learn”;
     int output = s.indexOf(“Share”); // returns 6

    ```

7.  **[int indexOf(字符串 s，int i)](https://www.geeksforgeeks.org/java-string-indexof/) :** 从指定的索引开始，返回指定字符串第一个匹配项的字符串内的索引。

    ```
     String s = ”Learn Share Learn”;
     int output = s.indexOf("ea",3);// returns 13

    ```

8.  **[Int lastIndexOf(字符串)](https://www.geeksforgeeks.org/java-lang-string-lastindexof-method/) :** 返回指定字符串最后一次出现的字符串内的索引。

    ```
     String s = ”Learn Share Learn”;
     int output = s.lastIndexOf("a"); // returns 14

    ```

9.  **布尔等于(对象其他对象):**将该字符串与指定的对象进行比较。

    ```
     Boolean out = “Geeks”.equals(“Geeks”); // returns true
     Boolean out = “Geeks”.equals(“geeks”); // returns false

    ```

10.  **[布尔 equalsIgnoreCase(String other String)](https://www.geeksforgeeks.org/equalsignorecase-in-java/):**将字符串与另一个字符串进行比较，忽略大小写。

    ```
     Boolean out= “Geeks”.equalsIgnoreCase(“Geeks”); // returns true
     Boolean out = “Geeks”.equalsIgnoreCase(“geeks”); // returns true
    ```

11.  **[int compare to(String other String)](https://www.geeksforgeeks.org/java-lang-string-compareto/):**按字典顺序比较两个字符串。

    ```
     int out = s1.compareTo(s2);  // where s1 ans s2 are
                                 // strings to be compared

     This returns difference s1-s2\. If :
     out < 0  // s1 comes before s2
     out = 0  // s1 and s2 are equal.
     out > 0   // s1 comes after s2.

    ```

12.  **int compareToIgnoreCase( String anotherString): **Compares two string lexicographically, ignoring case considerations.

    ```
     int out = s1.compareToIgnoreCase(s2);  
    // where s1 ans s2 are 
    // strings to be compared

     This returns difference s1-s2\. If :
     out < 0  // s1 comes before s2
     out = 0   // s1 and s2 are equal.
     out > 0   // s1 comes after s2.

    ```

    *注意-在这种情况下，它不会考虑字母的大小写(它会忽略它是大写还是小写)。*

13.  **[字符串到小写()](https://www.geeksforgeeks.org/java-string-tolowercase-examples/) :** 将字符串中的所有字符转换为小写。

    ```
    String word1 = “HeLLo”;
    String word3 = word1.toLowerCase(); // returns “hello"

    ```

14.  **[字符串 to ppercase()](https://www.geeksforgeeks.org/java-touppercase-examples/):**将字符串中的所有字符转换为大写。

    ```
    String word1 = “HeLLo”;
    String word2 = word1.toUpperCase(); // returns “HELLO”

    ```

15.  **[字符串修剪()](https://www.geeksforgeeks.org/java-string-trim-method-example/) :** 通过删除两端的空格来返回字符串的副本。它不影响中间的空白。

    ```
    String word1 = “ Learn Share Learn “;
    String word2 = word1.trim(); // returns “Learn Share Learn”

    ```

16.  **[ String replace (char oldChar, char newChar)](https://www.geeksforgeeks.org/java-lang-string-replace-method-java/): **Returns new string by replacing all occurrences of *oldChar* with *newChar.*

    ```
    String s1 = “feeksforfeeks“;
    String s2 = “feeksforfeeks”.replace(‘f’ ,’g’); // returns “geeksgorgeeks”

    ```

    *注意:- s1 仍然是 feeksforfeeks，s2 是 geeksgorgeeks*

    说明所有字符串方法的程序:

    ```
    // Java code to illustrate different constructors and methods 
    // String class.

    import java.io.*;
    import java.util.*;
    class Test
    {
        public static void main (String[] args)
        {
            String s= "GeeksforGeeks";
            // or String s= new String ("GeeksforGeeks");

            // Returns the number of characters in the String.
            System.out.println("String length = " + s.length());

            // Returns the character at ith index.
            System.out.println("Character at 3rd position = "
                               + s.charAt(3));

            // Return the substring from the ith  index character
            // to end of string
            System.out.println("Substring " + s.substring(3));

            // Returns the substring from i to j-1 index.
            System.out.println("Substring  = " + s.substring(2,5));

            // Concatenates string2 to the end of string1.
            String s1 = "Geeks";
            String s2 = "forGeeks";
            System.out.println("Concatenated string  = " +
                                s1.concat(s2));

            // Returns the index within the string
            // of the first occurrence of the specified string.
            String s4 = "Learn Share Learn";
            System.out.println("Index of Share " + 
                               s4.indexOf("Share"));

            // Returns the index within the string of the
            // first occurrence of the specified string,
            // starting at the specified index.
            System.out.println("Index of a  = " + 
                               s4.indexOf('a',3));

            // Checking equality of Strings
            Boolean out = "Geeks".equals("geeks");
            System.out.println("Checking Equality  " + out);
            out = "Geeks".equals("Geeks");
            System.out.println("Checking Equality  " + out);

            out = "Geeks".equalsIgnoreCase("gEeks ");
            System.out.println("Checking Equality " + out);

            //If ASCII difference is zero then the two strings are similar
            int out1 = s1.compareTo(s2);
            System.out.println("the difference between ASCII value is="+out1);
            // Converting cases
            String word1 = "GeeKyMe";
            System.out.println("Changing to lower Case " +
                                word1.toLowerCase());

            // Converting cases
            String word2 = "GeekyME";
            System.out.println("Changing to UPPER Case " + 
                                word2.toUpperCase());

            // Trimming the word
            String word4 = " Learn Share Learn ";
            System.out.println("Trim the word " + word4.trim());

            // Replacing characters
            String str1 = "feeksforfeeks";
            System.out.println("Original String " + str1);
            String str2 = "feeksforfeeks".replace('f' ,'g') ;
            System.out.println("Replaced f with g -> " + str2);
        } 
    }
    ```

    输出:

    ```
    String length = 13
    Character at 3rd position = k
    Substring ksforGeeks
    Substring = eks
    Concatenated string = GeeksforGeeks
    Index of Share 6
    Index of a = 8
    Checking Equality false
    Checking Equality true
    Checking Equality false
    the difference between ASCII value is=-31
    Changing to lower Case geekyme
    Changing to UPPER Case GEEKYME
    Trim the word Learn Share Learn
    Original String feeksforfeeks
    Replaced f with g -> geeksgorgeeks

    ```

    **对于第 2 集，您可以参考:** [Java 中的 Java.lang.String 类|第 2 集](https://www.geeksforgeeks.org/java-lang-string-class-java-set-2/)

    本文由拉胡尔·阿格拉瓦尔供稿。如果您发现任何不正确的地方，或者您想分享更多关于上述主题的信息，请写评论