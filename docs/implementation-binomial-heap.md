# 二项式堆的实现

> 原文:[https://www.geeksforgeeks.org/implementation-binomial-heap/](https://www.geeksforgeeks.org/implementation-binomial-heap/)

在[之前的文章](https://www.geeksforgeeks.org/binomial-heap-2/)中，我们已经讨论了二项式堆的相关概念。
 **示例二项式堆:**

```

12------------10--------------------20
             /  \                 /  | \
           15    50             70  50  40
           |                  / |    |     
           30               80  85  65 
                            |
                           100
A Binomial Heap with 13 nodes. It is a collection of 3 
Binomial Trees of orders 0, 2 and 3 from left to right. 

    10--------------------20
   /  \                 /  | \
 15    50             70  50  40
 |                  / |    |     
 30               80  85  65 
                  |
                 100

```

本文讨论了二项式堆的实现。实现了以下功能:

1.  **插入(H，k):** 向二项式堆“H”插入一个键“k”。这个操作首先创建一个带有单个键“k”的二项式堆，然后调用 H 和新的二项式堆的并集。
2.  **getMin(H):**getMin()的一个简单方法是遍历二叉树的根列表并返回最小键。这个实现需要 O(Logn)时间。通过维护一个指向最小键根的指针，可以将其优化为 0(1)。
3.  **extractMin(H):** 该操作也使用 union()。我们首先调用 getMin()来找到最小键二叉树，然后移除该节点，并通过连接移除的最小节点的所有子树来创建一个新的二叉树堆。最后我们在 H 和新创建的二项式堆上调用 union()。此操作需要 0(Logn)时间。

```
// C++ program to implement different operations
// on Binomial Heap
#include<bits/stdc++.h>
using namespace std;

// A Binomial Tree node.
struct Node
{
    int data, degree;
    Node *child, *sibling, *parent;
};

Node* newNode(int key)
{
    Node *temp = new Node;
    temp->data = key;
    temp->degree = 0;
    temp->child = temp->parent = temp->sibling = NULL;
    return temp;
}

// This function merge two Binomial Trees.
Node* mergeBinomialTrees(Node *b1, Node *b2)
{
    // Make sure b1 is smaller
    if (b1->data > b2->data)
        swap(b1, b2);

    // We basically make larger valued tree
    // a child of smaller valued tree
    b2->parent = b1;
    b2->sibling = b1->child;
    b1->child = b2;
    b1->degree++;

    return b1;
}

// This function perform union operation on two
// binomial heap i.e. l1 & l2
list<Node*> unionBionomialHeap(list<Node*> l1,
                               list<Node*> l2)
{
    // _new to another binomial heap which contain
    // new heap after merging l1 & l2
    list<Node*> _new;
    list<Node*>::iterator it = l1.begin();
    list<Node*>::iterator ot = l2.begin();
    while (it!=l1.end() && ot!=l2.end())
    {
        // if D(l1) <= D(l2)
        if((*it)->degree <= (*ot)->degree)
        {
            _new.push_back(*it);
            it++;
        }
        // if D(l1) > D(l2)
        else
        {
            _new.push_back(*ot);
            ot++;
        }
    }

    // if there remains some elements in l1
    // binomial heap
    while (it != l1.end())
    {
        _new.push_back(*it);
        it++;
    }

    // if there remains some elements in l2
    // binomial heap
    while (ot!=l2.end())
    {
        _new.push_back(*ot);
        ot++;
    }
    return _new;
}

// adjust function rearranges the heap so that
// heap is in increasing order of degree and
// no two binomial trees have same degree in this heap
list<Node*> adjust(list<Node*> _heap)
{
    if (_heap.size() <= 1)
        return _heap;
    list<Node*> new_heap;
    list<Node*>::iterator it1,it2,it3;
    it1 = it2 = it3 = _heap.begin();

    if (_heap.size() == 2)
    {
        it2 = it1;
        it2++;
        it3 = _heap.end();
    }
    else
    {
        it2++;
        it3=it2;
        it3++;
    }
    while (it1 != _heap.end())
    {
        // if only one element remains to be processed
        if (it2 == _heap.end())
            it1++;

        // If D(it1) < D(it2) i.e. merging of Binomial
        // Tree pointed by it1 & it2 is not possible
        // then move next in heap
        else if ((*it1)->degree < (*it2)->degree)
        {
            it1++;
            it2++;
            if(it3!=_heap.end())
                it3++;
        }

        // if D(it1),D(it2) & D(it3) are same i.e.
        // degree of three consecutive Binomial Tree are same
        // in heap
        else if (it3!=_heap.end() &&
                (*it1)->degree == (*it2)->degree &&
                (*it1)->degree == (*it3)->degree)
        {
            it1++;
            it2++;
            it3++;
        }

        // if degree of two Binomial Tree are same in heap
        else if ((*it1)->degree == (*it2)->degree)
        {
            Node *temp;
            *it1 = mergeBinomialTrees(*it1,*it2);
            it2 = _heap.erase(it2);
            if(it3 != _heap.end())
                it3++;
        }
    }
    return _heap;
}

// inserting a Binomial Tree into binomial heap
list<Node*> insertATreeInHeap(list<Node*> _heap,
                              Node *tree)
{
    // creating a new heap i.e temp
    list<Node*> temp;

    // inserting Binomial Tree into heap
    temp.push_back(tree);

    // perform union operation to finally insert
    // Binomial Tree in original heap
    temp = unionBionomialHeap(_heap,temp);

    return adjust(temp);
}

// removing minimum key element from binomial heap
// this function take Binomial Tree as input and return
// binomial heap after
// removing head of that tree i.e. minimum element
list<Node*> removeMinFromTreeReturnBHeap(Node *tree)
{
    list<Node*> heap;
    Node *temp = tree->child;
    Node *lo;

    // making a binomial heap from Binomial Tree
    while (temp)
    {
        lo = temp;
        temp = temp->sibling;
        lo->sibling = NULL;
        heap.push_front(lo);
    }
    return heap;
}

// inserting a key into the binomial heap
list<Node*> insert(list<Node*> _head, int key)
{
    Node *temp = newNode(key);
    return insertATreeInHeap(_head,temp);
}

// return pointer of minimum value Node
// present in the binomial heap
Node* getMin(list<Node*> _heap)
{
    list<Node*>::iterator it = _heap.begin();
    Node *temp = *it;
    while (it != _heap.end())
    {
        if ((*it)->data < temp->data)
            temp = *it;
        it++;
    }
    return temp;
}

list<Node*> extractMin(list<Node*> _heap)
{
    list<Node*> new_heap,lo;
    Node *temp;

    // temp contains the pointer of minimum value
    // element in heap
    temp = getMin(_heap);
    list<Node*>::iterator it;
    it = _heap.begin();
    while (it != _heap.end())
    {
        if (*it != temp)
        {
            // inserting all Binomial Tree into new
            // binomial heap except the Binomial Tree
            // contains minimum element
            new_heap.push_back(*it);
        }
        it++;
    }
    lo = removeMinFromTreeReturnBHeap(temp);
    new_heap = unionBionomialHeap(new_heap,lo);
    new_heap = adjust(new_heap);
    return new_heap;
}

// print function for Binomial Tree
void printTree(Node *h)
{
    while (h)
    {
        cout << h->data << " ";
        printTree(h->child);
        h = h->sibling;
    }
}

// print function for binomial heap
void printHeap(list<Node*> _heap)
{
    list<Node*> ::iterator it;
    it = _heap.begin();
    while (it != _heap.end())
    {
        printTree(*it);
        it++;
    }
}

// Driver program to test above functions
int main()
{
    int ch,key;
    list<Node*> _heap;

    // Insert data in the heap
    _heap = insert(_heap,10);
    _heap = insert(_heap,20);
    _heap = insert(_heap,30);

    cout << "Heap elements after insertion:\n";
    printHeap(_heap);

    Node *temp = getMin(_heap);
    cout << "\nMinimum element of heap "
         << temp->data << "\n";

    // Delete minimum element of heap
    _heap = extractMin(_heap);
    cout << "Heap after deletion of minimum element\n";
    printHeap(_heap);

    return 0;
}
```

输出:

```
The heap is:
50 10 30 40 20 
After deleing 10, the heap is:
20 30 40 50 

```

本文由 **[【萨希尔·查布拉(akku)](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder)****阿伦·米塔尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。