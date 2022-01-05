# 世界银行盗窃案

> 原文:[https://www.geeksforgeeks.org/theft-at-world-bank/](https://www.geeksforgeeks.org/theft-at-world-bank/)

给定一个容量囊 **W、**和两个[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**的长度 **N** ，其中**A【I】**代表一个 **i <sup>th</sup>** 块黄金的重量，而**B【I】**代表通过取**I<sup>th【T27】获得的利润</sup>**

**示例:**

> **输入:** *A[]= {4，5，7}，B[] = {8，5，4)，W = 10*
> T5**输出:** 7.857
> ***解释:***
> *获取最大利润的一种方式是:*
> 
> 1.  *取整块第二块，获利 5，产能降为 5。*
> 2.  *取第三块 5/7 的零头，得到(5/7)*4 = 2.857 的利润，产能降为 0。*
> 
> *这样，获得的最大利润等于(5+2.857 = 7.857)，这是最大可能。*
> 
> **输入:** A[]= {2，5，3}，B[] = {7，6，9 }，W = 8
> **输出:** 19.600

**方法:**给定的问题可以使用称为[分数背包](https://www.geeksforgeeks.org/fractional-knapsack-problem/)的[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。按照以下步骤解决问题:

*   初始化一个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)表示 **V** 来存储以数组**中的数组元素【B】**为第一个元素，以数组**中的数组元素【B】**为第二个元素组成的对，并出现在同一索引中。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**如果 **A[i]** 不是 A，[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)则推对 **{B[i]，A[i]}** 进入向量 **V** 。
*   [通过自定义比较器按对的比率对向量 V 进行降序排序。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-2-sort-in-descending-order-by-first-and-second/)
*   将一个变量**利润**初始化为 **0** 存储最大利润。
*   [遍历向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **V** ，在每次迭代中执行以下步骤:
    *   如果当前对的**第二元素小于或等于 **W** ，则以对的**第一元素增加**利润**，即取整块黄金，然后以当前对**的**第二元素减少 **W** 。****
    *   否则，取一个等于**W 与当前对第二元素**之比的量，存入变量 **P** 。然后将**利润**增加**P *当前对的第一个元素**然后断开。
*   最后，完成以上步骤后，打印**利润**中得到的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Custom comparator
bool comp(pair<long long, long long> p1,
          pair<long long, long long> p2)
{
    long double a = p1.first, b = p1.second;
    long double c = p2.first, d = p2.second;
    long double val1 = 0, val2 = 0;
    val1 = a / b;
    val2 = c / d;

    return val1 > val2;
}

// Function to find the maximum profit
long double maximumProfit(int A[], int B[], int N,
                          long long W)
{
    // Stores the pairs of elements
    // of B and A at the same index
    vector<pair<long long, long long> > V;

    // Iterate over the range
    //[0, N]
    for (int i = 0; i < N; i++) {

        long long temp = sqrt(A[i]);

        // If current integer is
        // perfect square
        if (temp * temp == A[i])
            continue;

        // Push the pair of B[i]
        // and A[i] in vector V
        V.push_back({ B[i], A[i] });
    }

    // Sorts the vector using
    // the custom comparator
    sort(V.begin(), V.end(), comp);

    // Stores the maximum profit
    long double profit = 0.00;

    // Traverse the vector V
    for (int i = 0; i < V.size(); i++) {
        // If V[i].second is less
        // than W
        if (V[i].second <= W) {
            // Increment profit by
            // V[i].first
            profit += V[i].first;

            // Decrement V[i].second
            // from W
            W -= V[i].second;
        }
        // Otherwise
        else {
            // Update profit
            profit += V[i].first
                      * ((long double)W / V[i].second);
            break;
        }
    }
    // Return the value of profit
    return profit;
}
// Driver Code
int main()
{

    int N = 3;
    long long W = 10;
    int A[] = { 4, 5, 7 };
    int B[] = { 8, 5, 4 };

    cout << maximumProfit(A, B, N, W) << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math
from functools import cmp_to_key

# Custom comparator
def comparator(p1, p2):

    a = p1[0]
    b = p1[1]
    c = p2[0]
    d = p2[1]
    val1 = a / b
    val2 = c / d
    return val1 > val2

# Function to find the maximum profit
def maximumProfit(A, B, N, W):

    # Stores the pairs of elements
    # of B and A at the same index
    V = []

    # Iterate over the range [0,N]
    for i in range(0, N):

        temp = int(math.sqrt(A[i]))

        # If current integer is
        # perfect square
        if temp * temp == A[i]:
            continue

        # Push the pair of B[i]
        # and A[i] in vector V
        V.append([B[i], A[i]])

    # Sort the vector using
    # the custom comparator
    V = sorted(V, key = cmp_to_key(comparator))

    # Stores the maximum profit
    profit = 0.00

    # Traverse the vector V
    k = len(V)
    for i in range(k):

        # If V[i][1] is less
        # than W
        if V[i][1] <= W:

            # Increment profit by
            # V[i][0]
            profit += V[i][0]

            # Decrement V[i][0]
            # from W
            W -= V[i][1]

        # Otherwise
        else:

            # Update profit
            profit += (V[i][0] * W) / V[i][1]
            break

    # Return the value of profit
    return profit

# Driver Code
if __name__ == '__main__':

    N = 3
    W = 10
    A = [ 4, 5, 7 ]
    B = [ 8, 5, 4 ]

    print(round(maximumProfit(A, B, N, W), 5))

# This code is contributed by MuskanKalra1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Custom comparator
function comp(p1, p2) {
    let a = p1[0], b = p1[1];
    let c = p2[0], d = p2[1];
    let val1 = 0, val2 = 0;
    val1 = Math.floor(a / b);
    val2 = Math.floor(c / d);

    return val1 > val2;
}

// Function to find the maximum profit
function maximumProfit(A, B, N, W) {
    // Stores the pairs of elements
    // of B and A at the same index
    let V = [];

    // Iterate over the range
    //[0, N]
    for (let i = 0; i < N; i++) {

        let temp = Math.sqrt(A[i]);

        // If current integer is
        // perfect square
        if (temp * temp == A[i])
            continue;

        // Push the pair of B[i]
        // and A[i] in vector V
        V.push([B[i], A[i]]);
    }

    // Sorts the vector using
    // the custom comparator
    V.sort(comp);

    // Stores the maximum profit
    let profit = 0.00;

    // Traverse the vector V
    for (let i = 0; i < V.length; i++) {
        // If V[i][1] is less
        // than W
        if (V[i][1] <= W) {
            // Increment profit by
            // V[i][0]
            profit += V[i][0];

            // Decrement V[i][1]
            // from W
            W -= V[i][1];
        }
        // Otherwise
        else {
            // Update profit
            profit += V[i][0]
                * (W / V[i][1]);
            break;
        }
    }
    // Return the value of profit
    return profit.toFixed(5);
}
// Driver Code

let N = 3;
let W = 10;
let A = [4, 5, 7];
let B = [8, 5, 4];

document.write(maximumProfit(A, B, N, W) + "<br>");

</script>
```

**Output**

```
7.85714
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*