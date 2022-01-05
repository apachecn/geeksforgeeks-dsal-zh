# 计算所有子阵列的 GCD 之和

> 原文:[https://www . geeksforgeeks . org/计算所有子阵列的 gcd 总和/](https://www.geeksforgeeks.org/calculate-the-sum-of-gcd-over-all-subarrays/)

给定一个整数数组，任务是计算一个数组的所有子数组的 GCD 之和。数组的 GCD 定义为数组中所有元素的 GCD。更正式地说，![GCD(A[n]) = GCD(A_1, A_2, A_3....A_n)     ](img/d1a2f39a4a850c697fb1a66fed0569b8.png "Rendered by QuickLaTeX.com")。所有 gcd 的总和可以定义为![\sum_{i=1}^{n}\sum_{j=i}^{n} GCD(A_{ij})     ](img/a74b88c4e12d59e3f97b62d7a848732f.png "Rendered by QuickLaTeX.com")，其中![A_{ij}     ](img/a2c3e330b34957c00bd7a4612d67a62f.png "Rendered by QuickLaTeX.com")表示从第一个索引开始到第一个索引结束的子阵列。
**示例:**

> **输入 1:** N = 5，A = {1，2，3，4，5 }
> T3】输出 1: 25
> **解释:**
> 长度一的子阵是[1]，[2]，[3]，[4]，[5]并且它们的 GCDs 之和是 15，同样长度二的子阵是[1，2]，[2，3]，[3，4]，[4，5]，以及它们的 GCDs 之和
> 总和变成 25。
> **输入 2:** N = 6，A = {2，2，2，3，5，5}
> **输出 2:** 41

**计算指标范围内 GCD 的先决条件**
[【二分搜索法】](https://www.geeksforgeeks.org/binary-search/)
[分段树法](https://www.geeksforgeeks.org/gcds-of-a-given-index-ranges-in-an-array/)
[计算指标范围内 GCD 的稀疏表](https://www.geeksforgeeks.org/sparse-table/)

**天真的方法(O(n^3)复杂度)**
我们可以找出 O(n^2 的每个子阵列)复杂度，并可以遍历它来找到该子阵列的 GCD，并将其添加到总答案中。
以下是上述办法的实施:

## C++

```
// C++ program to find
// Sum of GCD over all subarrays.

#include <bits/stdc++.h>
using namespace std;

// Utility function to calculate
// sum of gcd of all sub-arrays.

int findGCDSum(int n, int a[])
{
    int GCDSum = 0;
    int tempGCD = 0;
    for (int i = 0; i < n; i++) {
        // Fixing the starting index of a subarray
        for (int j = i; j < n; j++) {
            // Fixing the ending index of a subarray
            tempGCD = 0;
            for (int k = i; k <= j; k++) {
                // Finding the GCD of this subarray
                tempGCD = __gcd(tempGCD, a[k]);
            }
            // Adding this GCD in our sum
            GCDSum += tempGCD;
        }
    }
    return GCDSum;
}

// Driver Code
int main()
{
    int n = 5;
    int a[] = { 1, 2, 3, 4, 5 };
    int totalSum = findGCDSum(n, a);
    cout << totalSum << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// Sum of GCD over all subarrays.
class GFG
{

// Utility function to calculate
// sum of gcd of all sub-arrays.
static int findGCDSum(int n, int a[])
{
    int GCDSum = 0;
    int tempGCD = 0;
    for (int i = 0; i < n; i++)
    {
        // Fixing the starting index of a subarray
        for (int j = i; j < n; j++)
        {
            // Fixing the ending index of a subarray
            tempGCD = 0;
            for (int k = i; k <= j; k++)
            {
                // Finding the GCD of this subarray
                tempGCD = __gcd(tempGCD, a[k]);
            }

            // Adding this GCD in our sum
            GCDSum += tempGCD;
        }
    }
    return GCDSum;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    int a[] = { 1, 2, 3, 4, 5 };
    int totalSum = findGCDSum(n, a);
    System.out.print(totalSum + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find
# Sum of GCD over all subarrays.

# Utility function to calculate
# sum of gcd of all sub-arrays.
def findGCDSum(n, a):
    GCDSum = 0;
    tempGCD = 0;
    for i in range(n):

        # Fixing the starting index of a subarray
        for j in range(i, n):

            # Fixing the ending index of a subarray
            tempGCD = 0;
            for k in range(i, j + 1):

                # Finding the GCD of this subarray
                tempGCD = __gcd(tempGCD, a[k]);

            # Adding this GCD in our sum
            GCDSum += tempGCD;

    return GCDSum;

def __gcd(a, b):
    return a if(b == 0 ) else __gcd(b, a % b);    

# Driver Code
if __name__ == '__main__':
    n = 5;
    a = [1, 2, 3, 4, 5];
    totalSum = findGCDSum(n, a);
    print(totalSum);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find
// Sum of GCD over all subarrays.
using System;

class GFG
{

// Utility function to calculate
// sum of gcd of all sub-arrays.
static int findGCDSum(int n, int []a)
{
    int GCDSum = 0;
    int tempGCD = 0;
    for (int i = 0; i < n; i++)
    {
        // Fixing the starting index of a subarray
        for (int j = i; j < n; j++)
        {
            // Fixing the ending index of a subarray
            tempGCD = 0;
            for (int k = i; k <= j; k++)
            {
                // Finding the GCD of this subarray
                tempGCD = __gcd(tempGCD, a[k]);
            }

            // Adding this GCD in our sum
            GCDSum += tempGCD;
        }
    }
    return GCDSum;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    int []a = { 1, 2, 3, 4, 5 };
    int totalSum = findGCDSum(n, a);
    Console.Write(totalSum + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to find
// Sum of GCD over all subarrays.   

// Utility function to calculate
    // sum of gcd of all sub-arrays.
    function findGCDSum(n , a)
    {
        var GCDSum = 0;
        var tempGCD = 0;
        for (i = 0; i < n; i++)
        {

            // Fixing the starting index of a subarray
            for (j = i; j < n; j++)
            {

                // Fixing the ending index of a subarray
                tempGCD = 0;
                for (k = i; k <= j; k++)
                {

                    // Finding the GCD of this subarray
                    tempGCD = __gcd(tempGCD, a[k]);
                }

                // Adding this GCD in our sum
                GCDSum += tempGCD;
            }
        }
        return GCDSum;
    }

    function __gcd(a , b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver Code
        var n = 5;
        var a = [ 1, 2, 3, 4, 5 ];
        var totalSum = findGCDSum(n, a);
        document.write(totalSum + "<br/>");

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
25
```

我们可以优化您计算子阵列 GCD 的部分，我们可以使用段树或稀疏表来优化复杂性到 O(n^2 * logn(对于段树)或到 O(n^2(对于稀疏表)
**高效方法(O(n*(logn)^2)复杂性)** :
这种方法利用了这样的观察，即在向数组添加新元素时，数组的新 GCD 将总是小于或等于元素添加之前数组的先前 GCD。
我们创建了三个指针，我们称之为**开始指针**、**结束指针**和**预防指针**。最初，它们三个都指向数组的第一个元素。我们用第一个元素的值初始化一个变量 **tempGCD** 。我们现在将找到从第一个元素开始的所有子阵列的 gcd 之和。
现在根据我们之前的观察，如果把 endPointer 向右移动一个位置，计算 startPointer 和 endPointer 所指向的这两个元素的 GCD，总会小于等于 tempGCD。因此，如果我们想找出有多少子阵列的 GCD 为 tempGCD，我们需要找到一个合适的 endPointer 的位置，其中从 startPointer 开始到 endPointer 结束的子阵列的 GCD 值小于 tempGCD，endPointer 的值应该尽可能小，那么 prevEndPointer 和 EndPointer 的差异将为我们提供其 GCD 为 tempGCD 的子阵列的数量。现在，我们可以将这个值**(tempGCD *(end pointer-prevend pointer))**(表示这些特定子阵列组的 GCD 之和)添加到我们的变量**中，最后一个变量**存储所有子阵列的 GCD 之和。
现在问题依然存在，如何找到 GCD 降低的 endPointer 的合适位置？这就是**二分搜索法**开始使用的地方，我们的数组的起点是固定的，我们需要改变终点，让我们称之为 L 和 R，所以对于任何 R，我们将高初始化为 N，低初始化为 prevEndPointer，中初始化为(高+低)/2，现在如果我们检查 GCD[L，mid]的值，我们将其与 tempGCD 的值进行比较，如果小于它， 那么 R 可能是 endPointer 的合适位置，但可能是这样的情况，一些较小的值可能成为我们的答案，所以我们将高值改为 mid-1，如果发现 GCD[L，mid]等于 tempGCD，那么我们应该将低值改为 mid+1， **mid+1 的值可能是答案，所以我们将 mid 的值存储在变量 nextPos** 中。 最后我们返回 **nextPos+1** 的值。
GCD[L，mid]的值可以使用 O(logN)复杂度中的**段树**或 O(1)复杂度中的**稀疏表**来有效计算。
这种类型的二分搜索法给我们找到了合适的 endPointer 的位置。找到这个位置后，加上 finalAns，我们把**prevent pointer 改成 EndPointer，tempGCD 改成 GCD【start pointer，endPointer】**，再次开始寻找下一个 end pointer 的过程。一旦 endPointer 的值变为 N，这将停止，然后我们需要向右移动 startPointer，这将计算从第二个元素开始的所有子阵列的 GCD 之和。这将持续到 startPointer 的值变为 n 为止
下面是上述方法的实现:

## C++

```
// C++ program to find Sum
// of GCD over all subarrays

#include <bits/stdc++.h>
using namespace std;

//int a[100001];
int SparseTable[100001][51];

// Build Sparse Table
void buildSparseTable(int a[], int n)
{
    for (int i = 0; i < n; i++) {
        SparseTable[i][0] = a[i];
    }
    // Building the Sparse Table for GCD[L, R] Queries
    for (int j = 1; j <= 19; j++) {
        for (int i = 0; i <= n - (1 << j); i++) {
            SparseTable[i][j] = __gcd(SparseTable[i][j - 1],
                    SparseTable[i + (1 << (j - 1))][j - 1]);
        }
    }
}

// Utility Function to calculate GCD in range [L,R]
int queryForGCD(int L, int R)
{
    int returnValue;

    // Calculating where the answer is
    // stored in our Sparse Table
    int j = int(log2(R - L + 1));

    returnValue = __gcd(SparseTable[L][j],
                    SparseTable[R - (1 << j) + 1][j]);

    return returnValue;
}

// Utility Function to find next-farther
// position where gcd is same
int nextPosition(int tempGCD, int startPointer,
                            int prevEndPointer, int n)
{
    int high = n - 1;
    int low = prevEndPointer;
    int mid = prevEndPointer;
    int nextPos = prevEndPointer;

    // BinarySearch for Next Position
    // for EndPointer
    while (high >= low) {

        mid = ((high + low) >> 1);

        if (queryForGCD(startPointer, mid) == tempGCD) {
            nextPos = mid;
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return nextPos + 1;
}

// Utility function to calculate
// sum of gcd
int calculateSum(int a[], int n)
{
    buildSparseTable(a, n);

    int endPointer, startPointer, prevEndPointer, tempGCD;

    int tempAns = 0;

    for (int i = 0; i < n; i++) {
        // Initializing all the values
        endPointer = i;
        startPointer = i;
        prevEndPointer = i;
        tempGCD = a[i];
        while (endPointer < n) {

            // Finding the next position for endPointer
            endPointer = nextPosition(tempGCD, startPointer,
                                            prevEndPointer, n);

            // Adding the suitable sum to our answer
            tempAns += ((endPointer - prevEndPointer) * tempGCD);

            // Changing prevEndPointer
            prevEndPointer = endPointer;

            if (endPointer < n) {
                // Recalculating tempGCD
                tempGCD = __gcd(tempGCD, a[endPointer]);
            }
        }
    }
    return tempAns;
}

// Driver Code
int main()
{
    int n = 6;

    int a[] = {2, 2, 2, 3, 5, 5};

    cout << calculateSum(a, n) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum
// of GCD over all subarrays
class GFG
{

//int a[100001];
static int [][]SparseTable = new int[100001][51];

// Build Sparse Table
static void buildSparseTable(int a[], int n)
{
    for (int i = 0; i < n; i++)
    {
        SparseTable[i][0] = a[i];
    }

    // Building the Sparse Table
    // for GCD[L, R] Queries
    for (int j = 1; j <= 19; j++)
    {
        for (int i = 0; i <= n - (1 << j); i++)
        {
            SparseTable[i][j] = __gcd(SparseTable[i][j - 1],
                     SparseTable[i + (1 << (j - 1))][j - 1]);
        }
    }
}

// Utility Function to calculate GCD in range [L,R]
static int queryForGCD(int L, int R)
{
    int returnValue;

    // Calculating where the answer is
    // stored in our Sparse Table
    int j = (int) (Math.log(R - L + 1));

    returnValue = __gcd(SparseTable[L][j],
         SparseTable[R - (1 << j) + 1][j]);

    return returnValue;
}

// Utility Function to find next-farther
// position where gcd is same
static int nextPosition(int tempGCD, int startPointer,
                        int prevEndPointer, int n)
{
    int high = n - 1;
    int low = prevEndPointer;
    int mid = prevEndPointer;
    int nextPos = prevEndPointer;

    // BinarySearch for Next Position
    // for EndPointer
    while (high >= low)
    {
        mid = ((high + low) >> 1);

        if (queryForGCD(startPointer, mid) == tempGCD)
        {
            nextPos = mid;
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }
    return nextPos + 1;
}

// Utility function to calculate
// sum of gcd
static int calculateSum(int a[], int n)
{
    buildSparseTable(a, n);

    int endPointer, startPointer,
        prevEndPointer, tempGCD;

    int tempAns = 0;

    for (int i = 0; i < n; i++)
    {
        // Initializing all the values
        endPointer = i;
        startPointer = i;
        prevEndPointer = i;
        tempGCD = a[i];
        while (endPointer < n)
        {

            // Finding the next position for endPointer
            endPointer = nextPosition(tempGCD, startPointer,
                                         prevEndPointer, n);

            // Adding the suitable sum to our answer
            tempAns += ((endPointer -
                         prevEndPointer) * tempGCD);

            // Changing prevEndPointer
            prevEndPointer = endPointer;

            if (endPointer < n)
            {

                // Recalculating tempGCD
                tempGCD = __gcd(tempGCD, a[endPointer]);
            }
        }
    }
    return tempAns;
}

static int __gcd(int a, int b)
{
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int n = 6;

    int a[] = {2, 2, 2, 3, 5, 5};

    System.out.println(calculateSum(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find Sum
# of GCD over all subarrays
from math import gcd as __gcd,log,floor
SparseTable = [ [0 for i in range(51)] for i in range(100001)]

# Build Sparse Table
def buildSparseTable(a, n):
    for i in range(n):
        SparseTable[i][0] = a[i]

    # Building the Sparse Table for GCD[L, R] Queries
    for j in range(1,20):
        for i in range(n - (1 << j)+1):
            SparseTable[i][j] = __gcd(SparseTable[i][j - 1],
                                SparseTable[i + (1 << (j - 1))][j - 1])

# Utility Function to calculate GCD in range [L,R]
def queryForGCD(L, R):

    # Calculating where the answer is
    # stored in our Sparse Table
    j = floor(log(R - L + 1, 2))

    returnValue = __gcd(SparseTable[L][j],
                SparseTable[R - (1 << j) + 1][j])

    return returnValue

# Utility Function to find next-farther
# position where gcd is same
def nextPosition(tempGCD, startPointer,prevEndPointer, n):
    high = n - 1
    low = prevEndPointer
    mid = prevEndPointer
    nextPos = prevEndPointer

    # BinarySearch for Next Position
    # for EndPointer
    while (high >= low):

        mid = ((high + low) >> 1)

        if (queryForGCD(startPointer, mid) == tempGCD):
            nextPos = mid
            low = mid + 1
        else:
            high = mid - 1

    return nextPos + 1

# Utility function to calculate
# sum of gcd
def calculateSum(a, n):
    buildSparseTable(a, n)

    tempAns = 0

    for i in range(n):

        # Initializing all the values
        endPointer = i
        startPointer = i
        prevEndPointer = i
        tempGCD = a[i]
        while (endPointer < n):

            # Finding the next position for endPointer
            endPointer = nextPosition(tempGCD,
                        startPointer,prevEndPointer, n)

            # Adding the suitable sum to our answer
            tempAns += ((endPointer - prevEndPointer) * tempGCD)

            # Changing prevEndPointer
            prevEndPointer = endPointer

            if (endPointer < n):

                # Recalculating tempGCD
                tempGCD = __gcd(tempGCD, a[endPointer])

    return tempAns

# Driver code
if __name__ == '__main__':
    n = 6

    a = [2, 2, 2, 3, 5, 5]

    print(calculateSum(a, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find Sum
// of GCD over all subarrays
using System;

class GFG
{

//int a[100001];
static int [,]SparseTable = new int[100001,51];

// Build Sparse Table
static void buildSparseTable(int []a, int n)
{
    for (int i = 0; i < n; i++)
    {
        SparseTable[i,0] = a[i];
    }

    // Building the Sparse Table
    // for GCD[L, R] Queries
    for (int j = 1; j <= 19; j++)
    {
        for (int i = 0; i <= n - (1 << j); i++)
        {
            SparseTable[i,j] = __gcd(SparseTable[i,j - 1],
                    SparseTable[i + (1 << (j - 1)),j - 1]);
        }
    }
}

// Utility Function to calculate GCD in range [L,R]
static int queryForGCD(int L, int R)
{
    int returnValue;

    // Calculating where the answer is
    // stored in our Sparse Table
    int j = (int) (Math.Log(R - L + 1));

    returnValue = __gcd(SparseTable[L,j],
        SparseTable[R - (1 << j) + 1,j]);

    return returnValue;
}

// Utility Function to find next-farther
// position where gcd is same
static int nextPosition(int tempGCD, int startPointer,
                        int prevEndPointer, int n)
{
    int high = n - 1;
    int low = prevEndPointer;
    int mid = prevEndPointer;
    int nextPos = prevEndPointer;

    // BinarySearch for Next Position
    // for EndPointer
    while (high >= low)
    {
        mid = ((high + low) >> 1);

        if (queryForGCD(startPointer, mid) == tempGCD)
        {
            nextPos = mid;
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }
    return nextPos + 1;
}

// Utility function to calculate
// sum of gcd
static int calculateSum(int []a, int n)
{
    buildSparseTable(a, n);

    int endPointer, startPointer,
        prevEndPointer, tempGCD;

    int tempAns = 0;

    for (int i = 0; i < n; i++)
    {
        // Initializing all the values
        endPointer = i;
        startPointer = i;
        prevEndPointer = i;
        tempGCD = a[i];
        while (endPointer < n)
        {

            // Finding the next position for endPointer
            endPointer = nextPosition(tempGCD, startPointer,
                                        prevEndPointer, n);

            // Adding the suitable sum to our answer
            tempAns += ((endPointer -
                        prevEndPointer) * tempGCD);

            // Changing prevEndPointer
            prevEndPointer = endPointer;

            if (endPointer < n)
            {

                // Recalculating tempGCD
                tempGCD = __gcd(tempGCD, a[endPointer]);
            }
        }
    }
    return tempAns;
}

static int __gcd(int a, int b)
{
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int n = 6;

    int []a = {2, 2, 2, 3, 5, 5};

    Console.WriteLine(calculateSum(a, n));
}
}

// This code contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find Sum
// of GCD over all subarrays

// int a[100001];
let SparseTable = new Array(100001);
for(let i=0;i<100001;i++)
{
    SparseTable[i]=new Array(51);
    for(let j=0;j<51;j++)
    {
        SparseTable[i][j]=0;
    }
}

// Build Sparse Table
function buildSparseTable(a,n)
{
    for (let i = 0; i < n; i++)
    {
        SparseTable[i][0] = a[i];
    }

    // Building the Sparse Table
    // for GCD[L, R] Queries
    for (let j = 1; j <= 19; j++)
    {
        for (let i = 0; i <= n - (1 << j); i++)
        {
            SparseTable[i][j] = __gcd(SparseTable[i][j - 1],
                     SparseTable[i + (1 << (j - 1))][j - 1]);
        }
    }
}

// Utility Function to calculate GCD in range [L,R]
function queryForGCD(L,R)
{
    let returnValue;

    // Calculating where the answer is
    // stored in our Sparse Table
    let j =  Math.floor(Math.log(R - L + 1));

    returnValue = __gcd(SparseTable[L][j],
         SparseTable[R - (1 << j) + 1][j]);

    return returnValue;
}

// Utility Function to find next-farther
// position where gcd is same
function nextPosition(tempGCD,startPointer,prevEndPointer,n)
{
    let high = n - 1;
    let low = prevEndPointer;
    let mid = prevEndPointer;
    let nextPos = prevEndPointer;

    // BinarySearch for Next Position
    // for EndPointer
    while (high >= low)
    {
        mid = ((high + low) >> 1);

        if (queryForGCD(startPointer, mid) == tempGCD)
        {
            nextPos = mid;
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }
    return nextPos + 1;
}

// Utility function to calculate
// sum of gcd
function calculateSum(a,n)
{
    buildSparseTable(a, n);

    let endPointer, startPointer,
        prevEndPointer, tempGCD;

    let tempAns = 0;

    for (let i = 0; i < n; i++)
    {
        // Initializing all the values
        endPointer = i;
        startPointer = i;
        prevEndPointer = i;
        tempGCD = a[i];
        while (endPointer < n)
        {

            // Finding the next position for endPointer
            endPointer = nextPosition(tempGCD, startPointer,
                                         prevEndPointer, n);

            // Adding the suitable sum to our answer
            tempAns += ((endPointer -
                         prevEndPointer) * tempGCD);

            // Changing prevEndPointer
            prevEndPointer = endPointer;

            if (endPointer < n)
            {

                // Recalculating tempGCD
                tempGCD = __gcd(tempGCD, a[endPointer]);
            }
        }
    }
    return tempAns;
}

function __gcd(a,b)
{
    return b == 0? a: __gcd(b, a % b);
}

// Driver code
let n = 6;
let a=[2, 2, 2, 3, 5, 5];
document.write(calculateSum(a, n));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
41
```

**时间复杂度**:O(N * log(max(A[I])* log(N))
上述解决方案的时间复杂度包括知道二分搜索法将被调用多少次的知识，因此我们需要知道 endPointer 的值可能改变多少次。这个值大约是 **log(A[i])** ，因为，对于任何一个数 X，它的 GCD 在与其他数相加时可以减少的次数是它的任何质因数的最高幂的值。因此总的时间复杂度大约变成**O(N * log(max(A[I])* log(N))】**，其中另一个 logN 因子来自二分搜索法。当我们使用稀疏表时就是这种情况，如果我们使用段树进行 GCD 查询，将会出现另一个日志项(N)。