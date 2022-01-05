# Q 查询更新后

打印包含范围[0，M]值的大小 N 的数组

> 原文:[https://www . geesforgeks . org/print-the-array-of-size-n-in-values-in-range-0-m-after-q-query-updates/](https://www.geeksforgeeks.org/print-the-array-of-size-n-containing-values-in-range-0-m-after-q-query-updates/)

给定大小为 **N** 的数组**arr【】**，该数组包含具有从 **0** 到(**M–1)**的状态的循环变量(即，当从 **M-1** 递增时，它转到 **0** )。任务是完成以下两种类型的 **Q** 查询:

*   第一种类型:1l R K–循环递增指数[L，R]范围内的所有值，K 次。
*   第二种类型:2l R–打印索引范围内的更新值[L，R]。

**示例:**

> **输入:** arr[] = {2，2，7，2，5}，Q = 5，M = 8
> 查询[][] = {{1，0，3，4}，
> {1，4，4，2}，
> {1，0，0，7}，
> {2，1，3}，
> {2，3，3}}
> **输出:** {6，3，6}，{6}
> **3，6，7}
> 所以在索引 1 到 3 的第 4 个查询元素和索引 3 的第 5 个查询元素中都会打印。**
> 
> **输入:** arr[] = [2，3，4，5]，Q = 3，M = 6
> 查询[][] = {{1，0，0，3}，
> {1，1，2，2}，
> {1，3，3，1}，
> {2，0，3}}
> **输出:** {5，5，1，1}

**方法:**问题可以用贪心法解决。按照以下步骤实施该方法:

*   当查询是第一种类型时，更新范围[L，R]内的所有值，K 次。
*   当查询是第二种类型时，打印范围[1，R]内的值。

下面是上述方法的实现。

## C++14

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement the queries
void update(int arr[], int N, int M, int Q,
            vector<vector<int> >& queries)
{
    // Loop to implement the queries
    for (int i = 0; i < Q; i++) {
        if (queries[i][0] == 1) {
            for (int j = queries[i][1];
                 j <= queries[i][2];
                 j++)
                arr[j] = (arr[j] +
                          queries[i][3]) % M;
        }
        else if (queries[i][0] == 2) {
            for (int j = queries[i][1];
                 j <= queries[i][2];
                 j++)
                cout << arr[j] << " ";
            cout << endl;
        }
    }
}

// Driver's code
int main()
{
    int N = 5, M = 8, Q = 5;
    int arr[] = { 2, 2, 7, 2, 5 };
    vector<vector<int> > queries(Q);
    queries[0] = { 1, 0, 3, 4 };
    queries[1] = { 1, 4, 4, 2 };
    queries[2] = { 1, 0, 0, 7 };
    queries[3] = { 2, 1, 3 };
    queries[4] = { 2, 3, 3 };

    update(arr, N, M, Q, queries);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 code to implement above approach

# Function to implement the queries
def update(arr, N, M,  Q, queries):

    # Loop to implement the queries
    for i in range(Q):
        if (queries[i][0] == 1):
            for j in range(queries[i][1],
                           queries[i][2] + 1):

                arr[j] = (arr[j] +
                          queries[i][3]) % M

        elif (queries[i][0] == 2):
            for j in range(queries[i][1],
                           queries[i][2] + 1):

                print(arr[j], end = " ")

            print()

# Driver code
if __name__ == "__main__":

    N = 5
    M = 8
    Q = 5
    arr = [2, 2, 7, 2, 5]
    queries = []

    queries.append([1, 0, 3, 4])
    queries.append([1, 4, 4, 2])
    queries.append([1, 0, 0, 7])
    queries.append([2, 1, 3])
    queries.append([2, 3, 3])

    update(arr, N, M, Q, queries)

# This code is contributed by ukasp
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to implement the queries
       function update(arr, N, M, Q,
           queries)
       {
           // Loop to implement the queries
           for (let i = 0; i < Q; i++) {
               if (queries[i][0] == 1) {
                   for (let j = queries[i][1];
                       j <= queries[i][2];
                       j++)
                       arr[j] = (arr[j] +
                           queries[i][3]) % M;
               }
               else if (queries[i][0] == 2) {
                   for (let j = queries[i][1];
                       j <= queries[i][2];
                       j++)
                       document.write(arr[j] + " ");
                   document.write('<br>')
               }
           }
       }

       // Driver's code
       let N = 5, M = 8, Q = 5;
       let arr = [2, 2, 7, 2, 5];
       let queries = new Array(Q);
       queries[0] = [1, 0, 3, 4];
       queries[1] = [1, 4, 4, 2];
       queries[2] = [1, 0, 0, 7];
       queries[3] = [2, 1, 3];
       queries[4] = [2, 3, 3];

       update(arr, N, M, Q, queries);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
6 3 6 
6 
```

***时间复杂度:*** O(Q*N)
***辅助空间:*** O(1)