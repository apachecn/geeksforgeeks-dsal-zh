# 检查给定的数组元素是否可以形成回文矩阵

> 原文:[https://www . geesforgeks . org/check-if-a-回文-矩阵-可以从给定的数组元素中形成/](https://www.geeksforgeeks.org/check-if-a-palindromic-matrix-can-be-formed-from-the-given-array-elements/)

给定一个由 **N <sup>2</sup>** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是检查是否可以由给定的数组元素形成维度为 **N * N** 的[矩阵](https://www.geeksforgeeks.org/category/data-structures/matrix/)，即[回文](https://www.geeksforgeeks.org/tag/palindrome/)。如果可能，打印回文矩阵。

> 一个**回文矩阵**就是每一行每一列都是回文的矩阵。

**示例:**

> **输入:** arr[] = {5，1，3，4，5，3，5，4，5}
> **输出:**
> 是
> 5 3 5
> 4 1 4
> 5 3 5
> 
> **输入:** arr[] = {3，4，2，1，5，6，6，9}
> **输出:**否

**方法:**下面是一些观察结果，根据这些观察结果可以解决给定的问题:

*   这里的一个重要观察是–要将值放在第一行的第一列，需要将完全相同的值放在同一行的最后一列，以保留该行的回文行为。此外，要使列回文，需要将相同的值放在最后一行的第一列和最后一列。
*   因此，总共需要 4 个相同值的实例才能将它们对称地放入矩阵中。
*   同样，在具有奇数行和列的矩阵的情况下，中间的行和列只需要相同值的两个实例，因为中间的行和列中的元素将是自身对称的。
*   所以这里的元素可以分为三种类型:
    1.  频率为 4 的倍数的元素。
    2.  频率为 2 的倍数的元素。
    3.  只出现一次的元素。

现在使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)按照以下步骤填充矩阵:

1.  使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)以排序的方式[存储元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率。
2.  如果当前行不是中间行，则选择一个频率至少为**4**的元素，将这些 **4** 号对称地放置在四个角上，使得放置它的行和列保持回文状态。
3.  如果当前行是中间行，选择一个频率为**至少为 2** 的元素，对称放置这些值。
4.  如果在任何步骤中没有找到所需数量的元素，则回文矩阵是不可能的，然后打印**否**。
5.  否则，打印**是**并打印形成的回文矩阵。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to fill the matrix to
// make it palindromic if possible
void fill(vector<pair<int, int> >& temp,
          priority_queue<pair<int, int> >& q,
          vector<vector<int> >& grid)
{
    // First element of priority queue
    auto it = q.top();
    q.pop();

    // If the frequency of element is
    // less than desired frequency
    // then not possible
    if (it.first < temp.size()) {
        cout << "No\n";
        exit(0);
    }

    // If possible then assign value
    // to the matrix
    for (auto c : temp) {
        grid
            = it.second;
    }

    // Decrease the frequency
    it.first -= temp.size();

    // Again push inside queue
    q.push(it);
}

// Function to check if palindromic
// matrix of dimension N*N can be
// formed or not
void checkPalindrome(int A[], int N)
{
    // Stores the frequency
    map<int, int> mp;

    // Stores in the order of frequency
    priority_queue<pair<int, int> > q;

    // To store the palindromic
    // matrix if exists
    vector<vector<int> >
    grid(N, vector<int>(N));

    for (int c = 0; c < N * N; c++) {

        mp[A]++;
    }

    // Number of rows

    // Assign in priority queue
    for (auto c : mp)
        q.push({ c.second, c.first });

    // Middle index
    int m = N / 2;

    // Stores the indexes to be filled
    vector<pair<int, int> > temp;

    for (int i = 0; i < m; i++) {

        for (int j = 0; j < m; j++) {

            // Find the opposite indexes
            // which have same value
            int revI = N - i - 1;
            int revJ = N - j - 1;

            temp = { { i, j },
                     { revI, j },
                     { i, revJ },
                     { revI, revJ } };

            // Check if all the indexes
            // in temp can be filled
            // with same value
            fill(temp, q, grid);

            temp.clear();
        }
    }

    // If N is odd then to fill the
    // middle row and middle column
    if (N & 1) {

        for (int i = 0; i < m; i++) {

            // Fill the temp
            temp = { { i, m },
                     { N - i - 1, m } };

            // Fill grid with temp
            fill(temp, q, grid);

            // Clear temp
            temp.clear();

            // Fill the temp
            temp = { { m, i },
                     { m, N - i - 1 } };

            // Fill grid with temp
            fill(temp, q, grid);
            temp.clear();
        }

        // For the middle element
        // of middle row and column
        temp = { { m, m } };
        fill(temp, q, grid);
    }

    cout << "Yes" << endl;

    // Print the matrix
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            cout << grid[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given array A[]
    int A[] = { 1, 1, 1, 1, 2, 3, 3, 4, 4 };

    int N = sizeof(A) / sizeof(A[0]);

    N = sqrt(N);

    // Function call
    checkPalindrome(A, N);

    return 0;
}
```

**Output:**

```
Yes
1 4 1 
3 2 3 
1 4 1

```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*