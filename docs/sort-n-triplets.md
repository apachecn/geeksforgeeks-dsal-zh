# 排序 N 个三胞胎

> 原文:[https://www.geeksforgeeks.org/sort-n-triplets/](https://www.geeksforgeeks.org/sort-n-triplets/)

给定一个 **N** 三胞胎的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，任务是按照[降序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)排列三胞胎。三元组 **X** 将比三元组 **Y** 具有更高的优先级当且仅当三元组 **X** 的所有元素都将大于或等于三元组 **Y 的对应元素。如果不能订购三元组，则**打印**不可能**。

**示例:**

> **输入:** arr = {{1，2，3}、{1，3，4}、{4，7，4}}
> **输出:** {{4，7，4}、{1，3，4}、{1，2，3}}
> **解释:**
> 可以看出，三元组 C 的所有对应元素都大于等于三元组 B，三元组 B 的所有对应元素都大于等于三元组 a。
> 
> **输入:** arr = {{1，2，3 }，{1，2，4}，{1，3，1}，{10，20，30}，{16，9，25}}
> **输出:**不可能

**进场:**这个问题可以用 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 解决。将所有三元组及其三元组 id 保存在不同的列表中，并且[以降序对这些元组列表进行排序](https://www.geeksforgeeks.org/sort-in-python/)。按照以下步骤解决问题。

*   创建三个元组列表 **x** 、 **y** 、**T5】和 **z** 。**
*   列表 **x，y，z** 将保留三胞胎及其三胞胎 id。
*   基于三元组的第一个元素对 **x、**进行排序。
*   根据三元组的第二个元素对 **y、**进行排序。
*   基于三元组的第三元素对 **z、**进行排序。
*   迭代范围**【0，N-1】**中的 **i** ，检查所有 **i** ，如果 **x[i][3] = y[i][3] = z[i][3]** ，则打印相应的订单，否则打印“不可能”。

下面是上述方法的实现。

## C++

```
//  C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

//  Function to find any possible order
vector<vector<int>> findOrder(vector<vector<int>> &A, vector<vector<int>> &x, vector<vector<int>> &y, vector<vector<int>> &z)
{
    int flag = 1;

    // Checking if there is any possible ordering
    for (int i = 0; i < x.size(); ++i)
    {
        if (x[i][3] == y[i][3] && y[i][3] == z[i][3])
            continue;
        else
        {
            flag = 0;
            break;
        }
    }

    vector<vector<int>> Order;
    if (flag)
    {
        for (int i = 0; i < x.size(); ++i)
            Order.push_back(A[x[i][3]]);
    }

    // Return Order
    return Order;
}

// Function to print order of triplets if
// Any possible
void PrintOrder(vector<vector<int>> &A)
{

    // Creating list of paired x, y and z.
    vector<vector<int>> x, y, z;

    for (int i = 0; i < A.size(); ++i)
    {
        x.push_back({A[i][0], A[i][1], A[i][2], i});
        y.push_back({A[i][1], A[i][0], A[i][2], i});
        z.push_back({A[i][2], A[i][0], A[i][1], i});
    }

    // Sorting of x, y and z
    sort(x.rbegin(), x.rend());
    sort(y.rbegin(), y.rend());
    sort(z.rbegin(), z.rend());

    // Function Call
    vector<vector<int>> order = findOrder(A, x, y, z);

    // Printing Order
    if (order.size() == 0)
        cout << "Impossible";
    else
    {
        for (auto v : order)
        {
            for (auto i : v)
                cout << i << " ";
            cout << "\n";
        }
    }
}

// Driver Code
int main()
{

    vector<vector<int>> A = {{4, 1, 1}, {3, 1, 1}, {2, 1, 1}};

    // Function Call
    PrintOrder(A);
    return 0;
}

// This code is contributed by rakeshsahni
```

## 蟒蛇 3

```
# Python program for above approach

# Function to find any possible order
def findOrder(A, x, y, z):
  flag = 1

  # Checking if there is any possible ordering
  for i in range(len(x)):
    if x[i][3] == y[i][3] == z[i][3]:
      continue
    else:
      flag = 0
      break

  Order = 'Impossible'
  if flag:
    Order = []
    for i, j, k, l in x:
      Order += [A[l]]

  # Return Order  
  return Order

# Function to print order of triplets if
# Any possible
def PrintOrder(A):

  # Creating list of paired x, y and z.
  x, y, z = [], [], []

  for i in range(len(A)):
    x.append((A[i][0], A[i][1], A[i][2], i))
    y.append((A[i][1], A[i][0], A[i][2], i))
    z.append((A[i][2], A[i][0], A[i][1], i))

  # Sorting of x, y and z
  x.sort(reverse = True)
  y.sort(reverse = True)
  z.sort(reverse = True)

  # Function Call
  order = findOrder(A, x, y, z)

  # Printing Order
  print(order)

# Driver Code
A = [[4, 1, 1], [3, 1, 1], [2, 1, 1]]

# Function Call
PrintOrder(A)
```

## java 描述语言

```
<script>
    //  Javascript program for above approach
    //  Function to find any possible order
    const findOrder = (A, x, y, z) => {
        let flag = 1;

        // Checking if there is any possible ordering
        for (let i = 0; i < x.length; ++i) {
            let index_x = JSON.stringify(x[i]);
            let index_y = JSON.stringify(y[i]);
            let index_z = JSON.stringify(z[i]);
            // index_x = [[4,1,1,0]] as string
            // we have to find 0 mean index_x[8]

            if (index_x[8] == index_y[8] && index_y[8] == index_z[8])
                continue;
            else {
                flag = 0;
                break;
            }
        }

        let Order = [];
        if (flag) {
            for (let itm in x) {
                let index_x = JSON.stringify(x[itm]);
                Order.push(A[index_x[8] - '0']);
            }
        }

        // Return Order
        return Order;
    }

    // Function to print order of triplets if
    // Any possible
    const PrintOrder = (A) => {

        // Creating list of paired x, y and z.
        let x = [];
        let y = [];
        let z = [];

        for (let i = 0; i < A.length; ++i) {
            x.push([[A[i][0], A[i][1], A[i][2], i]]);
            y.push([[A[i][1], A[i][0], A[i][2], i]]);
            z.push([[A[i][2], A[i][0], A[i][1], i]]);
        }

        // Sorting of x, y and z
        x.sort((a, b) => a - b)
        y.sort((a, b) => a - b)
        z.sort((a, b) => a - b)
        // Function Call
        let order = findOrder(A, x, y, z);

        // Printing Order
        if (order.length === 0) document.write("Impossible");
        else document.write(order);

    }
    // Driver Code

    const A = [[4, 1, 1], [3, 1, 1], [2, 1, 1]];

    // Function Call
    PrintOrder(A);

// This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
[[4, 1, 1], [3, 1, 1], [2, 1, 1]]
```

***时间复杂度:*** O(NlogN)
***辅助空间:*** O(N)