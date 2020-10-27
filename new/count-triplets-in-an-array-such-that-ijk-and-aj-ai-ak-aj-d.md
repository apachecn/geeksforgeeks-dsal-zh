# 对数组中的三胞胎进行计数，使得 i

给定一个数组 **arr** 和一个整数 **D** ，任务是对数组中的三元组（arr [i]，arr [j]，arr [k]）进行计数 那：

1.  i
2.  arr [j] – arr [i] = arr [k] – arr [j] = D

**示例：**

> **输入：** arr = {1、6、7、7、8、10、12、13、14}，D = 3
> **输出：** 2
> **说明：**
> 阵列中有两个满足给定条件的三元组。
> ->第一个三元组（7，10，13），使得 i = 3，j = 6，k = 8，使得（i < j < k）和（10 – 7 = 13 – 10 = D（= 3））
> ->第二个三元组（7、10、13），使得 i = 4，j = 6，k = 8，使得（i < j < k）和（10 – 7 = 13 – 10 = D（= 3））
> 
> **输入：** arr = {6，3，4，5}，D = 1
> **输出：** 0

**天真的方法：**最简单的方法是使用三个嵌套的 for 循环并查找满足给定条件的三元组。 下面是此方法的实现。

## C++

```cpp

// C++ program to count the triplets 
#include<bits/stdc++.h> 
using namespace std; 

// Function to count the triplets 
int CountTriplets(int arr[], int d, int n) 
{ 
    int count = 0; 

    // Three nested for loops to count the 
    // triplets that satisfy the given criteria 
    for(int i = 0; i < n - 2; i++) 
    { 
       for(int j = i + 1; j < n - 1; j++) 
       { 
          for(int k = j + 1; k < n; k++) 
          { 
             if ((arr[j] - arr[i] == d) &&  
                 (arr[k] - arr[j] == d))  
             { 
                 count++; 
             } 
          } 
       } 
    } 
    return count; 
} 

// Driver Code 
int main() 
{ 
    int A[] = { 1, 6, 7, 7, 8, 10, 12, 13, 14 }; 
    int D = 3; 
    int n = sizeof(A) / sizeof(A[0]); 

    cout << (CountTriplets(A, D, n)); 
} 

// This code is contributed by chitranayal 

```

## Java

```java

// Java program to count the triplets 

class GFG { 

    // Function to count the triplets 
    static int CountTriplets(int[] arr, int d) 
    { 
        int count = 0; 
        int n = arr.length; 

        // Three nested for loops to count the 
        // triplets that satisfy the given criteria 
        for (int i = 0; i < n - 2; i++) { 
            for (int j = i + 1; j < n - 1; j++) { 
                for (int k = j + 1; k < n; k++) { 

                    if ((arr[j] - arr[i] == d) 
                        && (arr[k] - arr[j] == d)) { 
                        count++; 
                    } 
                } 
            } 
        } 
        return count; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        int A[] = { 1, 6, 7, 7, 8, 10, 12, 13, 14 }; 
        int D = 3; 
        System.out.println(CountTriplets(A, D)); 
    } 
} 

```

## Python3

```py

# Python3 program to count the triplets 

# Function to count the triplets 
def CountTriplets(arr, d): 

    count = 0; 
    n = len(arr); 

    # Three nested for loops to count the 
    # triplets that satisfy the given criteria 
    for i in range(n - 1): 
        for j in range(i + 1, n - 1): 
            for k in range(j + 1, n): 

                if ((arr[j] - arr[i] == d) and 
                    (arr[k] - arr[j] == d)): 
                    count += 1; 
    return count; 

# Driver Code 
if __name__ == '__main__': 

    A = [ 1, 6, 7, 7, 8, 10, 12, 13, 14 ]; 
    D = 3; 

    print(CountTriplets(A, D)); 

# This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# program to count the triplets  
using System; 

class GFG { 

    // Function to count the triplets 
    static int CountTriplets(int[] arr, int d) 
    { 
        int count = 0; 
        int n = arr.Length; 

        // Three nested for loops to count the 
        // triplets that satisfy the given criteria 
        for (int i = 0; i < n - 2; i++) { 
            for (int j = i + 1; j < n - 1; j++) { 
                for (int k = j + 1; k < n; k++) { 

                    if ((arr[j] - arr[i] == d) 
                        && (arr[k] - arr[j] == d)) { 
                        count++; 
                    } 
                } 
            } 
        } 
        return count; 
    } 

    // Driver Code 
    public static void Main(String []args) 
    { 
        int []A = { 1, 6, 7, 7, 8, 10, 12, 13, 14 }; 
        int D = 3; 
        Console.WriteLine(CountTriplets(A, D)); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
2

```

****时间复杂度：*** O（N ^ 3）。*

**有效方法：**

*   解决此问题的有效方法是使用映射存储（键，值）对，其中值将是键的计数。
*   The idea is to traverse the array from **0** to **N** and do following:
    *   检查地图中是否存在 **A [i] – D** 和 **A [i] – 2 * D** 。
    *   如果它在地图上，那么我们将简单地将它们各自的值相乘并以此增加答案。
    *   现在，我们只需要将 A [i]放入地图中并更新地图即可。

下面是上述方法的实现。

## C++ 14

```

// C++14 program to count the number  
// of triplets from an array. 
#include<bits/stdc++.h> 
using namespace std;  

// Function to count the triplets  
int countTriplets (int arr[], int d, int n) 
{ 
    int count = -1; 

    // Create a map to store (key, values) pair.  
    map<int, int> set; 

    // Traverse the array and check that we  
    // have already put (a[i]-d and a[i]-2*d)  
    // into map or not. If yes we have to get  
    // the values of both the keys and  
    // multiply them, else put a[i] into the map.  
    for(int i = 0; i < n; i++) 
    { 
        if ((set.find(arr[i] - d) != set.end()) && 
            (set.find(arr[i] - 2 * d) != set.end())) 
        { 
            count += (set[arr[i] - d] *  
                      set[arr[i] - 2 * d]); 
        } 

        // Update the map 
        if (set.find(arr[i]) == set.end()) 
            set[arr[i]] = 1; 
        else
            set[arr[i]] += 1; 
    } 
    return count; 
} 

// Driver Code 
int main()  
{  

    // Test Case 1:  
    int a1[] = { 1, 6, 7, 7, 8, 10, 12, 13, 14 };  
    int d1 = 3;  
    cout << countTriplets(a1, d1, 9) << endl;  

    // Test Case 2:  
    int a2[] = { 6, 3, 4, 5 };  
    int d2 = 1;  
    cout << countTriplets(a2, d2, 4) << endl;  

    // Test Case 3:  
    int a3[] = { 1, 2, 4, 5, 7, 8, 10 };  
    int d3 = 3;  
    cout << countTriplets(a3, d3, 7) << endl;  

    return 0;  
}  

// This code is contributed by himanshu77 

```

## Java

```java

// Java program to count the number 
// of triplets from an array. 

import java.util.*; 

class GFG { 

    // Function to count the triplets 
    static int countTriplets(int[] arr, int d) 
    { 
        int count = -1; 

        // Create a map to store (key, values) pair. 
        Map<Integer, Integer> set = new HashMap<>(); 

        // Traverse the array and check that we 
        // have already put (a[i]-d and a[i]-2*d) 
        // into map or not. If yes we have to get 
        // the values of both the keys and 
        // multiply them, else put a[i] into the map. 
        for (int i = 0; i < arr.length; i++) { 

            if (set.get(arr[i] - d) != null
                && set.get(arr[i] - 2 * d) != null) { 
                count += (set.get(arr[i] - d) 
                          * set.get(arr[i] - 2 * d)); 
            } 

            // Update the map. 
            if (set.get(arr[i]) == null) { 
                set.put(arr[i], 1); 
            } 
            else { 
                set.put(arr[i], set.get(arr[i]) + 1); 
            } 
        } 

        return count; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 

        // Test Case 1: 
        int a1[] = { 1, 6, 7, 7, 8, 10, 12, 13, 14 }; 
        int d1 = 3; 
        System.out.println(countTriplets(a1, d1)); 

        // Test Case 2: 
        int a2[] = { 6, 3, 4, 5 }; 
        int d2 = 1; 
        System.out.println(countTriplets(a2, d2)); 

        // Test Case 3: 
        int a3[] = { 1, 2, 4, 5, 7, 8, 10 }; 
        int d3 = 3; 
        System.out.println(countTriplets(a3, d3)); 
    } 
} 

```

## C#

```cs

// C# program to count the number 
// of triplets from an array. 
using System; 
using System.Collections.Generic; 

class GFG { 

    // Function to count the triplets 
    static int countTriplets(int[] arr, int d) 
    { 
        int count = -1; 

        // Create a map to store (key, values) pair. 
        Dictionary<int, int> set = new Dictionary<int, int>(); 

        // Traverse the array and check that we 
        // have already put (a[i]-d and a[i]-2*d) 
        // into map or not. If yes we have to get 
        // the values of both the keys and 
        // multiply them, else put a[i] into the map. 
        for (int i = 0; i < arr.Length; i++) { 

            if (set.ContainsKey(arr[i] - d) 
                && set.ContainsKey(arr[i] - 2 * d)) { 
                count += (set[arr[i] - d] 
                          * set[arr[i] - 2 * d]); 
            } 

            // Update the map. 
            if (!set.ContainsKey(arr[i])) { 
                set.Add(arr[i], 1); 
            } 
            else { 
                set[arr[i]] = set[arr[i]] + 1; 
            } 
        } 

        return count; 
    } 

    // Driver Code 
    public static void Main(String []args) 
    { 

        // Test Case 1: 
        int []a1 = { 1, 6, 7, 7, 8, 10, 12, 13, 14 }; 
        int d1 = 3; 
        Console.WriteLine(countTriplets(a1, d1)); 

        // Test Case 2: 
        int []a2 = { 6, 3, 4, 5 }; 
        int d2 = 1; 
        Console.WriteLine(countTriplets(a2, d2)); 

        // Test Case 3: 
        int []a3 = { 1, 2, 4, 5, 7, 8, 10 }; 
        int d3 = 3; 
        Console.WriteLine(countTriplets(a3, d3)); 
    } 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
1
0
2

```

****时间复杂度：*** O（N）*



* * *

* * *



