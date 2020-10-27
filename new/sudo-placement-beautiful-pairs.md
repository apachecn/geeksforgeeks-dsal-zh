# Sudo 放置| 美丽的一对

给定两个整数数组，其中第一个数组的最大大小很大，第二个数组的最大大小很小。 您的任务是查找第一个数组中是否存在一对，其和出现在第二个数组中。

例子：

```
Input: 
4
1 5 10 8
3
2 20 13
Output: 1

```

**方法：**我们有 x + y = z。 可以重写为 x = z – y。 这意味着，我们需要在数组 1 中找到一个元素 x，使其成为 z（第二个数组）-y（第一个数组）的结果。 为此，请使用散列来跟踪此类元素 x。

## CPP

```

// CPP code for finding required pairs 
#include <bits/stdc++.h> 
using namespace std; 

// The function to check if beautiful pair exists 
bool pairExists(int arr1[], int m, int arr2[], int n) 
{ 
    // Set for hashing 
    unordered_set<int> s; 

    // Traversing the first array 
    for (int i = 0; i < m; i++) { 

        // Traversing the second array to check for  
        // every j corresponding to single i 
        for (int j = 0; j < n; j++) { 

            // x + y = z => x = y - z 
            if (s.find(arr2[j] - arr1[i]) != s.end()) 

                // if such x exists then we return true 
                return true; 

        } 

       // hash to make use of it next time 
       s.insert(arr1[i]); 
 } 

    // no pair exists 
    return false; 
} 

// Driver Code 
int main() 
{ 
    int arr1[] = { 1, 5, 10, 8 }; 
    int arr2[] = { 2, 20, 13 }; 

    // If pair exists then 1 else 0 
    // 2nd argument as size of first array 
    // fourth argument as sizeof 2nd array 
    if (pairExists(arr1, 4, arr2, 3)) 
        cout << 1 << endl; 
    else
        cout << 0 << endl; 

    return 0; 
} 

```

## Java

```java

// Java code for finding required pairs 
import java.util.*; 
class GFG 
{ 
        // The function to check if beautiful pair exists 
        static boolean pairExists(int []arr1, int m, int []arr2, int n) 
        { 
            // Set for hashing 
            Set<Integer> s =new HashSet<Integer>(); 

            // Traversing the first array 
            for (int i = 0; i < m; i++) { 

                // Traversing the second array to check for  
                // every j corresponding to single i 
                for (int j = 0; j < n; j++)  
                { 

                    // x + y = z => x = y - z 
                    if (s.contains(arr2[j] - arr1[i])) 

                        // if such x exists then we return true 
                        return true; 

                } 

            // hash to make use of it next time 
            s.add(arr1[i]); 
        } 

            // no pair exists 
            return false; 
        } 

        // Driver Code 
        public static void main(String []args) 
        { 
            int []arr1 = { 1, 5, 10, 8 }; 
            int []arr2 = { 2, 20, 13 }; 

            // If pair exists then 1 else 0 
            // 2nd argument as size of first array 
            // fourth argument as sizeof 2nd array 
            if (pairExists(arr1, 4, arr2, 3)) 
                System.out.println(1); 
            else
                System.out.println(0); 

        } 

// This code is contributed by ihritik 
} 

```

## C#

```cs

// C# code for finding required pairs 
using System; 
using System.Collections.Generic; 

class GFG 
{ 
        // The function to check if 
        // beautiful pair exists 
        static bool pairExists(int []arr1, 
                int m, int []arr2, int n) 
        { 
            // Set for hashing 
            HashSet<int> s = new HashSet<int>(); 

            // Traversing the first array 
            for (int i = 0; i < m; i++)  
            { 

                // Traversing the second array to check for  
                // every j corresponding to single i 
                for (int j = 0; j < n; j++)  
                { 

                    // x + y = z => x = y - z 
                    if (s.Contains(arr2[j] - arr1[i])) 

                        // if such x exists then we return true 
                        return true; 

                } 

            // hash to make use of it next time 
            s.Add(arr1[i]); 
        } 

            // no pair exists 
            return false; 
        } 

        // Driver Code 
        public static void Main() 
        { 
            int []arr1 = { 1, 5, 10, 8 }; 
            int []arr2 = { 2, 20, 13 }; 

            // If pair exists then 1 else 0 
            // 2nd argument as size of first array 
            // fourth argument as sizeof 2nd array 
            if (pairExists(arr1, 4, arr2, 3)) 
                Console.WriteLine(1); 
            else
                Console.WriteLine(0); 
        } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
1

```



本文由 **Team GeeksforGeeks** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

