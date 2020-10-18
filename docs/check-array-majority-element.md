# 检查数组是否具有多数元素

> 原文： [https://www.geeksforgeeks.org/check-array-majority-element/](https://www.geeksforgeeks.org/check-array-majority-element/)

给定一个数组，任务是查找输入数组是否包含[多数元素](https://www.geeksforgeeks.org/majority-element/)。 

**示例**：

```
Input : arr[] = {2, 3, 9, 2, 2}
Output : Yes
A majority element 2 is present in arr[]

Input  : arr[] = {1, 8, 9, 2, 5}
Output : No

```



**简单解决方案**是遍历数组。 对于每个元素，计算其出现次数。 如果任何元素的出现次数变为`n / 2`，则返回`true`。

**有效解决方案**是使用哈希。 我们计算所有元素的出现。 如果`count`变为`n / 2`或更大，则返回`true`。

下面是该方法的实现。

## C++ 

```cpp

// Hashing based C++ program to find if there 
// is a majority element in input array. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns true if there is a majority element 
// in a[] 
bool isMajority(int a[], int n) 
{ 
    // Insert all elements in a hash table 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; i++)  
        mp[a[i]]++; 

    // Check if frequency of any element is 
    // n/2 or more. 
    for (auto x : mp) 
      if (x.second >= n/2) 
          return true; 
    return false; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 2, 3, 9, 2, 2 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    if (isMajority(a, n)) 
        cout << "Yes"; 
    else
        cout << "No"; 
    return 0; 
} 

```

## Java

```java
// Hashing based Java program 
// to find if there is a 
// majority element in input array. 
import java.util.*; 
import java.lang.*; 
import java.io.*; 
  
class Gfg 
{ 
    // Returns true if there is a 
    // majority element in a[] 
    static boolean isMajority(int a[], int n) 
    { 
        // Insert all elements  
        // in a hash table 
        HashMap <Integer,Integer> mp = new 
                            HashMap<Integer,Integer>(); 
          
        for (int i = 0; i < n; i++)  
          
            if (mp.containsKey(a[i])) 
                mp.put(a[i], mp.get(a[i]) + 1); 
          
            else mp.put(a[i] , 1); 
          
        // Check if frequency of any 
        // element is n/2 or more. 
        for (Map.Entry<Integer, Integer> x : mp.entrySet()) 
             
            if (x.getValue() >= n/2) 
                return true; 
        return false; 
    } 
      
    // Driver code 
    public static void main (String[] args) 
    { 
        int a[] = { 2, 3, 9, 2, 2 }; 
        int n = a.length; 
          
        if (isMajority(a, n)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 
  
// This code is contributed by Ansu Kumari 
```

## Python3

```py
# Hashing based Python  
# program to find if 
# there is a majority  
# element in input array. 
  
# Returns true if there  
# is a majority element 
# in a[] 
def isMajority(a): 
      
    # Insert all elements  
    # in a hash table 
    mp = {} 
      
    for i in a: 
        if i in mp: mp[i] += 1
        else: mp[i] = 1
      
    # Check if frequency  
    # of any element is 
    # n/2 or more. 
    for x in mp: 
        if mp[x] >= len(a)//2: 
            return True
    return False
  
# Driver code 
a = [ 2, 3, 9, 2, 2 ] 
  
print("Yes" if isMajority(a) else "No") 
  
#This code is contributed by Ansu Kumari 
```

## C#

```cs
// Hashing based C# program 
// to find if there is a 
// majority element in input array. 
using System; 
using System.Collections.Generic; 
  
class GFG 
{ 
    // Returns true if there is a 
    // majority element in a[] 
    static Boolean isMajority(int []a, int n) 
    { 
        // Insert all elements  
        // in a hash table 
        Dictionary<int,  
                   int> mp = new Dictionary<int, 
                                            int>(); 
          
        for (int i = 0; i < n; i++) 
        { 
            if(mp.ContainsKey(a[i])) 
            { 
                var val = mp[a[i]]; 
                mp.Remove(a[i]); 
                mp.Add(a[i], val + 1);  
            } 
            else
            { 
                mp.Add(a[i], 1); 
            } 
        } 
          
        // Check if frequency of any 
        // element is n/2 or more. 
        foreach(KeyValuePair<int, int> x in mp) 
              
            if (x.Value >= n / 2) 
                return true; 
        return false; 
    } 
      
    // Driver code 
    public static void Main (String[] args) 
    { 
        int []a = { 2, 3, 9, 2, 2 }; 
        int n = a.Length; 
          
        if (isMajority(a, n)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 
  
// This code is contributed by PrinciRaj1992 
```

输出：

```
Yes
```
