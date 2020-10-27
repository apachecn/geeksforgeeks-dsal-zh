# 最大子集，其所有元素均为斐波纳契数

给定一个具有正数的数组，任务是我们从数组中找到包含[斐波纳契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的元素的最大子集。

在 Facebook 问

**示例：**

```
Input : arr[] = {1, 4, 3, 9, 10, 13, 7};
Output : subset[] = {1, 3, 13}
The output three numbers are Fibonacci
numbers.

Input  : arr[] = {0, 2, 8, 5, 2, 1, 4, 
                  13, 23};
Output : subset[] = {0, 2, 8, 5, 2, 1, 
                    13, 23}

```

一个**简单解决方案**是遍历给定数组的所有元素。 对于每个数字，请检查是否为斐波那契。 如果是，则将其添加到结果中。

以下是基于哈希的**有效解决方案**。

1.  在数组中查找最大值
2.  生成斐波那契数直至最大值，并将其存储在哈希表中。
3.  如果哈希表中存在该数字，则再次遍历数组，然后将其添加到结果中。

## C ++

```

// C++ program to find largest Fibonacci subset 
#include<bits/stdc++.h> 
using namespace std; 

// Prints largest subset of an array whose 
// all elements are fibonacci numbers 
void findFibSubset(int arr[], int n) 
{ 
    // Find maximum element in arr[] 
    int max = *std::max_element(arr, arr+n); 

    // Generate all Fibonacci numbers till 
    // max and store them in hash. 
    int a = 0, b = 1; 
    unordered_set<int> hash; 
    hash.insert(a); 
    hash.insert(b); 
    while (b < max) 
    { 
        int c = a + b; 
        a = b; 
        b = c; 
        hash.insert(b); 
    } 

    // Npw iterate through all numbers and 
    // quickly check for Fibonacci using 
    // hash. 
    for (int i=0; i<n; i++) 
        if (hash.find(arr[i]) != hash.end()) 
            printf("%d ", arr[i]); 
} 

// Driver code 
int main() 
{ 
    int arr[] = {4, 2, 8, 5, 20, 1, 40, 13, 23}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    findFibSubset(arr, n); 
    return 0; 
} 

```

## 爪哇

```

// Java program to find  
// largest Fibonacci subset 
import java.util.*; 

class GFG 
{ 
    // Prints largest subset of an array whose 
    // all elements are fibonacci numbers 
    public static void findFibSubset(Integer[] x) 
    { 
        Integer max = Collections.max(Arrays.asList(x)); 
        List<Integer> fib = new ArrayList<Integer>();  
        List<Integer> result = new ArrayList<Integer>(); 

        // Generate all Fibonacci numbers  
        // till max and store them 
        Integer a = 0; 
        Integer b = 1; 
        while (b < max){ 
            Integer c = a + b; 
            a=b; 
            b=c; 
            fib.add(c); 
        } 

        // Now iterate through all numbers and 
        // quickly check for Fibonacci 
        for (Integer i = 0; i < x.length; i++){ 
        if(fib.contains(x[i])){ 
            result.add(x[i]);  
        }      
        } 
        System.out.println(result); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        Integer[] a = {4, 2, 8, 5, 20, 1, 40, 13, 23}; 
        findFibSubset(a); 
    } 
} 

// This code is contributed by prag93 

```

## Python3

```

# python3 program to find largest Fibonacci subset 

# Prints largest subset of an array whose 
# all elements are fibonacci numbers 
def findFibSubset(arr, n): 

    # Find maximum element in arr[] 
    m= max(arr) 

    # Generate all Fibonacci numbers till 
    # max and store them in hash. 
    a = 0
    b = 1
    hash = [] 
    hash.append(a) 
    hash.append(b) 
    while (b < m): 

        c = a + b 
        a = b 
        b = c 
        hash.append(b) 

    # Npw iterate through all numbers and 
    # quickly check for Fibonacci using 
    # hash. 
    for i in range (n): 
        if arr[i] in hash : 
            print( arr[i],end=" ") 

# Driver code 
if __name__ == "__main__": 

    arr = [4, 2, 8, 5, 20, 1, 40, 13, 23] 
    n = len(arr) 
    findFibSubset(arr, n) 

```

## C＃

```

// C# program to find  
// largest Fibonacci subset 
using System; 
using System.Linq; 
using System.Collections.Generic;  

class GFG 
{ 
    // Prints largest subset of an array whose 
    // all elements are fibonacci numbers 
    public static void findFibSubset(int[] x) 
    { 
        int max = x.Max(); 
        List<int> fib = new List<int>();  
        List<int> result = new List<int>(); 

        // Generate all Fibonacci numbers  
        // till max and store them 
        int a = 0; 
        int b = 1; 
        while (b < max) 
        { 
            int c = a + b; 
            a = b; 
            b = c; 
            fib.Add(c); 
        } 

        // Now iterate through all numbers and 
        // quickly check for Fibonacci 
        for (int i = 0; i < x.Length; i++) 
        { 
            if(fib.Contains(x[i])) 
            { 
                result.Add(x[i]);  
            }      
        } 
        foreach(int i in result) 
            Console.Write(i + " "); 
    } 

    // Driver code 
    public static void Main(String []args) 
    { 
        int[] a = {4, 2, 8, 5, 20, 1, 40, 13, 23}; 
        findFibSubset(a); 
    } 
} 

// This code is contributed by PrinciRaj1992  

```

**Output:**

```
2 8 5 1 13 

```

**参考：**
[https://www.careercup.com/question?id=5154130839470080](https://www.careercup.com/question?id=5154130839470080)

本文由 **DANISH_RAZA** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。