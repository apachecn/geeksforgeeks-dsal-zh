# 在 C++中使用开放式寻址线性探测实现自己的哈希表

**先决条件–** [散列简介](https://www.geeksforgeeks.org/hashing-set-1-introduction/)和[用 Java 中的单独链接实现我们自己的散列表](https://www.geeksforgeeks.org/implementing-our-own-hash-table-with-separate-chaining-in-java/)

在开放式寻址中，所有元素都存储在哈希表本身中。 因此，表的大小在任何时候都必须大于或等于键的总数（请注意，如果需要，我们可以通过复制旧数据来增加表的大小）。

*   **插入（k）–** 继续探测，直到找到一个空插槽。 找到空插槽后，插入 k。

*   **搜索（k）–** 继续探测，直到插槽的密钥不等于 k 或到达空插槽为止。

*   **Delete（k）–** 删除操作很有趣。 如果我们只是删除一个键，则搜索可能会失败。 因此，已删除密钥的插槽特别标记为“已删除”。

在这里，为了标记已删除的节点，我们使用了**虚拟节点**，其键和值为-1。

插入可以在已删除的广告位中插入项目，但搜索不会在已删除的广告位中停止。

整个过程确保对于任何键，我们在哈希表的大小内获得一个整数位置以插入相应的值。

这样的过程很简单，用户将一个（键，值）对设置为输入，并根据哈希函数生成的值生成索引，以存储对应于特定键的值。 因此，每当我们需要获取与仅 O（1）的键相对应的值时。

![](img/62b1efaa86a55f91e638f1fd76d1a5d4.png)

**代码–**

```
#include<bits/stdc++.h>
using namespace std;
//template for generic type
template < typename K, typename V>
[
//Hashnode class
class HashNode
{
public :
V value;
K key;
//Constructor of hashnode
HashNode(K key, V value)
{
this ->value = value;
this ->key = key;
}
};
//template for generic type
template < typename K, typename V>
//Our own Hashmap class
[H TG50] HashMap
{
//hash element array
HashNode<K,V> **arr;
int capacity;
//current size
int size;
//dummy node
HashNode<K,V> *dummy;
public :
HashMap()
{
//Initial capacity of hash array
capacity = 20;
size=0;
arr = new HashNode<K,V>*[capacity];
//Initialise all elements of array as NULL
for ( int i=0 ; i < capacity ; i++)
arr[i] = NULL;
//dummy node with value and key -1
dummy = new HashNode<K,V>(-1, -1);
}
// This implements hash function to find index
// for a key
int hashCode(K key)
{
return key % capacity;
}
//Function to add key value pair
void insertNode(K key, V value)
{
HashNode<K,V> *temp = new HashNode<K,V>(key, value);
// Apply hash function to find index for given key
int hashIndex = hashCode(key);
]          //find next free space
while (arr[hashIndex] != NULL && arr[hashIndex]->key != key
&& arr[hashIndex]->key != -1)
{
hashIndex++;
hashIndex %= capacity;
}
//if new node to be inserted increase the current size
if (arr[hashIndex] == NULL || arr[hashIndex]->key == -1)
size++;
]
}
//Function to delete a key value pair
V deleteNode( int key)
{
// Apply hash function to find index for given key
int hashIndex = hashCode(key);
//finding the node with given key
while (arr[hashIndex] != NULL)
{
//if node found
if (arr[hashIndex]->key == key)
{
HashNode<K,V> *temp = arr[hashIndex];
HTG565]
//Insert dummy node here for further use
arr[hashIndex] = dummy;
// Reduce size
size--;
return temp->value;
}
hashIndex++;
hashIndex %= capacity;
}
//If not found return null
return NULL;
}
//Function to search the value for a given key
V get( int key)
{
// Apply hash function to find index for given key
int hashIndex = hashCode(key);
int counter=0;
//finding the node with given key
while (arr[hashIndex] != NULL)
{    int counter =0;
if (counter++>capacity)  [HTG25 6]
return NULL;
//if node found return its value
if (arr[hashIndex]->key == key)
return arr[hashIndex]->value;
hashIndex++;
hashIndex %= capacity;
}
//If not found return null
return NULL;
}
[
//Return current size
int sizeofMap()
{
return size;
}
//Return true if size is 0
bool ] isEmpty()
{
return size == 0;
[HT G307]
//Function to display the stored key value pairs
void display()
{
for ( int i=0 ; i<capacity ; i++)
{
if (arr[i] != NULL && arr[i]->key != -1)
cout << "key = " << arr[i]->key
<< "  value = " << arr[i]->value << endl;
}
}
};
//Driver method to test map class
int main()
{
HashMap< int , int > *h = new HashMap< int , int >;
h->insertNode(1,1);
h->insertNode(2,2);
h->insertNode(2,3);
[HTG3 62] h->display();
cout << h->sizeofMap() <<endl;
cout << h->deleteNode(2) << endl;
cout << h->sizeofMap() <<endl;
cout << h->isEmpty() << endl;
cout << h->get(2);
return 0;
}
]
```

**输出–**

```
key = 1 value = 1
key = 2 value = 3
2
3
1
0
0

```

本文由 **Chhavi** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

