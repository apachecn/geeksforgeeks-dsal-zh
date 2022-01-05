# 使用多线程程序给定数组的非重复元素

> 原文:[https://www . geeksforgeeks . org/使用多线程程序的给定数组的非重复元素/](https://www.geeksforgeeks.org/non-repeating-elements-of-a-given-array-using-multithreaded-program/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个代表[线程](https://www.geeksforgeeks.org/thread-in-operating-system/)计数的整数 **T** ，任务是使用[多线程](https://www.geeksforgeeks.org/multithreading-c-2/)找到所有非重复的数组元素。

**示例:**

> **输入:** arr[] = { 1，0，5，5，2}，T = 3
> **输出:** 0 1 2
> **说明:**
> 数组 arr[]中 0 的出现频率为 1。
> 数组 arr[]中 1 的频率为 1。
> 数组 arr[]中 2 的频率为 1。
> 因此，要求的输出为 0 1 2
> 
> **输入:** arr[] = { 1，1，5，5，2，4 }，T = 3
> **输出:** 2 4
> **说明:**
> 数组 arr[]中 2 的出现频率为 1。
> 数组 arr[]中 4 的频率为 1。
> 因此，要求的输出是 2 ^ 4

**方法:**思路是利用 **C++** 提供的 [pthread](https://www.geeksforgeeks.org/thread-functions-in-c-c/) 库，为并发进程流创建多个线程，在多线程程序中执行多个操作(pthread create、pthread join、lock 等)。按照以下步骤解决问题:

*   将数组分成 **T** 子数组，这样每个大小为 **N / T** 的子数组将在一个线程中执行。
*   初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp** ，来存储每个阵元的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   创建一个 [pthread_mutex_lock](https://www.geeksforgeeks.org/mutex-lock-for-linux-thread-synchronization/) ，比如 **lock1** ，以确保所有线程不会相互绊倒并损坏地图容器。
*   定义一个函数 **func()** 来执行线程的主体。该函数通常称为线程内核，在线程创建期间提供。
    *   使用 [pthread_mutex_lock()](https://www.geeksforgeeks.org/mutex-lock-for-linux-thread-synchronization/) 锁定当前线程，使其不与其他线程重叠
    *   遍历给定范围，作为数组**arr【】**中函数 **func()** 的参数，并增加遇到的数组元素的频率。
    *   使用函数 [pthread_mutex_unlock()](https://www.geeksforgeeks.org/mutex-lock-for-linux-thread-synchronization/) 释放当前线程。
*   初始化一个数组，比如**线程[]** ，类型为 [pthread_t](https://www.geeksforgeeks.org/thread-functions-in-c-c/) ，用于存储线程。
*   迭代范围**【0，T】**并通过调用 [pthread_create()](https://www.geeksforgeeks.org/thread-functions-in-c-c/) 函数创建一个线程，并将其存储在**线程【I】**中
*   当每个线程执行各自的任务时， **main()** 函数需要等待，直到每个线程完成它们的工作。
    *   使用 [pthread_join()](https://www.geeksforgeeks.org/thread-functions-in-c-c/) 函数等待，直到每个线程完成执行函数 **func()**
    *   迭代范围**【0，T】**，为每个**线程【I】**调用 [pthread_create()](https://www.geeksforgeeks.org/thread-functions-in-c-c/) 函数
*   最后，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **mp** 并打印只出现一次的元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
#include <pthread.h>
using namespace std;

// Structure of subarray
// of the array
struct range_info {

    // Stores start index
    // of the subarray
    int start;

    // Stores end index
    // of the subarray
    int end;

    // Stores pointer to the
    // first array element
    int* a;
};

// Declaring map, and mutex for
// thread exclusion(lock)
map<int, int> mp;
pthread_mutex_t lock1;

// Function performed by every thread to
// count the frequency of array elements
// in current subarray
void* func(void* arg)
{
    // Taking a lock so that threads
    // do not overlap each other
    pthread_mutex_lock(&lock1);

    // Initialize range_info
    // for each thread
    struct range_info* rptr
    = (struct range_info*)arg;

    // Thread is going through the array
    // to check and update the map
    for (int i = rptr->start;
            i <= rptr->end; i++) {

        // Stores iterator to the map        
        map<int, int>::iterator it;

        // Update it
        it = mp.find(rptr->a[i]);

        // If rptr->a[i] not found
        // in map mp
        if (it == mp.end()) {

            // Insert rptr->a[i] with
            // frequency 1
            mp.insert({ rptr->a[i], 1 });
        }
        else {

            // Update frequency of
            // current element
            it->second++;
        }
    }

    // Thread releases the lock
    pthread_mutex_unlock(&lock1);
    return NULL;
}

// Function to find the unique
// numbers in the array
void numbers_occuring_once(int arr[],
                        int N, int T)
{
    // Stores all threads
    pthread_t threads[T];

    // Stores start index of
    // first thread
    int spos = 0;

    // Stores last index
    // of the first thread
    int epos = spos + (N / T) - 1;

    // Traverse each thread
    for (int i = 0; i < T; i++) {

        // Initialize range_info for
        // current thread
        struct range_info* rptr
            = (struct range_info*)malloc(
                sizeof(struct range_info));

        // Update start index of
        // current subarray    
        rptr->start = spos;

        // Stores end index of
        // current subarray
        rptr->end = epos;

        // Update pointer to the first
        // element of the array
        rptr->a = arr;

        // creating each thread with
        // appropriate parameters
        int a
        = pthread_create(&threads[i], NULL,
                        func, (void*)(rptr));

        // updating the parameters
        // for the next thread
        spos = epos + 1;
        epos = spos + (N / T) - 1;
        if (i == T - 2) {
            epos = N - 1;
        }
    }

    // Waiting for threads to finish
    for (int i = 0; i < T; i++) {
        int rc
        = pthread_join(threads[i], NULL);
    }

    // Traverse the map
    for (auto it: mp) {

    // If frequency of current
    // element is 1                            
        if (it.second == 1) {

            // Print the element
            cout << it.first << " ";
        }
    }
}

// Drivers Code
int main()
{
    // initializing the mutex lock
    pthread_mutex_init(&lock1, NULL);
    int T = 3;
    int arr[] = { 1, 0, 5, 5, 2, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    numbers_occuring_once(arr, N, T);
}
```

**Output:** 

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*

**注意:**建议在基于 Linux 的系统中使用以下命令执行程序:

> g++ -pthread program_name.cpp