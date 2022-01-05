# 一个数组的值比另一个数组的值小的排列

> 原文:[https://www . geeksforgeeks . org/从另一个数组获得较小值的数组排列/](https://www.geeksforgeeks.org/permutation-of-an-array-that-has-smaller-values-from-another-array/)

给定两个大小相等的数组 **A** 和 **B** 。任务是打印**数组 A** 的任何排列，使得**A【I】>B【I】**的索引数量 **i** 最大化**。**

****示例:****

```
Input: A = [12, 24, 8, 32], 
       B = [13, 25, 32, 11]
Output: 24 32 8 12

Input: A = [2, 7, 11, 15], 
       B = [1, 10, 4, 11]
Output: 2 11 7 15
```

**如果 **A** 中的**最小**元素打败了 **B** 中的最小元素，我们应该把它们配对。否则对我们的分数没用，因为打不过 **B** 的任何其他元素。
通过上述策略，我们为 **A** 和**B**制作了两对**向量**、 **Ap** 以及它们各自的**索引**。然后**对**两个向量进行排序并模拟。每当我们在向量 **Ap** 中找到任何元素，使得**Ap【I】。第一>Bp【j】。首先**对于一些 **(i，j)** 我们将它们配对，即我们将我们的答案数组更新为 **ans[Bp[j]。第二] = Ap[i]。第一**。然而如果 **Ap[i]。第一<Bp【j】。首先**对于一些 **(i，j)** 然后我们将它们存储在 vector **剩余**中，最后将它们与任意一个配对。**

****以下是上述方法的实施:****

## **C++**

```
// C++ program to find permutation of an array that
// has smaller values from another array
#include <bits/stdc++.h>
using namespace std;

// Function to print required permutation
void anyPermutation(int A[], int B[], int n)
{
    // Storing elements and indexes
    vector<pair<int, int> > Ap, Bp;
    for (int i = 0; i < n; i++)
        Ap.push_back(make_pair(A[i], i));
    for (int i = 0; i < n; i++)
        Bp.push_back(make_pair(B[i], i));

    sort(Ap.begin(), Ap.end());
    sort(Bp.begin(), Bp.end());

    int i = 0, j = 0, ans[n] = { 0 };

    // Filling the answer array
    vector<int> remain;
    while (i < n && j < n) {

        // pair element of A and B
        if (Ap[i].first > Bp[j].first) {
            ans[Bp[j].second] = Ap[i].first;
            i++;
            j++;
        }
        else {
            remain.push_back(i);
            i++;
        }
    }

    // Fill the remaining elements of answer
    j = 0;
    for (int i = 0; i < n; ++i)
        if (ans[i] == 0) {
            ans[i] = Ap[remain[j]].first;
            j++;
        }

    // Output required permutation
    for (int i = 0; i < n; ++i)
        cout << ans[i] << " ";
}

// Driver program
int main()
{
    int A[] = { 12, 24, 8, 32 };
    int B[] = { 13, 25, 32, 11 };
    int n = sizeof(A) / sizeof(A[0]);
    anyPermutation(A, B, n);
    return 0;
}

// This code is written by Sanjit_Prasad
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find permutation of an
// array that has smaller values from
// another array
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to print required permutation
static void anyPermutation(int A[], int B[], int n)
{

    // Storing elements and indexes
    ArrayList<int[]> Ap = new ArrayList<>();
    ArrayList<int[]> Bp = new ArrayList<>();

    for(int i = 0; i < n; i++)
        Ap.add(new int[] { A[i], i });

    for(int i = 0; i < n; i++)
        Bp.add(new int[] { B[i], i });

    // Sorting the Both Ap and Bp
    Collections.sort(Ap, (x, y) -> {
        if (x[0] != y[0])
            return x[0] - y[0];

        return y[1] - y[1];
    });

    Collections.sort(Bp, (x, y) -> {
        if (x[0] != y[0])
            return x[0] - y[0];

        return y[1] - y[1];
    });

    int i = 0, j = 0;
    int ans[] = new int[n];

    // Filling the answer array
    ArrayList<Integer> remain = new ArrayList<>();
    while (i < n && j < n)
    {

        // Pair element of A and B
        if (Ap.get(i)[0] > Bp.get(j)[0])
        {
            ans[Bp.get(j)[1]] = Ap.get(i)[0];
            i++;
            j++;
        }
        else
        {
            remain.add(i);
            i++;
        }
    }

    // Fill the remaining elements of answer
    j = 0;
    for(i = 0; i < n; ++i)
        if (ans[i] == 0)
        {
            ans[i] = Ap.get(remain.get(j))[0];
            j++;
        }

    // Output required permutation
    for(i = 0; i < n; ++i)
        System.out.print(ans[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 12, 24, 8, 32 };
    int B[] = { 13, 25, 32, 11 };
    int n = A.length;

    anyPermutation(A, B, n);
}
}

// This code is contributed by Kingash
```

## **蟒蛇 3**

```
# Python3 program to find permutation of
# an array that has smaller values from
# another array

# Function to print required permutation
def anyPermutation(A, B, n):

    # Storing elements and indexes
    Ap, Bp = [], []

    for i in range(0, n):
        Ap.append([A[i], i])
    for i in range(0, n):
        Bp.append([B[i], i])

    Ap.sort()
    Bp.sort()

    i, j = 0, 0,
    ans = [0] * n

    # Filling the answer array
    remain = []
    while i < n and j < n:

        # pair element of A and B
        if Ap[i][0] > Bp[j][0]:
            ans[Bp[j][1]] = Ap[i][0]
            i += 1
            j += 1

        else:
            remain.append(i)
            i += 1

    # Fill the remaining elements
    # of answer
    j = 0
    for i in range(0, n):
        if ans[i] == 0:
            ans[i] = Ap[remain[j]][0]
            j += 1

    # Output required permutation
    for i in range(0, n):
        print(ans[i], end = " ")

# Driver Code
if __name__ == "__main__":

    A = [ 12, 24, 8, 32 ]
    B = [ 13, 25, 32, 11 ]
    n = len(A)
    anyPermutation(A, B, n)

# This code is contributed
# by Rituraj Jain
```

****Output:** 

```
24 32 8 12
```** 

****时间复杂度:** O(N*log(N))，其中 N 为数组长度。**