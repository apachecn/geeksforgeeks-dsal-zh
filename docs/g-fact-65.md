# Java 中的数组

> 原文:[https://www.geeksforgeeks.org/g-fact-65/](https://www.geeksforgeeks.org/g-fact-65/)

与 C++不同，数组是 Java 中的第一类对象。例如，在下面的程序中，使用 *arr[]* 对象的成员 *length* 来访问数组的大小。

```
// file name: Main.java
public class Main {
    public static void main(String args[]) {
       int arr[] = {10, 20, 30, 40, 50};
       for(int i=0; i < arr.length; i++)
       {
             System.out.print(" " + arr[i]);              
       }
    }
}
```

产量:
*10 20 30 40 50*

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。