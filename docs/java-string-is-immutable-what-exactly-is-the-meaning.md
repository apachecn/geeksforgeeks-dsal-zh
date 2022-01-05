# Java:字符串是不可变的。到底是什么意思？

> 原文:[https://www . geeksforgeeks . org/Java-string-is-immune-到底是什么意思/](https://www.geeksforgeeks.org/java-string-is-immutable-what-exactly-is-the-meaning/)

在继续讨论*不变性*之前，我们先来看一下`String`类及其功能，然后再下结论。

`[String](https://www.geeksforgeeks.org/string-class-in-java/)`是这样工作的:

```
String str = "knowledge"; 
```

像往常一样，这会创建一个包含`"knowledge"`的字符串，并为其分配一个引用`str`。够简单吗？让我们执行更多功能:

```
// assigns a new reference to the 
// same string "knowledge"
String s = str; 
```

让我们看看下面的语句是如何工作的:

```
 str = str.concat(" base"); 
```

这会将一个字符串`" base"`附加到`str`上。但是等等，既然`String`对象是不可变的，这怎么可能呢？让你惊讶的是，它是。

执行上述语句时，VM 取`String str`的值，即`"knowledge"`并追加`" base"`，给我们取值`"knowledge base"`。现在，由于`String`是不可变的，VM 不能将这个值分配给`str`，所以它创建一个新的`String`对象，给它一个值`"knowledge base"`，并给它一个引用`str`。

这里需要注意的一点是，虽然`String`对象是不可变的，**它的引用变量不是。**这就是为什么在上面的例子中，引用是为了引用一个新形成的`String`对象。

在上面的例子中，此时我们有两个`String`对象:第一个是我们用值`"knowledge"`创建的，由`s`指向，第二个是`"knowledge base"`，由`str`指向。但是，从技术上讲，我们有三个`String`对象，第三个是`concat`语句中的字面`"base"`。

# 关于字符串和内存使用的重要事实

如果我们没有另一个参考`s`到`"knowledge"`呢？我们会失去那个`String`。然而，它仍然会存在，但会因为没有引用而被认为是丢失的。
再看下面一个例子

```
/*package whatever // do not write package name here */

import java.io.*;

class GFG {
    public static void main(String[] args)
    {
        String s1 = "java";
        s1.concat(" rules");

        // Yes, s1 still refers to "java"
        System.out.println("s1 refers to " + s1);
    }
}
```

**Output:**

```
s1 refers to java

```

**发生了什么:**

1.  第一行非常简单:创建一个新的`String` `"java"`并引用`s1`给它。
2.  接下来，VM 创建另一个新的`String` `"java rules"`，但是没有任何东西引用它。于是，第二`String`就瞬间失守了。我们够不到它。

参考变量`s1`仍然是指原来的`String` `"java"`。

几乎每一种应用于`String`对象以对其进行修改的方法都会创建新的`String`对象。那么，这些`String`物件去哪里了呢？嗯，*这些都存在于内存中，任何编程语言的关键目标之一就是高效利用内存。*

随着应用程序的增长，*经常会占用大量内存，这甚至会导致冗余。*所以，为了让 Java 更高效，**JVM 留出了一个名为“[字符串常量池](https://www.geeksforgeeks.org/how-to-initialize-and-compare-strings-in-java/)的特殊内存区域。**

当编译器看到一个`String`文字时，它会在池中寻找`String`。如果找到匹配项，对新文字的引用将指向现有的`String`，并且不会创建新的`String`对象。现有的`String`只是多了一个参照物。使`String`对象不变的要点来了:

在`String`常量池中，`String`对象可能有一个或多个引用。*如果几个引用指向同一个`String`却不知道，如果其中一个引用修改了`String`值，那就不好了。这就是为什么`String`对象是不可变的。*

嗯，现在你可以说，*如果有人覆盖了`String`类的功能怎么办？*这就是**`String`类被标记为`final`** 的原因，这样就没有人可以覆盖其方法的行为。