# 在给定的句子中查找字谜最多的单词

给定句子形式的字符串 **S** ，任务是从文本中查找具有 [**字谜**](https://www.geeksforgeeks.org/tag/anagram/) 出现在给定句子中。
**例如：** [

> **输入：** S =“请保持沉默，听听教授的话” 单词“ **沉默**”的句子中带有一个字谜（**听**）。
> **输入：** S =“当政府采取行动时，猫不是狗，没有剑，所以什么是 TAC？”
> **输出：**猫
> **解释：**
> 单词“ **cat** ”在句子中有两个字谜（“ act”，“ tac”）。
> 单词“ **单词**”在句子中带有一个字谜（“剑”）。
> 因此，带有最大字谜的单词是**“猫”** 。

**方法：**
需要观察以下问题才能解决程序：

> [**质数的属性 **质数。****](https://www.geeksforgeeks.org/prime-numbers/)

请按照以下步骤解决问题：

*   为每个字母分配一个不同的**质数**。
*   对于给定字符串中的每个单词，计算分配给该单词字符的素数乘积，并将其存储在 **HashMap** 中。
*   计算分配给单词字符的质数乘积，并将其存储在 [**HashMap**](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中。
*   在 **HashMap** 中找到频率最高的产品，并打印相应的字谜之一作为答案。

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

**Output:** 

```
silent

```

***时间复杂度：** O（N），N 是不包括空格的字符串的长度。*
***辅助空间：** O（N）*



* * *

* * *



