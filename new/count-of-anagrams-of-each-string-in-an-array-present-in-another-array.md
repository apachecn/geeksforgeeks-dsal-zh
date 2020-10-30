# 另一个数组中存在的数组中每个字符串的异序词计数

> 原文：[https://www.geeksforgeeks.org/count-of-anagrams-of-each-string-in-an-array-present-in-another-array/](https://www.geeksforgeeks.org/count-of-anagrams-of-each-string-in-an-array-present-in-another-array/)

给定两个由字符串组成的数组`arr1[]`和`arr2[]`，任务是打印`arr1[]`中存在的`arr2[]`中每个字符串的字首计数。

**示例**：

> **输入**：`arr1[] = ["geeks", "learn", "for", "egeks", "ealrn"], arr2[] = ["kgees", "rof", "nrael"]`
>
> **输出**：`2 1 2`
>
> **说明**：
>
> `arr1`中`arr2[0]`（`"kgees"`）的异序词：`"geeks"`和`"egeks"`。
>
> `arr1`中`arr2[1]`（`"rof"`）的异序词：`"for"`。
>
> `arr1`中`arr2[2]`（`"nrael"`）的异序词：`"learn"`和`"ealrn`。
> 
> **输入**：`arr1[] = ["code", "to", "grow", "odce"], arr2[] = ["edoc", "wgor", "ot"]`
>
> **输出**：`2 1 1`
>
> **说明**：
>
> `arr1`中`arr2[0]`（`"edoc"`）的异序词：`"code`和`"odce"`。
>
> `arr1`中`arr2[1]`（`"wgor"`）的异序词：`"grow"`。
>
> `arr1`中`arr2[2]`（`"ot"`）的异序词：`"to"`。

**方法**：

为了解决该问题，想法是在[`HashMap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)的帮助下使用[频率计数](https://www.geeksforgeeks.org/basic/frequency-counting/)。 将每个字符串的频率以其排序形式存储在哈希映射中的`arr1[]`中。 遍历`arr2[]`，在`arr2[]`中对字符串进行排序，然后在`HashMap`中打印它们各自的频率。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to count the
// number of anagrams of
// each string in a given
// array present in
// another array

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of anagrams
void count(string arr1[],
           string arr2[],
           int n, int m)
{
    // Store the frequencies
    // of strings in arr1[]
    map<string, int> freq;

    for (int i = 0; i < n; i++) {

        // Sort the string
        sort(arr1[i].begin(),
             arr1[i].end());

        // Increase its frequency
        // in the map
        freq[arr1[i]]++;
    }

    for (int i = 0; i < m; i++) {

        // Sort the string
        sort(arr2[i].begin(),
             arr2[i].end());

        // Display its anagrams
        // in arr1[]
        cout << freq[arr2[i]]
             << " ";
    }
}

// Driver Code
int main()
{

    string arr1[] = { "geeks", "learn",
                      "for", "egeks",
                      "ealrn" };
    int n = sizeof(arr1)
            / sizeof(string);

    string arr2[] = { "kgees", "rof",
                      "nrael" };
    int m = sizeof(arr2)
            / sizeof(string);

    count(arr1, arr2, n, m);
}

```

## Java

```java

// Java program to count the number 
// of anagrams of each String in a
// given array present in
// another array
import java.util.*;

class GFG{

static String sortString(String inputString) 
{ 

    // Convert input string to char array 
    char tempArray[] = inputString.toCharArray(); 

    // Sort tempArray 
    Arrays.sort(tempArray); 

    // Return new sorted string 
    return new String(tempArray); 
} 

// Function to return the
// count of anagrams
static void count(String arr1[],
                  String arr2[],
                  int n, int m)
{

    // Store the frequencies
    // of Strings in arr1[]
    HashMap<String, Integer> freq = new HashMap<>();

    for(int i = 0; i < n; i++) 
    {

        // Sort the String
        arr1[i] = sortString(arr1[i]);

        // Increase its frequency
        // in the map
        if (freq.containsKey(arr1[i]))
        {
            freq.put(arr1[i], 
            freq.get(arr1[i]) + 1);
        }
        else
        {
            freq.put(arr1[i], 1);
        }
    }

    for(int i = 0; i < m; i++) 
    {

        // Sort the String
        arr2[i] = sortString(arr2[i]);

        // Display its anagrams
        // in arr1[]
        System.out.print(freq.get(arr2[i]) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    String arr1[] = { "geeks", "learn",
                      "for", "egeks",
                      "ealrn" };
    int n = arr1.length;

    String arr2[] = { "kgees", "rof",
                      "nrael" };
    int m = arr2.length;

    count(arr1, arr2, n, m);
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program to count the number
# of anagrams of each string in a 
# given array present in another array 

# Function to return the count of anagrams
def count(arr1, arr2, n, m):

    # Store the frequencies of 
    # strings in arr1
    freq = {}

    for word in arr1:

        # Sort the string
        word = ' '.join(sorted(word))

        # Increase its frequency
        if word in freq.keys():
            freq[word] = freq[word] + 1
        else:
            freq[word] = 1

    for word in arr2:

        # Sort the string
        word = ' '.join(sorted(word))

        # Display its anagrams
        # in arr1
        if word in freq.keys():
            print(freq[word], end = " ")
        else:
            print(0, end = " ")

    print()     

# Driver Code
if __name__ == '__main__':

    arr1 = [ "geeks", "learn", "for",
             "egeks", "ealrn" ]
    n = len(arr1)

    arr2 = [ "kgees", "rof", "nrael" ]
    m = len(arr2)

    count(arr1, arr2, n, m)

# This code is contributed by Pawan_29

```

## C#

```cs

// C# program to count the number 
// of anagrams of each String in a
// given array present in
// another array
using System;
using System.Collections.Generic;

class GFG{

static String sortString(String inputString) 
{ 

    // Convert input string to char array 
    char []tempArray = inputString.ToCharArray(); 

    // Sort tempArray 
    Array.Sort(tempArray); 

    // Return new sorted string 
    return new String(tempArray); 
} 

// Function to return the
// count of anagrams
static void count(String []arr1,
                  String []arr2,
                  int n, int m)
{

    // Store the frequencies
    // of Strings in arr1[]
    Dictionary<String,
               int> freq = new Dictionary<String,
                                          int>();

    for(int i = 0; i < n; i++) 
    {

        // Sort the String
        arr1[i] = sortString(arr1[i]);

        // Increase its frequency
        // in the map
        if (freq.ContainsKey(arr1[i]))
        {
            freq[arr1[i]] = 
            freq[arr1[i]] + 1;
        }
        else
        {
            freq.Add(arr1[i], 1);
        }
    }

    for(int i = 0; i < m; i++) 
    {

        // Sort the String
        arr2[i] = sortString(arr2[i]);

        // Display its anagrams
        // in arr1[]
        Console.Write(freq[arr2[i]] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    String []arr1 = { "geeks", "learn",
                      "for", "egeks",
                      "ealrn" };
    int n = arr1.Length;

    String []arr2 = { "kgees", "rof",
                      "nrael" };
    int m = arr2.Length;

    count(arr1, arr2, n, m);
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
2 1 2

```



* * *

* * *



