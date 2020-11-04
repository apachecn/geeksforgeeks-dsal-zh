# 以很大的数字打印所有 K 位重复数字

> 原文：[https://www.geeksforgeeks.org/print-all-k-digit-repeating-numbers-in-a-very-large-number/](https://www.geeksforgeeks.org/print-all-k-digit-repeating-numbers-in-a-very-large-number/)

给定非常大的字符串形式的 **N** 和数字 **K** ，任务是打印所有 **K 数字**重复频率大于 1\.

**示例**：

> **输入**：str =“ 123412345123456”，K = 4
> **输出**：。
> 1234 – 3
> 2345 – 2
> **说明**：
> 频率大于 1 的 4 位数字是 1234 和 2345。
> 
> **输入**：N = 1432543214325432，K = 5
> **输出**：
> 14325 – 2
> 32543 – 2
> 43254 – 2
> **说明**：
> 频率大于 1 的 5 位数字是 14325、32543 和 43254。

**方法**：由于数字是以字符串形式给出的，因此，想法是将大小为 **K** 的所有子字符串及其频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中 。 现在，在迭代 Map 时，仅打印那些频率大于 1 的子字符串及其出现的次数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach  
#include <bits/stdc++.h>  
using namespace std;  

// Function to print all K digit  
// repeating numbers  
void print_Kdigit(string S, int K)  
{  

    // Map to store the substrings  
    // with their frequencies  
    map<string, int> m;  

    // Iterate over every substring  
    // and store their frequencies  
    // in the map  
    for (int i = 0; i < S.length() - K;  
        i++) {  
        string a = S.substr(i, K);  

        // Increment the count of  
        // substrings in map  
        m[a]++;  
    }  

    // Iterate over all the substrings  
    // present in the map  
    for (auto x : m) {  

        // Condition to check if the  
        // frequency of the substring  
        // present in the map  
        // is greater than 1  
        if (x.second > 1) {  
            cout << x.first << " - "
                << x.second << "\n";  
        }  
    }  
}  

// Driver Code  
int main()  
{  
    // Given Number in form of string  
    string str = "123412345123456";  

    // Given K  
    int K = 4;  

    // Function Call  
    print_Kdigit(str, K);  
}  

```

## Java

```java

// Java program for the above approach  
import java.util.*;  

class GFG{  

// Function to print all K digit  
// repeating numbers  
static void print_Kdigit(String S, int K)  
{  

    // Map to store the substrings  
    // with their frequencies  
    Map<String, Integer> m = new HashMap<>();  

    // Iterate over every substring  
    // and store their frequencies  
    // in the map  
    for(int i = 0; i < S.length() - K; i++)  
    {  
        String a = S.substring(i, i + K);  

        // Increment the count of  
        // substrings in map  
        m.put(a, m.getOrDefault(a, 0) + 1);  

    }  

    // Iterate over all the substrings  
    // present in the map  
    for(Map.Entry<String, Integer> x : m.entrySet())  
    {  

        // Condition to check if the  
        // frequency of the substring  
        // present in the map  
        // is greater than 1  
        if (x.getValue() > 1)  
        {  
            System.out.println(x.getKey() + " - " +  
                            x.getValue());  
        }  
    }  
}  

// Driver code  
public static void main(String[] args)  
{  

    // Given Number in form of string  
    String str = "123412345123456";  

    // Given K  
    int K = 4;  

    // Function call  
    print_Kdigit(str, K);  
}  
}  

// This code is contributed by offbeat  

```

## Python3

```py

# Python3 program of the above approach  
def print_Kdigit(S, K):  

    # Dictionary to store the substrings  
    # with their frequencies  
    m = {}  

    # Iterate over every substring  
    # and store their frequencies  
    # in the dictionary  
    for i in range(len(S) - K):  
        a = S[i:i + K]  

        # Initialize the count of  
        # substrings in dictionary with 0  
        m[a] = 0

    for i in range(len(S) - K):  
        a = S[i:i + K]  

        # Increment the count of  
        # substrings in dictionary  
        m[a] += 1

    # Iterate over all the substrings  
    # present in the dictionary  
    for key, value in m.items():  
        if value > 1:  
            print(key, "-", value)  

# Driver Code  
str = "123412345123456"

# Given K  
K = 4

# Function Call  
print_Kdigit(str, K)  

# This code is contributed by Vishal Maurya  

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

// Function to print all K digit 
// repeating numbers 
static void print_Kdigit(string S, int K) 
{ 

    // Map to store the substrings 
    // with their frequencies 
    Dictionary<string,  
               int> m = new Dictionary<string, 
                                       int>(); 

    // Iterate over every substring 
    // and store their frequencies 
    // in the map 
    for(int i = 0; i < S.Length - K; i++)  
    { 
        string a = S.Substring(i, K); 

        // Increment the count of 
        // substrings in map 
        m[a] = m.GetValueOrDefault(a, 0) + 1; 
    } 

    // Iterate over all the substrings 
    // present in the map 
    foreach(KeyValuePair<string, int> x in m) 
    { 

        // Condition to check if the 
        // frequency of the substring 
        // present in the map 
        // is greater than 1 
        if (x.Value > 1) 
        { 
            Console.Write(x.Key + " - " +  
                          x.Value + "\n");  
        } 
    } 
} 

// Driver code 
public static void Main(string[] args) 
{ 

    // Given number in form of string 
    string str = "123412345123456"; 

    // Given K 
    int K = 4; 

    // Function call 
    print_Kdigit(str, K); 
} 
} 

// This code is contributed by rutvik_56 

```

**Output:** 

```
1234 - 3
2345 - 2

```

**时间复杂度**：*`O(N * K)`*



* * *

* * *



