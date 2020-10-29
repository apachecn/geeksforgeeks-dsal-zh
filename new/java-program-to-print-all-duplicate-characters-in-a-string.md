# Java 程序以字符串形式打印所有重复的字符

> 原文：[https://www.geeksforgeeks.org/java-program-to-print-all-duplicate-characters-in-a-string/](https://www.geeksforgeeks.org/java-program-to-print-all-duplicate-characters-in-a-string/)

给定字符串，任务是编写 [Java](http://www.geeksforgeeks.org/java/) 程序以按频率打印所有重复的字符

**示例**：

> **输入**：str =“ geeksforgeeks”
> **输出**：
> s：2
> e：4
> g：2
> k：2
> 
> **输入**：str =“ java”
> **输出**：
> a：2

**方法**：的想法是使用 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 进行[散列](http://www.geeksforgeeks.org/hashing-data-structure/)。

*   创建类型为 **{char，int}** 的 hashMap。

*   遍历字符串，检查 **hashMap** 是否已包含遍历的字符。

*   如果存在，则增加计数或在频率为 1 的哈希图中插入字符。

*   现在，遍历哈希图并查找频率大于 1 的字符。以它们各自的频率打印这些字符。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach 
import java.util.*; 
class GFG { 

    // Function to print all duplicate 
    // characters in string using HashMap 
    public static void
    countDuplicateCharacters(String str) 
    { 

        // Creating a HashMap containing char 
        // as a key and occurrences as a value 
        Map<Character, Integer> map 
            = new HashMap<Character, Integer>(); 

        // Converting given string into 
        // a char array 
        char[] charArray = str.toCharArray(); 

        // Checking each character 
        // of charArray 
        for (char c : charArray) { 

            if (map.containsKey(c)) { 

                // If character is present 
                // in map incrementing it's 
                // count by 1 
                map.put(c, map.get(c) + 1); 
            } 
            else { 

                // If character is not present 
                // in map putting this 
                // character into map with 
                // 1 as it's value. 
                map.put(c, 1); 
            } 
        } 

        // Traverse the HashMap, check 
        // if the count of the character 
        // is greater than 1 then print 
        // the character and its frequency 
        for (Map.Entry<Character, Integer> entry : 
             map.entrySet()) { 

            if (entry.getValue() > 1) { 
                System.out.println(entry.getKey() 
                                   + " : "
                                   + entry.getValue()); 
            } 
        } 
    } 

    // Driver Code 
    public static void
    main(String args[]) 
    { 
        // Given String str 
        String str = "geeksforgeeks"; 

        // Function Call 
        countDuplicateCharacters(str); 
    } 
} 

```

**Output:**

```
s : 2
e : 4
g : 2
k : 2

```

**时间复杂度**：*`O(n)`*

**辅助空间**：*O（1）*



* * *

* * *



