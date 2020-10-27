# 具有双链表的哈希表链接

**先决条件–** [哈希简介](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，[使用单链接列表的哈希表](https://www.geeksforgeeks.org/c-program-hashing-chaining/) & [用 Java 中的单独链接实现我们自己的哈希表](https://www.geeksforgeeks.org/implementing-our-own-hash-table-with-separate-chaining-in-java/)

使用通过双向链接列表链接实现哈希表类似于使用单链接列表实现[哈希表。 唯一的区别是，链表的每个节点都具有下一个节点和上一个节点的地址。 这将加快从列表中添加和删除元素的过程，因此，时间复杂度将大大降低。
**例如**：](https://www.geeksforgeeks.org/c-program-hashing-chaining/)

> 如果我们有一个单链表：
> 
> ```
> 1->2->3->4
> 
> ```
> 
> 如果我们位于 3，并且需要将其删除，则需要将 2 与 4 链接起来，并且从 3 开始，由于 2 是单链接列表，因此无法访问 2。 因此，必须再次遍历列表，即 O（n），但是如果我们有双重链接的列表即
> 
> ```
> 1234
> ->->->
> ```
> 
> 2 和 4 可以从 3 访问，因此在 O（1）中可以删除 3。

下面是上述方法的实现：

```
// C++ implementation of Hashtable
// using doubly linked list
#include <bits/stdc++.h>
using namespace std;
const int tablesize = 25;
// declaration of node
struct hash_node {
[
int val, key;
hash_node* next;
hash_node* prev;
};
// hashmap's declaration
class HashMap {
public :
hash_node **hashtable, **top;
[
// constructor
HashMap()
{
// create a empty hashtable
hashtable = new hash_node*[tablesize];
top = new hash_node*[tablesize];
for ( int i = 0; i < tablesize; i++) {
hashtable[i] = NULL;
top[i] = NULL;
}
}
// destructor
~HashMap()
{
delete [] hashtable;
}
// hash function definition
int HashFunc( int key)
{
return key % tablesize;
}
// searching method
void find( int key)
{
// Applying hashFunc to find
// index for given key
int hash_val = HashFunc(key);
[HTG45 9]          bool flag = false ;
hash_node* entry = hashtable[hash_val];
[
// if hashtable at that index has some
// values stored
if (entry != NULL) {
while (entry != NULL) {
if (entry->key == key) {
flag = true ;
}
if (flag) {
cout << "Element found at key "
<< key << ": " ;
cout << entry->val << endl;
}
entry = entry->next;
}
}
if (!flag)
cout << "No Element found at key "
<< key << endl;
}
// removing an element
void remove ( int key) ]
{
// Applying hashFunc to find
// index for given key
int hash_val = HashFunc(key);
hash_node* entry = hashtable[hash_val];
if (entry->key != key || entry == NULL) {
cout << "Couldn't find any element at this key "
<< key << endl;
return ;
}
// if some values are present at that key &
// traversing the list and removing all values
while (entry != NULL) {
if (entry->next == NULL) {
if (entry->prev == NULL) {
hashtable[hash_val] = NULL;
top[hash_val] = NULL;
delete entry;
break ;
}
else {
top[hash_val] = entry->prev;
top[hash_val]->next = NULL;
delete entry;
entry = top[hash_val];
}
}
entry = entry->next;
}
cout << "Element was successfully removed at the key "
<< key << endl;
}
HTG576]
// inserting method
void add( int key, int value)
{
// Applying hashFunc to find
// index for given key
int hash_val = HashFunc(key);
hash_node* entry = hashtable[hash_val];
// if key has no value stored
if (entry == NULL) {
]              // creating new node
entry = new hash_node;
entry->val = value;
entry->key = key;
entry->next = NULL;
entry->prev = NULL;
hashtable[hash_val] = entry;
top[hash_val] = entry;
}
// if some values are present
else {
// traversing till the end of
// the list
while (entry != NULL)
entry = entry->next;
[
// creating the new node
entry = new hash_node;
[HTG63 5]              entry->val = value;
entry->key = key;
entry->next = NULL;
entry->prev = top[hash_val];
top[hash_val]->next = entry;
top[hash_val] = entry;
}
cout << "Value " << value << " was successfully"
" added at key " << key << endl;
}
};
// Driver Code
int main()
{
HashMap hash;
hash.add(4, 5);
hash.find(4);
hash. remove (4);
return 0;
}
```

**Output:**

```
Value 5 was successfully added at key 4
Element found at key 4: 5
Element was successfully removed at the key 4

```



* * *

* * *



