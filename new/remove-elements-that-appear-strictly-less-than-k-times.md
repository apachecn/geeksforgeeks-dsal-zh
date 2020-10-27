# 删除出现严格少于 k 次的元素

给定一个整数数组，删除严格小于 k 次的所有元素。

**示例：**

```
Input : arr[] = {1, 2, 2, 3, 2, 3, 4}
        k = 2
Output : 2 2 3 2 3
Explanation : {1, 4} appears less than 2 times.

```

**方法：**

*   拿一个哈希图，它将存储数组中所有元素的频率。
*   现在，再次遍历。
*   删除出现少于 k 次的元素。
*   否则，打印它。

## C ++

```

// C++ program to remove the elements which 
// appear strictly less than k times from the array. 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

void removeElements(int arr[], int n, int k) 
{ 
    // Hash map which will store the 
    // frequency of the elements of the array. 
    unordered_map<int, int> mp; 

    for (int i = 0; i < n; ++i) { 
        // Incrementing the frequency 
        // of the element by 1\. 
        mp[arr[i]]++; 
    } 

    for (int i = 0; i < n; ++i) { 

        // Print the element which appear 
        // more than or equal to k times. 
        if (mp[arr[i]] >= k) { 
            cout << arr[i] << " "; 
        } 
    } 
} 

int main() 
{ 
    int arr[] = { 1, 2, 2, 3, 2, 3, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 2; 
    removeElements(arr, n, k); 
    return 0; 
} 

```

## 爪哇

```

// Java program to remove the elements which  
// appear strictly less than k times from the array.  
import java.util.HashMap; 

class geeks  
{ 

    public static void removeElements(int[] arr,  
                                        int n, int k) 
    { 

        // Hash map which will store the 
        // frequency of the elements of the array. 
        HashMap<Integer, Integer> mp = new HashMap<>(); 

        for (int i = 0; i < n; ++i)  
        { 

            // Incrementing the frequency 
            // of the element by 1\. 
            if (!mp.containsKey(arr[i])) 
                mp.put(arr[i], 1); 
            else
            { 
                int x = mp.get(arr[i]); 
                mp.put(arr[i], ++x); 
            } 
        } 

        for (int i = 0; i < n; ++i)  
        { 

            // Print the element which appear 
            // more than or equal to k times. 
            if (mp.get(arr[i]) >= k) 
                System.out.print(arr[i] + " "); 
        } 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        int[] arr = { 1, 2, 2, 3, 2, 3, 4 }; 
        int n = arr.length; 
        int k = 2; 
        removeElements(arr, n, k); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```

# Python3 program to remove the elements which 
# appear strictly less than k times from the array. 
def removeElements(arr, n, k): 

    # Hash map which will store the 
    # frequency of the elements of the array. 
    mp = dict() 

    for i in range(n): 

        # Incrementing the frequency 
        # of the element by 1\. 
        mp[arr[i]] = mp.get(arr[i], 0) + 1

    for i in range(n): 

        # Print the element which appear 
        # more than or equal to k times. 
        if (arr[i] in mp and mp[arr[i]] >= k): 
            print(arr[i], end = " ") 

# Driver Code 
arr = [1, 2, 2, 3, 2, 3, 4] 
n = len(arr) 
k = 2
removeElements(arr, n, k) 

# This code is contributed by Mohit Kumar 

```

## C＃

```

// C# program to remove the elements which  
// appear strictly less than k times from the array.  
using System; 
using System.Collections.Generic; 

class geeks  
{ 

    public static void removeElements(int[] arr,  
                                        int n, int k) 
    { 

        // Hash map which will store the 
        // frequency of the elements of the array. 
        Dictionary<int, int> mp = new Dictionary<int, int>(); 

        for (int i = 0; i < n; ++i)  
        { 

            // Incrementing the frequency 
            // of the element by 1\. 
            if (!mp.ContainsKey(arr[i])) 
                mp.Add(arr[i], 1); 
            else
            { 
                int x = mp[arr[i]]; 
                mp[arr[i]] = mp[arr[i]] + ++x; 
            } 
        } 

        for (int i = 0; i < n; ++i)  
        { 

            // Print the element which appear 
            // more than or equal to k times. 
            if (mp[arr[i]] >= k) 
                Console.Write(arr[i] + " "); 
        } 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        int[] arr = { 1, 2, 2, 3, 2, 3, 4 }; 
        int n = arr.Length; 
        int k = 2; 
        removeElements(arr, n, k); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
2 2 3 2 3

```

**时间复杂度** – O（N）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。