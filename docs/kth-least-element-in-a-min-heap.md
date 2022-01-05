# 最小堆中的第 K 个最小元素

> 原文:[https://www . geesforgeks . org/kth-最小堆中最少元素/](https://www.geeksforgeeks.org/kth-least-element-in-a-min-heap/)

给定一个 n 大小的最小堆，在最小堆中找到第 k<sup>个最少的元素。</sup>

**示例:**

> **输入** : {10，50，40，75，60，65，45}
> k = 4
> **输出** : 50
> 
> **输入** : {10，50，40，75，60，65，45}
> k = 2
> **输出** : 40

**天真方法** :
我们可以从[最小堆](https://www.geeksforgeeks.org/binary-heap/)中提取最小元素 k 次，最后提取的元素将是第 k 个<sup>最小元素</sup>。每次删除操作需要 O(log n)个时间，因此这种方法的总时间复杂度为 O(k * log n)。

```
// C++ program to find k-th smallest
// element in Min Heap.
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
    if (l < h.n && h.v[i] > h.v[l])
        m = l;
    if (r < h.n && h.v[m] > h.v[r])
        m = r;
    if (m != i) {
        swap(h.v[m], h.v[i]);
        heapify(h, m);
    }
}

// Extracts the minimum element
int extractMin(Heap& h)
{
    if (!h.n)
        return -1;
    int m = h.v[0];
    h.v[0] = h.v[h.n-- - 1];
    heapify(h, 0);
    return m;
}

int findKthSmalles(Heap &h, int k)
{
    for (int i = 1; i < k; ++i)
        extractMin(h);
    return extractMin(h);
}

int main()
{
    Heap h(7);
    h.v = vector<int>{ 10, 50, 40, 75, 60, 65, 45 };
    int k = 2;
    cout << findKthSmalles(h, k);
    return 0;
}
```

**Output:**

```
40

```

**时间复杂度:O(k * log n)**

**高效方法** :
我们可以注意到一个关于最小堆的有趣观察。i <sup>级</sup>的元素 x 有 I–1 个祖先。根据最小堆的属性，这些 I-1 祖先保证小于 x。这意味着 x 不能是堆中最少的 I-1 元素。利用这个属性，我们可以得出结论，k <sup>第</sup>个最少元素最多可以有 k 个级别。

我们可以减小最小堆的大小，使它只有 k 个级别。然后，我们可以通过之前提取 k 次最小元素的策略来获得第 k 个<sup>最小元素。请注意，堆的大小减少到最大 2<sup>k</sup>–1，因此每个堆操作将花费 O(log 2 <sup>k</sup> ) = O(k)时间。总时间复杂度为 0(k<sup>2</sup>)。如果 n > > k，那么这种方法的性能会比前一种更好。</sup>

```
// C++ program to find k-th smallest
// element in Min Heap using k levels
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
    if (l < h.n && h.v[i] > h.v[l])
        m = l;
    if (r < h.n && h.v[m] > h.v[r])
        m = r;
    if (m != i) {
        swap(h.v[m], h.v[i]);
        heapify(h, m);
    }
}

// Extracts the minimum element
int extractMin(Heap& h)
{
    if (!h.n)
        return -1;
    int m = h.v[0];
    h.v[0] = h.v[h.n-- - 1];
    heapify(h, 0);
    return m;
}

int findKthSmalles(Heap &h, int k)
{
    h.n = min(h.n, int(pow(2, k) - 1));
    for (int i = 1; i < k; ++i)
        extractMin(h);
    return extractMin(h);
}

int main()
{
    Heap h(7);
    h.v = vector<int>{ 10, 50, 40, 75, 60, 65, 45 };
    int k = 2;
    cout << findKthSmalles(h, k);
    return 0;
}
```

**Output:**

```
40

```

**时间复杂度:O(k <sup>2</sup> )**

**更有效的方法** :
我们可以通过以下算法进一步提高这个问题的时间复杂度:

1.  创建一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) P(或最小堆)，并将最小堆的根节点插入到 P 中。优先级队列的比较器功能应该是弹出最少的元素。
2.  重复这些步骤 k-1 次:
    1.  从 p 中弹出最少的元素。
    2.  插入弹出元素的左右子元素。(如果存在的话)。
3.  P 中最少的元素是最小堆中第 k 个最少的元素。

优先级队列的初始大小为 1，并且在 k-1 个步骤中的每一步最多增加 1。因此，优先级队列中最多有 k 个元素，pop 和 insert 操作的时间复杂度为 O(log k)。因此，总时间复杂度为 0(k * log k)。

```
// C++ program to find k-th smallest
// element in Min Heap using another
// Min Heap (Or Priority Queue)
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

int findKthSmalles(Heap &h, int k)
{
    // Create a Priority Queue
    priority_queue<pair<int, int>,
                   vector<pair<int, int> >,
                   greater<pair<int, int> > >
        p;

    // Insert root into the priority queue
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

int main()
{
    Heap h(7);
    h.v = vector<int>{ 10, 50, 40, 75, 60, 65, 45 };
    int k = 4;
    cout << findKthSmalles(h, k);
    return 0;
}
```

**Output:**

```
50

```

**时间复杂度:O(k * log k)**