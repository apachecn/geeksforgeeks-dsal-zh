# 如何在 Java 中检查字符串是否只包含数字

> 原文:[https://www . geesforgeks . org/如何检查字符串是否仅包含 java 数字/](https://www.geeksforgeeks.org/how-to-check-if-string-contains-only-digits-in-java/)

给定一个字符串 **str** ，任务是编写一个 [Java](https://www.geeksforgeeks.org/java/) 程序来检查一个字符串是否只包含数字。如果是，那么打印真，否则打印假。
**例:**

> **输入:** str = "1234"
> **输出:**真
> **解释:**
> 给定字符串只包含数字，因此输出为真。
> 
> **输入:**str = " geeksforgeeck 2020 "
> **输出:**假
> **说明:**
> 给定字符串包含字母字符和数字，因此输出为假。

1.  **Using Traversal:** The idea is to traverse each character in the string and check if the character of the string contains only digits from **0 to 9**. If all the character of the string contains only digits then return true, otherwise, return false.

    下面是上述方法的实现:

    ```
    // Java program for the above approach
    // contains only digits
    class GFG {

        // Function to check if a string
        // contains only digits
        public static boolean
        onlyDigits(String str, int n)
        {
            // Traverse the string from
            // start to end
            for (int i = 0; i < n; i++) {

                // Check if character is
                // digit from 0-9
                // then return true
                // else false
                if (str.charAt(i) >= '0'
                    && str.charAt(i) <= '9') {
                    return true;
                }
                else {
                    return false;
                }
            }
            return false;
        }

        // Driver Code
        public static void main(String args[])
        {
            // Given string str
            String str = "1234";
            int len = str.length();

            // Function Call
            System.out.println(onlyDigits(str, len));
        }
    }
    ```

    **Output:**

    ```
    true

    ```

    **时间复杂度:** *O(N)* ，其中 N 为给定字符串的长度。
    **辅助空间:** *O(1)*

2.  **Using Character.isDigit(char ch):** The idea is to iterate over each character of the string and check whether the specified character is a digit or not using [Character.isDigit(char ch)](https://www.geeksforgeeks.org/character-isdigit-method-in-java-with-examples/). If the character is digit then return true, else return false.

    下面是上述方法的实现:

    ```
    // Java program to check if a string
    // contains only digits
    class GFG {

        // Function to check if a string
        // contains only digits
        public static boolean
        onlyDigits(String str, int n)
        {

            // Traverse the string from
            // start to end
            for (int i = 0; i < n; i++) {

                // Check if the sepecified
                // character is a digit then
                // return true,
                // else return false
                if (Character.isDigit(str.charAt(i))) {
                    return true;
                }
                else {
                    return false;
                }
            }
            return false;
        }

        // Driver Code
        public static void main(String args[])
        {
            // Given string str
            String str = "1234";
            int len = str.length();

            // Function Call
            System.out.println(onlyDigits(str, len));
        }
    }
    ```

    **Output:**

    ```
    true

    ```

    **时间复杂度:** *O(N)* ，其中 N 为给定字符串的长度。
    **辅助空间:** *O(1)*

3.  **Using Regular Expression:**
    1.  获取字符串。
    2.  创建一个[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来检查字符串是否只包含数字，如下所述:

        ```
        regex = "[0-9]+";

        ```

    3.  用正则表达式匹配给定的字符串。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
    4.  如果字符串与给定的正则表达式匹配，则返回 true，否则返回 false。

    下面是上述方法的实现:

    ```
    // Java program to check if a string
    // contains only digits
    import java.util.regex.*;
    class GFG {

        // Function to validate URL
        // using regular expression
        public static boolean
        onlyDigits(String str)
        {
            // Regex to check string
            // contains only digits
            String regex = "[0-9]+";

            // Compile the ReGex
            Pattern p = Pattern.compile(regex);

            // If the string is empty
            // return false
            if (str == null) {
                return false;
            }

            // Find match between given string
            // and regular expression
            // using Pattern.matcher()
            Matcher m = p.matcher(str);

            // Return if the string
            // matched the ReGex
            return m.matches();
        }

        // Driver Code
        public static void main(String args[])
        {
            // Given string str
            String str = "1234";

            // Function Call
            System.out.println(onlyDigits(str));
        }
    }
    ```

    **Output:**

    ```
    true

    ```

    **时间复杂度:** *O(N)* ，其中 N 为给定字符串的长度。
    **辅助空间:** *O(1)*