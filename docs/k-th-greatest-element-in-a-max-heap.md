# 最大堆中第 K 大元素

> 原文:[https://www . geesforgeks . org/k-th-max-heap 中最大元素/](https://www.geeksforgeeks.org/k-th-greatest-element-in-a-max-heap/)

给定大小为 n 的最大堆，在最大堆中找到第 k 个最大的元素。

**示例:**

> **输入** : maxHeap = {20，15，18，8，10，5，17}
> k = 4
> **输出** : 15
> 
> **输入** : maxHeap = {100，50，80，10，25，20，75}
> k = 2
> **输出** : 80

**天真方法**:我们可以从最大堆 k 次提取最大元素，最后提取的元素将是第 k 个<sup>最大元素</sup>。每次删除操作需要 O(log n)个时间，因此这种方法的总时间复杂度为 O(k * log n)。

下面是该方法的实现:

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Structure for the heap
struct Heap {
    vector<int> v;
    int n; // Size of the heap

    Heap(int i = 0)
        : n(i)
    {
        v = vector<int>(n);
    }
};

// Generic function to
// swap two integers
void swap(int& a, int& b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Returns the index of
// the parent node
inline int parent(int i)
{
    return (i - 1) / 2;
}

// Returns the index of
// the left child node
inline int left(int i)
{
    return 2 * i + 1;
}

// Returns the index of
// the right child node
inline int right(int i)
{
    return 2 * i + 2;
}

// Maintains the heap property
void heapify(Heap& h, int i)
{
    int l = left(i), r = right(i), m = i;
    if (l < h.n && h.v[i] < h.v[l])
        m = l;
    if (r < h.n && h.v[m] < h.v[r])
        m = r;
    if (m != i) {
        swap(h.v[m], h.v[i]);
        heapify(h, m);
    }
}

// Extracts the maximum element
int extractMax(Heap& h)
{
    if (!h.n)
        return -1;
    int m = h.v[0];
    h.v[0] = h.v[h.n-- - 1];
    heapify(h, 0);
    return m;
}

int kThGreatest(Heap &h, int k)
{
    for (int i = 1; i < k; ++i)
        extractMax(h);
    return extractMax(h);
}

// Driver Code
int main()
{
    Heap h(7);
    h.v = vector<int>{ 20, 15, 18, 8, 10, 5, 17 };
    int k = 4;

    cout << kThGreatest(h, k);
    return 0;
}
```

**Output:**

```
15

```

**时间复杂度** : O(k * log n)

**高效方法**:我们可以注意到一个关于最大堆的有趣观察。i <sup>第</sup>级的元素 x 有 I–1 个祖先。根据最大堆的属性，这些**I–1**祖先保证大于 x。这意味着 x 不能是堆中最大的**I–1**元素。利用这个性质，我们可以得出结论，k <sup>第</sup>个最大的元素最多可以有 k 级。

我们可以减少最大堆的大小，使它只有 k 个级别。然后，我们可以通过前面提取最大元素 k 次的策略来获得第 k 个最大元素。请注意，堆的大小减少到最大 2<sup>k</sup>–1，因此每个堆操作将花费 O(log 2 <sup>k</sup> ) = O(k)时间。总时间复杂度为 0(k<sup>2</sup>)。如果 n > > k，那么这种方法的性能会比前一种更好。

下面是该方法的实现:

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Structure for the heap
struct Heap {
    vector<int> v;
    int n; // Size of the heap

    Heap(int i = 0)
        : n(i)
    {
        v = vector<int>(n);
    }
};

// Generic function to
// swap two integers
void swap(int& a, int& b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Returns the index of
// the parent node
inline int parent(int i)
{
    return (i - 1) / 2;
}

// Returns the index of
// the left child node
inline int left(int i)
{
    return 2 * i + 1;
}

// Returns the index of
// the right child node
inline int right(int i)
{
    return 2 * i + 2;
}

// Maintains the heap property
void heapify(Heap& h, int i)
{
    int l = left(i), r = right(i), m = i;
    if (l < h.n && h.v[i] < h.v[l])
        m = l;
    if (r < h.n && h.v[m] < h.v[r])
        m = r;
    if (m != i) {
        swap(h.v[m], h.v[i]);
        heapify(h, m);
    }
}

// Extracts the maximum element
int extractMax(Heap& h)
{
    if (!h.n)
        return -1;
    int m = h.v[0];
    h.v[0] = h.v[h.n-- - 1];
    heapify(h, 0);
    return m;
}

int kThGreatest(Heap &h, int k)
{
    // Change size of heap
    h.n = min(h.n, int(pow(2, k) - 1));

    for (int i = 1; i < k; ++i)
        extractMax(h);

    return extractMax(h);
}

// Driver Code
int main()
{
    Heap h(7);
    h.v = vector<int>{ 20, 15, 18, 8, 10, 5, 17 };
    int k = 2;

    cout << kThGreatest(h, k);
    return 0;
}
```

**Output:**

```
18

```

**时间复杂度** : O(k <sup>2</sup>

**更高效的方法**:我们可以通过以下算法进一步提高这个问题的时间复杂度:

1.  创建一个优先级队列 P，并将最大堆的根节点插入到 P 中
2.  重复这些步骤 k-1 次:
    1.  从 p 中弹出最大的元素。
    2.  插入弹出元素的左右子元素。(如果存在的话)。
3.  P 中最大的元素是最大堆的第 k <sup>个</sup>最大元素。

优先级队列的初始大小为 1，并且在 k-1 个步骤中的每一步最多增加 1。因此，优先级队列中最多有 k 个元素，pop 和 insert 操作的时间复杂度为 O(log k)。因此，总时间复杂度为 0(k * log k)。

下面是上述方法的实现:

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Structure for the heap
struct Heap {
    vector<int> v;
    int n; // Size of the heap

    Heap(int i = 0)
        : n(i)
    {
        v = vector<int>(n);
    }
};

// Returns the index of
// the left child node
inline int left(int i)
{
    return 2 * i + 1;
}

// Returns the index of
// the right child node
inline int right(int i)
{
    return 2 * i + 2;
}

int kThGreatest(Heap &h, int k)
{
    priority_queue<pair<int, int> > p;
    p.push(make_pair(h.v[0], 0));

    for (int i = 0; i < k - 1; ++i) {
        int j = p.top().second;
        p.pop();
        int l = left(j), r = right(j);
        if (l < h.n)
            p.push(make_pair(h.v[l], l));
        if (r < h.n)
            p.push(make_pair(h.v[r], r));
    }
    return p.top().first;
}

// Driver Code
int main()
{
    Heap h(7);
    h.v = vector<int>{ 20, 15, 18, 8, 10, 5, 17 };
    int k = 2;

    cout << kThGreatest(h, k);
    return 0;
}
```

**Output:**

```
18

```

**时间复杂度** : O(k * log k)