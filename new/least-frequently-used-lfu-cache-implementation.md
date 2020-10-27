# 最少使用（LFU）缓存实现

**最少使用（LFU）**是一种缓存算法，其中，每当缓存溢出时，都会删除最不常用的缓存块。 在 LFU 中，我们检查旧页面以及该页面的频率，如果该页面的频率大于旧页面，我们将无法删除它，并且如果所有旧页面具有相同的频率，则最后采用 FIFO 方法 并删除该页面。

**最小堆**数据结构是实现此算法的一个不错的选择，因为它可以处理对数时间复杂度的插入，删除和更新。 可以通过删除最近最少使用的缓存块来解决冲突。 以下两个容器已用于解决问题：

*   整数对的向量已用于表示高速缓存，其中每对均由块号和已使用的次数组成。 向量以最小堆的形式排序，这使我们可以在恒定时间内访问最不常用的块。
*   哈希图已用于存储高速缓存块的索引，从而允许在恒定时间内进行搜索。

下面是上述方法的实现：

```
// C++ program for LFU cache implementation
#include <bits/stdc++.h>
using namespace std;
// Generic function to swap two pairs
void swap(pair< int , int >& a, pair< int , int >& b)
{
pair< int , int > temp = a;
a = b;
b = temp;
}
// Returns the index of the parent node
inline int parent( int i)
{
return (i - 1) / 2;
}
// Returns the index of the left child node
inline int left( int i)
{
return 2 * i + 1;
}
[HTG3 24]
// Returns the index of the right child node
inline int right( int i)
{
return 2 * i + 2;
}
// Self made heap tp Rearranges
//  the nodes in order to maintain the heap property
void heapify(vector<pair< ] int , int > >& v,
unordered_map< int , int >& m, int i, int n)
{
int l = left(i), r = right(i), minim;
if (l < n)
minim = ((v[i].second < v[l].second) ? i : l);
else
minim = i;
if (r < n)
minim = ((v[minim].second < v[r].second) ? minim : r);
if (minim != i) {
m[v[minim].first] = i;
m[v[i].first] = minim;
swap(v[minim], v[i]);
heapify(v, m, minim, n);
}
}
// Function to Increment the frequency
// of a node and rearranges the heap
void increment(vector<pair< int , int > >& v,
unordered_map< int , int >& m, int i, int n)
{
++v[i].second;
heapify(v, m, i, n);
}
// Function to Insert a new node in the heap
void insert(vector<pair< int , int > >& v,
unordered_map< int , int >& m, int value, int & n)
{
if (n == v.size()) {
m.erase(v[0].first);
cout << "Cache block " << v[0].first
<< " removed.\n" ;
v[0] = v[--n];
heapify(v, m, 0, n);
}
v[n++] = make_pair(value, 1);
m.insert(make_pair(value, n - 1));
int i = n - 1;
// Insert a node in the heap by swapping elements
while (i && v[parent(i)].second > v[i].second) {
m[v[i].first] = parent(i);
m[v[parent(i)].first] = i;
swap(v[i], v[parent(i)]);
i = parent(i);
}
cout << "Cache block " << value << " inserted.\n" ;
}
// Function to refer to the block value in the cache
void refer(vector<pair< int , int > >& cache, unordered_map< int ,
int >& indices, int value, int & cache_size)
{
if (indices.find(value) == indices.end())
insert(cache, indices, value, cache_size);
else
increment(cache, indices, indices[value], cache_size);
}
// Driver Code
int main()
{
int cache_max_size = 4, cache_size = 0;
vector<pair< int , int > > cache(cache_max_size);
unordered_map< int , int > indices;
refer(cache, indices, 1, cache_size);
refer(cache, indices, 2, cache_size);
refer(cache, indices, 1, cache_size);
refer(cache, indices, 3, cache_size);
refer(cache, indices, 2, cache_size);
refer(cache, indices, 4, cache_size);
refer(cache, indices, 5, cache_size);
return 0;
[ }
```

**Output:**

```
Cache block 1 inserted.
Cache block 2 inserted.
Cache block 3 inserted.
Cache block 4 inserted.
Cache block 3 removed.
Cache block 5 inserted.

```



* * *

* * *



