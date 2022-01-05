# 布尔搜索

> 原文:[https://www.geeksforgeeks.org/boolean-search/](https://www.geeksforgeeks.org/boolean-search/)

在本文中，我们将了解什么是布尔表达式。

在直接开始主题之前，让我们看看**什么是布尔表达式**，所以它是一个在求值时总是产生两个值的表达式，要么是真，要么是假。如果条件为真，那么它将返回真或假，反之亦然。

让我们举一个简单的例子，它将明确布尔表达式的概念，所以表达式(5>2)，即 5 大于 2，正如我们所看到的，它是真的，意味着 5 大于 2，因此结果将是真的，因为我们可以看到表达式产生真值，因此它被称为布尔表达式。

**需要布尔运算符:**
当要计算两个以上的表达式时，如(表达式 1，表达式 2)，因此使用布尔运算符完成，因此我们需要使用布尔运算符连接它们，如(表达式 1，布尔运算符，表达式 2)

**布尔运算符** **:**
布尔运算符用于连接两个以上的表达式，以便对它们进行求值。当您想要计算多个表达式时，我们使用布尔运算符，并使用该运算符计算多个表达式，我们得到的答案是真还是假

**布尔运算符的类型:**

*   在大多数情况下，它可以用作 AND，或者它取决于编程语言，如在 C CPP 编程中，它被表示为&和
*   或在大多数情况下，它可以用作运行经验，或者它也取决于编程语言，如在 C CPP 编程中，它被表示为||
*   NOT 也表示为 NOT 或者像 C CPP 编程中那样依赖表示为！(感叹号)

**布尔运算符的使用:**

*   当您希望两个表达式都计算为真时，使用 AND 运算符。
*   当您希望两个表达式中的任何一个都被计算为真时，使用或运算符。

**布尔表达式的应用:**

*   布尔表达式用于编程概念，如 if else 条件、开关情况等。
*   它用于布尔代数、数字逻辑和设计。

**示例-** 让我们使用布尔运算符和表达式检查 5 是否大于 2 且小于 10，因此在编程中，它们将写成(5 > 2 & & 5 < 10)，因为我们希望两个表达式都被评估为真，所以我们使用了 and，因此这个布尔表达式的结果将为真，因为 5 大于 2 且小于 10，因此它将产生 GFG！作为下面给出的程序的输出，它还包括各种例子。

## C++

```
#include <iostream>
using namespace std;

int main()
{

    if (5 > 2&&5<10)  //checking if 5 is greater then 2 and 5 less then 10
        cout << "GFG!";
    else
        cout << "GeeksforGeeks";
    return 0;
}
```

## C

```
#include <stdio.h>

int main()
{

    if (5 > 2||5<1)  //checking if 5 is greater then 2 or 5 less then 1
        printf("GFG!");
    else
        printf("GeeksforGeeks");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    public static void main(String[] args)
    {

        if (5 > 6&&5<10)  //checking if 5 is greater then 6 and less then 10
            System.out.println("GFG!");
        else
            System.out.println("GeeksforGeeks");
    }
}
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Driver Code
public static void Main()
{
    if (5 > 6&&5<10)  //checking if 5 is greater then 6 and less then 10
        Console.Write("GFG!");
    else
        Console.Write("GeeksforGeeks");
}
}

// This code is contributed by sanjoy_62.
```

## C++14

```
#include <iostream>
using namespace std;

int main()
{

    if (5 > 2&&5<10)   //checking if 5 is greater then 2 and less then 10
        cout << "GFG!";
    else
        cout << "GeeksforGeeks";
    return 0;
}
```

## java 描述语言

```
<script>

// javascript program for above approach

// Driver code

    if (5 > 6&&5<10)  //checking if 5 is greater then 6 and less then 10
        document.write("GFG!");
    else
        document.write("GeeksforGeeks");

    // This code is contributed by code_hunt.
</script>
```

布尔表达式用于许多领域，如编程和数字逻辑，因为它使任务和逻辑清晰，从而提高了程序的效率和可读性。