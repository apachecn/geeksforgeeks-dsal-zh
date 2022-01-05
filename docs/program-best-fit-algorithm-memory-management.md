# 内存管理中最佳匹配算法的程序

> 原文:[https://www . geesforgeks . org/program-best-fit-algorithm-memory-management/](https://www.geeksforgeeks.org/program-best-fit-algorithm-memory-management/)

前提条件:[分区分配方式](https://www.geeksforgeeks.org/partition-allocation-methods-in-memory-management/)

最佳匹配将进程分配给一个分区，该分区是可用空闲分区中最小的分区。

**示例:**

```
Input : blockSize[]   = {100, 500, 200, 300, 600};
        processSize[] = {212, 417, 112, 426};
Output:
Process No.    Process Size    Block no.
 1        212        4
 2        417        2
 3        112        3
 4        426        5

```

[![first-fit](img/91cd8d99abe0a241bafbc5b5ebfa8f08.png)](https://media.geeksforgeeks.org/wp-content/uploads/Page_replacement_all_three.jpg)

```
Implementation:
1- Input memory blocks and processes with sizes.
2- Initialize all memory blocks as free.
3- Start by picking each process and find the
   minimum block size that can be assigned to
   current process i.e., find min(bockSize[1], 
   blockSize[2],.....blockSize[n]) > 
   processSize[current], if found then assign 
   it to the current process.
5- If not then leave that process and keep checking
   the further processes.

```

下面是实现。

## C/C++

```
// C++ implementation of Best - Fit algorithm
#include<bits/stdc++.h>
using namespace std;

// Function to allocate memory to blocks as per Best fit
// algorithm
void bestFit(int blockSize[], int m, int processSize[], int n)
{
    // Stores block id of the block allocated to a
    // process
    int allocation[n];

    // Initially no block is assigned to any process
    memset(allocation, -1, sizeof(allocation));

    // pick each process and find suitable blocks
    // according to its size ad assign to it
    for (int i=0; i<n; i++)
    {
        // Find the best fit block for current process
        int bestIdx = -1;
        for (int j=0; j<m; j++)
        {
            if (blockSize[j] >= processSize[i])
            {
                if (bestIdx == -1)
                    bestIdx = j;
                else if (blockSize[bestIdx] > blockSize[j])
                    bestIdx = j;
            }
        }

        // If we could find a block for current process
        if (bestIdx != -1)
        {
            // allocate block j to p[i] process
            allocation[i] = bestIdx;

            // Reduce available memory in this block.
            blockSize[bestIdx] -= processSize[i];
        }
    }

    cout << "\nProcess No.\tProcess Size\tBlock no.\n";
    for (int i = 0; i < n; i++)
    {
        cout << "   " << i+1 << "\t\t" << processSize[i] << "\t\t";
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
    int m = sizeof(blockSize)/sizeof(blockSize[0]);
    int n = sizeof(processSize)/sizeof(processSize[0]);

    bestFit(blockSize, m, processSize, n);

    return 0 ;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of Best - Fit algorithm

public class GFG 
{
    // Method to allocate memory to blocks as per Best fit
    // algorithm
    static void bestFit(int blockSize[], int m, int processSize[], 
                                                     int n)
    {
        // Stores block id of the block allocated to a
        // process
        int allocation[] = new int[n];

        // Initially no block is assigned to any process
        for (int i = 0; i < allocation.length; i++)
            allocation[i] = -1;

     // pick each process and find suitable blocks
        // according to its size ad assign to it
        for (int i=0; i<n; i++)
        {
            // Find the best fit block for current process
            int bestIdx = -1;
            for (int j=0; j<m; j++)
            {
                if (blockSize[j] >= processSize[i])
                {
                    if (bestIdx == -1)
                        bestIdx = j;
                    else if (blockSize[bestIdx] > blockSize[j])
                        bestIdx = j;
                }
            }

            // If we could find a block for current process
            if (bestIdx != -1)
            {
                // allocate block j to p[i] process
                allocation[i] = bestIdx;

                // Reduce available memory in this block.
                blockSize[bestIdx] -= processSize[i];
            }
        }

        System.out.println("\nProcess No.\tProcess Size\tBlock no.");
        for (int i = 0; i < n; i++)
        {
            System.out.print("   " + (i+1) + "\t\t" + processSize[i] + "\t\t");
            if (allocation[i] != -1)
                System.out.print(allocation[i] + 1);
            else
                System.out.print("Not Allocated");
            System.out.println();
        }
    }

    // Driver Method
    public static void main(String[] args)
    {
         int blockSize[] = {100, 500, 200, 300, 600};
         int processSize[] = {212, 417, 112, 426};
         int m = blockSize.length;
         int n = processSize.length;

         bestFit(blockSize, m, processSize, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of Best - Fit algorithm 

# Function to allocate memory to blocks 
# as per Best fit algorithm 
def bestFit(blockSize, m, processSize, n):

    # Stores block id of the block 
    # allocated to a process 
    allocation = [-1] * n 

    # pick each process and find suitable 
    # blocks according to its size ad 
    # assign to it
    for i in range(n):

        # Find the best fit block for
        # current process 
        bestIdx = -1
        for j in range(m):
            if blockSize[j] >= processSize[i]:
                if bestIdx == -1: 
                    bestIdx = j 
                elif blockSize[bestIdx] > blockSize[j]: 
                    bestIdx = j

        # If we could find a block for 
        # current process 
        if bestIdx != -1:

            # allocate block j to p[i] process 
            allocation[i] = bestIdx 

            # Reduce available memory in this block. 
            blockSize[bestIdx] -= processSize[i]

    print("Process No. Process Size     Block no.")
    for i in range(n):
        print(i + 1, "         ", processSize[i], 
                                end = "         ") 
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

    bestFit(blockSize, m, processSize, n)

# This code is contributed by PranchalK
```

## C#

```
// C# implementation of Best - Fit algorithm
using System;

public class GFG {

    // Method to allocate memory to blocks
    // as per Best fit
    // algorithm
    static void bestFit(int []blockSize, int m,
                      int []processSize, int n)
    {

        // Stores block id of the block 
        // allocated to a process
        int []allocation = new int[n];

        // Initially no block is assigned to
        // any process
        for (int i = 0; i < allocation.Length; i++)
            allocation[i] = -1;

        // pick each process and find suitable
        // blocks according to its size ad
        // assign to it
        for (int i = 0; i < n; i++)
        {

            // Find the best fit block for
            // current process
            int bestIdx = -1;
            for (int j = 0; j < m; j++)
            {
                if (blockSize[j] >= processSize[i])
                {
                    if (bestIdx == -1)
                        bestIdx = j;
                    else if (blockSize[bestIdx]
                                   > blockSize[j])
                        bestIdx = j;
                }
            }

            // If we could find a block for
            // current process
            if (bestIdx != -1)
            {

                // allocate block j to p[i] 
                // process
                allocation[i] = bestIdx;

                // Reduce available memory in
                // this block.
                blockSize[bestIdx] -= processSize[i];
            }
        }

        Console.WriteLine("\nProcess No.\tProcess"
                            + " Size\tBlock no.");
        for (int i = 0; i < n; i++)
        {
            Console.Write(" " + (i+1) + "\t\t" 
                        + processSize[i] + "\t\t");

            if (allocation[i] != -1)
                Console.Write(allocation[i] + 1);
            else
                Console.Write("Not Allocated");

            Console.WriteLine();
        }
    }

    // Driver Method
    public static void Main()
    {
        int []blockSize = {100, 500, 200, 300, 600};
        int []processSize = {212, 417, 112, 426};
        int m = blockSize.Length;
        int n = processSize.Length;

        bestFit(blockSize, m, processSize, n);
    }
}

// This code is contributed by nitin mittal.
```

Output:

```
Process No.    Process Size    Block no.
 1        212        4
 2        417        2
 3        112        3
 4        426        5

```

**Best-Fit 真的是最好的吗？**
虽然最佳拟合最小化了空间浪费，但是它消耗了大量处理器时间来搜索接近所需大小的块。此外，在某些情况下，最佳拟合的性能可能比其他算法差。例如，见下面的练习。

示例:考虑来自给定顺序 300K、25K、125K 和 50K 的进程的请求。假设有两个大小为 150K 的可用内存块，后跟一个大小为 350K 的块。

**最佳匹配:**
从大小为 350K 的块中分配 300K。街区还剩 50 个。
从剩余的 50K 块中分配 25K。街区还剩 25K。
125K 从 150 K 区块分配。这个街区还剩下 25K。
即使有 25K + 25K 的可用空间，也无法分配 50K。

**首次匹配:**
300K 请求从 350K 块中分配，50K 被遗漏。
25K 从 150K 区块分配，125K 遗漏。
然后将 125K 和 50K 分配给剩余的遗漏分区。
所以，first fit 可以处理请求。

本文由 **[萨希尔·查布拉](https://www.facebook.com/sahil.chhabra.965)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。