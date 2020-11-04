# 对 Q 查询用 K 替换给定索引后，数组中最频繁的元素

> 原文：[https://www.geeksforgeeks.org/most-frequent-element-in-array-after-replacing-given-index-by-k-for-q-queries/](https://www.geeksforgeeks.org/most-frequent-element-in-array-after-replacing-given-index-by-k-for-q-queries/)

给定大小为 **N** 的数组 **arr []** ，并以 **{i，k}** 的形式查询 **Q** 在**用 k** 替换 arr [i]之后，将在数组中打印**最频繁元素**。

**示例**：

> **输入**：arr [] = {2，2，2，3，3}，Querry = {{0，3}，{4，2}，{0，4}}
> **输出**：3 2 2
> 第一个查询：设置 arr [0] = 3 会修改 arr [] = {3，2，2，3，3}。 因此，3 具有最大频率。
> 第二个查询：设置 arr [4] = 2，修改 arr [] = {3，2，2，3，2}。 因此，2 具有最大频率。
> 第三个查询：设置 arr [0] = 4，修改 arr [] = {4，2，2，3，2}。 所以 2 有最大频率
> 
> **输入**：arr [] = {1,2,3,4,3,3} Querry = {{0，2}，{3，2}，{2，4}}}
> [ **输出**：3 2 2

**朴素的方法**：

对于每个查询，将 arr [i]替换为 K，遍历整个数组并计算每个数组元素的频率并打印最频繁的元素。

**时间复杂度**：O（N * Q）

**辅助空间**：`O(n)`

**高效方法**：

可以通过预先计算每个数组元素的频率并将频率数组元素配对保持在一组中以获得`O(1)`中最频繁的元素来优化上述方法。 请按照以下步骤解决问题：

1.  初始化[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)以存储所有数组元素的频率，并初始化[对](https://www.geeksforgeeks.org/set-in-cpp-stl/)[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的集以存储频率元素对。 在集合中，将频率存储为负数。 这确保了存储在集合开头的第一对，即 [s.begin（），](https://www.geeksforgeeks.org/setbegin-setend-c-stl/)是 **{-（最大频率），最频繁元素}** 配对。

2.  对于每个查询，在删除第<sup>个第</sup>索引处的数组元素的同时，执行以下任务：

    *   从图中找到 arr [i]的频率，即 **mp [arr [i]]。**

    *   从集合中删除对 **{-mp [arr [i]]，arr [i]}** 。

    *   通过将 **{-（mp [arr [i] – 1），arr [i]}** 插入频率降低 **arr [i]** 的频率后更新该集合。

    *   降低映射中 **arr [i]** 的频率。

    *   要将每个查询的 **K** 插入数组，请执行以下操作：

        *   从图中找到 **K** 的频率，即 **mp [K]** 。

        *   从集合中删除对 **{-mp [K]，K}** 。

        *   通过将 **{-（mp [K] + 1），K}** 插入到 **K** 的频率中来更新该集合。

        *   在图中增加 **K** 的频率。

    *   最后，对于每个查询，在集合的开头提取对。 集合中的**第一元素**表示**-（最大频率）**。 因此，第二个元素将是最常见的元素。 打印该对的第二个元素。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the most  
// frequent element after every  
// update query on the array  

#include <bits/stdc++.h>  
using namespace std;  

typedef long long int ll;  

// Function to print the most  
// frequent element of array  
// along with update querry  
void mostFrequent(ll arr[], ll n, ll m,  
                vector<vector<ll> > q)  
{  
    ll i;  

    // Stores element->fequencies  
    // mappings  
    map<ll, ll> mp;  

    for (i = 0; i < n; i++)  
        mp[arr[i]] += 1;  

    // Stores frequencies->element  
    // mappings  
    set<pair<ll, ll> > s;  

    // Store the frequencies in  
    // negative  
    for (auto it : mp) {  
        s.insert(make_pair(-(it.second),  
                        it.first));  
    }  

    for (i = 0; i < m; i++) {  

        // Index to be modified  
        ll j = q[i][0];  

        // Value to be inserted  
        ll k = q[i][1];  

        // Store the frequency of  
        // arr[j] and k  
        auto it = mp.find(arr[j]);  
        auto it2 = mp.find(k);  

        // Remove mapping of arr[j]  
        // with previous frequency  
        s.erase(make_pair(-(it->second),  
                        it->first));  

        // Update mapping with new  
        // frequency  
        s.insert(make_pair(-((it->second)  
                            - 1),  
                        it->first));  

        // Update frequency of arr[j]  
        // in the map  
        mp[arr[j]]--;  

        // Remove mapping of k  
        // with previous frequency  
        s.erase(make_pair(-(it2->second),  
                        it2->first));  

        // Update mapping of k  
        // with previous frequency  
        s.insert(make_pair(-((it2->second)  
                            + 1),  
                        it2->first));  

        // Update frequency of k  
        mp[k]++;  

        // Replace arr[j] by k  
        arr[j] = k;  

        // Display maximum frequent element  
        cout << (*s.begin()).second << " ";  
    }  
}  
// Driver Code  
int main()  
{  

    ll i, N, Q;  
    N = 5;  
    Q = 3;  
    ll arr[] = { 2, 2, 2, 3, 3 };  
    vector<vector<ll> > querry = {  
        { 0, 3 },  
        { 4, 2 },  
        { 0, 4 }  
    };  

    mostFrequent(arr, N, Q, querry);  
}  

```

## Java

```java

// Java program to find the most  
// frequent element after every  
// update query on the array  
import java.util.*; 
import java.io.*; 

class GFG{ 

// Pair class represents 
// a pair of elements 
static class Pair 
{ 
    int first, second; 
    Pair(int f,int s) 
    { 
        first = f; 
        second = s; 
    } 
} 

// Function to print the most  
// frequent element of array  
// along with update querry  
static void mostFrequent(int arr[], int n, int m,  
                         ArrayList<Pair> q)  
{  
    int i;  

    // Stores element->fequencies  
    // mappings  
    HashMap<Integer, Integer> map = new HashMap<>(); 
    HashMap<Integer, Pair> map1 = new HashMap<>(); 

    for(i = 0; i < n; i++)  
    { 
        if(!map.containsKey(arr[i])) 
            map.put(arr[i], 1); 
        else
            map.put(arr[i], map.get(arr[i]) + 1); 
    }  

    // Stores frequencies->element  
    // mappings  
    TreeSet<Pair> set = new TreeSet<>( 
                        new Comparator<Pair>() 
    { 
        public int compare(Pair p1, Pair p2) 
        { 
            return p2.first - p1.first; 
        } 
    }); 

    // Store the frequencies in  
    // bigger to smaller 
    for(Map.Entry<Integer,  
                  Integer> entry : map.entrySet()) 
    {  
        Pair p = new Pair(entry.getValue(),  
                          entry.getKey()); 
        set.add(p); 
        map1.put(entry.getKey(), p); 
    }  

    for(i = 0; i < m; i++) 
    {  

        // Index to be modified  
        int j = q.get(i).first; 

        // Value to be inserted  
        int k = q.get(i).second;  

        // Insert the new Pair 
        // with value k if it was 
        // not inserted 
        if(map1.get(k) == null) 
        { 
            Pair p = new Pair(0, k); 
            map1.put(k, p); 
            set.add(p); 
        } 

        // Get the Pairs of  
        // arr[j] and k  
        Pair p1 = map1.get(arr[j]);  
        set.remove(p1); 
        Pair p2 = map1.get(k); 
        set.remove(p2); 

        // Decrease the frequency of  
        // mapping with value arr[j] 
        p1.first--; 
        set.add(p1); 

        // Update frequency of arr[j]  
        // in the map  
        map.put(arr[j], map.get(arr[j]) - 1);  

        // Increase the frequency of  
        // mapping with value k 
        p2.first++; 
        set.add(p2); 

        // Update frequency of k  
        if(map.containsKey(k)) 
            map.put(k, map.get(k) + 1);  
        else
            map.put(k, 1); 

        // Replace arr[j] by k  
        arr[j] = k;  

        // Display maximum frequent element  
        System.out.print( 
            set.iterator().next().second + " ");  
    }  
}  

// Driver Code  
public static void main(String []args) 
{  
    int i, N, Q;  
    N = 5;  
    Q = 3;  
    int arr[] = { 2, 2, 2, 3, 3 };  

    ArrayList<Pair> query = new ArrayList<>(); 
    query.add(new Pair(0, 3)); 
    query.add(new Pair(4, 2)); 
    query.add(new Pair(0, 4)); 

    mostFrequent(arr, N, Q, query);  
}  
} 

// This code is contributed by Ganeshchowdharysadanala 

```

**Output:**

```
3 2 2 
```

**时间复杂度**：O（N +（Q * LogN））

**辅助空间**：`O(n)`



* * *

* * *



