# 如果给定范围，Java 程序扩展字符串？

> 原文:[https://www . geesforgeks . org/Java-program-expand-string-range-given/](https://www.geeksforgeeks.org/java-program-expand-string-range-given/)

假设我们给出了一个字符串，其中指定了一些范围，为了更好地理解，我们必须将给定范围之间的数字放在指定的位置，如下图所示。

插图:

```
Input  : string x = "1-5, 8, 11-14, 18, 20, 26-29" 
Output : string y = "1, 2, 3, 4, 5, 8, 11, 12, 
                    13, 14, 18, 20, 26, 27, 28, 29"
```

**进场:**

为了解决上述问题，我们可以遵循以下方法:

*   首先，我们必须将字符串分割成字符串[]数组。我们必须在找到符号的地方分割字符串。
*   现在我们有一个包含元素的字符串[]数组。现在我们只去第一个索引最后一个元素，即 1，字符串[]数组的前一个索引第一个元素说它是 5。
*   之后，在 for 循环的帮助下，我们可以将 1 到 5 之间的数字相加，并将它们存储在 String 变量中。
*   上述过程一直持续到字符串数组的长度。

> **注:**
> 
> 在集合和各种实用方法的帮助下，我们可以很容易地解决这个问题，但是从性能角度来看，集合概念并不是一个好的选择。如果我们进行收集，性能会降低，时间复杂度也会增加。在下面的程序中，我们明确定义了自己的拆分方法和逻辑。

**实施:**

在这里，我们现在将在 clean java 程序的帮助下提出并讨论所有三个场景，如下所示:

**例 1**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Expand a String if Range is Given

// Main class
public class Solution {

    // Main driver method
    public static void expand(String word)
    {

        // Creating an object of StringBuffer class to
        // make a modifiable string object
        StringBuilder sb = new StringBuilder();

        // Get all intervals
        String[] strArr = word.split(", ");

        // Traverse through every interval
        for (int i = 0; i < strArr.length; i++) {

            // Get lower and upper
            String[] a = strArr[i].split("-");

            // Setting high and low counters
            if (a.length == 2) {

                int low = Integer.parseInt(a[0]);
                int high
                    = Integer.parseInt(a[a.length - 1]);

                // Condition check holds true
                // Till low counter is lesser or equal to
                // high counter
                while (low <= high) {

                    // Append all numbers
                    sb.append(low + " ");
                    low++;
                }
            }

            // If we reaches here then
            // High counter exceeds lower counter
            else {

                sb.append(strArr[i] + " ");
            }
        }

        // Print the modifiable string
        System.out.println(sb.toString());
    }

    // Method 2
    // Main driver method
    public static void main(String args[])
    {
        // Custom input string as input
        String s = "1-5, 8, 11-14, 18, 20, 26-29";
        expand(s);
    }
}
```

**Output:** 

```
1 2 3 4 5 8 11 12 13 14 18 20 26 27 28 29
```

**例 2**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Illustrate Expansion of String

// Main class
public class StringExpand {

    // Method 1
    // To split the string
    static String[] split(String st)
    {
        // Count how many words in our string
        // Irrespective of spaces
        int wc = countWords(st);
        String w[] = new String[wc];
        char[] c = st.toCharArray();
        int k = 0;

        for (int i = 0; i < c.length; i++) {

            // Initially declaring and initializing
            // string as empty
            String s = "";

            // Whenever we found an non-space character
            while (i < c.length && c[i] != ' ') {

                // Concat with the String s
                // Increment the value of i
                s = s + c[i];
                i++;
            }

            // If the String is not empty
            if (s.length() != 0) {

                // Add the String to the String[]
                // array
                w[k] = s;
                k++;
            }
        }

        // Returning the string array
        return w;
    }

    // Method 2
    // To count the number of words in a string
    static int countWords(String str)
    {
        int count = 0;
        for (int i = 0; i < str.length(); i++) {

            // The below condition to check
            // whether the first character is
            // space or not
            if (i == 0 && str.charAt(i) != ' '
                || str.charAt(i) != ' '
                       && str.charAt(i - 1) == ' ') {
                count++;
            }
        }

        // Returning the count
        return count;
    }

    // Method 3
    // To expand the string
    public static void expand(String s)
    {
        String p = s;
        String[] arr = p.split("\\-");
        String k = "";

        // Traversing over array using for loop
        for (int i = 0; i < arr.length; i++) {

            // Case 1
            if (i != arr.length - 1) {

                String[] arr1 = arr[i].split(", ");
                String[] arr2 = arr[i + 1].split(", ");

                int a = Integer.parseInt(
                    arr1[arr1.length - 1]);
                int b = Integer.parseInt(arr2[0]);

                for (int j = a + 1; j < b; j++) {
                    arr[i] = arr[i] + ", " + j;
                }
            }

            // Case 2
            if (k != "")
                k = k + ", " + arr[i];

            // Case 3
            else
                k = k + arr[i];
        }

        // Print the expanded string
        System.out.println(k);
    }

    // Method 4
    // Main driver method
    public static void main(String[] args)
    {
        // Custom string input
        String s = "1-5, 8, 11-14, 18, 20, 26-29";

        // Calling the method 3 to
        // expand the string
        expand(s);
    }
}
```

**Output:** 

```
1, 2, 3, 4, 5, 8, 11, 12, 13, 14, 18, 20, 26, 27, 28, 29
```

**例 3**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Expand a String if Range is Given

// Main class
// GenerateStringOnRange
class GFG {

    // Method 1
    // To generate string on range
    public static String generateStringOn(String input)
    {
        String[] words = input.split(" ");

        // Initially setting up range
        String[] ranges = null;
        int number = 0;

        // Creating a StringBuffer object so that
        // we can modify the string
        StringBuffer buffer = new StringBuffer();

        // Looking out for words by
        // iterating using for each loop
        for (String word : words) {

            // To be replaced by
            // using replace() method
            word = word.replace(",", "");

            // If word is containing "-" character
            if (word.contains("-")) {
                ranges = word.split("-");
                number = Integer.parseInt(ranges[0]);

                // Till number is within range
                while (number
                       <= Integer.parseInt(ranges[1])) {

                    // Append , in between them
                    buffer.append(number + ", ");
                    number++;
                }
            }

            // If we reaches here then
            // word does contains "-"
            else {
                buffer.append(word + ", ");
            }
        }

        // Return the StringBuffer object
        return buffer.toString();
    }

    // Method 2
    // Main driver method
    public static void main(String[] args)
    {
        // Custom input string
        String input = "1-5, 8, 11-14, 18, 20, 26-29";

        // Calling the method 1 as created above
        System.out.println(generateStringOn(input));
    }
}
```

**Output**

```
1, 2, 3, 4, 5, 8, 11, 12, 13, 14, 18, 20, 26, 27, 28, 29, 
```