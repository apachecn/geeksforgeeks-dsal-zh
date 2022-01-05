# 将前 N 个自然数的平方分成两组，其和的绝对差最小

> 原文:[https://www . geeksforgeeks . org/将第一个 n 个自然数的平方分成两个具有最小绝对和差的集合/](https://www.geeksforgeeks.org/split-squares-of-first-n-natural-numbers-into-two-sets-with-minimum-absolute-difference-of-their-sums/)

给定一个整数 **N** ，任务是将第一个 **N** ( *始终是 **8*** ) [自然数](https://www.geeksforgeeks.org/natural-numbers/)的倍数划分为两个集合，使得它们的子集和之差最小。将两个子集打印为所需答案。

**示例:**

> **输入:** N = 8
> **输出:**
> 0
> 1 16 36 49
> 4 9 25 64
> **说明:**前 N 个自然数的平方为{1，4，9，16，25，36，49，64}
> 子集{1，16，36，49}和{4，9，25，64}的和为 102。因此，它们的和之差为 0。
> 
> **输入:** N = 16
> **输出:**
> 0
> 1 16 36 49 81 144 196 225
> 4 9 25 64 100 121 169 256

**天真方法:**想法是[生成所有可能的子集对](https://www.geeksforgeeks.org/find-distinct-subsets-given-set/)将第一个 **N 个**自然数的平方分割在它们之间，并计算子集差和的子集。打印发现其和的差最小的子集对。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**为了优化上述方法，其思想是利用连续平方数的[和](https://www.geeksforgeeks.org/python-program-for-sum-of-squares-of-first-n-natural-numbers/)的数学性质。请注意，总是有可能将 **8 个连续的平方数**分成 **2 组**，使得它们的子集和差为 **0** 。

> **证明:**
> 8 个连续的平方数可以分成 2 个子集，其和之差为 0。
> 4 个连续的正方形编号可以表示为 k <sup>2</sup> 、(k + 1) <sup>2</sup> 、(k + 2) <sup>2</sup> 和(k + 3) <sup>2</sup> 。
> 
> 让我们取子集 A 中的第 1 个和第 4 个元素，因此
> A = k 的和<sup>2</sup>+(k+3)<sup>2</sup>
> <sup>= 2k<sup>2</sup>+6k+9</sup>
> 
> 让我们取子集 B 中的第二个和第三个元素，因此，
> B 之和=(k+1)<sup>2</sup>+(k+2)<sup>2</sup>
> <sup>= 2k<sup>2</sup>+6k+5
> 子集差= A 之和–B 之和= 4</sup>
> 
> 因此，4 个连续的平方数可以分成 2 个子集，它们的和之差为 4。
> 
> 现在，假设连续正方形的数组是 arr[] = {a1，a2，a3，a4，a5，a6，a7，a8}。
> 由上述性质可以写成:
> a1+a4 –( a2+a3)= 4、
> a5+A8–(a6+a7)= 4
> 
> 减去上面的等式:
> a1+a4–(a2+a3)–(a5+A8–(a6+a7))= 0
> 因此，(a1+a4+a6+a7)–(a2+a3+a5+A8)= 0
> 因此，8 个连续的平方数可以分成 2 个子集，其差值为 0。

按照以下步骤解决问题:

*   初始化一个变量来存储最小子集差，并声明为 **0** 。
*   初始化变量 **cnt** 以存储大小为 8 的块数并将 **N** 除以 8 并将其存储在变量 **cnt** 中。
*   初始化一个字符串**分区**并通过连接字符串**“abbaab”**、 **cnt** 的次数来存储 **N** 元素的分区模式，其中**“abbaab”**表示大小为 **8** 的子数组中的每个元素必须进入的子集。
*   初始化 2 个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **A** 和 **B** 来存储子集 **A** 和子集 **B** 的元素。
*   [在范围**【0，N–1】**上迭代一个循环](https://www.geeksforgeeks.org/for-each-loop-in-java/)，如果**模式【I】**为**【A】**，则在向量 **A** 中插入 **(i + 1) <sup>2</sup>** 。否则，在向量 **B** 中插入 **(i + 1) <sup>2</sup>** 。
*   完成上述步骤后，打印最小子集差，矢量 **A** 和矢量 **B** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to partition squares of N
// natural number in two subset
void minimumSubsetDifference(int N)
{
    // Store the count of blocks of size 8
    int blockOfSize8 = N / 8;

    // Partition of block of 8 element
    string str = "ABBABAAB";

    // Store the minimum subset difference
    int subsetDifference = 0;

    // Partition of N elements to minimize
    // their subset sum difference
    string partition = "";
    while (blockOfSize8--) {
        partition += str;
    }

    // Store elements of subset A and B
    vector<int> A, B;

    for (int i = 0; i < N; i++) {

        // If element is of type A
        if (partition[i] == 'A') {
            A.push_back((i + 1) * (i + 1));
        }

        // If the element is of type B
        else {
            B.push_back((i + 1) * (i + 1));
        }
    }

    // Print the minimum subset difference
    cout << subsetDifference << "\n";

    // Print the first subset
    for (int i = 0; i < A.size(); i++)
        cout << A[i] << " ";

    cout << "\n";

    // Print the second subset
    for (int i = 0; i < B.size(); i++)
        cout << B[i] << " ";
}

// Driver Code
int main()
{
    int N = 8;

    // Function Call
    minimumSubsetDifference(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to partition squares of N
// natural number in two subset
static void minimumSubsetDifference(int N)
{

    // Store the count of blocks of size 8
    int blockOfSize8 = N / 8;

    // Partition of block of 8 element
    String str = "ABBABAAB";

    // Store the minimum subset difference
    int subsetDifference = 0;

    // Partition of N elements to minimize
    // their subset sum difference
    String partition = "";
    while (blockOfSize8-- > 0)
    {
        partition += str;
    }

    // Store elements of subset A and B
    int A[] = new int[N];
    int B[] = new int[N];
    int x = 0, y = 0;

    for(int i = 0; i < N; i++)
    {

        // If element is of type A
        if (partition.charAt(i) == 'A')
        {
            A[x++] = ((i + 1) * (i + 1));
        }

        // If the element is of type B
        else
        {
            B[y++] = ((i + 1) * (i + 1));
        }
    }

    // Print the minimum subset difference
    System.out.println(subsetDifference);

    // Print the first subset
    for(int i = 0; i < x; i++)
        System.out.print(A[i] + " ");

    System.out.println();

    // Print the second subset
    for(int i = 0; i < y; i++)
        System.out.print(B[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;

    // Function Call
    minimumSubsetDifference(N);
}
}

// This code is contributed by shailjapriya
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to partition squares of N
# natural number in two subset
def minimumSubsetDifference(N):

    # Store the count of blocks of size 8
    blockOfSize8 = N // 8

    # Partition of block of 8 element
    str = "ABBABAAB"

    # Store the minimum subset difference
    subsetDifference = 0

    # Partition of N elements to minimize
    # their subset sum difference
    partition = ""

    while blockOfSize8 != 0:
        partition = partition + str
        blockOfSize8 = blockOfSize8 - 1

    # Store elements of subset A and B
    A = []
    B = []

    for i in range(N):

        # If element is of type A
        if partition[i] == 'A':
            A.append((i + 1) * (i + 1))

        # If the element is of type B
        else:
            B.append((i + 1) * (i + 1))

    # Print the minimum subset difference
    print(subsetDifference)

    # Print the first subset
    for i in A:
        print(i, end = " ")
    print()

    # Print the second subset
    for i in B:
        print(i, end = " ")

# Driver Code
N = 8

# Function call
minimumSubsetDifference(N)

# This code is contributed by shailjapriya
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to partition squares of N
    // natural number in two subset
    static void minimumSubsetDifference(int N)
    {

        // Store the count of blocks of size 8
        int blockOfSize8 = N / 8;

        // Partition of block of 8 element
        string str = "ABBABAAB";

        // Store the minimum subset difference
        int subsetDifference = 0;

        // Partition of N elements to minimize
        // their subset sum difference
        string partition = "";
        while (blockOfSize8-- > 0)
        {
            partition += str;
        }

        // Store elements of subset A and B
        int []A = new int[N];
        int []B = new int[N];
        int x = 0, y = 0;

        for(int i = 0; i < N; i++)
        {

            // If element is of type A
            if (partition[i] == 'A')
            {
                A[x++] = ((i + 1) * (i + 1));
            }

            // If the element is of type B
            else
            {
                B[y++] = ((i + 1) * (i + 1));
            }
        }

        // Print the minimum subset difference
        Console.WriteLine(subsetDifference);

        // Print the first subset
        for(int i = 0; i < x; i++)
            Console.Write(A[i] + " ");

        Console.WriteLine();

        // Print the second subset
        for(int i = 0; i < y; i++)
            Console.Write(B[i] + " ");
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 8;

        // Function Call
        minimumSubsetDifference(N);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to partition squares of N
// natural number in two subset
function minimumSubsetDifference(N)
{

    // Store the count of blocks of size 8
    let blockOfSize8 = N / 8;

    // Partition of block of 8 element
    let str = "ABBABAAB";

    // Store the minimum subset difference
    let subsetDifference = 0;

    // Partition of N elements to minimize
    // their subset sum difference
    let partition = "";
    while (blockOfSize8-- > 0)
    {
        partition += str;
    }

    // Store elements of subset A and B
    let A = [];
    let B = [];
    let x = 0, y = 0;

    for(let i = 0; i < N; i++)
    {

        // If element is of type A
        if (partition[i] == 'A')
        {
            A[x++] = ((i + 1) * (i + 1));
        }

        // If the element is of type B
        else
        {
            B[y++] = ((i + 1) * (i + 1));
        }
    }

    // Print the minimum subset difference
    document.write(subsetDifference + "<br/>");

    // Print the first subset
    for(let i = 0; i < x; i++)
        document.write(A[i] + " ");

    document.write("<br/>");

    // Print the second subset
    for(let i = 0; i < y; i++)
        document.write(B[i] + " ");
}

// Driver code
    let N = 8;

    // Function Call
    minimumSubsetDifference(N);

   // This code is contributed by splevel62.
</script>
```

**Output**

```
0
1 16 36 49 
4 9 25 64
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)