# 第一个元素在数组

中出现 k 次

给定 n 个整数数组。 任务是找到出现 k 次的第一个元素。 如果没有元素出现 k 倍，则打印-1。 整数元素的分布可以在任何范围内。

**示例：**

> **输入**：{1、7、4、3、4、8、7}，
> k = 2
> **输出**：7
> 都 **7** 和 **4** 出现 2 次。
> 但是 **7** 是第一次出现 2 次。
> 
> **输入**：{4，1，6，1，6，6，}，
> k = 1
> **输出**：-1

**简单方法：**通过使用两个循环，计算数字在数组中出现的次数。

**时间复杂度**：O（n <sup>2</sup> ）。

**高效方法：**将 [unordered_map](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) 用于散列，因为范围未知。 脚步：

1.  从左到右遍历数组元素。
2.  遍历时，它们在哈希表中的计数增加。
3.  再次从左到右遍历数组，并检查哪个元素的计数等于 k。 打印该元素并停止。
4.  如果没有元素的计数等于 k，则打印-1。

以下是上述方法的模拟：

![](img/ced39014dfd59d214209390f1be799aa.png)

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find first 
// element occurring k times 
#include <bits/stdc++.h> 

using namespace std; 

// function to find the first element 
// occurring k number of times 
int firstElement(int arr[], int n, int k) 
{ 
    // unordered_map to count 
    // occurrences of each element 
    unordered_map<int, int> count_map; 
    for (int i=0; i<n; i++) 
        count_map[arr[i]]++; 

    for (int i=0; i<n; i++)   

        // if count of element == k ,then 
        // it is the required first element  
        if (count_map[arr[i]] == k) 
            return arr[i]; 

    // no element occurs k times 
    return -1; 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = {1, 7, 4, 3, 4, 8, 7}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 2; 
    cout << firstElement(arr, n, k); 
    return 0; 
}  

```

## Java

```java

import java.util.HashMap; 

// Java implementation to find first 
// element occurring k times 
class GFG { 

// function to find the first element 
// occurring k number of times 
    static int firstElement(int arr[], int n, int k) { 
        // unordered_map to count 
        // occurrences of each element 

        HashMap<Integer, Integer> count_map = new HashMap<>(); 
        for (int i = 0; i < n; i++) { 
            int a = 0; 
            if(count_map.get(arr[i])!=null){ 
                a = count_map.get(arr[i]); 
            } 

            count_map.put(arr[i], a+1); 
        } 
        //count_map[arr[i]]++; 

        for (int i = 0; i < n; i++) // if count of element == k ,then 
        // it is the required first element  
        { 
            if (count_map.get(arr[i]) == k) { 
                return arr[i]; 
            } 
        } 

        // no element occurs k times 
        return -1; 
    } 

// Driver program to test above 
    public static void main(String[] args) { 
        int arr[] = {1, 7, 4, 3, 4, 8, 7}; 
        int n = arr.length; 
        int k = 2; 
        System.out.println(firstElement(arr, n, k)); 
    } 
} 

//this code contributed by Rajput-Ji 

```

## Python3

```py

# Python3 implementation to  
# find first element  
# occurring k times 

# function to find the  
# first element occurring  
# k number of times 
def firstElement(arr, n, k): 

    # dictionary to count 
    # occurrences of  
    # each element 
    count_map = {}; 
    for i in range(0, n): 
        if(arr[i] in count_map.keys()): 
            count_map[arr[i]] += 1
        else: 
            count_map[arr[i]] = 1
        i += 1

    for i in range(0, n):  

        # if count of element == k , 
        # then it is the required 
        # first element  
        if (count_map[arr[i]] == k): 
            return arr[i] 
        i += 1

    # no element occurs k times 
    return -1

# Driver Code 
if __name__=="__main__": 

    arr = [1, 7, 4, 3, 4, 8, 7]; 
    n = len(arr) 
    k = 2
    print(firstElement(arr, n, k)) 

# This code is contributed  
# by Abhishek Sharma 

```

## C#

```cs

// C# implementation to find first  
// element occurring k times  
using System; 
using System.Collections.Generic; 

class GFG  
{  

    // function to find the first element  
    // occurring k number of times  
    static int firstElement(int []arr, int n, int k)  
    {  
        // unordered_map to count  
        // occurrences of each element  

        Dictionary<int, int> count_map = new Dictionary<int,int>();  
        for (int i = 0; i < n; i++) 
        {  
            int a = 0;  
            if(count_map.ContainsKey(arr[i])) 
            {  
                a = count_map[arr[i]];  
                count_map.Remove(arr[i]); 
                count_map.Add(arr[i], a+1); 
            }  
            else
                count_map.Add(arr[i], 1);  
        }  
        //count_map[arr[i]]++;  

        for (int i = 0; i < n; i++) // if count of element == k ,then  
        // it is the required first element  
        {  
            if (count_map[arr[i]] == k)  
            {  
                return arr[i];  
            }  
        }  

        // no element occurs k times  
        return -1;  
    }  

    // Driver code  
    public static void Main(String[] args)  
    {  
        int []arr = {1, 7, 4, 3, 4, 8, 7};  
        int n = arr.Length;  
        int k = 2;  
        Console.WriteLine(firstElement(arr, n, k));  
    }  
}  

// This code has been contributed by 29AjayKumar  

```

**Output:**

```
7

```

**时间复杂度：** O（n）

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

