# 在给定的句子中查找异序词最多的单词

> 原文：[https://www.geeksforgeeks.org/find-the-word-with-most-anagrams-in-a-given-sentence/](https://www.geeksforgeeks.org/find-the-word-with-most-anagrams-in-a-given-sentence/)

给定句子形式的字符串`S`，任务是从文本中查找出现在给定句子中的[**异序词**](https://www.geeksforgeeks.org/tag/anagram/)。

**例如**：

> **输入**：`S = "please be silent and listen to what the professor says"`
>
> **输出**：`silent`
>
> **解释**：单词`silent`有一个出现在句子中的异序词(`listen`)。
>
> **输入**：`S = "cat is not a dog and sword has no words when government creates act so what is tac"`
>
> **输出**：`cat`
>
> **解释**：
>
> 单词`cat`在句子中有两个异序词（`act`，`tac`）。
>
> 单词`words`在句子中带有一个异序词（`sword`）。
>
> 因此，带有最大异序词的单词是`cat`。

**方法**：

需要观察以下问题才能解决程序：

> [**质数的属性**](https://www.geeksforgeeks.org/prime-numbers/)

请按照以下步骤解决问题：

*   为每个字母分配一个不同的**质数**。

*   对于给定字符串中的每个单词，计算分配给该单词字符的质数乘积，并将其存储在`HashMap`中。

*   计算分配给单词字符的质数乘积，并将其存储在[`HashMap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)中。

*   在`HashMap`中找到频率最高的产品，并打印相应的异序词之一作为答案。

下面是上述方法的实现：

## Java

```java

// Java Program to find the word 
// with most anagrams in a sentence 
import java.util.*; 

class GFG { 

    // Function to find the word with 
    // maximum number of anagrams 
    private static String largestAnagramGrp( 
        String arr[]) 
    { 
        // Primes assigned to 26 alphabets 
        int prime[] 
            = { 2, 3, 5, 7, 11, 13, 17, 
                19, 23, 29, 31, 37, 41, 
                43, 47, 53, 59, 61, 67, 71, 
                73, 79, 83, 89, 97, 101 }; 

        int max = -1; 
        long maxpdt = -1; 

        // Stores the product and 
        // word mappings 
        HashMap<Long, String> W 
            = new HashMap<>(); 

        // Stores the frequencies 
        // of products 
        HashMap<Long, Integer> P 
            = new HashMap<>(); 

        for (String temp : arr) { 
            char c[] = temp.toCharArray(); 
            long pdt = 1; 

            // Calculate the product of 
            // primes assigned 
            for (char t : c) { 
                pdt *= prime[t - 'a']; 
            } 

            // If product already exists 
            if (P.containsKey(pdt)) { 
                P.put(pdt, P.get(pdt) + 1); 
            } 

            // Otherwise 
            else { 
                W.put(pdt, temp); 
                P.put(pdt, 1); 
            } 
        } 

        // Fetch the most frequent product 
        for (Map.Entry<Long, Integer> 
                 e : P.entrySet()) { 
            if (max < e.getValue()) { 
                max = e.getValue(); 
                maxpdt = e.getKey(); 
            } 
        } 

        // Return a string 
        // with that product 
        return W.get(maxpdt); 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        String S = "please be silent and listen"
                   + " to what the professor says "; 
        String arr[] = S.split("[ ]+"); 
        System.out.println(largestAnagramGrp(arr)); 
    } 
} 

```

## C#

```cs

// C# program to find the word 
// with most anagrams in a sentence 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to find the word with 
// maximum number of anagrams 
private static String largestAnagramGrp(String []arr) 
{ 

    // Primes assigned to 26 alphabets 
    int []prime = { 2, 3, 5, 7, 11, 13, 17, 
                    19, 23, 29, 31, 37, 41, 
                    43, 47, 53, 59, 61, 67, 71, 
                    73, 79, 83, 89, 97, 101 }; 

    int max = -1; 
    long maxpdt = -1; 

    // Stores the product and 
    // word mappings 
    Dictionary<long,  
               String> W = new Dictionary<long, 
                                          String>(); 

    // Stores the frequencies 
    // of products 
    Dictionary<long,  
               int> P = new Dictionary<long,  
                                       int>(); 

    foreach(String temp in arr)  
    { 
        char []c = temp.ToCharArray(); 
        long pdt = 1; 

        // Calculate the product of 
        // primes assigned 
        foreach(char t in c) 
        { 
            pdt *= prime[t - 'a']; 
        } 

        // If product already exists 
        if (P.ContainsKey(pdt)) 
        { 
            P[pdt] = P[pdt] + 1; 
        } 

        // Otherwise 
        else 
        { 
            W.Add(pdt, temp); 
            P.Add(pdt, 1); 
        } 
    } 

    // Fetch the most frequent product 
    foreach(KeyValuePair<long, int> e in P) 
    { 
        if (max < e.Value) 
        { 
            max = e.Value; 
            maxpdt = e.Key; 
        } 
    } 

    // Return a string 
    // with that product 
    return W[maxpdt]; 
} 

// Driver Code 
public static void Main(String []args) 
{ 
    String S = "please be silent and listen" + 
               " to what the professor says "; 

    String []arr = S.Split(' '); 

    Console.WriteLine(largestAnagramGrp(arr)); 
} 
} 

// This code is contributed by sapnasingh4991 

```

**输出**： 

```
silent

```

**时间复杂度**：`O(n)`，`N`是不包括空格的字符串的长度。

**辅助空间**：`O(n)`。



* * *

* * *



