# `K`个出现次数最多的字符串

> 原文：[https://www.geeksforgeeks.org/k-most-occurring-strings/](https://www.geeksforgeeks.org/k-most-occurring-strings/)

给定`N`个字符串的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`和一个整数`K`，任务是打印`K`在`arr[]`中出现次数最多的字符串。 如果两个或两个以上的字符串具有相同的频率，请打印[词典序最小的字符串](https://www.geeksforgeeks.org/lexicographically-smallest-string-obtained-concatenating-array/)。

**注意**：`K`的值始终小于或等于数组中不同元素的数量。

**示例**：

> **输入**：`str[] = {"geeks", "geeksforgeeks", "geeks", "article"}, K = 1 `
>
> **输出**：`"geeks"`
>
> **解释**：
>
> ```
> "geeks" –> 2 
> "geeksforgeeks" –> 1 
> "article" –> 1 
> ```
> 
> 因此，出现次数最多的字符串是`"geeks"`。
> 
> **输入**：`str[] = {"car", "bus", "car", "bike", "car", "bus", "bike", "cycle"}, K = 2` 
>
> **输出**：`"car", "bus"`
>
> **说明**：
> 
> ```
> "car" –> 3 
> "bus" –> 2 
> "bike" –> 2 
> "cycle" –> 1 
> ```
>
> 字符串`"car"`的频率最高，字符串`"bus"`和`"bike"`的频率均次高，但字符串`"bus"`在字典上很小，因为它的长度较短。

**方法**：

1.  计算数组中每个字符串的频率，并将其存储在 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中，其中字符串是键，而频率是值。

2.  现在，按照**升序**的频率对这些键进行排序，这样做是为了将频率最低的键保持在顶部。

3.  频率相等的字符串按字母顺序优先，即**的字母顺序更高的字符串具有更高的优先级**。

4.  从`HashMap`中删除顶部的`N – K`个键值对。 这样，容器将以，**最高频率的 `K`个键保持相反的顺序**。

5.  打印存储在`HashMap`中的字符串。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach 
import java.util.*; 

class FrequentWords { 

    // Function that returns list of K 
    // most frequent strings 
    public static ArrayList<String> 
    frequentWords(ArrayList<String> arr, int K) 
    { 

        // Hash map to store the frequency 
        // of each string 
        HashMap<String, Integer> Freq 
            = new HashMap<>(); 

        // Set the default frequency of 
        // each string 0 
        for (String word : arr) { 
            Freq.put(word, 
                     Freq.getOrDefault(word, 0) 
                         + 1); 
        } 

        // Using a priority queue to store 
        // the strings in accordance of the 
        // frequency and alphabetical order 
        // (if frequency is equal) 

        // Lambda expression is used set the 
        // priority, if frequencies are not 
        // equal than the string with greater 
        // frequency is returned else the 
        // string which is lexically smaller 
        // is returned 
        PriorityQueue<String> Order 
            = new PriorityQueue<>( 
                (a, b) 
                    -> (Freq.get(a) != Freq.get(b)) 
                           ? Freq.get(a) - Freq.get(b) 
                           : b.compareTo(a)); 

        // Traverse the HashMap 
        for (String word : Freq.keySet()) { 
            Order.offer(word); 

            // Remove top (N - K) elements 
            if (Order.size() > K) { 
                Order.poll(); 
            } 
        } 

        // Order queue has K most frequent 
        // strings in a reverse order 
        ArrayList<String> ans 
            = new ArrayList<>(); 

        while (!Order.isEmpty()) { 
            ans.add(Order.poll()); 
        } 

        // Reverse the ArrayList so as 
        // to get in the desired order 
        Collections.reverse(ans); 

        return ans; 
    } 

    // Driver Code 
    public static void
        main(String[] args) 
    { 
        int N = 3, K = 2; 

        // Given array 
        ArrayList<String> arr 
            = new ArrayList<String>(); 
        arr.add("car"); 
        arr.add("bus"); 
        arr.add("car"); 

        // Function Call 
        ArrayList<String> ans 
            = frequentWords(arr, K); 

        // Print the K most occurring strings 
        for (String word : ans) { 
            System.out.println(word + " "); 
        } 
    } 
}

```

**Output:**

```
car 
bus

```

**时间复杂度**：`O（N * log2(N))`

**辅助空间**：`O(n)`



* * *

* * *



