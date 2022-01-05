# 使用开放寻址实现哈希表的程序

> 原文:[https://www . geesforgeks . org/program-to-implement-hash-table-use-open-addressing/](https://www.geeksforgeeks.org/program-to-implement-hash-table-using-open-addressing/)

任务是设计一个通用的[哈希表数据结构](https://www.geeksforgeeks.org/hashing-data-structure/)，处理碰撞情况，支持**插入()**、**查找()、**和**删除()**功能。

**示例:**

> 假设操作是在成对的数组上执行的，{{1，5}、{2，15}、{3，20}、{4，7}}。并且容量阵列 20 被用作哈希表:
> 
> 1.  **插入(1，5** ):在哈希表的索引处(1%20 =1)分配对{1，5}。
> 2.  **插入(2，15** ):在哈希表的索引处(2%20 =2)分配对{2，15}。
> 3.  **插入(3，20** ):在哈希表的索引处(3%20 =3)分配对{3，20}。
> 4.  **插入(4，7** ):在哈希表的索引处(4%20 =4)分配对{4，7}。
> 5.  **Find(4):** 键 4 存储在索引处(4%20 = 4)。因此，打印哈希表索引 4 处的 7，因为它是键 4 的值。
> 6.  **删除(4):** 键 4 存储在索引处(4%20 = 4)。删除键 4 后，哈希表有键{1，2，3}。
> 7.  **查找(4):** 打印-1，**因为哈希表中不存在键 4。**

****方法:**给定的问题可以通过使用[模数散列函数](https://www.geeksforgeeks.org/what-are-hash-functions-and-how-to-choose-a-good-hash-function/)并使用一个[结构数组](https://www.geeksforgeeks.org/array-of-structures-vs-array-within-a-structure-in-c-and-cpp/)作为散列表来解决，其中每个数组元素将存储要被散列的 **{key，value}** 对。碰撞情况可通过[线性探测](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)、[开放寻址](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)处理。按照以下步骤解决问题:**

*   **定义一个节点，[结构](https://www.geeksforgeeks.org/structures-c/)表示**哈希码，**表示要哈希的键值对。**
*   **初始化类型为**的指针的[数组，比如 ***arr[]** 来存储所有键值对。](https://www.geeksforgeeks.org/pointer-array-array-pointer/)****
*   ****插入(键，值):**在哈希表中插入对**{键，值}** 。

    *   初始化一个**散列码**变量，比如说**温度**，值为**{键，值}。**
    *   使用[散列函数](https://www.geeksforgeeks.org/hashing-set-1-introduction/)找到可以存储密钥的索引，然后将索引存储在一个变量中，比如**散列**。
    *   如果**arr【HashIndex】**不为空或存在另一个**键**，则通过连续更新 **HashIndex** 为**HashIndex =(HashIndex+1)%容量来进行[线性探测](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)。**
    *   如果 **arr【哈希索引】**不为空，则通过将 **temp** 的地址分配给 **arr【哈希索引】来插入给定的节点。**** 
*   ****查找(键):**在哈希表中查找**键**的值。

    *   使用[哈希函数](https://www.geeksforgeeks.org/hashing-set-1-introduction/)找到**键**可能存在的索引，然后将该索引存储在一个变量中，比如**哈希索引**。
    *   如果 **arr【哈希索引】**包含密钥，**密钥**则返回其值。
    *   否则，通过将**哈希指数**连续更新为**哈希指数=(哈希指数+1)%容量，进行[线性探测](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)。**然后**，**如果找到**键**，则返回**键**在该**的值，然后返回**真**。**
    *   如果没有找到**键**，则返回代表没有找到的 **-1** 。否则，返回**键的值。**** 
*   ****删除(键):**从哈希表中删除**键**。

    *   使用[哈希函数](https://www.geeksforgeeks.org/hashing-set-1-introduction/)找到**键**可能存在的索引，然后将该索引存储在一个变量中，比如**哈希索引**。
    *   如果**arr【HashIndex**】包含密钥， **Key** 则通过将 **{-1，-1}** 分配给**arr【HashIndex】**进行删除，然后返回 **true** 。
    *   否则，通过将**哈希指数**连续更新为**哈希指数=(哈希指数+1)%容量，进行[线性探测](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)。**然后**、**如果找到**键**，则删除**键**在该**处的值，然后返回**真**。**
    *   如果没有找到**键**，则返回为假。** 

**以下是上述方法的实现:**

## **C**

```
// C program for the above approach
#include <stdio.h>
#include <stdlib.h>

struct HashNode {
    int key;
    int value;
};

const int capacity = 20;
int size = 0;

struct HashNode** arr;
struct HashNode* dummy;

// Function to add key value pair
void insert(int key, int V)
{

    struct HashNode* temp
        = (struct HashNode*)malloc(sizeof(struct HashNode));
    temp->key = key;
    temp->value = V;

    // Apply hash function to find
    // index for given key
    int hashIndex = key % capacity;

    // Find next free space
    while (arr[hashIndex] != NULL
           && arr[hashIndex]->key != key
           && arr[hashIndex]->key != -1) {
        hashIndex++;
        hashIndex %= capacity;
    }

    // If new node to be inserted
    // increase the current size
    if (arr[hashIndex] == NULL
        || arr[hashIndex]->key == -1)
        size++;

    arr[hashIndex] = temp;
}

// Function to delete a key value pair
int delete (int key)
{
    // Apply hash function to find
    // index for given key
    int hashIndex = key % capacity;

    // Finding the node with given
    // key
    while (arr[hashIndex] != NULL) {
        // if node found
        if (arr[hashIndex]->key == key) {
            // Insert dummy node here
            // for further use
            arr[hashIndex] = dummy;

            // Reduce size
            size--;

            // Return the value of the key
            return 1;
        }
        hashIndex++;
        hashIndex %= capacity;
    }

    // If not found return null
    return 0;
}

// Function to search the value
// for a given key
int find(int key)
{
    // Apply hash function to find
    // index for given key
    int hashIndex = (key % capacity);

    int counter = 0;

    // Find the node with given key
    while (arr[hashIndex] != NULL) {

        int counter = 0;
        // If counter is greater than
        // capacity
        if (counter++ > capacity)
            break;

        // If node found return its
        // value
        if (arr[hashIndex]->key == key)
            return arr[hashIndex]->value;

        hashIndex++;
        hashIndex %= capacity;
    }

    // If not found return
    // -1
    return -1;
}

// Driver Code
int main()
{
    // Space allocation
    arr = (struct HashNode**)malloc(sizeof(struct HashNode*)
                                    * capacity);
    // Assign NULL initially
    for (int i = 0; i < capacity; i++)
        arr[i] = NULL;

    dummy
        = (struct HashNode*)malloc(sizeof(struct HashNode));

    dummy->key = -1;
    dummy->value = -1;

    insert(1, 5);
    insert(2, 15);
    insert(3, 20);
    insert(4, 7);

    if (find(4) != -1)
        printf("Value of Key 4 = %d\n", find(4));
    else
        printf("Key 4 does not exists\n");

    if (delete (4))
        printf("Node value of key 4 is deleted "
               "successfully\n");
    else {
        printf("Key does not exists\n");
    }

    if (find(4) != -1)
        printf("Value of Key 4 = %d\n", find(4));
    else
        printf("Key 4 does not exists\n");
}
```

****Output**

```
Value of Key 4 = 7
Node value of key 4 is deleted successfully
Key 4 does not exists
```** 

*****时间复杂度:** O(容量)，每次操作*
***辅助空间:** O(容量)***