# 使用 Java 中的 LinkedHashMap 按出现的顺序打印字符及其频率。

给定仅包含小写字符的字符串 **str** 。 任务是按照给定字符串中出现的顺序打印字符及其频率。

**示例：**

> **输入：** str =“ geeksforgeeks”
> **输出：** g2 e4 k2 s2 f1 o1 r1
> 
> **输入：** str =“ helloworld”
> **输出：** h1 e1 l3 o2 w1 r1 d1

**方法：**逐字符遍历给定的字符串，并将所有字符串的频率存储在 [LinkedHashMap](https://www.geeksforgeeks.org/linkedhashmap-class-java-examples/) 中，该字符串维护存储它们的元素的顺序。 现在，遍历 LinkedhashMap 的元素并打印内容。

下面是上述方法的实现：

```
// Java implementation of the approach
import java.util.LinkedHashMap;
public class GFG {
[
// Function to print the characters and their
// frequencies in the order of their occurrence
static void printCharWithFreq(String str, int n)
{
// LinkedHashMap preserves the order in
LinkedHashMap<Character, Integer> lhm
= new LinkedHashMap<Character, Integer>();
// For every character of the input string
for ( int i = 0 ; i < n; i++) {
// Using java 8 getorDefault method
char c = str.charAt(i);
lhm.put(c, lhm.getOrDefault(c, 0 ) + 1 );
}
// Iterate using java 8 forEach method
charFreqMap.forEach((k,v) -> System.out.print(k + "" + v));
}
的
// Driver code
public static void main(String[] args)
{
String str = "geeksforgeeks" ;
int n = str.length();
printCharWithFreq(str, n);
}
}
```

**Output:**

```
g2 e4 k2 s2 f1 o1 r1

```

注意读者！ 现在不要停止学习。 通过 [**Java 和 Java Collections 基础课程**](https://practice.geeksforgeeks.org/courses/Java-Collections?vC=1) 以对学生方便的价格掌握所有重要的 Java 和 Collections 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。