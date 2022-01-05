# 共享内存中并发合并排序

> 原文:[https://www . geesforgeks . org/concurrent-merge-sort-in-shared-memory/](https://www.geeksforgeeks.org/concurrent-merge-sort-in-shared-memory/)

给定一个数字“n”和一个 n，使用**并发**合并排序对数字进行排序。(提示:尽量使用 shmget、shmat 系统调用)。
**第一部分:算法(如何？)**
递归做两个子进程，一个为左半，一个为右半。如果一个过程的数组中的元素数少于 5，执行[插入排序](https://www.geeksforgeeks.org/insertion-sort/)。然后，两个子代的父代合并结果并返回给父代，以此类推。但是如何让它同时发生呢？
**第二部分:逻辑(为什么？)**
解决这个问题的重要部分不是算法，而是解释操作系统和内核的概念。
为了实现并发排序，我们需要一种方法让两个进程同时在同一个数组上工作。为了让事情变得更简单，Linux 通过简单的应用编程接口端点提供了大量的系统调用。其中两个是， [**shmget()**](http://man7.org/linux/man-pages/man2/shmget.2.html) (用于共享内存分配)和 [**shmat()**](http://man7.org/linux/man-pages/man2/shmat.2.html) (用于共享内存操作)。我们在分叉的子进程之间创建一个共享内存空间。每个片段被分成左、右两个子片段进行排序，有趣的是它们同时工作！shmget()请求内核为两个进程分配一个[共享页面](https://en.wikipedia.org/wiki/Paging#Sharing)。
**为什么传统叉子()不起作用？**
答案在于 fork()实际做什么。从文档中，“fork()通过复制调用进程来创建一个新的进程”。子进程和父进程在不同的内存空间中运行。在 fork()时，两个内存空间具有相同的内容。由其中一个进程执行的内存写入、文件描述符(fd)更改等不会影响另一个进程。因此，我们需要一个共享内存段。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C program to implement concurrent merge sort
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

void insertionSort(int arr[], int n);
void merge(int a[], int l1, int h1, int h2);

void mergeSort(int a[], int l, int h)
{
    int i, len=(h-l+1);

    // Using insertion sort for small sized array
    if (len<=5)
    {
        insertionSort(a+l, len);
        return;
    }

    pid_t lpid,rpid;
    lpid = fork();
    if (lpid<0)
    {
        // Lchild proc not created
        perror("Left Child Proc. not created\n");
        _exit(-1);
    }
    else if (lpid==0)
    {
        mergeSort(a,l,l+len/2-1);
        _exit(0);
    }
    else
    {
        rpid = fork();
        if (rpid<0)
        {
            // Rchild proc not created
            perror("Right Child Proc. not created\n");
            _exit(-1);
        }
        else if(rpid==0)
        {
            mergeSort(a,l+len/2,h);
            _exit(0);
        }
    }

    int status;

    // Wait for child processes to finish
    waitpid(lpid, &status, 0);
    waitpid(rpid, &status, 0);

    // Merge the sorted subarrays
    merge(a, l, l+len/2-1, h);
}

/* Function to sort an array using insertion sort*/
void insertionSort(int arr[], int n)
{
   int i, key, j;
   for (i = 1; i < n; i++)
   {
       key = arr[i];
       j = i-1;

       /* Move elements of arr[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
       while (j >= 0 && arr[j] > key)
       {
           arr[j+1] = arr[j];
           j = j-1;
       }
       arr[j+1] = key;
   }
}

// Method to merge sorted subarrays
void merge(int a[], int l1, int h1, int h2)
{
    // We can directly copy  the sorted elements
    // in the final array, no need for a temporary
    // sorted array.
    int count=h2-l1+1;
    int sorted[count];
    int i=l1, k=h1+1, m=0;
    while (i<=h1 && k<=h2)
    {
        if (a[i]<a[k])
            sorted[m++]=a[i++];
        else if (a[k]<a[i])
            sorted[m++]=a[k++];
        else if (a[i]==a[k])
        {
            sorted[m++]=a[i++];
            sorted[m++]=a[k++];
        }
    }

    while (i<=h1)
        sorted[m++]=a[i++];

    while (k<=h2)
        sorted[m++]=a[k++];

    int arr_count = l1;
    for (i=0; i<count; i++,l1++)
        a[l1] = sorted[i];
}

// To check if array is actually sorted or not
void isSorted(int arr[], int len)
{
    if (len==1)
    {
        printf("Sorting Done Successfully\n");
        return;
    }

    int i;
    for (i=1; i<len; i++)
    {
        if (arr[i]<arr[i-1])
        {
            printf("Sorting Not Done\n");
            return;
        }
    }
    printf("Sorting Done Successfully\n");
    return;
}

// To fill randome values in array for testing
// purpose
void fillData(int a[], int len)
{
    // Create random arrays
    int i;
    for (i=0; i<len; i++)
        a[i] = rand();
    return;
}

// Driver code
int main()
{
    int shmid;
    key_t key = IPC_PRIVATE;
    int *shm_array;

    // Using fixed size array.  We can uncomment
    // below lines to take size from user
    int length = 128;

    /* printf("Enter No of elements of Array:");
    scanf("%d",&length); */

    // Calculate segment length
    size_t SHM_SIZE = sizeof(int)*length;

    // Create the segment.
    if ((shmid = shmget(key, SHM_SIZE, IPC_CREAT | 0666)) < 0)
    {
        perror("shmget");
        _exit(1);
    }

    // Now we attach the segment to our data space.
    if ((shm_array = shmat(shmid, NULL, 0)) == (int *) -1)
    {
        perror("shmat");
        _exit(1);
    }

    // Create a random array of given length
    srand(time(NULL));
    fillData(shm_array, length);

    // Sort the created array
    mergeSort(shm_array, 0, length-1);

    // Check if array is sorted or not
    isSorted(shm_array, length);

    /* Detach from the shared memory now that we are
       done using it. */
    if (shmdt(shm_array) == -1)
    {
        perror("shmdt");
        _exit(1);
    }

    /* Delete the shared memory segment. */
    if (shmctl(shmid, IPC_RMID, NULL) == -1)
    {
        perror("shmctl");
        _exit(1);
    }

    return 0;
}
```

输出:

```
Sorting Done Successfully
```

**性能提升？**
尝试对代码进行计时，并将其性能与传统的顺序代码进行比较。您会惊讶地知道顺序排序性能更好！
当比如说左子访问左数组时，该数组被加载到处理器的缓存中。现在，当访问右数组时(因为并发访问)，会出现高速缓存未命中，因为高速缓存被左段填满，然后右段被复制到高速缓存中。这种往复过程继续，它将性能降低到比顺序代码性能差的程度。
有办法通过控制代码的工作流程来减少缓存未命中。但是它们不能完全避免！
本文由**平克什·巴杰蒂亚**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。