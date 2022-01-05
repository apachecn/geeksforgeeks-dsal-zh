# 在 Java 中生成给定大小的随机字符串

> 原文:[https://www . geesforgeks . org/generate-random-string-of-size-in-Java/](https://www.geeksforgeeks.org/generate-random-string-of-given-size-in-java/)

假设大小为 n，任务是生成一个随机的字母数字字符串。

以下是生成给定大小的随机字母数字字符串的各种方法:

先决条件:[用 Java 生成随机数](https://www.geeksforgeeks.org/generating-random-numbers-in-java/)

*   **Method 1: Using Math.random()**

    这里函数 GetalHanumeRichString(n)生成一个长度为字符串的随机数。这个数字是一个字符的索引，这个字符附加在临时局部变量 sb 中。最后某人回来了。

    ```
    // Java program generate a random AlphaNumeric String
    // using Math.random() method

    public class RandomString {

        // function to generate a random string of length n
        static String getAlphaNumericString(int n)
        {

            // chose a Character random from this String
            String AlphaNumericString = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
                                        + "0123456789"
                                        + "abcdefghijklmnopqrstuvxyz";

            // create StringBuffer size of AlphaNumericString
            StringBuilder sb = new StringBuilder(n);

            for (int i = 0; i < n; i++) {

                // generate a random number between
                // 0 to AlphaNumericString variable length
                int index
                    = (int)(AlphaNumericString.length()
                            * Math.random());

                // add Character one by one in end of sb
                sb.append(AlphaNumericString
                              .charAt(index));
            }

            return sb.toString();
        }

        public static void main(String[] args)
        {

            // Get the size n
            int n = 20;

            // Get and display the alphanumeric string
            System.out.println(RandomString
                                   .getAlphaNumericString(n));
        }
    }
    ```

    **Output:**

    ```
    kU9vRVm9T1lFMbi3duO1

    ```

    **方法二:使用字符集**

    使用 **java.nio.charset 包**中的 Charset 随机生成 20 个字符长的字母数字字符串。

    1.  首先取 0 到 256 之间的字符并遍历。
    2.  检查字符是字母还是数字。
    3.  如果是，那么在字符串的末尾添加
    4.  返回字符串

    下面是上述方法的实现:

    ```
    // Java program generate a random AlphaNumeric String
    // using CharSet method

    import java.util.*;
    import java.nio.charset.*;

    class RandomString {

        static String getAlphaNumericString(int n)
        {

            // length is bounded by 256 Character
            byte[] array = new byte[256];
            new Random().nextBytes(array);

            String randomString
                = new String(array, Charset.forName("UTF-8"));

            // Create a StringBuffer to store the result
            StringBuffer r = new StringBuffer();

            // Append first 20 alphanumeric characters
            // from the generated random String into the result
            for (int k = 0; k < randomString.length(); k++) {

                char ch = randomString.charAt(k);

                if (((ch >= 'a' && ch <= 'z')
                     || (ch >= 'A' && ch <= 'Z')
                     || (ch >= '0' && ch <= '9'))
                    && (n > 0)) {

                    r.append(ch);
                    n--;
                }
            }

            // return the resultant string
            return r.toString();
        }

        public static void main(String[] args)
        {
            // size of random alphanumeric string
            int n = 20;

            // Get and display the alphanumeric string
            System.out.println(getAlphaNumericString(n));
        }
    }
    ```

    **Output:**

    ```
    jj06CyZKfSBZQHM6KAUd

    ```

*   **Method 3: Using Regular Expressions**
    1.  首先取 0 到 256 之间的字符。
    2.  除去除 0-9、a-z 和 A-Z 以外所有字符
    3.  随机选择一个字符
    4.  在末尾添加我们需要的变量

    下面是上述方法的实现:

    ```
    // Java program generate a random AlphaNumeric String
    // using Regular Expressions method

    import java.util.*;
    import java.nio.charset.*;

    class RandomString {

        static String getAlphaNumericString(int n)
        {

            // length is bounded by 256 Character
            byte[] array = new byte[256];
            new Random().nextBytes(array);

            String randomString
                = new String(array, Charset.forName("UTF-8"));

            // Create a StringBuffer to store the result
            StringBuffer r = new StringBuffer();

            // remove all spacial char
            String  AlphaNumericString
                = randomString
                      .replaceAll("[^A-Za-z0-9]", "");

            // Append first 20 alphanumeric characters
            // from the generated random String into the result
            for (int k = 0; k < AlphaNumericString.length(); k++) {

                if (Character.isLetter(AlphaNumericString.charAt(k))
                        && (n > 0)
                    || Character.isDigit(AlphaNumericString.charAt(k))
                           && (n > 0)) {

                    r.append(AlphaNumericString.charAt(k));
                    n--;
                }
            }

            // return the resultant string
            return r.toString();
        }

        public static void main(String[] args)
        {
            // size of random alphanumeric string
            int n = 20;

            // Get and display the alphanumeric string
            System.out.println(getAlphaNumericString(n));
        }
    }
    ```

    **Output:**

    ```
    4J8pirLzX6oIF0IIIaUU

    ```

*   **Method 4: Generating random String of UpperCaseLetter/LowerCaseLetter/Numbers**

    当字母数字字符串中需要一些特定的字符时，例如只有大写字母或小写字母或数字，请使用此方法。以下示例生成一个随机的大小为 n 的小写字母字符串。

    下面是上述方法的实现:

    ```
    // Java program generate a random
    // UpperCase or LowerCase or Number String

    import java.util.*;

    public class GFG {

        static String getAlphaNumericString(int n)
        {

            // lower limit for LowerCase Letters
            int lowerLimit = 97;

            // lower limit for LowerCase Letters
            int upperLimit = 122;

            Random random = new Random();

            // Create a StringBuffer to store the result
            StringBuffer r = new StringBuffer(n);

            for (int i = 0; i < n; i++) {

                // take a random value between 97 and 122
                int nextRandomChar = lowerLimit
                                     + (int)(random.nextFloat()
                                             * (upperLimit - lowerLimit + 1));

                // append a character at the end of bs
                r.append((char)nextRandomChar);
            }

            // return the resultant string
            return r.toString();
        }

        public static void main(String[] args)
        {
            // size of random alphanumeric string
            int n = 20;

            // Get and display the alphanumeric string
            System.out.println(getAlphaNumericString(n));
        }
    }
    ```

    **Output:**

    ```
    qbhalyuzrenuwgvqidno

    ```