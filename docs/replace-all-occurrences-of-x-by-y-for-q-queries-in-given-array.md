# 用 Y 替换给定数组中 Q 查询的所有 X 出现次数

> 原文:[https://www . geesforgeks . org/replace-all-occurs-of-x-by-y-for-q-query-in-给定数组/](https://www.geeksforgeeks.org/replace-all-occurrences-of-x-by-y-for-q-queries-in-given-array/)

给定一个数组 **arr[]** 和一个由查询组成的 2D 数组**查询[][]** 。对于每个查询 **q** ，将**arr【】**中所有出现的**查询【I】【0】**替换为**查询【I】【1】**。

**示例:**

> **输入:** arr[] = {2，2，5，1}查询= {{2，4}，{5，2}}
> **输出:** {4，4，2，1}
> **解释:**下面是根据给定的查询在给定数组中执行的操作。
> 对于第一个查询{2，4}，将 arr[]中出现的所有 2 替换为 4。arr[]将更新为 arr[] = {4，4，5，1}。
> 对于第二个查询{5，2}，将所有出现的 5 替换为 2。arr[]将更新为 arr[] = {4，4，2，1}。
> 
> **输入:** arr[] ={2，2，5}，查询= {{4，5}，{2，5}，{1，3}，{2，4}}
> **输出:** {5，5，5}

天真方法:(蛮力解决方案)天真方法是遍历**查询**的所有查询，对于每个**查询【I】【0】**，在**arr【】**中找到它的所有出现，并替换为**查询【I】【1】**。

**时间复杂度:** O(N*Q)，其中 N 为 arr[]的大小，Q 为查询[][]的大小。
**辅助空间:** O(1)

**高效方法:**更好的解决方案是使用 Hashmap，它在数组中存储元素的索引。按照以下步骤解决给定的问题。

*   初始化一个 **hashmap = {}** ，用数组元素作为键填充，并列出指示其在数组中的位置。
*   遍历**查询[][]** 的每个查询 **q** 。
    *   如果**散列表**中存在 **q[0]** ，
        *   如果**散列表**中存在 **q[1]** ，则将 **q[0]** 的值扩展至 **q[1]** 键的值。
        *   否则，将 q[0]键的值加到 **q[1]** 键上。
        *   从**散列表**中删除 q[0]的键值对。
*   现在，根据**散列表**的值创建一个新的变量**映射= {}** 。
*   交换键值对，这样**映射**将包含键值对作为索引，**的键值作为 hashmap。**
*   使用这个**地图**，我们现在可以更新原始数组 **arr** ，通过更新 **arr** 每个位置的值，值来自**地图**。

以下是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace all the
// occurrences of a number with
// another given number for Q queries
void update(vector<int>& A, int N, vector<vector<int> >& Q)
{

    // Creating a hashmap
    map<int, vector<int> > hashmap;
    for (int i = 0; i < N; ++i) {
        hashmap[A[i]].push_back(i);
    }

    // Iterating with q in given queries
    for (auto q : Q) {
        if (hashmap.count(q[0])) {
            if (hashmap.count(q[1]))
                hashmap[q[1]].insert(hashmap[q[1]].end(),
                                     hashmap[q[0]].begin(),
                                     hashmap[q[0]].end());
            else
                hashmap[q[1]] = hashmap[q[0]];
            hashmap.erase(q[0]);
        }
    }

    // Creating map to store key value pairs
    map<int, int> new_map;
    for (auto it = hashmap.begin(); it != hashmap.end();
         ++it) {
        for (auto index : it->second)
            new_map[index] = it->first;
    }

    // Updating the main array with final values
    for (auto it = new_map.begin(); it != new_map.end();
         ++it)
        A[it->first] = it->second;
}

// Driver Code
int main()
{
    vector<int> arr = { 2, 2, 5, 1 };
    int N = arr.size();
    vector<vector<int> > query = { { 2, 4 }, { 5, 2 } };
    update(arr, N, query);
    for (int i = 0; i < N; ++i) {
        cout << arr[i] << " ";
    }

   return 0;
}

    // This code is contributed by rakeshsahni
```

## 蟒蛇 3

```
# Python program for above approach

# Function to replace all the
# occurrences of a number with
# another given number for Q queries
def update(A, N, Q):
      # Creating a hashmap
    hashmap = {a:[] for a in A}
    for i in range(N):
        hashmap[A[i]].append(i)

    # Iterating with q in given queries
    for q in Q:
        if q[0] in hashmap:
            if q[1] in hashmap:
                hashmap[q[1]].extend(hashmap[q[0]])
            else:
                hashmap[q[1]] = hashmap[q[0]]
            del hashmap[q[0]]

    # Creating map to store key value pairs
    new_map = {}
    for key, value in hashmap.items():
        for index in value:
            new_map[index] = key

    # Updating the main array with final values
    for key in new_map.keys():
        A[key] = new_map[key]

# Driver Code
if __name__ == '__main__':
  arr = [2, 2, 5, 1]
  N = len(arr)
  query = [[2, 4], [5, 2]]
  update(arr, N, query)
  print(arr)
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to replace all the
// occurrences of a number with
// another given number for Q queries
function update(A, N, Q)
{

      // Creating a hashmap
    let hashmap = new Map();
    for(let i = 0; i < N; i++){
        if(hashmap.has(A[i])){
          let temp = hashmap.get(A[i])
          temp.push(i)
          hashmap.set(A[i], temp)
        }else{
          hashmap.set(A[i], [i])
        }

    }

    // Iterating with q in given queries
    for(q of Q){
        if(hashmap.has(q[0])){
            if (hashmap.has(q[1])){
                let temp = hashmap.get(q[1]);

                temp = [...temp, ...hashmap.get(q[0])]
                hashmap.set(q[1], temp);
            }
            else{
                hashmap.set(q[1], hashmap.get(q[0]))
            }
            hashmap.delete(q[0])
        }
    }

    // Creating map to store key value pairs
    let new_map = new Map()
    for(x of hashmap)
        for(index of x[1])
            new_map.set(index, x[0])

    // Updating the main array with final values
    for(key of new_map.keys())
        A[key] = new_map.get(key)
    document.write(`[ ${A}] `)
}

// Driver Code
let arr = [2, 2, 5, 1]
let N = arr.length
let query = [[2, 4], [5, 2]]
update(arr, N, query)

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
[4, 4, 2, 1]
```

**时间复杂度:** O(max(N，Q))，其中 N 为 arr[]的大小，Q 为查询[][]的大小。
**辅助空间:** O(N)