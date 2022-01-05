# 使用二元提升技术的 N 元树中节点的第 k 个祖先

> 原文:[https://www . geesforgeks . org/kth-n 进制树中节点的祖先-使用二进制提升技术/](https://www.geeksforgeeks.org/kth-ancestor-of-a-node-in-an-n-ary-tree-using-binary-lifting-technique/)

给定一个 N 元树的顶点 **V** 和一个整数 **K** ，任务是打印树中给定顶点的 **K <sup>th</sup>** 祖先。如果不存在这样的祖先，那么打印 **-1** 。
**举例:**

> **输入:** K = 2，V = 4
> 
> ![](img/532fb70f0517a897d2597d0b550d775d.png)
> 
> **输出:**1
> T3】2<sup>nd</sup>T6】顶点 **4** 的父节点为 **1** 。
> **输入:** K = 3，V = 4
> 
> ![](img/532fb70f0517a897d2597d0b550d775d.png)
> 
> **输出:** -1

**方法:**思路是使用[二元提升技术](https://www.geeksforgeeks.org/lca-in-a-tree-using-binary-lifting-technique/)。这种技术基于这样一个事实，即每个整数都可以用二进制形式表示。通过预处理，可以计算出一个稀疏表**表【v】【I】**，该表存储了顶点 **v** 的 **2 <sup>和</sup>T9】父级，其中 **0 ≤ i ≤ log <sub>2</sub> N** 。该预处理需要 **O(NlogN)** 时间。
要找到顶点 **V** 的 **K <sup>th</sup>** 父项，让**K = b<sub>0</sub>b<sub>1</sub>b<sub>2</sub>…b<sub>n</sub>T34】成为二进制表示中的一个 **n** 比特数，让**p<sub>1</sub>T40】，** **p <sub>j</sub>** 是位值为 **1** 的指数，那么 **K** 可以表示为**K = 2<sup>p</sup>T60<sup>1</sup>T63+2<sup>p</sup>T66<sup>2</sup>T69】+2<sup>p</sup>T71 因此，要到达 **V** 的父级**K<sup>th</sup>T86，我们必须跳至**2<sup>PTH</sup>T92<sup>1</sup>T95**，**2<sup>PTH</sup>T100<sup>2</sup>T103**， **2 <sup>pth 这可以通过先前在 **O(logN)** 中计算的稀疏表来有效地完成。
以下是上述方法的实施:</sup>********** 

## C++

```
// CPP implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Table for storing 2^ith parent
int **table;

// To store the height of the tree
int height;

// initializing the table and
// the height of the tree
void initialize(int n)
{
    height = (int)ceil(log2(n));
    table = new int *[n + 1];
}

// Filling with -1 as initial
void preprocessing(int n)
{
    for (int i = 0; i < n + 1; i++)
    {
        table[i] = new int[height + 1];
        memset(table[i], -1, sizeof table[i]);
    }
}

// Calculating sparse table[][] dynamically
void calculateSparse(int u, int v)
{
    // Using the recurrence relation to
    // calculate the values of table[][]
    table[v][0] = u;
    for (int i = 1; i <= height; i++)
    {
        table[v][i] = table[table[v][i - 1]][i - 1];

        // If we go out of bounds of the tree
        if (table[v][i] == -1)
            break;
    }
}

// Function to return the Kth ancestor of V
int kthancestor(int V, int k)
{
    // Doing bitwise operation to
    // check the set bit
    for (int i = 0; i <= height; i++)
    {
        if (k & (1 << i))
        {
            V = table[V][i];
            if (V == -1)
                break;
        }
    }
    return V;
}

// Driver Code
int main()
{
    // Number of vertices
    int n = 6;

    // initializing
    initialize(n);

    // Pre-processing
    preprocessing(n);

    // Calculating ancestors of v
    calculateSparse(1, 2);
    calculateSparse(1, 3);
    calculateSparse(2, 4);
    calculateSparse(2, 5);
    calculateSparse(3, 6);

    int K = 2, V = 5;
    cout << kthancestor(V, K) << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GfG {

    // Table for storing 2^ith parent
    private static int table[][];

    // To store the height of the tree
    private static int height;

    // Private constructor for initializing
    // the table and the height of the tree
    private GfG(int n)
    {

        // log(n) with base 2
        height = (int)Math.ceil(Math.log10(n) / Math.log10(2));
        table = new int[n + 1][height + 1];
    }

    // Filling with -1 as initial
    private static void preprocessing()
    {
        for (int i = 0; i < table.length; i++) {
            Arrays.fill(table[i], -1);
        }
    }

    // Calculating sparse table[][] dynamically
    private static void calculateSparse(int u, int v)
    {

        // Using the recurrence relation to
        // calculate the values of table[][]
        table[v][0] = u;
        for (int i = 1; i <= height; i++) {
            table[v][i] = table[table[v][i - 1]][i - 1];

            // If we go out of bounds of the tree
            if (table[v][i] == -1)
                break;
        }
    }

    // Function to return the Kth ancestor of V
    private static int kthancestor(int V, int k)
    {

        // Doing bitwise operation to
        // check the set bit
        for (int i = 0; i <= height; i++) {
            if ((k & (1 << i)) != 0) {
                V = table[V][i];
                if (V == -1)
                    break;
            }
        }
        return V;
    }

    // Driver code
    public static void main(String args[])
    {
        // Number of vertices
        int n = 6;

        // Calling the constructor
        GfG obj = new GfG(n);

        // Pre-processing
        preprocessing();

        // Calculating ancestors of v
        calculateSparse(1, 2);
        calculateSparse(1, 3);
        calculateSparse(2, 4);
        calculateSparse(2, 5);
        calculateSparse(3, 6);

        int K = 2, V = 5;
        System.out.print(kthancestor(V, K));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

class GfG :

    # Private constructor for initializing
    # the table and the height of the tree
    def __init__(self, n):

        # log(n) with base 2
        # To store the height of the tree
        self.height = int(math.ceil(math.log10(n) / math.log10(2)))

        # Table for storing 2^ith parent
        self.table = [0] * (n + 1)

    # Filling with -1 as initial
    def preprocessing(self):
        i = 0
        while ( i < len(self.table)) :
            self.table[i] = [-1]*(self.height + 1)
            i = i + 1

    # Calculating sparse table[][] dynamically
    def calculateSparse(self, u, v):

        # Using the recurrence relation to
        # calculate the values of table[][]
        self.table[v][0] = u
        i = 1
        while ( i <= self.height) :
            self.table[v][i] = self.table[self.table[v][i - 1]][i - 1]

            # If we go out of bounds of the tree
            if (self.table[v][i] == -1):
                break
            i = i + 1

    # Function to return the Kth ancestor of V
    def kthancestor(self, V, k):
        i = 0

        # Doing bitwise operation to
        # check the set bit
        while ( i <= self.height) :
            if ((k & (1 << i)) != 0) :
                V = self.table[V][i]
                if (V == -1):
                    break
            i = i + 1

        return V

# Driver code

# Number of vertices
n = 6

# Calling the constructor
obj = GfG(n)

# Pre-processing
obj.preprocessing()

# Calculating ancestors of v
obj.calculateSparse(1, 2)
obj.calculateSparse(1, 3)
obj.calculateSparse(2, 4)
obj.calculateSparse(2, 5)
obj.calculateSparse(3, 6)

K = 2
V = 5
print(obj.kthancestor(V, K))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    class GfG
    {

        // Table for storing 2^ith parent
        private static int [,]table ;

        // To store the height of the tree
        private static int height;

        // Private constructor for initializing
        // the table and the height of the tree
        private GfG(int n)
        {

            // log(n) with base 2
            height = (int)Math.Ceiling(Math.Log10(n) / Math.Log10(2));
            table = new int[n + 1, height + 1];
        }

        // Filling with -1 as initial
        private static void preprocessing()
        {
            for (int i = 0; i < table.GetLength(0); i++)
            {
                for (int j = 0; j < table.GetLength(1); j++)
                {
                    table[i, j] = -1;
                }
            }
        }

        // Calculating sparse table[,] dynamically
        private static void calculateSparse(int u, int v)
        {

            // Using the recurrence relation to
            // calculate the values of table[,]
            table[v, 0] = u;
            for (int i = 1; i <= height; i++)
            {
                table[v, i] = table[table[v, i - 1], i - 1];

                // If we go out of bounds of the tree
                if (table[v, i] == -1)
                    break;
            }
        }

        // Function to return the Kth ancestor of V
        private static int kthancestor(int V, int k)
        {

            // Doing bitwise operation to
            // check the set bit
            for (int i = 0; i <= height; i++)
            {
                if ((k & (1 << i)) != 0)
                {
                    V = table[V, i];
                    if (V == -1)
                        break;
                }
            }
            return V;
        }

        // Driver code
        public static void Main()
        {
            // Number of vertices
            int n = 6;

            // Calling the constructor
            GfG obj = new GfG(n);

            // Pre-processing
            preprocessing();

            // Calculating ancestors of v
            calculateSparse(1, 2);
            calculateSparse(1, 3);
            calculateSparse(2, 4);
            calculateSparse(2, 5);
            calculateSparse(3, 6);

            int K = 2, V = 5;
            Console.Write(kthancestor(V, K));
        }
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Table for storing 2^ith parent
    let table;

    // To store the height of the tree
    let height;

    // initializing the table and
    // the height of the tree
    function initialize(n)
    {
        height = Math.ceil(Math.log2(n));
    }

    // Filling with -1 as initial
    function preprocessing()
    {
        table = new Array(n + 1);
        for (let i = 0; i < n + 1; i++) {
            table[i] = new Array(height + 1);
            for (let j = 0; j < height + 1; j++) {
                table[i][j] = -1;
            }
        }
    }

    // Calculating sparse table[][] dynamically
    function calculateSparse(u, v)
    {

        // Using the recurrence relation to
        // calculate the values of table[][]
        table[v][0] = u;
        for (let i = 1; i <= height; i++) {
            table[v][i] = table[table[v][i - 1]][i - 1];

            // If we go out of bounds of the tree
            if (table[v][i] == -1)
                break;
        }
    }

    // Function to return the Kth ancestor of V
    function kthancestor(V, k)
    {

        // Doing bitwise operation to
        // check the set bit
        for (let i = 0; i <= height; i++) {
            if ((k & (1 << i)) != 0) {
                V = table[V][i];
                if (V == -1)
                    break;
            }
        }
        return V;
    }

    // Number of vertices
    let n = 6;

    // Calling the constructor
    initialize(n);

    // Pre-processing
    preprocessing();

    // Calculating ancestors of v
    calculateSparse(1, 2);
    calculateSparse(1, 3);
    calculateSparse(2, 4);
    calculateSparse(2, 5);
    calculateSparse(3, 6);

    let K = 2, V = 5;
    document.write(kthancestor(V, K));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(NlogN)用于预处理，logN 用于寻找祖先。