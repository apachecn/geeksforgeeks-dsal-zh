# 连续元素排序数组中唯一重复元素的数量

> 原文： [https://www.geeksforgeeks.org/count-of-only-repeated-element-in-a-sorted-array-of-consecutive-elements/](https://www.geeksforgeeks.org/count-of-only-repeated-element-in-a-sorted-array-of-consecutive-elements/)

给定一个连续元素的排序数组。 该数组只有一个元素重复多次。 任务是找到重复元素序列的长度。

预期时间复杂度：小于`0(n)`。

**示例**：

```
Input  : arr[] = {1, 2, 3, 4, 4, 4, 5, 6}
Output : 4 3
Repeated element is 4 and it appears 3 times.

Input  : arr[] = {4, 4, 4, 4, 4}
Output : 4 5 

Input  : arr[] = {6, 7, 8, 9, 10, 10, 11}
Output : 10 2

Input  : arr[] = {6, 7, 8, 9, 10, 10, 10}
Output : 10 3

```



我们需要找到两件事：

1.  元素重复的次数。 如果对数组排序，并且两个相邻元素的最大差为 1，则重复序列的长度为`n – 1 – (array[n-1] – array[0])`。

2.  元素的值。 对于该值，我们执行[二分搜索](https://www.geeksforgeeks.org/binary-search/)。

## C++ 

```cpp

// C++ program to find the only repeated element 
// and number of times it appears 
#include <bits/stdc++.h> 
using namespace std; 

// Assumptions : vector a is sorted, max-difference 
// of two adjacent elements is 1 
pair<int, int> sequence(const vector<int>& a) 
{ 
    if (a.size() == 0) 
        return {0, 0}; 

    int s = 0; 
    int e = a.size() - 1; 
    while (s < e) 
    { 
        int m = (s + e) / 2; 

        // if a[m] = m + a[0], there is no 
        // repeating character in [s..m] 
        if (a[m] >= m + a[0]) 
            s = m + 1; 

       // if a[m] < m + a[0], there is a 
       // repeating character in [s..m] 
        else
            e = m; 
    } 
    return {a[s], a.size() - (a[a.size() - 1] - a[0])}; 
} 

// Driver code 
int main() 
{ 
    pair<int, int>p = sequence({ 1, 2, 3, 4, 4, 4, 5, 6 }); 
    cout << "Repeated element is " << p.first 
         << ", it appears " << p.second << " times"; 
    return 0; 
} 

```

## Java

```java

// Java program to find the only repeated element 
// and number of times it appears 

import java.awt.Point; 
import java.util.Arrays; 
import java.util.Vector; 

class Test 
{ 
    // Assumptions : vector a is sorted, max-difference 
    // of two adjacent elements is 1 
    static Point sequence(Vector<Integer> a) 
    { 
        if (a.size() == 0) 
            return new Point(0, 0); 

        int s = 0; 
        int e = a.size() - 1; 
        while (s < e) 
        { 
            int m = (s + e) / 2; 

            // if a[m] = m + a[0], there is no 
            // repeating character in [s..m] 
            if (a.get(m) >= m + a.get(0)) 
                s = m + 1; 

           // if a[m] < m + a[0], there is a 
           // repeating character in [s..m] 
            else
                e = m; 
        } 
        return new Point(a.get(s), a.size() - (a.get(a.size() - 1) - a.get(0))); 
    } 

    // Driver method 
    public static void main(String args[]) 
    { 
        Integer array[] = new Integer[]{1, 2, 3, 4, 4, 4, 5, 6}; 
        Point p = sequence(new Vector<>(Arrays.asList(array))); 
        System.out.println("Repeated element is " + p.x + 
                           ", it appears " + p.y + " times"); 
    } 
} 

```

## Python3

```py

# Python3 program to find the  
# only repeated element and  
# number of times it appears 

# Assumptions : vector a is sorted,  
# max-difference of two adjacent 
# elements is 1 
def sequence(a): 
    if (len(a) == 0): 
        return [0, 0] 

    s = 0
    e = len(a) - 1
    while (s < e): 
        m = (s + e) // 2

        # if a[m] = m + a[0], there is no 
        # repeating character in [s..m] 
        if (a[m] >= m + a[0]): 
            s = m + 1

        # if a[m] < m + a[0], there is a 
        # repeating character in [s..m] 
        else: 
            e = m 
    return [a[s], len(a) - ( 
                a[len(a) - 1] - a[0])] 

# Driver code 
p = sequence([1, 2, 3, 4, 4, 4, 5, 6]) 
print("Repeated element is", p[0],  
             ", it appears", p[1], "times") 

# This code is contributed by Mohit Kumar 

```

## C# 

```cs

// C# program to find the only repeated element 
// and number of times it appears 
using System; 
using System.Collections.Generic; 

public class Point  
{  
    public int first, second;  

        public Point(int first, int second)  
        {  
            this.first = first;  
            this.second = second;  
        }  

}  
public class Test 
{ 
    // Assumptions : vector a is sorted, max-difference 
    // of two adjacent elements is 1 
    static Point sequence(List<int> a) 
    { 
        if (a.Count == 0) 
            return new Point(0, 0); 

        int s = 0; 
        int e = a.Count - 1; 
        while (s < e) 
        { 
            int m = (s + e) / 2; 

            // if a[m] = m + a[0], there is no 
            // repeating character in [s..m] 
            if (a[m] >= m + a[0]) 
                s = m + 1; 

        // if a[m] < m + a[0], there is a 
        // repeating character in [s..m] 
            else
                e = m; 
        } 
        return new Point(a[s], a.Count - (a[a.Count - 1] - a[0])); 
    } 

    // Driver code 
    public static void Main(String []args) 
    { 
        int []array = new int[]{1, 2, 3, 4, 4, 4, 5, 6}; 
        Point p = sequence(new List<int>(array)); 
        Console.WriteLine("Repeated element is " + p.first + 
                        ", it appears " + p.second + " times"); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
Repeated element is 4, it appears 3 times

```

