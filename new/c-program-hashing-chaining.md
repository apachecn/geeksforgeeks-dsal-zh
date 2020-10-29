# 用于通过链接进行哈希处理的 C++ 程序

> 原文：[https://www.geeksforgeeks.org/c-program-hashing-chaining/](https://www.geeksforgeeks.org/c-program-hashing-chaining/)

在[散列](http://www.geeksforgeeks.org/hashing-data-structure/)中，存在一个散列函数，可将键映射到某些值。 但是这些哈希函数可能会导致将两个或更多键映射到相同值的冲突。 **链哈希**避免了冲突。 这个想法是使哈希表的每个单元指向具有相同哈希函数值的记录的链接列表。

让我们创建一个哈希函数，使我们的哈希表具有`N`个存储桶。

要将节点插入哈希表，我们需要找到给定键的哈希索引。 并且可以使用哈希函数进行计算。

示例：`hashIndex = key % noOfBuckets`

**插入**：移至对应于上述计算得出的哈希索引的存储桶，并将新节点插入列表的末尾。

**删除**：要从哈希表中删除节点，请计算密钥的哈希索引，移动到与计算出的哈希索引相对应的存储桶中，在当前存储桶中搜索列表以查找并删除节点 给定密钥（如果找到）。

![](img/9f7240401363f22b94eb01c1c94738d1.png)

请参考[哈希 | 系列 2（单独链接）](https://www.geeksforgeeks.org/hashing-set-2-separate-chaining/)以获得详细信息。

我们在 C++ 中使用[列表](https://www.geeksforgeeks.org/list-cpp-stl/)，该列表在内部实现为链接列表（更快的插入和删除）。

```
// CPP program to implement hashing with chaining
#include<bits/stdc++.h>
using namespace std;
class Hash
{
int BUCKET;    // No. of buckets
[
// Pointer to an array containing buckets
list< int > *table;
public :
Hash( int V);  // Constructor
// inserts a key into hash table
void insertItem( int x);
// deletes a key from hash table
void deleteItem( int key);
// hash function to map values to key
int hashFunction( int x) {
return (x % BUCKET);
} [HTG24 6]
void displayHash();
};
Hash::Hash( int b)
{
this ->BUCKET = b;
table = new list< int >[BUCKET];
}
void Hash::insertItem( int key)
{
int index = hashFunction(key);
table[index].push_back(key);
}
void Hash::deleteItem( int key)
{
// get the hash index of key
int index = hashFunction(key);
// find the key in (inex)th list
list < int > :: iterator i;
for [ (i = table[index].begin();
i != table[index].end(); i++) {
if (*i == key)
break ;
}
// if key is found in hash table, remove it
if (i != table[index].end())
table[index].erase(i); ]
}
// function to display hash table
void Hash::displayHash() {
for ( int i = 0; i < BUCKET; i++) {
cout << i;
for ( auto x : table[i])
cout << " --> " << x;
cout << endl;
}
}
// Driver program
int main()
{
[HTG3 41]    // array that contains keys to be mapped
int a[] = {15, 11, 27, 8, 12};
int n = sizeof (a)/ sizeof (a[0]);
// insert the keys into the hash table
Hash h(7);   // 7 is count of buckets in
// hash table
]
for ( int i = 0; i < n; i++)
h.insertItem(a[i]);
[
// delete 12 from hash table
h.deleteItem(12);
// display the Hash table
h.displayHash();
return 0;
}
```

**Output:**

```
0
1 --> 15 --> 8
2
3
4 --> 11
5
6 --> 27

```



* * *

* * *



