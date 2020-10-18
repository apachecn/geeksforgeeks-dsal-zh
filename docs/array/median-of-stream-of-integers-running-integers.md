# 中位数为整数流（运行整数）

> 原文： [https://www.geeksforgeeks.org/median-of-stream-of-integers-running-integers/](https://www.geeksforgeeks.org/median-of-stream-of-integers-running-integers/)

假定从数据流中读取整数。 查找所读元素的中位数，以便高效地进行阅读。 为简单起见，假设没有重复项。 例如，让我们考虑流 5、15、1、3…

```
After reading 1st element of stream - 5 -> median - 5
After reading 2nd element of stream - 5, 15 -> median - 10
After reading 3rd element of stream - 5, 15, 1 -> median - 5
After reading 4th element of stream - 5, 15, 1, 3 -> median - 4, so on...
```

明确地说，当输入大小为奇数时，我们采用排序数据的中间元素。 如果输入大小为偶数，则选择排序流中中间两个元素的平均值。

请注意，输出是到目前为止从流中读取的整数的**有效中位数**。 这种算法称为在线算法。 在处理完第`i`个元素之后，可以保证`i`元素输出的任何算法都称为**在线算法**。 让我们讨论上述问题的三种解决方案。



**方法 1 - 插入排序**：

如果我们可以对显示的数据进行排序，则可以轻松地找到中值元素。 **插入排序**是一种在线算法，用于对到目前为止出现的数据进行排序。 在任何排序实例中，例如，在对第`i`个元素进行排序之后，将对数组的第`i + 1`个元素进行排序。 在此之前，插入排序并不依赖将来的数据来对输入的数据进行排序。 换句话说，插入排序考虑到插入下一个元素时到目前为止已排序的数据。 这是使其成为在线算法的插入排序的关键部分。

但是，插入排序需要 `O(n^2)`时间来对`n`个元素进行排序。 也许我们可以对**插入排序**使用**二分搜索**来查找`O(log n)`时间中下一个元素的位置。 但是，我们无法在`O(log n)`时间内进行数据移动。 无论实现的效率如何，在插入排序的情况下都需要多项式时间。

有兴趣的读者可以尝试方法 1 的实现。

**方法 2 - 增强的自平衡二分搜索树（AVL，RB 等）**：

在 BST 的每个节点上，维护以该节点为根的子树中的元素数量。 我们可以将节点用作简单二叉树的根，其左子节点是具有小于根的元素的自平衡 BST，右子节点是具有大于根的元素的自平衡 BST。 根元素始终保持**有效中位数**。

如果左右子树包含相同数量的元素，则根节点将保存左右子树根数据的平均值。 否则，根包含与具有更多元素的子树的根相同的数据。 处理完传入元素后，左右子树（BST）相差最大 1。

自平衡 BST 在管理 BST 的平衡因子方面成本很高。 但是，它们提供了我们不需要的排序数据。 我们只需要中位数。 下一种方法利用堆来跟踪中位数。

**方法 3 - 堆**：

与上述方法 2 中的平衡 BST 相似，我们可以在左侧使用最大堆表示小于**有效中位数**的元素，在右侧使用最小堆表示大于**有效中位数**的元素 。

处理传入的元素后，堆中的元素数量最大相差 1 个元素。 当两个堆包含相同数量的元素时，我们选择堆根数据的平均值作为**有效中位数**。 当堆不平衡时，我们从包含更多元素的堆根中选择**有效中位数**。

下面给出上述方法的实现。 有关构建这些堆的算法，请阅读突出显示的代码。

```

#include <iostream> 
using namespace std; 

// Heap capacity 
#define MAX_HEAP_SIZE (128) 
#define ARRAY_SIZE(a) sizeof(a)/sizeof(a[0]) 

//// Utility functions 

// exchange a and b 
inline
void Exch(int &a, int &b) 
{ 
    int aux = a; 
    a = b; 
    b = aux; 
} 

// Greater and Smaller are used as comparators 
bool Greater(int a, int b) 
{ 
    return a > b; 
} 

bool Smaller(int a, int b) 
{ 
    return a < b; 
} 

int Average(int a, int b) 
{ 
    return (a + b) / 2; 
} 

// Signum function 
// = 0  if a == b  - heaps are balanced 
// = -1 if a < b   - left contains less elements than right 
// = 1  if a > b   - left contains more elements than right 
int Signum(int a, int b) 
{ 
    if( a == b ) 
        return 0; 

    return a < b ? -1 : 1; 
} 

// Heap implementation 
// The functionality is embedded into 
// Heap abstract class to avoid code duplication 
class Heap 
{ 
public: 
    // Initializes heap array and comparator required 
    // in heapification 
    Heap(int *b, bool (*c)(int, int)) : A(b), comp(c) 
    { 
        heapSize = -1; 
    } 

    // Frees up dynamic memory 
    virtual ~Heap() 
    { 
        if( A ) 
        { 
            delete[] A; 
        } 
    } 

    // We need only these four interfaces of Heap ADT 
    virtual bool Insert(int e) = 0; 
    virtual int  GetTop() = 0; 
    virtual int  ExtractTop() = 0; 
    virtual int  GetCount() = 0; 

protected: 

    // We are also using location 0 of array 
    int left(int i) 
    { 
        return 2 * i + 1; 
    } 

    int right(int i) 
    { 
        return 2 * (i + 1); 
    } 

    int parent(int i) 
    { 
        if( i <= 0 ) 
        { 
            return -1; 
        } 

        return (i - 1)/2; 
    } 

    // Heap array 
    int   *A; 
    // Comparator 
    bool  (*comp)(int, int); 
    // Heap size 
    int   heapSize; 

    // Returns top element of heap data structure 
    int top(void) 
    { 
        int max = -1; 

        if( heapSize >= 0 ) 
        { 
            max = A[0]; 
        } 

        return max; 
    } 

    // Returns number of elements in heap 
    int count() 
    { 
        return heapSize + 1; 
    } 

    // Heapification 
    // Note that, for the current median tracing problem 
    // we need to heapify only towards root, always 
    void heapify(int i) 
    { 
        int p = parent(i); 

        // comp - differentiate MaxHeap and MinHeap 
        // percolates up 
        if( p >= 0 && comp(A[i], A[p]) ) 
        { 
            Exch(A[i], A[p]); 
            heapify(p); 
        } 
    } 

    // Deletes root of heap 
    int deleteTop() 
    { 
        int del = -1; 

        if( heapSize > -1) 
        { 
            del = A[0]; 

            Exch(A[0], A[heapSize]); 
            heapSize--; 
            heapify(parent(heapSize+1)); 
        } 

        return del; 
    } 

    // Helper to insert key into Heap 
    bool insertHelper(int key) 
    { 
        bool ret = false; 

        if( heapSize < MAX_HEAP_SIZE ) 
        { 
            ret = true; 
            heapSize++; 
            A[heapSize] = key; 
            heapify(heapSize); 
        } 

        return ret; 
    } 
}; 

// Specilization of Heap to define MaxHeap 
class MaxHeap : public Heap 
{ 
private: 

public: 
    MaxHeap() : Heap(new int[MAX_HEAP_SIZE], &Greater)  {  } 

    ~MaxHeap()  { } 

    // Wrapper to return root of Max Heap 
    int GetTop() 
    { 
        return top(); 
    } 

    // Wrapper to delete and return root of Max Heap 
    int ExtractTop() 
    { 
        return deleteTop(); 
    } 

    // Wrapper to return # elements of Max Heap 
    int  GetCount() 
    { 
        return count(); 
    } 

    // Wrapper to insert into Max Heap 
    bool Insert(int key) 
    { 
        return insertHelper(key); 
    } 
}; 

// Specilization of Heap to define MinHeap 
class MinHeap : public Heap 
{ 
private: 

public: 

    MinHeap() : Heap(new int[MAX_HEAP_SIZE], &Smaller) { } 

    ~MinHeap() { } 

    // Wrapper to return root of Min Heap 
    int GetTop() 
    { 
        return top(); 
    } 

    // Wrapper to delete and return root of Min Heap 
    int ExtractTop() 
    { 
        return deleteTop(); 
    } 

    // Wrapper to return # elements of Min Heap 
    int  GetCount() 
    { 
        return count(); 
    } 

    // Wrapper to insert into Min Heap 
    bool Insert(int key) 
    { 
        return insertHelper(key); 
    } 
}; 

// Function implementing algorithm to find median so far. 
int getMedian(int e, int &m, Heap &l, Heap &r) 
{ 
    // Are heaps balanced? If yes, sig will be 0 
    int sig = Signum(l.GetCount(), r.GetCount()); 
    switch(sig) 
    { 
    case 1: // There are more elements in left (max) heap 

        if( e < m ) // current element fits in left (max) heap 
        { 
            // Remore top element from left heap and 
            // insert into right heap 
            r.Insert(l.ExtractTop()); 

            // current element fits in left (max) heap 
            l.Insert(e); 
        } 
        else
        { 
            // current element fits in right (min) heap 
            r.Insert(e); 
        } 

        // Both heaps are balanced 
        m = Average(l.GetTop(), r.GetTop()); 

        break; 

    case 0: // The left and right heaps contain same number of elements 

        if( e < m ) // current element fits in left (max) heap 
        { 
            l.Insert(e); 
            m = l.GetTop(); 
        } 
        else
        { 
            // current element fits in right (min) heap 
            r.Insert(e); 
            m = r.GetTop(); 
        } 

        break; 

    case -1: // There are more elements in right (min) heap 

        if( e < m ) // current element fits in left (max) heap 
        { 
            l.Insert(e); 
        } 
        else
        { 
            // Remove top element from right heap and 
            // insert into left heap 
            l.Insert(r.ExtractTop()); 

            // current element fits in right (min) heap 
            r.Insert(e); 
        } 

        // Both heaps are balanced 
        m = Average(l.GetTop(), r.GetTop()); 

        break; 
    } 

    // No need to return, m already updated 
    return m; 
} 

void printMedian(int A[], int size) 
{ 
    int m = 0; // effective median 
    Heap *left  = new MaxHeap(); 
    Heap *right = new MinHeap(); 

    for(int i = 0; i < size; i++) 
    { 
        m = getMedian(A[i], m, *left, *right); 

        cout << m << endl; 
    } 

    // C++ more flexible, ensure no leaks 
    delete left; 
    delete right; 
} 
// Driver code 
int main() 
{ 
    int A[] = {5, 15, 1, 3, 2, 8, 7, 9, 10, 6, 11, 4}; 
    int size = ARRAY_SIZE(A); 

    // In lieu of A, we can also use data read from a stream 
    printMedian(A, size); 

    return 0; 
} 

```

**时间复杂度**：如果我们省略读取流的方式，则中位数查找的复杂度为`O(N log N)`，因为我们需要读取流 ，以及由于堆的插入/删除。

乍一看，上面的代码可能看起来很复杂。 如果仔细阅读代码，这是简单的算法。

[**使用 STL**](https://www.geeksforgeeks.org/median-of-stream-of-running-integers-using-stl/) 的运行整数流的中位数。


