# 二分搜索法使用 pthread

> 原文:[https://www.geeksforgeeks.org/binary-search-using-pthread/](https://www.geeksforgeeks.org/binary-search-using-pthread/)

**二分搜索法**是一种在排序的数组或列表中搜索的流行方法。它只是将列表分成两半，并丢弃拥有密钥概率为零的那一半。在划分时，我们检查键的中点，如果键小于中点，则使用下半部分，如果键大于中点，则使用上半部分。二分搜索法的时间复杂度为 0(对数(n))。

二分搜索法也可以使用**多线程**来实现，我们通过为每个线程提供一部分列表来搜索密钥，从而利用处理器的内核。

线程数量取决于处理器的内核数量，最好为每个内核创建一个线程。

示例:

```
Input :  list = 1, 5, 7, 10, 12, 14, 15, 18, 20, 22, 25, 27, 30, 64, 110, 220
         key = 7
Output : 7 found in list

Input :  list = 1, 5, 7, 10, 12, 14, 15, 18, 20, 22, 25, 27, 30, 64, 110, 220
         key = 111
Output : 111 not found in list

```

**注意–**建议在基于 Linux 的系统中执行程序。
使用以下代码在 linux 中编译:

```
g++ -pthread program_name.cpp

```

```
// CPP Program to perform binary search using pthreads
#include <iostream>
using namespace std;

// size of array
#define MAX 16

// maximum number of threads
#define MAX_THREAD 4

// array to be searched
int a[] = { 1, 5, 7, 10, 12, 14, 15, 18, 20, 22, 25, 27, 30, 64, 110, 220 };

// key that needs to be searched
int key = 110;
bool found = false;
int part = 0;

void* binary_search(void* arg)
{

    // Each thread checks 1/4 of the array for the key
    int thread_part = part++;
    int mid;

    int low = thread_part * (MAX / 4);
    int high = (thread_part + 1) * (MAX / 4);

    // search for the key until low < high
    // or key is found in any portion of array
    while (low < high && !found)  {

        // normal iterative binary search algorithm
        mid = (high - low) / 2 + low;

        if (a[mid] == key)  {
            found = true;
            break;
        }

        else if (a[mid] > key)
            high = mid - 1;
        else
            low = mid + 1;
    }
}

// Driver Code
int main()
{
    pthread_t threads[MAX_THREAD];

    for (int i = 0; i < MAX_THREAD; i++)
        pthread_create(&threads[i], NULL, binary_search, (void*)NULL);

    for (int i = 0; i < MAX_THREAD; i++)
        pthread_join(threads[i], NULL);

    // key found in array
    if (found)
        cout << key << " found in array" << endl;

    // key not found in array
    else
        cout << key << " not found in array" << endl;

    return 0;
}
```

输出:

```
110 found in array

```