# Java 中的按位右移运算符

> 原文:[https://www . geesforgeks . org/bitwise-shift-operators-in-Java/](https://www.geeksforgeeks.org/bitwise-shift-operators-in-java/)

在 C/C++中，只有一个右移位运算符“> >”，它应该只用于正整数或无符号整数。C/C++中不建议对负数使用右移运算符，当用于负数时，输出取决于编译器。与 C++不同，Java 支持以下两种右移运算符。

这里我们将讨论两种右移运算符，如下所示:

*   **[signed right shift] > >**
*   **Unsigned right shift 】> > >**

### 类型 1:带符号右移

在 Java 中，运算符“> >”是带符号的右移位运算符。所有的整数在 Java 中都是有符号的，负数用>>就可以了。运算符“> >”使用符号位(最左边的位)来填充移位后的尾随位置。如果数字为负，则使用 1 作为填充符，如果数字为正，则使用 0 作为填充符。例如，如果一个数的二进制表示是**1**0…100，那么使用> >将其右移 2 将使其成为**11**……1。

**示例:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Illustrate Signed Right Shift Operator

// Main class
class GFG {

    // Main driver method
    public static void main(String args[])
    {

        int x = -4;
        System.out.println(x >> 1);

        int y = 4;
        System.out.println(y >> 1);
    }
}
```

**Output**

```
-2
2
```

### 类型 2:无符号右移运算符

在 Java 中，运算符“> > >”表示无符号右移运算符，并且总是填充 0，而不管数字的符号是什么。

**示例:**

## Java

```
// Java Program to Illustrate Unsigned Right Shift Operator

// Main class
class GFG {

    // main driver method
    public static void main(String args[])
    {

        // x is stored using 32 bit 2's complement form.
        // Binary representation of -1 is all 1s (111..1)
        int x = -1;

        // The value of 'x>>>29' is 00...0111
        System.out.println(x >>> 29);

        // The value of 'x>>>30' is 00...0011
        System.out.println(x >>> 30);

        // The value of 'x>>>31' is 00...0001
        System.out.println(x >>> 31);
    }
}
```

**输出**

```
7
3
1
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。