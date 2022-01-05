# 检查一个字符串在 Java 中是否只包含字母

> 原文:[https://www . geesforgeks . org/check-if-a-string-contains-only-alphabets-in-Java/](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java/)

给定一个字符串，任务是编写一个 Java 程序来检查该字符串是否只包含字母。如果是，那么打印真，否则打印假。

**示例:**

> **输入:** GeeksforGeeks
> **输出:** true
> **解释:**给定的字符串只包含字母，因此输出为 true。
> 
> **输入:**geeksforgeeck 2020
> **输出:**假
> **解释:**给定字符串包含字母和数字，因此输出为假。
> 
> **输入:**
> **输出:**假
> **说明:**给定字符串为空，因此输出为假。

**方法 1:** 这个问题可以用 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)来解决。该方法请参考[这篇文章](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-ascii-values/)。

**方法二:**这个问题可以用[λ表达式](https://www.geeksforgeeks.org/lambda-expressions-java-8/)来解决。该方法请参考[这篇文章](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-lambda-expression/)。

**方法三:**这个问题可以用[正则表达式](https://www.geeksforgeeks.org/regular-expressions-in-java/)解决。该方法请参考[这篇文章](https://www.geeksforgeeks.org/check-if-a-string-contains-only-alphabets-in-java-using-regex/)。

**方法 4:** 该方法使用 Java 中[字符类的方法](https://www.geeksforgeeks.org/character-class-java/)

*   其思想是使用 **Character.isLetter()方法**对字符串的每个字符进行迭代，检查指定的字符是否为字母。
*   如果字符是字母，则*继续*，否则返回*假*。
*   如果我们能够迭代整个字符串，那么返回*真*。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    // Function to check if a string
    // contains only alphabets
    public static boolean onlyAlphabets(
      String str, int n)
    {

        // Return false if the string
        // has empty or null
        if (str == null || str == "") {
            return false;
        }

        // Traverse the string from
        // start to end
        for (int i = 0; i < n; i++) {
            // Check if the specified
            // character is not a letter then
            // return false,
            // else return true
            if (!Character
                .isLetter(str.charAt(i))) {
                return false;
            }
        }
        return true;
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given string str
        String str = "GeeksforGeeks";
        int len = str.length();

        // Function Call
        System.out.println(
          onlyAlphabets(str, len));
    }
}
```

**Output**

```
true

```