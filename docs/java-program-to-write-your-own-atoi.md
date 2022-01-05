# 编写自己 atoi()的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-write-your-atoi/](https://www.geeksforgeeks.org/java-program-to-write-your-own-atoi/)

C 语言中的 **atoi()函数**以一个字符串(代表一个整数)为参数，返回其 int 类型的值。所以基本上这个函数是用来把字符串参数转换成整数的。

**语法:**

```
int atoi(const char strn)
```

**参数:**函数接受一个参数 **strn** ，该参数是指需要转换为其整数等价物的字符串参数。

**返回值:**如果 strn 是有效的输入，则函数返回传递的字符串数字的等效整数。如果没有发生有效的转换，则函数返回零。

**现在让我们来理解一个人可以在各种条件支持下创建自己的 atoi()函数的各种方式:**

**<u>方法 1:</u>** 以下是一个简单的转换实现，不考虑任何特例。

*   将结果初始化为 0。
*   从第一个字符开始，更新每个字符的结果。
*   对于每个字符，将答案更新为*结果=结果* 10+(s[I]–‘0’)*

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program for
// implementation of atoi
class GFG {

    // A simple atoi() function
    static int myAtoi(String str)
    {
        // Initialize result
        int res = 0;

        // Iterate through all characters
        // of input string and update result
        // take ASCII character of corresponding digit and
        // subtract the code from '0' to get numerical
        // value and multiply res by 10 to shuffle
        // digits left to update running total
        for (int i = 0; i < str.length(); ++i)
            res = res * 10 + str.charAt(i) - '0';

        // return result.
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "89789";

        // Function call
        int val = myAtoi(str);
        System.out.println(val);
    }
}

// This code is contributed by PrinciRaj1992
```

**Output**

```
89789
```

**<u>方法 2:</u>** 这个实现处理负数。如果第一个字符是“-”，则将符号存储为负数，然后使用前面的方法将字符串的其余部分转换为数字，同时将符号与数字相乘。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// implementation of atoi
class GFG {

    // A simple atoi() function
    static int myAtoi(char[] str)
    {

        // Initialize result
        int res = 0;

        // Initialize sign as positive
        int sign = 1;

        // Initialize index of first digit
        int i = 0;

        // If number is negative, then
        // update sign
        if (str[0] == '-') {
            sign = -1;

            // Also update index of first
            // digit
            i++;
        }

        // Iterate through all digits
        // and update the result
        for (; i < str.length; ++i)
            res = res * 10 + str[i] - '0';

        // Return result with sign
        return sign * res;
    }

    // Driver code
    public static void main(String[] args)
    {
        char[] str = "-123".toCharArray();

        // Function call
        int val = myAtoi(str);
        System.out.println(val);
    }
}

// This code is contributed by 29AjayKumar
```

**Output**

```
-123
```

**<u>方法 3:</u>** 这个实现*处理各种类型的错误*。如果*字符串*为空或*字符串*包含非数字字符，则返回 0，因为该数字无效。

**Output**

```
 -134
```

**<u>进场 4:</u>** 需要处理的四角案件:

*   丢弃所有前导空格
*   数字的符号
*   泛滥
*   无效输入

要删除前导空格，请运行一个循环，直到到达数字的某个字符。如果该数字大于或等于 INT_MAX/10。然后如果符号为正，返回 INT_MAX，如果符号为负，返回 INT_MIN。其他情况在以前的方法中处理。

**试运行:**

![](img/c80bdd9aad200a1b98189cea1bc5fcaf.png)

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program for
// implementation of atoi
class GFG {
    static int myAtoi(char[] str)
    {
        int sign = 1, base = 0, i = 0;

        // if whitespaces then ignore.
        while (str[i] == ' ')
        {
            i++;
        }

        // sign of number
        if (str[i] == '-' || str[i] == '+')
        {
            sign = 1 - 2 * (str[i++] == '-' ? 1 : 0);
        }

        // checking for valid input
        while (i < str.length 
               && str[i] >= '0'
               && str[i] <= '9') {

            // handling overflow test case
            if (base > Integer.MAX_VALUE / 10
                || (base == Integer.MAX_VALUE / 10
                    && str[i] - '0' > 7)) 
            {
                if (sign == 1)
                    return Integer.MAX_VALUE;
                else
                    return Integer.MIN_VALUE;
            }
            base = 10 * base + (str[i++] - '0');
        }
        return base * sign;
    }

    // Driver code
    public static void main(String[] args)
    {
        char str[] = " -123".toCharArray();

        // Function call
        int val = myAtoi(str);
        System.out.printf("%d ", val);
    }
}

// This code is contributed by 29AjayKumar
```

**Output**

```
 -123
```

**上述所有方法的复杂性分析:**

*   **时间复杂度:** O(n)。
    只需要遍历一次字符串。
*   **空间复杂度:** O(1)。
    因为不需要额外的空间。

[atoi()](http://geeksquiz.com/recursive-implementation-of-atoi/)的递归程序。

**练习:**
写你的韩元 [atof()](http://www.cplusplus.com/reference/cstdlib/atof/) 该函数将一个字符串(代表一个浮点值)作为参数，并将其值作为 double 返回。

更多详情请参考[写自己的 atoi()](https://www.geeksforgeeks.org/write-your-own-atoi/) 整篇文章！