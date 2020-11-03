# 双重哈希

> 原文：[https://www.geeksforgeeks.org/double-hashing/](https://www.geeksforgeeks.org/double-hashing/)

**双散列**是[**开放式**哈希表](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)中的冲突解决技术。 双重哈希使用在冲突发生时对密钥应用第二个哈希函数的想法。

> 可以使用以下方式完成双哈希处理：
>
> `(hash1(key) + i * hash2(key)) % TABLE_SIZE`
>
> 这里的`hash1()`和`hash2()`是哈希函数，而`TABLE_SIZE`是哈希表的大小。
>
> （发生碰撞时，我们通过增加`i`来重复）

第一个哈希函数通常是`hash1(key) = key % TABLE_SIZE`

流行的第二个哈希函数是： `hash2(key) = PRIME – (key % PRIME)`，其中`PRIME`是小于`TABLE_SIZE`的质数。

一个好的第二个哈希函数是：

*   绝对不能为零

*   必须确保可以探测所有细胞

![](img/c6a37eaf7e93d2178700f05f33f0a26f.png)

```
// CPP program to implement double hashing
#include <bits/stdc++.h>
using namespace std;
// Hash table size
#define TABLE_SIZE 13
// Used in second hash function.
#define PRIME 7
class DoubleHash {
// Pointer to an array containing buckets
int * hashTable;
int curr_size;
public :
// function to check if hash table is full
bool isFull()
{
// if hash size reaches maximum size
return (curr_size == TABLE_SIZE);
}
// function to calculate first hash
int hash1( int key)
{
return (key % TABLE_SIZE);
}
// function to calculate second hash
int hash2( int key)
{
return (PRIME - (key % PRIME));
}
DoubleHash()
{
]
hashTable = new int [TABLE_SIZE];
curr_size = 0;
for ( int i = 0; i < TABLE_SIZE; i++)
hashTable[i] = -1;
}
// function to insert key into hash table
void insertHash( int key)
{
// if hash table is full
if (isFull())
return ;
）
// get index from first hash
int index = hash1(key);
// if collision occurs
if (hashTable[index] != -1) {
// get index2 from second hash
int index2 = hash2(key);
int i = 1;
while (1) {
// get newIndex
int newIndex = (index + i * index2) % TABLE_SIZE;
// if no collision occurs, store
// the key
if (hashTable[newIndex] == -1) {
hashTable[newIndex] = key;
break ;
}
i++;
}
}
[
// if no collision occurs
else
hashTable[index] = key;
curr_size++;
}
// function to search key in hash table
void search( int key)
{
int index1 = hash1(key);
int index2 = hash2(key);
int i = 0;
while (hashTable[(index1 + i * index2) % TABLE_SIZE] != key) {
if (hashTable[(index1 + i * index2) % TABLE_SIZE] == -1) {
cout << key << " does not exist" << endl;
return ;
}
i++;
}
cout << key << " found" << endl;
}
// function to display the hash table
void displayHash()
]
{
for ( int i = 0; i < TABLE_SIZE; i++) {
if (hashTable[i] != -1)
cout << i << " --> "
<< hashTable[i] << endl;
else
cout << i << endl;
}
}
};
// Driver's code
]
int main()
{
int a[] = { 19, 27, 36, 10, 64 };
int n = sizeof (a) / sizeof (a[0]);
// inserting keys into hash table
[HTG26 1] DoubleHash h;
for ( int i = 0; i < n; i++) {
h.insertHash(a[i]);
}
// searching some keys
h.search(36); // This key is present in hash table
h.search(100); // This key does not exist in hash table
// display the hash Table
h.displayHash();
return 0;
}
```

**Output:**

```
36 found
100 does not exist
0
1 --> 27
2
3
4
5 --> 10
6 --> 19
7
8
9
10 --> 36
11
12 --> 64

```



* * *

* * *



