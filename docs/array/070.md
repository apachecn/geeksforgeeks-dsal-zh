# 数组中不同的相邻元素

> 原文： [https://www.geeksforgeeks.org/distinct-adjacent-elements-array/](https://www.geeksforgeeks.org/distinct-adjacent-elements-array/)

给定一个数组，找出是否有可能通过交换两个相邻的数组元素来获得具有不同的相邻元素的数组。

例子：

```
Input : 1 1 2
Output : YES
swap 1 (second last element) and 2 (last element), 
to obtain 1 2 1, which has distinct neighbouring 
elements .

Input : 7 7 7 7
Output : NO
We can't swap to obtain distinct elements in 
neighbor .

```



为了获得具有不同的相邻元素的数组，只有在最常出现的元素的频率小于或等于数组大小的一半（即`<= (n + 1) / 2)`时才可能使用。为了更清楚地考虑不同的示例：

第一个例子：`a[] = {1, 1, 2, 3, 1}`。

我们可以通过交换数组`a`中的（第 2 和第 3）和（第 4 和第 5）元素，获得数组`{1, 2, 1, 3, 1}`。

这里 1 出现最多，其频率为`3 (6 + 1) / 2`。因此，它将永远不可能。

下面是这种方法的实现。

## C++ 

```cpp

// C++ program to check if we can make 
// neighbors distinct. 
#include <bits/stdc++.h> 
using namespace std; 

void distinctAdjacentElement(int a[], int n) 
{ 
    // map used to count the frequency 
    // of each element occurring in the 
    // array 
    map<int, int> m; 

    // In this loop we count the frequency 
    // of element through map m . 
    for (int i = 0; i < n; ++i) 
        m[a[i]]++; 

    // mx store the frequency of element which 
    // occurs most in array . 
    int mx = 0; 

    // In this loop we calculate the maximum 
    // frequency and store it in variable mx. 
    for (int i = 0; i < n; ++i) 
        if (mx < m[a[i]]) 
            mx = m[a[i]]; 

    // By swapping we can adjust array only 
    // when the frequency of the element 
    // which occurs most is less than or 
    // equal to (n + 1)/2 . 
    if (mx > (n + 1) / 2) 
        cout << "NO" << endl; 
    else
        cout << "YES" << endl; 
} 

// Driver program to test the above function 
int main() 
{ 
    int a[] = { 7, 7, 7, 7 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    distinctAdjacentElement(a, n); 
    return 0; 
} 

```

## Java

```java
// Java program to check if we can make 
// neighbors distinct. 
import java.io.*; 
import java.util.HashMap; 
import java.util.Map; 
class GFG { 
      
    static void distinctAdjacentElement(int a[], int n) 
    { 
        // map used to count the frequency 
        // of each element occurring in the 
        // array 
        HashMap<Integer,Integer> m = new HashMap<Integer, 
                                             Integer>(); 
       
        // In this loop we count the frequency 
        // of element through map m . 
        for (int i = 0; i < n; ++i){ 
     
            // checks if map already contains a[i] then  
            // update the previous value by incrementing  
          // by 1 
            if(m.containsKey(a[i])){ 
                int x = m.get(a[i]) + 1; 
                m.put(a[i],x);  
            } 
            else{ 
                m.put(a[i],1); 
            } 
              
        } 
       
        // mx store the frequency of element which 
        // occurs most in array . 
        int mx = 0; 
       
        // In this loop we calculate the maximum 
        // frequency and store it in variable mx. 
        for (int i = 0; i < n; ++i) 
            if (mx < m.get(a[i])) 
                mx = m.get(a[i]); 
       
        // By swapping we can adjust array only 
        // when the frequency of the element 
        // which occurs most is less than or 
        // equal to (n + 1)/2 . 
        if (mx > (n + 1) / 2) 
            System.out.println("NO"); 
        else
            System.out.println("YES"); 
    } 
          
    // Driver program to test the above function 
    public static void main (String[] args) { 
        int a[] = { 7, 7, 7, 7 }; 
        int n = 4; 
        distinctAdjacentElement(a, n); 
    } 
} 
// This code is contributed by Amit Kumar 
```

## Python3

```py
# Python program to check if we can make 
# neighbors distinct. 
def distantAdjacentElement(a, n): 
  
    # dict used to count the frequency 
    # of each element occurring in the 
    # array 
    m = dict() 
  
    # In this loop we count the frequency 
    # of element through map m 
    for i in range(n): 
        if a[i] in m: 
            m[a[i]] += 1
        else: 
            m[a[i]] = 1
  
    # mx store the frequency of element which 
    # occurs most in array . 
    mx = 0
  
    # In this loop we calculate the maximum 
    # frequency and store it in variable mx. 
    for i in range(n): 
        if mx < m[a[i]]: 
            mx = m[a[i]] 
  
    # By swapping we can adjust array only 
    # when the frequency of the element 
    # which occurs most is less than or 
    # equal to (n + 1)/2 . 
    if mx > (n+1) // 2: 
        print("NO") 
    else: 
        print("YES") 
  
  
# Driver Code 
if __name__ == "__main__": 
    a = [7, 7, 7, 7] 
    n = len(a) 
    distantAdjacentElement(a, n) 
  
# This code is contributed by 
# sanjeev2552 
```

## C#

```cs
// C# program to check if we can make  
// neighbors distinct.  
using System; 
using System.Collections.Generic; 
  
class GFG { 
  
public static void distinctAdjacentElement(int[] a, int n) 
{ 
    // map used to count the frequency  
    // of each element occurring in the  
    // array  
    Dictionary<int, int> m = new Dictionary<int, int>(); 
  
    // In this loop we count the frequency  
    // of element through map m .  
    for (int i = 0; i < n; ++i) 
    { 
  
        // checks if map already  
        // contains a[i] then  
        // update the previous 
        // value by incrementing  
        // by 1  
        if (m.ContainsKey(a[i])) 
        { 
            int x = m[a[i]] + 1; 
            m[a[i]] = x; 
        } 
        else
        { 
            m[a[i]] = 1; 
        } 
  
    } 
  
    // mx store the frequency 
    // of element which  
    // occurs most in array .  
    int mx = 0; 
  
    // In this loop we calculate 
    // the maximum frequency and 
    // store it in variable mx.  
    for (int i = 0; i < n; ++i) 
    { 
        if (mx < m[a[i]]) 
        { 
            mx = m[a[i]]; 
        } 
    } 
  
    // By swapping we can adjust array only  
    // when the frequency of the element  
    // which occurs most is less than or  
    // equal to (n + 1)/2 .  
    if (mx > (n + 1) / 2) 
    { 
        Console.WriteLine("NO"); 
    } 
    else
    { 
        Console.WriteLine("YES"); 
    } 
} 
  
    // Main Method 
    public static void Main(string[] args) 
    { 
        int[] a = new int[] {7, 7, 7, 7}; 
        int n = 4; 
        distinctAdjacentElement(a, n); 
    } 
} 
  
// This code is contributed 
// by Shrikant13 
```

输出：

```
NO
```

