# 查找满足 ab = cd 的所有对（a，b）和（c，d）对

> 原文：[https://www.geeksforgeeks.org/find-pairs-ab-cd-array-satisfy-ab-cd/](https://www.geeksforgeeks.org/find-pairs-ab-cd-array-satisfy-ab-cd/)

给定一个由不同整数组成的数组，任务是找到两对（a，b）和（c，d），使得 ab = cd，其中 a，b，c 和 d 是不同元素。

**示例**：

```
Input  : arr[] = {3, 4, 7, 1, 2, 9, 8}
Output : 4 2 and 1 8
Product of 4 and 2 is 8 and 
also product of 1 and 8 is 8 .

Input  : arr[] = {1, 6, 3, 9, 2, 10};
Output : 6 3 and 9 2

```

**简单解决方案**是运行四个循环以生成数组元素的所有可能的四倍。 对于每个四元组（a，b，c，d），检查 a * b = c * d。 该解决方案的时间复杂度为 O（n <sup>4</sup> ）。

此问题的**有效解决方案**是使用哈希。 我们在哈希表中将乘积用作键，将对用作值。

```
1\. For i=0 to n-1
2\.   For j=i+1 to n-1
       a) Find  prod = arr[i]*arr[j]       
       b) If prod is not available in hash then make 
            H[prod] = make_pair(i, j) // H is hash table
       c) If product is also available in hash 
          then print previous and current elements
          of array 

```

## C++

```cpp

// C++ program to find four elements a, b, c 
// and d in array such that ab = cd 
#include<bits/stdc++.h> 
using namespace std; 

// Function to find out four elements in array 
// whose product is ab = cd 
void findPairs(int arr[], int n) 
{ 
    bool found = false; 
    unordered_map<int, pair < int, int > > H; 
    for (int i=0; i<n; i++) 
    { 
        for (int j=i+1; j<n; j++) 
        { 
            // If product of pair is not in hash table, 
            // then store it 
            int prod = arr[i]*arr[j]; 
            if (H.find(prod) == H.end()) 
                H[prod] = make_pair(i,j); 

            // If product of pair is also available in 
            // then print current and previous pair 
            else
            { 
                pair<int,int> pp = H[prod]; 
                cout << arr[pp.first] << " " << arr[pp.second] 
                     << " and " << arr[i]<<" "<<arr[j]<<endl; 
                found = true; 
            } 
        } 
    } 
    // If no pair find then print not found 
    if (found == false) 
        cout << "No pairs Found" << endl; 
} 

//Driven code 
int main() 
{ 
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8}; 
    int n = sizeof(arr)/sizeof(int); 
    findPairs(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find four elements a, b, c 
// and d in array such that ab = cd 
import java.io.*; 
import java.util.*; 

class GFG { 

    public static class pair { 

        int first,second; 

        pair(int f, int s) 
        { 
            first = f; 
            second = s; 
        } 
    }; 

    // Function to find out four elements  
    // in array whose product is ab = cd 
    public static void findPairs(int arr[], int n) 
    { 

        boolean found = false; 
        HashMap<Integer, pair> hp =  
                     new HashMap<Integer, pair>(); 

        for(int i = 0; i < n; i++) 
        { 
            for(int j = i + 1; j < n; j++) 
            { 

                // If product of pair is not in  
                // hash table, then store it 
                int prod = arr[i] * arr[j]; 

                if(!hp.containsKey(prod)) 
                    hp.put(prod, new pair(i,j)); 

                // If product of pair is also  
                // available in then print  
                // current and previous pair  
                else
                { 
                    pair p = hp.get(prod); 
                    System.out.println(arr[p.first]  
                              + " " + arr[p.second] 
                              + " " + "and" + " " +  
                             arr[i] + " " + arr[j]); 
                    found = true; 
                } 
            } 
        } 

        // If no pair find then print not found 
        if(found == false) 
        System.out.println("No pairs Found"); 
    } 

    // Driver code 
    public static void main (String[] args)  
    { 
        int arr[] = {1, 2, 3, 4, 5, 6, 7, 8}; 
        int n = arr.length; 
        findPairs(arr, n);     
    } 
} 

// This code is contributed by akash1295\. 

```

## Python3

```py

# Python3 program to find four elements  
# a, b, c and d in array such that ab = cd 

# Function to find out four elements in array 
# whose product is ab = cd 
def findPairs(arr, n): 

    found = False
    H = dict() 

    for i in range(n): 

        for j in range(i + 1, n): 

            # If product of pair is not in hash table, 
            # then store it 
            prod = arr[i] * arr[j] 

            if (prod not in H.keys()): 
                H[prod] = [i, j] 

            # If product of pair is also available in 
            # then prcurrent and previous pair 
            else: 

                pp = H[prod] 
                print(arr[pp[0]], arr[pp[1]],  
                      "and", arr[i], arr[j]) 
                found = True

    # If no pair find then prnot found 
    if (found == False): 
        print("No pairs Found") 

# Driver code 
arr = [1, 2, 3, 4, 5, 6, 7, 8] 
n = len(arr) 
findPairs(arr, n) 

# This code is contributed 
# by mohit kumar 

```

## C#

```cs

// C# program to find four elements a, b, c 
// and d in array such that ab = cd 
using System; 
using System.Collections.Generic;  

class GFG  
{ 

    public class pair 
    { 

        public int first,second; 

        public pair(int f, int s) 
        { 
            first = f; 
            second = s; 
        } 
    }; 

    // Function to find out four elements  
    // in array whose product is ab = cd 
    public static void findPairs(int[] arr, int n) 
    { 

        bool found = false; 
        Dictionary<int, pair> hp =  
                    new Dictionary<int, pair>(); 

        for(int i = 0; i < n; i++) 
        { 
            for(int j = i + 1; j < n; j++) 
            { 

                // If product of pair is not in  
                // hash table, then store it 
                int prod = arr[i] * arr[j]; 

                if(!hp.ContainsKey(prod)) 
                    hp.Add(prod, new pair(i,j)); 

                // If product of pair is also  
                // available in then print  
                // current and previous pair  
                else
                { 
                    pair p = hp[prod]; 
                    Console.WriteLine(arr[p.first]  
                            + " " + arr[p.second] 
                            + " " + "and" + " " +  
                            arr[i] + " " + arr[j]); 
                    found = true; 
                } 
            } 
        } 

        // If no pair find then print not found 
        if(found == false) 
        Console.WriteLine("No pairs Found"); 
    } 

    // Driver code 
    public static void Main (String[] args)  
    { 
        int []arr = {1, 2, 3, 4, 5, 6, 7, 8}; 
        int n = arr.Length; 
        findPairs(arr, n);  
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
1 6 and 2 3
1 8 and 2 4
2 6 and 3 4
3 8 and 4 6

```

**时间复杂度**：`O(N ^ 2)`假设哈希搜索和插入操作花费`O(1)`时间。

**相关文章**：

[在数组中找到四个元素 a，b，c 和 d，使得 a + b = c + d](https://www.geeksforgeeks.org/find-four-elements-a-b-c-and-d-in-an-array-such-that-ab-cd/)

本文由 [DANISH_RAZA](https://www.facebook.com/danish.raza.98096721) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

