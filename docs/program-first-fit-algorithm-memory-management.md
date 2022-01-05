# 内存管理中首次拟合算法的程序

> 原文:[https://www . geesforgeks . org/program-first-fit-algorithm-memory-management/](https://www.geeksforgeeks.org/program-first-fit-algorithm-memory-management/)

先决条件:[分区分配方法](https://www.geeksforgeeks.org/partition-allocation-methods-in-memory-management/)
在第一次拟合中，首先从主内存顶部分配足够的分区。
**例:**

```
Input : blockSize[]   = {100, 500, 200, 300, 600};
        processSize[] = {212, 417, 112, 426};
Output:
Process No.    Process Size    Block no.
   1               212            2
   2               417            5
   3               112            3
   4               426        Not Allocated
```

*   它的优点是它是最快的搜索，因为它只搜索第一个块，即足以分配一个进程。
*   即使可以分配，它也可能存在不允许进程占用空间的问题。考虑上面的例子，4 号进程(大小为 426)没有获得内存。然而，如果我们使用[最佳分配](https://www.geeksforgeeks.org/partition-allocation-methods-in-memory-management/)【块号 4(大小为 300)到进程 1，块号 2 到进程 2，块号 3 到进程 3，块号 5 到进程 4】来分配内存，则可以分配内存。

```
Implementation:
1- Input memory blocks with size and processes with size.
2- Initialize all memory blocks as free.
3- Start by picking each process and check if it can
   be assigned to current block. 
4- If size-of-process <= size-of-block if yes then 
   assign and check for next process.
5- If not then keep checking the further blocks.
```

![first-fit](img/91cd8d99abe0a241bafbc5b5ebfa8f08.png)

下面是上述步骤的实现。

## C++

```
// C++ implementation of First - Fit algorithm
#include<bits/stdc++.h>
using namespace std;

// Function to allocate memory to
// blocks as per First fit algorithm
void firstFit(int blockSize[], int m,
              int processSize[], int n)
{
    // Stores block id of the
    // block allocated to a process
    int allocation[n];

    // Initially no block is assigned to any process
    memset(allocation, -1, sizeof(allocation));

    // pick each process and find suitable blocks
    // according to its size ad assign to it
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (blockSize[j] >= processSize[i])
            {
                // allocate block j to p[i] process
                allocation[i] = j;

                // Reduce available memory in this block.
                blockSize[j] -= processSize[i];

                break;
            }
        }
    }

    cout << "\nProcess No.\tProcess Size\tBlock no.\n";
    for (int i = 0; i < n; i++)
    {
        cout << " " << i+1 << "\t\t"
             << processSize[i] << "\t\t";
        if (allocation[i] != -1)
            cout << allocation[i] + 1;
        else
            cout << "Not Allocated";
        cout << endl;
    }
}

// Driver code
int main()
{
    int blockSize[] = {100, 500, 200, 300, 600};
    int processSize[] = {212, 417, 112, 426};
    int m = sizeof(blockSize) / sizeof(blockSize[0]);
    int n = sizeof(processSize) / sizeof(processSize[0]);

    firstFit(blockSize, m, processSize, n);

    return 0 ;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of First - Fit algorithm

// Java implementation of First - Fit algorithm
class GFG
{
    // Method to allocate memory to
    // blocks as per First fit algorithm
    static void firstFit(int blockSize[], int m,
                         int processSize[], int n)
    {
        // Stores block id of the
        // block allocated to a process
        int allocation[] = new int[n];

        // Initially no block is assigned to any process
        for (int i = 0; i < allocation.length; i++)
            allocation[i] = -1;

        // pick each process and find suitable blocks
        // according to its size ad assign to it
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (blockSize[j] >= processSize[i])
                {
                    // allocate block j to p[i] process
                    allocation[i] = j;

                    // Reduce available memory in this block.
                    blockSize[j] -= processSize[i];

                    break;
                }
            }
        }

        System.out.println("\nProcess No.\tProcess Size\tBlock no.");
        for (int i = 0; i < n; i++)
        {
            System.out.print(" " + (i+1) + "\t\t" +
                             processSize[i] + "\t\t");
            if (allocation[i] != -1)
                System.out.print(allocation[i] + 1);
            else
                System.out.print("Not Allocated");
            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int blockSize[] = {100, 500, 200, 300, 600};
        int processSize[] = {212, 417, 112, 426};
        int m = blockSize.length;
        int n = processSize.length;

        firstFit(blockSize, m, processSize, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of First-Fit algorithm

# Function to allocate memory to
# blocks as per First fit algorithm
def firstFit(blockSize, m, processSize, n):

    # Stores block id of the
    # block allocated to a process
    allocation = [-1] * n

    # Initially no block is assigned to any process

    # pick each process and find suitable blocks
    # according to its size ad assign to it
    for i in range(n):
        for j in range(m):
            if blockSize[j] >= processSize[i]:

                # allocate block j to p[i] process
                allocation[i] = j

                # Reduce available memory in this block.
                blockSize[j] -= processSize[i]

                break

    print(" Process No. Process Size      Block no.")
    for i in range(n):
        print(" ", i + 1, "         ", processSize[i],
                          "         ", end = " ")
        if allocation[i] != -1:
            print(allocation[i] + 1)
        else:
            print("Not Allocated")

# Driver code
if __name__ == '__main__':
    blockSize = [100, 500, 200, 300, 600]
    processSize = [212, 417, 112, 426]
    m = len(blockSize)
    n = len(processSize)

    firstFit(blockSize, m, processSize, n)

# This code is contributed by PranchalK
```

## C#

```
// C# implementation of First - Fit algorithm
using System;

class GFG
{
    // Method to allocate memory to
    // blocks as per First fit algorithm
    static void firstFit(int []blockSize, int m,
                         int []processSize, int n)
    {
        // Stores block id of the block
        // allocated to a process
        int []allocation = new int[n];

        // Initially no block is assigned to any process
        for (int i = 0; i < allocation.Length; i++)
            allocation[i] = -1;

        // pick each process and find suitable blocks
        // according to its size ad assign to it
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (blockSize[j] >= processSize[i])
                {
                    // allocate block j to p[i] process
                    allocation[i] = j;

                    // Reduce available memory in this block.
                    blockSize[j] -= processSize[i];

                    break;
                }
            }
        }

    Console.WriteLine("\nProcess No.\tProcess Size\tBlock no.");
        for (int i = 0; i < n; i++)
        {
            Console.Write(" " + (i+1) + "\t\t" +
                          processSize[i] + "\t\t");
            if (allocation[i] != -1)
            Console.Write(allocation[i] + 1);
            else
                Console.Write("Not Allocated");
            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main()
    {
        int []blockSize = {100, 500, 200, 300, 600};
        int []processSize = {212, 417, 112, 426};
        int m = blockSize.Length;
        int n = processSize.Length;

        firstFit(blockSize, m, processSize, n);
    }
}

// This code is contributed by nitin mittal.
```

**输出:**

```
Process No.    Process Size    Block no.
   1        212        2
   2        417        5
   3        112        2
   4        426        Not Allocated
```

本文由 [**萨希尔·查布拉(akku)**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。