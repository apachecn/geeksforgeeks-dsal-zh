# 用于解析分子并获取原子数的程序

> 原文：[https://www.geeksforgeeks.org/program-to-parse-the-molecules-and-get-the-atoms-count/](https://www.geeksforgeeks.org/program-to-parse-the-molecules-and-get-the-atoms-count/)

给定化学式为字符串，任务是获取该化学式中的原子数。

**示例**：

```
Input: str = "Fe2H3OH"
Output: Fe 2
        H 4
        O 1

Input: str = "NaCl2NaO2"
Output: Na 2
        Cl 2
        O 2

```

**方法**：以下方法在 Java 编程语言中起作用：

*   以[`LinkedHashMap`](https://www.geeksforgeeks.org/linkedhashmap-class-java-examples/)按插入顺序存储原子名称（键）和计数（值）。

*   检查字符串字符是否为小写，然后添加到前一个大写的字符串字符。

*   检查字符串是否包含数字，然后将计数（值）添加到其特定的原子名称（键）。

*   打印原子名称（键）和计数（值）。

下面是上述方法的实现：

```
// Java program to parse the molecule
// and get the atoms count
import java.io.*;
import java.util.*;
class GFG {
static void getCount(String str)
{
// Use LinkedHashmap to store
// elements in insertion oreder
Map<String, Integer> mp
= new LinkedHashMap<String, Integer>();
for ( int i = 0 ; i < str.length(); i++) {
int count = 0 ;
// Convert the string element into character
char c = str.charAt(i);
String a = " " ;
// Convert the character element [HT G270]
// into string element
a = String.valueOf(c);
// Check string contains the Capital A - Z value.
if (a.matches( "[A-Z]" )) {
for ( int j = i + 1 ; j < str.length(); j++) {
char d = str.charAt(j);
String b = String.valueOf(d);
// Check string contains the small a-z value.
if (b.matches( "[a-z]" )) {
a += b;
if (mp.get(a) == null )
mp.put(a, 1 );
else
mp.put(a, mp.get(a) + 1 );
count = 1 ;
[
[HTG1 11] }
[
// Check string contains the number value.
else if (b.matches( "[\\d]" )) {
int k = Integer.parseInt(b);
mp.put(a, k);
count = 1 ;
}
else {
i = j - 1 ;
break ;
}
}
if (count == 0 ) {
if (mp.get(a) == null )
mp.put(a, 1 );
else
mp.put(a, mp.get(a) + [HTG1 68] );
}
}
}
System.out.println( "\nAtom count:" );
for (Map.Entry<String, Integer>
entry : mp.entrySet())
System.out.println(entry.getKey()
+ " "
+ entry.getValue());
mp.clear();
}
// Driver code
public static void main(String[] args)
{
String str = "Fe2H3OH" ;
System.out.println( "Given molecule: "
+ str);
getCount(str);
} [HTG39 8]
}
```

**输出**：

```
Given molecule: Fe2H3OH

Atom count:
Fe 2
H 4
O 1

```



* * *

* * *



