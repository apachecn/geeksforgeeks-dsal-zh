# Java 中开关盒中的字符串

> 原文:[https://www . geesforgeks . org/string-in-switch-case-in-Java/](https://www.geeksforgeeks.org/string-in-switch-case-in-java/)

[开关语句](https://www.geeksforgeeks.org/switch-statement-in-java/)是多路分支语句。它提供了一种简单的方法，可以根据表达式的值将执行分派到代码的不同部分。基本上，表达式可以是字节、短、字符和 int 基本数据类型。从 JDK7 开始，它还可以处理枚举类型([枚举(java 中的](https://www.geeksforgeeks.org/enum-in-java/))、[字符串类](https://www.geeksforgeeks.org/string-class-in-java/)和[包装类](https://www.geeksforgeeks.org/primitive-wrapper-classes-are-immutable-in-java/)。

因此，switch 语句中的字符串概念在 JDK 7 中出现，因为我们可以使用字符串或常量来控制 switch 语句，而这在 C/C++中是不可能的。与使用 if/else 语句的等效序列相比，使用基于字符串的开关是一种改进。我们现在将字符串声明为字符串类对象，如下所示:

**插图:**

```
String geeks = "GeeksforGeeks" ; // Valid from JDK7 and onwards 
Object geeks = "GeeksforGeeks" ; // Invalid from JDK7 and onwards 
```

在使用 switch 语句时，有一些关键点需要记住，因为它确实提供了便利，但同时也是一把双刃剑，因此我们最好仔细研究一下列出的特性:

**1。昂贵的操作:**在执行方面，打开字符串可能比打开原始数据类型更昂贵。因此，最好只在控制数据已经是字符串形式的情况下才打开字符串。

**2。字符串不应为空:**使用字符串时，确保任何 switch 语句中的表达式不为空，以防止在运行时引发[空指针异常](http://www.geeksforgeeks.org/null-pointer-exception-in-java/)。

**3。区分大小写比较:**switch 语句将表达式中的 String 对象与每个大小写标签相关联的表达式进行比较，就像它使用 String 类的 *equals()方法*一样。因此，switch 语句中 String 对象的比较区分大小写。

**4。比 if-else 更好:**Java 编译器通常从使用 String 对象的 switch 语句生成比从链式 if-then-else 语句生成更高效的字节码。

**例 1:**

## Java

```
// Java Program to Demonstrate use of String to
// Control a Switch Statement

// Main class
public class GFG {

    // Main driver method
    public static void main(String[] args)
    {

        // Custom input string
        String str = "two";

        // Switch statement over above string
        switch (str) {

        // Case 1
        case "one":

            // Print statement corresponding case
            System.out.println("one");

            // break keyword terminates the
            // code execution here itself
            break;

        // Case 2
        case "two":

            // Print statement corresponding case
            System.out.println("two");
            break;

        // Case 3
        case "three":

            // Print statement corresponding case
            System.out.println("three");
            break;

        // Case 4
        // Default case
        default:

            // Print statement corresponding case
            System.out.println("no match");
        }
    }
}
```

**输出**

```
two
```

**例 2:**

## Java

```
// Java Program to Demonstrate use of String to
// Control a Switch Statement

// Main class
public class GFG {

    // Main driver method
    public static void main(String[] args)
    {

        // Custom input string
        // Null string is passed
        String str = "";

        // Switch statement over above string
        switch (str) {

        // Case 1
        case "one":

            // Print statement corresponding case
            System.out.println("one");

            // break keyword terminates the
            // code execution here itself
            break;

        // Case 2
        case "two":

            // Print statement corresponding case
            System.out.println("two");
            break;

        // Case 3
        case "three":

            // Print statement corresponding case
            System.out.println("three");
            break;

        // Case 4
        // Default case
        default:

            // Print statement corresponding case
            System.out.println("no match");
        }
    }
}
```

**输出**

```
no match
```

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。