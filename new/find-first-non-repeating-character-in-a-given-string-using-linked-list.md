# 使用链表

> 原文：[https://www.geeksforgeeks.org/find-first-non-repeating-character-in-a-given-string-using-linked-list/](https://www.geeksforgeeks.org/find-first-non-repeating-character-in-a-given-string-using-linked-list/)

查找给定字符串中的第一个非重复字符

给定长度为 **L** 的字符串 **str** ，任务是查找字符串中第一个非重复字符。

**示例**：

> **输入**：str =“ geeksforgeeks”
> **输出**：f
> 
> **输入**：str =“编程器”
> **输出**：p

**注意**：请参考[本文](https://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/)的 HashMap 方法，[本文](https://www.geeksforgeeks.org/first-non-repeating-character-using-one-traversal-of-string-set-2/)作为空间优化的方法。

**链表方法**：的想法是使用[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)来跟踪字符串中的唯一元素。 下面是该方法的说明：

*   为字符串中的每个字符遍历字符串，并根据以下条件在链表中添加该字符：

    *   如果链表中已经存在该字符，则从链表中删除现有的字符节点。

    *   否则，将字符添加到链表中。

*   最后，链表的第一个节点处的字符是字符串的第一个非重复字符。

下面是上述方法的实现：

## Java

```java

// Java implementation to find the  
// first non-repeating element  
// of the string using Linked List  

import java.util.LinkedList;  

public class FirstNonRepeatingElement {  

    // Function to find the first  
    // non-repeating element of the  
    // given string using Linked List  
    static void firstNonRepElement(String str)  
    {  
        LinkedList<Character> list  
            = new LinkedList<Character>();  

        list.add(str.charAt(0));  

        for (int i = 1; i < str.length(); i++) {  
            if (list.contains(str.charAt(i)))  
                list.remove(list.indexOf(  
                    str.charAt(i)));  
            else
                list.add(str.charAt(i));  
        }  
        System.out.println(list.get(0));  
    }  

    // Driver Code  
    public static void main(String[] args)  
    {  
        String str = "geeksforgeeks";  

        // Function Call  
        firstNonRepElement(str);  
    }  
} 

```

## C#

```cs

// C# implementation to find the 
// first non-repeating element 
// of the string using Linked List 
using System;  
using System.Collections;  
using System.Collections.Generic; 

class FirstNonRepeatingElement{ 

// Function to find the first 
// non-repeating element of the 
// given string using Linked List 
static void firstNonRepElement(string str) 
{ 
    LinkedList<char> list = new LinkedList<char>(); 

    list.AddLast(str[0]); 

    for(int i = 1; i < str.Length; i++)  
    { 
        if (list.Contains(str[i])) 
            list.Remove(str[i]); 
        else
            list.AddLast(str[i]); 
    } 
    Console.Write(list.First.Value); 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    string str = "geeksforgeeks"; 

    // Function call 
    firstNonRepElement(str); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output**

```
f

```

**效果分析**：

*   **时间复杂度**：O（N * 26）

*   **辅助空间**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。