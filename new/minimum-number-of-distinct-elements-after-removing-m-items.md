# 删除 m 个项目后的最小不同元素数

给定一个项目数组，第 i 个索引元素表示该项目 ID，给定数字 m，任务是删除 m 个元素，以使剩余的唯一 ID 最少。打印不同 ID 的数量。

例子：

```
Input : arr[] = { 2, 2, 1, 3, 3, 3} 
            m = 3
Output : 1
Remove 1 and both 2's.So, only 3 will be 
left that's why distinct id is 1.

Input : arr[] = { 2, 4, 1, 5, 3, 5, 1, 3} 
            m = 2
Output : 3
Remove 2 and 4 completely. So, remaining ids 
are 1, 3 and 5 i.e. 3

```

询问：摩根士丹利

1-计算元素的出现并存储在哈希中。
2-对哈希进行排序。
3-开始从哈希中删除元素。
4-返回哈希中剩余的值数。

## C++

```cpp

// C++ program for above implementation 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find distintc id's 
int distinctIds(int arr[], int n, int mi) 
{ 
    unordered_map<int, int> m; 
    vector<pair<int, int> > v; 
    int count = 0; 

    // Store the occurrence of ids 
    for (int i = 0; i < n; i++) 
        m[arr[i]]++; 

    // Store into the vector second as first and vice-versa 
    for (auto it = m.begin(); it != m.end(); it++) 
        v.push_back(make_pair(it->second, it->first)); 

    // Sort the vector 
    sort(v.begin(), v.end()); 

    int size = v.size(); 

    // Start removing elements from the beginning 
    for (int i = 0; i < size; i++) { 

        // Remove if current value is less than  
        // or equal to mi 
        if (v[i].first <= mi) { 
            mi -= v[i].first; 
            count++; 
        } 

        // Return the remaining size 
        else
            return size - count; 
    } 
    return size - count; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 2, 3, 1, 2, 3, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int m = 3; 

    cout << distinctIds(arr, n, m); 
    return 0; 
} 

```

## Java

```java

//Java program for Minimum number of 
//distinct elements after removing m items 
import java.util.HashMap; 
import java.util.Map; 
import java.util.Map.Entry; 

public class DistinctIds 
{ 
    // Function to find distintc id's 
    static int distinctIds(int arr[], int n, int mi) 
    { 

        Map<Integer, Integer> m = new HashMap<Integer, Integer>(); 
        int count = 0; 
        int size = 0; 

        // Store the occurrence of ids 
        for (int i = 0; i < n; i++) 
        { 

            // If the key is not add it to map 
            if (m.containsKey(arr[i]) == false) 
            { 
                m.put(arr[i], 1); 
                size++; 
            } 

            // If it is present then increase the value by 1 
            else m.put(arr[i], m.get(arr[i]) + 1); 
        } 

        // Start removing elements from the beginning 
        for (Entry<Integer, Integer> mp:m.entrySet()) 
        { 
            // Remove if current value is less than 
            // or equal to mi 
            if (mp.getKey() <= mi) 
            { 
                mi -= mp.getKey(); 
                count++; 
            } 
            // Return the remaining size 
            else return size - count; 
        } 

        return size - count; 
    } 

    //Driver method to test above function 
    public static void main(String[] args) 
    { 
        // TODO Auto-generated method stub 
        int arr[] = {2, 3, 1, 2, 3, 3}; 
        int m = 3; 

        System.out.println(distinctIds(arr, arr.length, m)); 
    } 
} 
//This code is contributed by Sumit Ghosh 

```

Output:

```
1

```

时间复杂度：O（n log n）

本文由 **[Sahil Chhabra](https://www.facebook.com/sahil.chhabra.965)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

