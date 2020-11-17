# Java 程序的输出 | 系列 55（Java 集合框架）

> 原文：[https://www.geeksforgeeks.org/output-of-java-programs-set-55-java-collections-framework/](https://www.geeksforgeeks.org/output-of-java-programs-set-55-java-collections-framework/)

**先决条件**：[Java 集合框架](https://www.geeksforgeeks.org/java-collection-tutorial/)。

> **1\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void main(String[] args)
{
ArrayList<Integer> arr = new ArrayList<Integer>();
arr.add( 11 );
arr.add( 2 );
arr.add( 3 );
arr.add( 5 );
arr.add( 7 );
arr.remove( new Integer( 7 ));
arr.remove( 2 );
for ( int i = 0 ; i < arr.size(); i++)
System.out.print(arr.get(i) + " " );
}
}
```

**A.** 编译错误。

**B.** 11 3 5

**C.** 11 2 5

```
Answer: C.
```

**说明**：[`ArrayList.remove()`](https://www.geeksforgeeks.org/arraylist-linkedlist-remove-methods-java-examples/)方法采用索引或`Integer`类对象。 在这里，它获取索引并删除该索引处的元素。 因此，当我们使用`new Integer(7)`时，它将从[`ArrayList`](https://www.geeksforgeeks.org/arraylist-in-java/)中删除值 7。

> **2\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
Deque<Integer> dq = new LinkedList<Integer>();
dq.offerFirst( 1 );
dq.offerFirst( 2 );
dq.offerFirst( 3 );
dq.offerLast( 4 );
Queue<Integer> q = new LinkedList<Integer>();
Iterator it = dq.descendingIterator();
while (it.hasNext()) {
System.out.print(it.next() + " " );
}
}
}
```

**A.** 1 2 3 4

**B.** 4 1 2 3

**C.** 4 3 2 1

```
Answer: B.
```

**说明**：[双端队列](https://www.geeksforgeeks.org/deque-interface-java-example/)是双端队列，可以在其中插入数据以及从两端删除数据。 当我们使用[`escentingIterator()`](https://www.geeksforgeeks.org/deque-descendingiterator-method-in-java/)时，我们实际上以与存储数据相反的顺序获取输出。

> **3.以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
Set<Integer> h1
= new TreeSet<Integer>(
Collections.reverseOrder());
h1.addAll(
Arrays.asList(
new Integer[] { 1 , 2 , 3 ,
3 , 5 , 6 ,
7 , 1 , 4 }));
for ( int h : h1)
System.out.print(h + " " );
}
}
```

**A.** 1 2 3 3 5 6 7 1 4

**B.** 3 2 1 7 6 4 5

**C.** 7 6 5 4 3 2 1

**D.** 1 2 3 4 5 6 7

```
Answer: C.
```

**说明**：[集合](https://www.geeksforgeeks.org/set-in-java/)不存储重复值。 [`TreeSet`](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)以排序顺序（即升序）存储数据，但是在这里，我们使用[`Collections.reverseOrder()`](https://www.geeksforgeeks.org/collections-reverseorder-java-examples/)使其明确地以降序存储数据。

> **4\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
Set<Integer> h1 = new LinkedHashSet<Integer>();
Stack<Integer> s1 = new Stack<Integer>();
for ( int i = 0 ; i < 6 ; i++)
h1.add(i);
for ( int h : h1) {
s1.push(h);
}
while (!s1.isEmpty()) {
System.out.print(s1.pop() + " " );
}
} [
}
```

**A.** 3 4 1 2 5 0

**B.** 5 4 3 2 1 0

**C.** 1 2 3 4 5 0

**D.** 3 1 2 5 0 4

```
Answer: B.
```

**说明**：[`LinkedHashSet`](https://www.geeksforgeeks.org/linkedhashset-in-java-with-examples/)不存储任何重复值，而是按原始插入顺序存储数据。 另外，[栈](https://www.geeksforgeeks.org/stack-class-in-java/)是 [LIFO 数据结构](https://www.geeksforgeeks.org/lifo-last-in-first-out-approach-in-programming/)。 因此，弹出在栈中的最新插入的值。

> **5\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
LinkedHashMap<String, Integer> hm
= new LinkedHashMap<String, Integer>();
hm.put( "John" , 1 );
hm.put( "Ron" , 2 );
hm.put( "George" , 3 );
hm.put( "Ray" , 4 );
for (Map.Entry<String, Integer> e : hm.entrySet())
System.out.println(
e.getKey() + " "
+ e.getValue());
[
}
}
```

**A.**

```
   Ray 4
   George 3
   John 1
   Ron 2

```

**B.**

```
   John 1
   Ron 2
   George 3
   Ray 4

```

**C.**

```
   Ray 4
   George 3
   Ron 2 
   John 1 

```

```
Answer: B.
```

**说明**：[`LinkedHashMap`](https://www.geeksforgeeks.org/linkedhashmap-class-java-examples/)按插入顺序存储数据。

> **6\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
HashMap<String, Integer> hm
= new HashMap<String, Integer>();
hm.put( "Karan" , 1 );
hm.put( "Deepak" , 2 );
hm.put( "Aman" , 3 );
hm.put( "Ayan" , 4 );
TreeMap<String, Integer> hm1
= new TreeMap<String, Integer>();
hm1.putAll(hm);
for (Map.Entry<String, Integer>
entry : hm1.entrySet())
System.out.println(
entry.getKey()
+ " " + entry.getValue());
}
}
```

**A.**

```
Karan 1
Ayan 4
Deepak 2
Aman 3
```

**B.**

```
Karan 1
Deepak 2
Aman 3
Ayan 4
```

**C.**

```
Karan 1
Deepak 2
Ayan 4
Aman 3
```

**D.**

```
Aman 3
Ayan 4
Deepak 2
Karan 1
```

```
Answer: D.
```

**说明**：[`TreeMap`](https://www.geeksforgeeks.org/treemap-in-java/)以键值的排序顺序存储数据。

> **7\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
Stack<Integer> s1 = new Stack<Integer>();
Queue<Integer> q = new LinkedList<Integer>();
for ( int i = 0 ; i < 5 ; i++)
s1.push(i);
while (s1.isEmpty())
q.add(s1.pop());
System.out.print(q.peek());
}
}
```

**A.** 4

**B.** 0

**C.** 编译错误

**D.** null

```
Answer: D.
```

**说明**：由于未在[队列](https://www.geeksforgeeks.org/queue-interface-java/)内放置任何值，因此`while`循环的条件为`false`。

> **8\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
HashSet<Integer> h1 = new HashSet<Integer>();
h1.addAll(
Arrays.asList(
new Integer[] { 1 , 2 , 2 ,
3 , 6 , 4 ,
4 , 0 , 7 , 5 }));
h1.remove( 1 );
h1.remove( 2 );
h1.remove( 4 );
for ( int h : h1)
System.out.print(h + " " );
}
}
```

**A.** 1 3 4 4 0 7 5

**B.** 2 3 6 4 0 7 5

**C.** 0 3 5 6 7 [

D. 5 6 3 2 0 7 4

```
Answer: C.
```

**说明**：[`HashSet`](http://www.geeksforgeeks.org/hashset-in-java/)不包含任何重复值。 因此 2 和 4 仅存储一次。 调用`remove`函数时，它将删除作为参数传递给该函数的值。

> **9\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
TreeSet<Integer> ts
= new TreeSet<Integer>();
ts.add( 101 );
ts.add( 76 );
ts.add( 89 );
ts.add( 7 );
System.out.print(ts.first() + " " );
ts.remove( 7 );
System.out.print(ts.last() + " " );
System.out.print(ts.first() + " " );
[ }
}
```

**A.** 101 89 101

**B.** 7 76 101

**C.** 7 101 76

```
Answer: C.
```

**说明**：[`TreeSet`](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)以排序顺序（升序）存储值。 同样， [`TreeSet.first()`](https://www.geeksforgeeks.org/treeset-first-method-in-java/)返回最小值， [`TreeSet.last()`](https://www.geeksforgeeks.org/treeset-last-method-in-java/)返回该集中存在的最大值。

> **10\. 以下 Java 程序的输出是什么？**

```
import java.util.*;
class Demo {
public static void ] main(String[] args)
{
Deque<Integer> dq
= new LinkedList<Integer>();
Stack<Integer> s1
= new Stack<Integer>();
dq.addFirst( 10 );
dq.addFirst( 20 );
dq.addLast( 30 );
dq.addFirst( 40 );
while (!dq.isEmpty())
s1.push(dq.poll());
while (!s1.isEmpty())
System.out.print(s1.pop() + " " );
}
}
```

**A.** 30 10 20 40

**B.** 40 30 20 10

**C.** 编译错误。

**D.** 40 20 10 30

```
Answer: C.
```

**说明**：由于[双端队列](https://www.geeksforgeeks.org/deque-interface-java-example/)是[接口](https://www.geeksforgeeks.org/interfaces-in-java/)，因此可以在[`LinkedList`类](https://www.geeksforgeeks.org/linked-list-in-java/)的帮助下实例化它。



* * *

* * *



