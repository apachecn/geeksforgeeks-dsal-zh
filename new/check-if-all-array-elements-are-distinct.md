# 检查所有数组元素是否都不同

> 原文：[https://www.geeksforgeeks.org/check-if-all-array-elements-are-distinct/](https://www.geeksforgeeks.org/check-if-all-array-elements-are-distinct/)

给定一个数组，请检查数组中的所有元素是否互不相同。

**示例**：

```
Input : 1, 3, 2, 4
Output : Yes

Input : "Geeks", "for", "Geeks"
Output : No

Input : "All", "Not", "Equal"
Output : Yes

```

一种**简单解决方案**是使用两个嵌套循环。 对于每个元素，请检查是否重复。 如果任何元素重复，则返回`false`。 如果没有元素重复，则返回`false`。

**有效解决方案**是哈希。 我们将所有数组元素放入[`HashSet`](http://www.geeksforgeeks.org/hashset-in-java/)中。 如果`HashSet`的大小与数组大小相同，则返回`true`。

## C++

```cpp

// C++ program to check if all array  
// elements are distinct 
#include <bits/stdc++.h> 
using namespace std; 

bool areDistinct(vector<int> arr) 
{ 
    int n = arr.size(); 

    // Put all array elements in a map 
    unordered_set<int> s; 
    for (int i = 0; i < n; i++) { 
        s.insert(arr[i]); 
    } 

    // If all elements are distinct, size of 
    // set should be same array. 
    return (s.size() == arr.size()); 
} 

// Driver code 
int main() 
{ 
    std::vector<int> arr = { 1, 2, 3, 2 }; 

    if (areDistinct(arr)) { 
        cout << "All Elements are Distinct"; 
    } 
    else { 
        cout << "Not all Elements are Distinct"; 
    } 

    return 0; 
} 

```

## Java

```java

// Java program to check if all array elements are 
// distinct or not. 
import java.util.Arrays; 
import java.util.HashSet; 
import java.util.Set; 

public class DistinctElements { 
    public static boolean areDistinct(Integer arr[]) 
    { 
        // Put all array elements in a HashSet 
        Set<Integer> s =  
           new HashSet<Integer>(Arrays.asList(arr)); 

        // If all elements are distinct, size of 
        // HashSet should be same array. 
        return (s.size() == arr.length); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        Integer[] arr = { 1, 2, 3, 2 }; 
        if (areDistinct(arr)) 
            System.out.println("All Elements are Distinct"); 
        else
            System.out.println("Not all Elements are Distinct"); 
    } 
} 

```

## Python3

```py

# Python3 program to check if all array  
# elements are distinct 
def areDistinct(arr) : 

    n = len(arr) 

    # Put all array elements in a map 
    s = set() 
    for i in range(0, n):  
        s.add(arr[i]) 

    # If all elements are distinct,  
    # size of set should be same array. 
    return (len(s) == len(arr)) 

# Driver code 
arr = [ 1, 2, 3, 2 ] 

if (areDistinct(arr)):  
    print("All Elements are Distinct") 

else :  
    print("Not all Elements are Distinct") 

# This code is contributed by ihritik 

```

## C#

```cs

// C# program to check if all array elements are 
// distinct or not. 
using System; 
using System.Collections.Generic; 

public class DistinctElements  
{ 
    public static bool areDistinct(int []arr) 
    { 
        // Put all array elements in a HashSet 
        HashSet<int> s = new HashSet<int>(arr); 

        // If all elements are distinct, size of 
        // HashSet should be same array. 
        return (s.Count == arr.Length); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 1, 2, 3, 2 }; 
        if (areDistinct(arr)) 
            Console.WriteLine("All Elements are Distinct"); 
        else
            Console.WriteLine("Not all Elements are Distinct"); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Not all Elements are Distinct

```



* * *

* * *



