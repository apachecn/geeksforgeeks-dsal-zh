# 使用 pthreads 对数组求和

> 原文:[https://www.geeksforgeeks.org/sum-array-using-pthreads/](https://www.geeksforgeeks.org/sum-array-using-pthreads/)

数组的和是一个小问题，我们必须通过遍历整个数组来添加数组中的每个元素。但是当元素的数量太大时，可能需要很多时间。但是这可以通过将阵列分成多个部分并同时求出每个部分的和来解决，即通过并行求出每个部分的和。

这可以通过使用处理器的每个内核的**多线程**来实现。在我们的例子中，每个核心将计算一个部分的和，最后我们将把所有部分的和相加，得到最终的和。通过这种方式，我们可以提高程序的性能以及利用处理器的内核。

最好每个内核使用一个线程。尽管为了更好地理解多线程，您可以创建任意多个线程。

示例:

```
Input :  1, 5, 7, 10, 12, 14, 15, 18, 20, 22, 25, 27, 30, 64, 110, 220
Output : sum is 600

Input :  10, 50, 70, 100, 120, 140, 150, 180, 200, 220, 250, 270, 300, 640, 110, 220
Output : sum is 3030

```

**注意–**建议在基于 Linux 的系统中执行程序。
使用以下代码在 linux 中编译:

```
g++ -pthread program_name.cpp

```

代码–

```
// CPP Program to find sum of array
#include <iostream>
#include <pthread.h>

// size of array
#define MAX 16

// maximum number of threads
#define MAX_THREAD 4

using namespace std;

int a[] = { 1, 5, 7, 10, 12, 14, 15, 18, 20, 22, 25, 27, 30, 64, 110, 220 };
int sum[4] = { 0 };
int part = 0;

void* sum_array(void* arg)
{

    // Each thread computes sum of 1/4th of array
    int thread_part = part++;

    for (int i = thread_part * (MAX / 4); i < (thread_part + 1) * (MAX / 4); i++)
        sum[thread_part] += a[i];
}

// Driver Code
int main()
{

    pthread_t threads[MAX_THREAD];

    // Creating 4 threads
    for (int i = 0; i < MAX_THREAD; i++)
        pthread_create(&threads[i], NULL, sum_array, (void*)NULL);

    // joining 4 threads i.e. waiting for all 4 threads to complete
    for (int i = 0; i < MAX_THREAD; i++)
        pthread_join(threads[i], NULL);

    // adding sum of all 4 parts
    int total_sum = 0;
    for (int i = 0; i < MAX_THREAD; i++)
        total_sum += sum[i];

    cout << "sum is " << total_sum << endl;

    return 0;
}
```

输出:

```
sum is 600

```