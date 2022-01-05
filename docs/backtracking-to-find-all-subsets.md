# 回溯查找所有子集

> 原文:[https://www . geeksforgeeks . org/回溯查找所有子集/](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)

给定一组正整数，求其所有子集。
**例:**

```
Input: array = {1, 2, 3}
Output: // this space denotes null element. 
         1
         1 2
         1 2 3
         1 3
         2
         2 3
         3
Explanation: These are all the subsets that 
can be formed using the array.

Input: 1 2
Output: 
         1 
         2
         1 2
Explanation: These are all the subsets that 
can be formed using the array.
```

这里已经讨论了迭代解:寻找所有子集的[迭代方法](https://www.geeksforgeeks.org/power-set/)。本文旨在提供一种[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)的方法。
**方法:**想法很简单，如果一个数组中有 n 个元素，那么每个元素有两个选择。要么在子集中包含该元素，要么不包含它。
利用上述思想形成问题的递归解。
**算法:**

1.  创建一个递归函数，该函数接受以下参数:输入数组、当前索引、输出数组或当前子集。如果需要存储所有子集，则需要数组的向量。如果只需要打印子集，则可以忽略该空间。
2.  如果当前索引等于数组的大小，则打印子集或输出数组，或将输出数组插入数组向量(或多个向量)中并返回。
3.  非常指数有两种选择。
4.  忽略当前元素，用当前子集和下一个索引调用递归函数，即+ 1。
5.  在子集中插入当前元素，用当前子集和下一个索引调用递归函数，即+ 1。

**执行:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
class GFG {
    public static void
    findSubsets(List<List<Integer>> subset, ArrayList<Integer> nums, ArrayList<Integer> output, int index)
    {
      // Base Condition
        if (index == nums.size()) {
            subset.add(output);
            return;
        }

        // Not Including Value which is at Index
        findSubsets(subset, nums, new ArrayList<>(output), index + 1);

        // Including Value which is at Index
        output.add(nums.get(index));
        findSubsets(subset, nums, new ArrayList<>(output), index + 1);
    }

    public static void main(String[] args) {

      //Main List for storing all subsets
      List<List<Integer>> subset = new ArrayList<>();

      // Input ArrayList
      ArrayList<Integer> input = new ArrayList<>();
      input.add(1);
      input.add(2);
      input.add(3);

      findSubsets(subset, input, new ArrayList<>(), 0);

      // Comparator is used so that all subset get
      // sorted in ascending order of values
        Collections.sort(subset, (o1, o2) -> {
            int n = Math.min(o1.size(), o2.size());
            for (int i = 0; i < n; i++) {
                if (o1.get(i) == o2.get(i)){
                    continue;
                }else{
                    return o1.get(i) - o2.get(i);
                }
            }
            return 1;
        });

      // Printing Subset
      for(int i = 0; i < subset.size(); i++){
          for(int j = 0; j < subset.get(i).size(); j++){
              System.out.print(subset.get(i).get(j) + " ");
          }
          System.out.println();
      }

    }
}
```

## 蟒蛇 3

```
# Python3 program to find all subsets
# by backtracking.

# In the array A at every step we have two
# choices for each element either we can
# ignore the element or we can include the
# element in our subset
def subsetsUtil(A, subset, index):
    print(*subset)
    for i in range(index, len(A)):

        # include the A[i] in subset.
        subset.append(A[i])

        # move onto the next element.
        subsetsUtil(A, subset, i + 1)

        # exclude the A[i] from subset and
        # triggers backtracking.
        subset.pop(-1)
    return

# below function returns the subsets of vector A.
def subsets(A):
    global res
    subset = []

    # keeps track of current element in vector A
    index = 0
    subsetsUtil(A, subset, index)

# Driver Code

# find the subsets of below vector.
array = [1, 2, 3]

# res will store all subsets.
# O(2 ^ (number of elements inside array))
# because at every step we have two choices
# either include or ignore.
subsets(array)

# This code is contributed by SHUBHAMSINGH8410
```

## C++

```
// CPP program to find all subsets by backtracking.
#include <bits/stdc++.h>
using namespace std;

// In the array A at every step we have two
// choices for each element either  we can
// ignore the element or we can include the
// element in our subset
void subsetsUtil(vector<int>& A, vector<vector<int> >& res,
                 vector<int>& subset, int index)
{
    res.push_back(subset);
    for (int i = index; i < A.size(); i++) {

        // include the A[i] in subset.
        subset.push_back(A[i]);

        // move onto the next element.
        subsetsUtil(A, res, subset, i + 1);

        // exclude the A[i] from subset and triggers
        // backtracking.
        subset.pop_back();
    }

    return;
}

// below function returns the subsets of vector A.
vector<vector<int> > subsets(vector<int>& A)
{
    vector<int> subset;
    vector<vector<int> > res;

    // keeps track of current element in vector A;
    int index = 0;
    subsetsUtil(A, res, subset, index);

    return res;
}

// Driver Code.
int main()
{
    // find the subsets of below vector.
    vector<int> array = { 1, 2, 3 };

    // res will store all subsets.
    // O(2 ^ (number of elements inside array))
    // because at every step we have two choices
    // either include or ignore.
    vector<vector<int> > res = subsets(array);

    // Print result
    for (int i = 0; i < res.size(); i++) {
        for (int j = 0; j < res[i].size(); j++)
            cout << res[i][j] << " ";
        cout << endl;
    }

    return 0;
}
```

**Output**

```
1 
1 2 
1 2 3 
1 3 
2 
2 3 
3 

```

**复杂度分析:**

*   **时间复杂度:** O(n(2 ^ n))。
    对于每个索引 I，都会产生两个递归情况，因此时间复杂度为 O(2^n).如果我们包括将子集向量复制到 res 向量所花费的时间，所花费的时间将等于子集向量的大小。
*   **空间复杂度:** O(n)。
    如果不存储输出数组，使用静态全局变量存储输出字符串，可以降低空间复杂度。