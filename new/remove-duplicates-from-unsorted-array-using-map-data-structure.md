# 使用 Map 数据结构

从未排序的数组中删除重复项

给定一个未排序的整数数组，请从中删除重复的元素后再打印该数组。 我们需要根据它们的首次出现来打印不同的数组元素。

**示例：**

```
Input : arr[] = { 1, 2, 5, 1, 7, 2, 4, 2}
Output : 1 2 5 7 4
Explanation : {1, 2} appear more than one time.

```

**方法：**

*   拿一个哈希图，其中将存储之前出现的所有元素。
*   遍历数组。
*   检查元素是否存在于哈希图中。
*   如果是，请继续遍历数组。
*   其他打印元素。

## C ++

```

// C++ program to remove the duplicates from the array. 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

void removeDups(int arr[], int n) 
{ 
    // Hash map which will store the 
    // elements which has appeared previously. 
    unordered_map<int, bool> mp; 

    for (int i = 0; i < n; ++i) { 

        // Print the element if it is not 
        // there in the hash map 
        if (mp.find(arr[i]) == mp.end()) { 
            cout << arr[i] << " "; 
        } 

        // Insert the element in the hash map 
        mp[arr[i]] = true; 
    } 
} 

int main(int argc, char const* argv[]) 
{ 
    int arr[] = { 1, 2, 5, 1, 7, 2, 4, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    removeDups(arr, n); 
    return 0; 
} 

```

## 爪哇

```

// Java program to remove 
// the duplicates from the array. 
import java.util.HashMap; 

class GFG  
{ 
    static void removeDups(int[] arr, int n)  
    { 

        // Hash map which will store the 
        // elements which has appeared previously. 
        HashMap<Integer,  
                Boolean> mp = new HashMap<>(); 

        for (int i = 0; i < n; ++i) 
        { 

            // Print the element if it is not 
            // there in the hash map 
            if (mp.get(arr[i]) == null) 
                System.out.print(arr[i] + " "); 

            // Insert the element in the hash map 
            mp.put(arr[i], true); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int[] arr = { 1, 2, 5, 1, 7, 2, 4, 2 }; 
        int n = arr.length; 
        removeDups(arr, n); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```

# Python 3 program to remove the 
# duplicates from the array  
def removeDups(arr, n): 

    # dict to store every element 
    # one time 
    mp = {i : 0 for i in arr} 

    for i in range(n): 

        if mp[arr[i]] == 0: 
            print(arr[i], end = " ") 
            mp[arr[i]] = 1

# Driver code 
arr = [ 1, 2, 5, 1, 7, 2, 4, 2 ] 

# len of array 
n = len(arr) 

removeDups(arr,n) 

# This code is contributed 
# by Mohit Kumar 

```

## C＃

```

// C# program to remove 
// the duplicates from the array. 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    static void removeDups(int[] arr, int n)  
    { 

        // Hash map which will store the 
        // elements which has appeared previously. 
        Dictionary<int,  
                Boolean> mp = new Dictionary<int, Boolean>(); 

        for (int i = 0; i < n; ++i) 
        { 

            // Print the element if it is not 
            // there in the hash map 
            if (!mp.ContainsKey(arr[i])) 
                Console.Write(arr[i] + " "); 

            // Insert the element in the hash map 
            mp[arr[i]] = true; 
        } 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 1, 2, 5, 1, 7, 2, 4, 2 }; 
        int n = arr.Length; 
        removeDups(arr, n); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
1 2 5 7 4

```

**时间复杂度–** O（N）

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。