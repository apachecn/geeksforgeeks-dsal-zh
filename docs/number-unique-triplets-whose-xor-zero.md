# XOR 为零的唯一三元组数

> 原文： [https://www.geeksforgeeks.org/number-unique-triplets-whose-xor-zero/](https://www.geeksforgeeks.org/number-unique-triplets-whose-xor-zero/)

给定`N`个没有重复的数字，请计算 XOR 为 0 的唯一三元组`(i, j, k)`的数量。如果三元组中的所有三个数字都是唯一的，则说三元组是唯一的。

**示例**：

```
Input : a[] = {1, 3, 5, 10, 14, 15};
Output : 2 
Explanation : {1, 14, 15} and {5, 10, 15} are the 
              unique triplets whose XOR is 0\. 
              {1, 14, 15} and all other combinations of 
              1, 14, 15 are considered as 1 only.

Input : a[] = {4, 7, 5, 8, 3, 9};
Output : 1
Explanation : {4, 7, 3} is the only triplet whose XOR is 0 

```



**朴素的方法**：朴素的方法是运行三个嵌套循环，第一个从 0 到`n`，第二个从`i + 1`到`n`，最后一个从`j + 1`到`n`，以获得唯一的三元组 。 计算`i, j, k`的 XOR，检查其是否等于 0，如果等于 0，则增加计数。

时间复杂度：`O(n ^ 3)`。

**有效方法**：一种有效方法是使用两个相同数字的 XOR 等于 0 的 XOR 属性之一。因此，我们仅需要计算唯一对的 XOR，并且如果计算出的 XOR 是数组元素，则得到 XOR 为 0 的三元组。以下是计算唯一三元组数的步骤：

以下是此方法的完整算法：

1.  使用映射标记所有数组元素。

2.  运行两个嵌套循环，一个来自`i-n`，另一个来自`i + 1-n`，以获取所有对。

3.  获得对的异或。

4.  检查 XOR 是否为数组元素，而不是`i`或`j`之一。

5.  如果条件成立，请增加计数。

6.  返回`count / 3`，因为我们只需要唯一的三元组。 由于`i-n`和`j + 1-n`给我们唯一的对而不是三元组，所以我们做一个`count / 3`来删除其他两个可能的组合。

以下是上述想法的实现：

## C++ 

```cpp

// CPP program to count the number of 
// unique triplets whose XOR is 0 
#include <bits/stdc++.h> 
using namespace std; 

// function to count the number of  
// unique triplets whose xor is 0 
int countTriplets(int a[], int n)  
{ 
    // To store values that are present 
    unordered_set<int> s; 
    for (int i = 0; i < n; i++) 
        s.insert(a[i]); 

    // stores the count of unique triplets 
    int count = 0; 

    // traverse for all i, j pairs such that j>i 
    for (int i = 0; i < n; i++) { 
        for (int j = i + 1; j < n; j++) { 

          // xor of a[i] and a[j] 
          int xr = a[i] ^ a[j]; 

          // if xr of two numbers is present,  
          // then increase the count 
          if (s.find(xr) != s.end() && xr != a[i] &&  
                                       xr != a[j]) 
            count++; 
        } 
    } 

    // returns answer 
    return count / 3; 
} 

// Driver code to test above function 
int main()  
{ 
    int a[] = {1, 3, 5, 10, 14, 15}; 
    int n = sizeof(a) / sizeof(a[0]);    
    cout << countTriplets(a, n);     
    return 0; 
} 

```

## Java

```java
// Java program to count 
// the number of unique 
// triplets whose XOR is 0
import java.io.*;
import java.util.*;
 
class GFG
{
    // function to count the 
    // number of unique triplets
    // whose xor is 0
    static int countTriplets(int []a, 
                             int n) 
    {
        // To store values 
        // that are present
        ArrayList<Integer> s = 
                  new ArrayList<Integer>();
        for (int i = 0; i < n; i++)
            s.add(a[i]);
         
        // stores the count 
        // of unique triplets
        int count = 0;
         
        // traverse for all i, 
        // j pairs such that j>i
        for (int i = 0; i < n; i++) 
        {
            for (int j = i + 1; 
                     j < n; j++)
            {
     
            // xor of a[i] and a[j]
            int xr = a[i] ^ a[j];
         
            // if xr of two numbers 
            // is present, then 
            // increase the count
            if (s.contains(xr) &&
                xr != a[i] && xr != a[j])
                count++;
            }
        }
         
        // returns answer
        return count / 3;
    }
     
    // Driver code
    public static void main(String srgs[])
    {
        int []a = {1, 3, 5, 
                   10, 14, 15};
        int n = a.length;
        System.out.print(countTriplets(a, n));
    }
}
 
// This code is contributed by 
// Manish Shaw(manishshaw1)
```

## Python3

```py
# Python 3 program to count the number of
# unique triplets whose XOR is 0
 
# function to count the number of 
# unique triplets whose xor is 0
def countTriplets(a, n):
     
    # To store values that are present
    s = set()
    for i in range(n):
        s.add(a[i])
     
    # stores the count of unique triplets
    count = 0
     
    # traverse for all i, j pairs such that j>i
    for i in range(n):
        for j in range(i + 1, n, 1):
             
            # xor of a[i] and a[j]
            xr = a[i] ^ a[j]
             
            # if xr of two numbers is present,
            # then increase the count
            if (xr in s and xr != a[i] and
                            xr != a[j]):
                count += 1;
         
    # returns answer
    return int(count / 3)
 
# Driver code
if __name__ == '__main__':
    a = [1, 3, 5, 10, 14, 15]
    n = len(a) 
    print(countTriplets(a, n)) 
     
# This code is contributed by
# Surendra_Gangwar
```

## C#

```cs
// C# program to count 
// the number of unique 
// triplets whose XOR is 0
using System;
using System.Collections.Generic;
 
class GFG
{
    // function to count the 
    // number of unique triplets
    // whose xor is 0
    static int countTriplets(int []a, 
                             int n) 
    {
        // To store values 
        // that are present
        List<int> s = new List<int>();
        for (int i = 0; i < n; i++)
            s.Add(a[i]);
         
        // stores the count 
        // of unique triplets
        int count = 0;
         
        // traverse for all i, 
        // j pairs such that j>i
        for (int i = 0; i < n; i++) 
        {
            for (int j = i + 1; 
                     j < n; j++)
            {
     
            // xor of a[i] and a[j]
            int xr = a[i] ^ a[j];
         
            // if xr of two numbers 
            // is present, then 
            // increase the count
            if (s.Exists(item => item == xr) &&
                   xr != a[i] && xr != a[j])
                count++;
            }
        }
         
        // returns answer
        return count / 3;
    }
     
    // Driver code
    static void Main()
    {
        int []a = new int[]{1, 3, 5, 
                            10, 14, 15};
        int n = a.Length;
        Console.Write(countTriplets(a, n));
    }
}
 
// This code is contributed by 
// Manish Shaw(manishshaw1)
```

输出：

```
2
```

时间复杂度：`O(n ^ 2)`。