# 实现单链表的迭代器模式

> 原文：[https://www.geeksforgeeks.org/implementing-iterator-pattern-of-a-single-linked-list/](https://www.geeksforgeeks.org/implementing-iterator-pattern-of-a-single-linked-list/)



STL 是 C++ 的支柱之一。 它使工作变得更加轻松，尤其是当您专注于解决问题并且不想花时间去实现已经可用的东西时，这可以保证可靠的解决方案。 软件工程的关键方面之一是避免重新发明轮子。 为了可重用性应始终首选它。

尽管依赖库函数会直接影响我们的效率，但是如果对库的工作原理没有正确的了解，有时会失去我们一直在谈论的工程效率的含义。 错误选择的数据结构可能在将来的某个时候回来困扰我们。 解决方案很简单。 使用库方法，但要知道它如何在后台处理操作。

说够了！ 今天，我们将研究如何自己实现单链表的**迭代器模式**。 因此，这是链表的 STL 实现的样子：

```

#include <bits/stdc++.h> 
using namespace std; 

int main() 
{ 
    // creating  a list 
    vector<int> list; 

    // elements to be added at the end. 
    // in the above created list. 
    list.push_back(1); 
    list.push_back(2); 
    list.push_back(3); 

    // elements of list are retrieved through iterator. 
    for (vector<int>::iterator it = list.begin(); 
                                it != list.end(); ++it) 
        cout << *it << " "; 

    return 0; 
} 

```

输出量

```
1 2 3 

```

`cin`和`cout`的优点之一是它们不需要格式说明符来处理数据类型。 结合模板，使代码更清晰易读。 尽管我更喜欢 C++ 中的命名方法以大写字母开头，但是此实现遵循 STL 规则来模拟精确的方法调用集，即`push_back`，`begin`，`end`。

这是我们自己的`LinkedList`及其`Iterator`模式的实现：

```

// C++ program to implement Custom Linked List and 
// iterator pattern. 
#include <bits/stdc++.h> 
using namespace std; 

// Custom class to handle Linked List operations 
// Operations like push_back, push_front, pop_back, 
// pop_front, erase, size can be added here 
template <typename T> 
class LinkedList 
{ 
    // Forward declaration 
    class Node; 

public: 
    LinkedList<T>() noexcept 
    { 
        // caution: static members can't be 
        // initialized by initializer list 
        m_spRoot = nullptr; 
    } 

    // Forward declaration must be done 
    // in the same access scope 
    class Iterator; 

    // Root of LinkedList wrapped in Iterator type 
    Iterator begin() 
    { 
        return Iterator(m_spRoot); 
    } 

    // End of LInkedList wrapped in Iterator type 
    Iterator end() 
    { 
        return Iterator(nullptr); 
    } 

    // Adds data to the end of list 
    void push_back(T data); 

    void Traverse(); 

    // Iterator class can be used to 
    // sequentially access nodes of linked list 
    class Iterator 
    { 
    public: 
    Iterator() noexcept : 
        m_pCurrentNode (m_spRoot) { } 

    Iterator(const Node* pNode) noexcept : 
        m_pCurrentNode (pNode) { } 

        Iterator& operator=(Node* pNode) 
        { 
            this->m_pCurrentNode = pNode; 
            return *this; 
        } 

        // Prefix ++ overload 
        Iterator& operator++() 
        { 
            if (m_pCurrentNode) 
                m_pCurrentNode = m_pCurrentNode->pNext; 
            return *this; 
        } 

        // Postfix ++ overload 
        Iterator operator++(int) 
        { 
            Iterator iterator = *this; 
            ++*this; 
            return iterator; 
        } 

        bool operator!=(const Iterator& iterator) 
        { 
            return m_pCurrentNode != iterator.m_pCurrentNode; 
        } 

        int operator*() 
        { 
            return m_pCurrentNode->data; 
        } 

    private: 
        const Node* m_pCurrentNode; 
    }; 

private: 

    class Node 
    { 
        T data; 
        Node* pNext; 

        // LinkedList class methods need 
        // to access Node information 
        friend class LinkedList; 
    }; 

    // Create a new Node 
    Node* GetNode(T data) 
    { 
        Node* pNewNode = new Node; 
        pNewNode->data = data; 
        pNewNode->pNext = nullptr; 

        return pNewNode; 
    } 

    // Return by reference so that it can be used in 
    // left hand side of the assignment expression 
    Node*& GetRootNode() 
    { 
        return m_spRoot; 
    } 

    static Node* m_spRoot; 
}; 

template <typename T> 
/*static*/ typename LinkedList<T>::Node* LinkedList<T>::m_spRoot = nullptr; 

template <typename T> 
void LinkedList<T>::push_back(T data) 
{ 
    Node* pTemp = GetNode(data); 
    if (!GetRootNode()) 
    { 
        GetRootNode() = pTemp; 
    } 
    else
    { 
        Node* pCrawler = GetRootNode(); 
        while (pCrawler->pNext) 
        { 
            pCrawler = pCrawler->pNext; 
        } 

        pCrawler->pNext = pTemp; 
    } 
} 

template <typename T> 
void LinkedList<T>::Traverse() 
{ 
    Node* pCrawler = GetRootNode(); 

    while (pCrawler) 
    { 
        cout << pCrawler->data << " "; 
        pCrawler = pCrawler->pNext; 
    } 

    cout << endl; 
} 

//Driver program 
int main() 
{ 
    LinkedList<int> list; 

    // Add few items to the end of LinkedList 
    list.push_back(1); 
    list.push_back(2); 
    list.push_back(3); 

    cout << "Traversing LinkedList through method" << endl; 
    list.Traverse(); 

    cout << "Traversing LinkedList through Iterator" << endl; 
    for ( LinkedList<int>::Iterator iterator = list.begin(); 
            iterator != list.end(); iterator++) 
    { 
        cout << *iterator << " "; 
    } 

    cout << endl; 

    return 0; 
} 

```

输出：

```
Traversing LinkedList through method
1 2 3 
Traversing LinkedList through Iterator
1 2 3 

```

**练习**：当我们只有一个数据时，上述实现效果很好。 扩展此代码以处理包装在类中的数据集。

本文由 [**Aashish Barnwal**](https://about.me/aashishbarnwal) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

![design-pattern-img](img/14db468c0f00e6c64bfe591457d1b437.png)