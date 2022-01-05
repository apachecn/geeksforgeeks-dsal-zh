# 通过交换满足给定条件的对来排序前 N 个自然数的排列

> 原文:[https://www . geeksforgeeks . org/sort-a-通过交换满足给定条件的对来排列第一个 n 个自然数/](https://www.geeksforgeeks.org/sort-a-permutation-of-first-n-natural-numbers-by-swapping-pairs-satisfying-given-conditions/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**p【】**表示第一个**N**T8】自然数的排列，其中 **N** 是一个[偶数](https://www.geeksforgeeks.org/program-for-n-th-even-number/)，任务是[通过取一对索引 **a，b** 对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，并交换**p**和**p【b】打印在每个操作中交换的索引对。**

**示例:**

> **输入:** p[] = {2，5，3，1，4，6 }
> T3】输出:3
> 1 5
> 2 5
> 1 4
> T9】说明:
> 操作 1:互换 p[1]和 p[5]。因此，p[]修改为{4，5，3，1，2，6}。
> 操作 2:对换 p[2]和 p[5]。因此，p[]修改为{4，2，3，1，5，6}。
> 操作 3:互换 p[1]和 p[4]。因此，p[]修改为{1，2，3，4，5，6}。
> 因此，对数组进行排序。
> 
> **输入:** p[] = {1，2，3，4 }
> T3】输出: 0

**方法:**按照以下步骤解决问题:

*   创建一个[数组](https://www.geeksforgeeks.org/array-data-structure/)， **posOfCurrNum[]** ，该数组存储出现在 **p[]** 中的数字的位置。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**中迭代，并将**设定为**至 **i** 。
*   声明一对**和**的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，以存储对给定数组 **p[]** 进行排序时要执行的交换。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**中迭代
    *   如果**p【I】**等于 **i** ，那么这意味着当前号码 **i** 已经出现在正确的位置。所以，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)到下一个迭代。
    *   用**posofcurrenum【I】**初始化一个变量 **j** 来存储数字 **i** 的当前位置。
    *   现在，出现了 4 种情况:
        *   情况 1:如果**| I–j | * 2**大于 **n** ，那么，**交换(I，j)** 并将该对存储在 **ans** 中。
        *   情况 2:如果 **n/2** 小于或等于**I–1**，那么，**交换(I，1) →交换(1，j) →交换(I，1)** 并将这些配对存储在 **ans** 中。
        *   情况 3:如果 **n/2** 小于或等于**n–j**，那么，**交换(I，n) →交换(j，n) →交换(I，n)** 并将这些对存储在 **ans** 中。
        *   情况 4:如果 **n/2** 小于 **j -1** 且 **n/2** 小于或等于**n–I**，则**交换(I，n) →交换(n，1) →交换(1，j) →交换(1，n) →交换(I，n)** 并将这些对存储在 **ans** 中。
*   打印矢量、**和**的[大小。](https://www.geeksforgeeks.org/vectorempty-vectorsize-c-stl/)
*   [遍历对的向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)、**和**，打印每对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to swap integers
// in an operation
void Swap(int x, int y, int p[],
          int posOfCurrNum[])
{
    swap(posOfCurrNum[p[x]],
         posOfCurrNum[p[y]]);

    swap(p[x], p[y]);
}

// Function to sort permutation
// using given operations
void sortArray(int p[], int n)
{
    // Store the position of the
    // array elements
    int posOfCurrNum[n + 1];
    for (int i = 1; i <= n; i++) {
        posOfCurrNum[p[i]] = i;
    }

    // Store the result
    vector<pair<int, int> > ans;

    // Traverse the given array, p[]
    for (int i = 1; i <= n; i++) {

        // If current number is already
        // present at the right position
        if (p[i] == i) {
            continue;
        }

        // Store the current position of
        // the number 'i'
        int j = posOfCurrNum[i];

        // Case 1: If both the indices
        // satisfies the given condition
        if (abs(i - j) * 2 >= n) {

            Swap(i, j, p, posOfCurrNum);

            ans.push_back({ i, j });
        }

        // Case 2: If the current number
        // 'i' is present at right side
        // of half of the given array
        else if (n / 2 <= i - 1) {

            Swap(1, i, p, posOfCurrNum);
            ans.push_back({ i, 1 });

            Swap(1, j, p, posOfCurrNum);
            ans.push_back({ 1, j });

            Swap(i, 1, p, posOfCurrNum);
            ans.push_back({ i, 1 });
        }

        // Case 3: If the position of the
        // current number 'i' is left side
        // of half of the given array
        else if (n - j >= n / 2) {

            Swap(i, n, p, posOfCurrNum);
            ans.push_back({ i, n });

            Swap(j, n, p, posOfCurrNum);
            ans.push_back({ j, n });

            Swap(i, n, p, posOfCurrNum);
            ans.push_back({ i, n });
        }

        // Case 4: For all other cases
        else {
            Swap(i, n, p, posOfCurrNum);
            ans.push_back({ i, n });

            Swap(n, 1, p, posOfCurrNum);
            ans.push_back({ n, 1 });

            Swap(1, j, p, posOfCurrNum);
            ans.push_back({ 1, j });

            Swap(1, n, p, posOfCurrNum);
            ans.push_back({ 1, n });

            Swap(i, n, p, posOfCurrNum);
            ans.push_back({ i, n });
        }
    }

    // Print the number of operations
    cout << ans.size() << '\n';

    // Print the steps
    for (auto p : ans)
        cout << p.first << " "
             << p.second << '\n';
}

// Driver Code
int main()
{

    // Given Input
    int n = 6;

    // Append 0 to consider
    // 1-based indexing
    int p[] = { 0, 2, 5, 3, 1, 4, 6 };

    // Function Call
    sortArray(p, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class pair
{
  int first, second;
  pair(int first, int second)
  {
    this.first = first;
    this.second = second;
  }
}
class GFG
{

  // Function to swap integers
  // in an operation
  static void Swap(int x, int y, int p[],
                   int posOfCurrNum[])
  {
    int t1 = posOfCurrNum[p[x]];
    posOfCurrNum[p[x]] = posOfCurrNum[p[y]];
    posOfCurrNum[p[y]] = t1;

    int t2 = p[x];
    p[x] = p[y];
    p[y] = t2;
  }

  // Function to sort permutation
  // using given operations
  static void sortArray(int p[], int n)
  {
    // Store the position of the
    // array elements
    int[] posOfCurrNum = new int[n + 1];
    for (int i = 1; i <= n; i++) {
      posOfCurrNum[p[i]] = i;
    }

    // Store the result
    ArrayList<pair > ans=new ArrayList<>();

    // Traverse the given array, p[]
    for (int i = 1; i <= n; i++) {

      // If current number is already
      // present at the right position
      if (p[i] == i) {
        continue;
      }

      // Store the current position of
      // the number 'i'
      int j = posOfCurrNum[i];

      // Case 1: If both the indices
      // satisfies the given condition
      if (Math.abs(i - j) * 2 >= n) {

        Swap(i, j, p, posOfCurrNum);

        ans.add(new pair( i, j ));
      }

      // Case 2: If the current number
      // 'i' is present at right side
      // of half of the given array
      else if (n / 2 <= i - 1) {

        Swap(1, i, p, posOfCurrNum);
        ans.add(new pair( i, 1 ));

        Swap(1, j, p, posOfCurrNum);
        ans.add(new pair( 1, j ));

        Swap(i, 1, p, posOfCurrNum);
        ans.add(new pair( i, 1 ));
      }

      // Case 3: If the position of the
      // current number 'i' is left side
      // of half of the given array
      else if (n - j >= n / 2) {

        Swap(i, n, p, posOfCurrNum);
        ans.add(new pair( i, n ));

        Swap(j, n, p, posOfCurrNum);
        ans.add(new pair( j, n ));

        Swap(i, n, p, posOfCurrNum);
        ans.add(new pair( i, n ));
      }

      // Case 4: For all other cases
      else {
        Swap(i, n, p, posOfCurrNum);
        ans.add(new pair( i, n ));

        Swap(n, 1, p, posOfCurrNum);
        ans.add(new pair( n, 1 ));

        Swap(1, j, p, posOfCurrNum);
        ans.add(new pair( 1, j ));

        Swap(1, n, p, posOfCurrNum);
        ans.add(new pair( 1, n ));

        Swap(i, n, p, posOfCurrNum);
        ans.add(new pair( i, n ));
      }
    }

    // Print the number of operations
    System.out.println(ans.size());

    // Print the steps
    for (pair pp : ans)
      System.out.println(pp.first+" "+pp.second);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given Input
    int n = 6;

    // Append 0 to consider
    // 1-based indexing
    int p[] = { 0, 2, 5, 3, 1, 4, 6 };

    // Function Call
    sortArray(p, n);

  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to swap integers
# in an operation
def Swap(x, y, p, posOfCurrNum):

    posOfCurrNum[p[x]], posOfCurrNum[p[y]] = posOfCurrNum[p[y]], posOfCurrNum[p[x]]

    p[x], p[y] = p[y], p[x]
    return p, posOfCurrNum

# Function to sort permutation
# using given operations
def sortArray(p, n):

    # Store the position of the
    # array elements
    posOfCurrNum = [0] * (n + 1)
    for i in range(1, n + 1):
        posOfCurrNum[p[i]] = i

    # Store the result
    ans = []

    # Traverse the given array, p[]
    for i in range(1, n + 1):

        # If current number is already
        # present at the right position
        if (p[i] == i):
            continue

        # Store the current position of
        # the number 'i'
        j = posOfCurrNum[i]

        # Case 1: If both the indices
        # satisfies the given condition
        if (abs(i - j) * 2 >= n):
            p, posOfCurrNum = Swap(i, j, p, posOfCurrNum)

            ans.append([i, j])

        # Case 2: If the current number
        # 'i' is present at right side
        # of half of the given array
        elif (n // 2 <= i - 1):
            p, posOfCurrNum = Swap(1, i, p, posOfCurrNum)
            ans.append([i, 1])

            p, posOfCurrNum = Swap(1, j, p, posOfCurrNum)
            ans.append([1, j])

            p, posOfCurrNum = Swap(i, 1, p, posOfCurrNum)
            ans.append([i, 1])

        # Case 3: If the position of the
        # current number 'i' is left side
        # of half of the given array
        elif (n - j >= n // 2):
            p, posOfCurrNum = Swap(i, n, p, posOfCurrNum)
            ans.append([i, n])

            p, posOfCurrNum = Swap(j, n, p, posOfCurrNum)
            ans.append([j, n])

            p, posOfCurrNum = Swap(i, n, p, posOfCurrNum)
            ans.append([i, n])

        # Case 4: For all other cases
        else:
            p, posOfCurrNum = Swap(i, n, p, posOfCurrNum)
            ans.append([i, n])

            p, posOfCurrNum = Swap(n, 1, p, posOfCurrNum)
            ans.append([n, 1])

            p, posOfCurrNum = Swap(1, j, p, posOfCurrNum)
            ans.append([1, j])

            p, posOfCurrNum = Swap(1, n, p, posOfCurrNum)
            ans.append([1, n])

            p, posOfCurrNum = Swap(i, n, p, posOfCurrNum)
            ans.append([i, n])

    # Print the number of operations
    print(len(ans))

    # Print the steps
    for p in ans:
        print(p[0], p[1])

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 6

    # Append 0 to consider
    # 1-based indexing
    p = [ 0, 2, 5, 3, 1, 4, 6 ]

    # Function Call
    sortArray(p, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to swap integers
  // in an operation
  static void Swap(int x, int y, int[] p,
                   int[] posOfCurrNum)
  {
    int t1 = posOfCurrNum[p[x]];
    posOfCurrNum[p[x]] = posOfCurrNum[p[y]];
    posOfCurrNum[p[y]] = t1;

    int t2 = p[x];
    p[x] = p[y];
    p[y] = t2;
  }

  // Function to sort permutation
  // using given operations
  static void sortArray(int[] p, int n)
  {
    // Store the position of the
    // array elements
    int[] posOfCurrNum = new int[n + 1];
    for (int i = 1; i <= n; i++) {
      posOfCurrNum[p[i]] = i;
    }

    // Store the result
    List<Tuple<int,int>> ans = new List<Tuple<int,int>>();

    // Traverse the given array, p[]
    for (int i = 1; i <= n; i++) {

      // If current number is already
      // present at the right position
      if (p[i] == i) {
        continue;
      }

      // Store the current position of
      // the number 'i'
      int j = posOfCurrNum[i];

      // Case 1: If both the indices
      // satisfies the given condition
      if (Math.Abs(i - j) * 2 >= n) {

        Swap(i, j, p, posOfCurrNum);

        ans.Add(new Tuple<int,int>(i, j));
      }

      // Case 2: If the current number
      // 'i' is present at right side
      // of half of the given array
      else if (n / 2 <= i - 1) {

        Swap(1, i, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(i, 1));

        Swap(1, j, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(1, j));

        Swap(i, 1, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(i, 1));
      }

      // Case 3: If the position of the
      // current number 'i' is left side
      // of half of the given array
      else if (n - j >= n / 2) {

        Swap(i, n, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(i, n));

        Swap(j, n, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(j, n));

        Swap(i, n, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(i, n));
      }

      // Case 4: For all other cases
      else {
        Swap(i, n, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(i, n));

        Swap(n, 1, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(n, 1));

        Swap(1, j, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(1, 4));

        Swap(1, n, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(1, 6));

        Swap(i, n, p, posOfCurrNum);
        ans.Add(new Tuple<int,int>(i, n));
      }
    }

    // Print the number of operations
    Console.WriteLine(ans.Count);

    // Print the steps
    foreach(Tuple<int,int> pp in ans)
      Console.WriteLine(pp.Item1+" "+pp.Item2);
  }

 // Driver code
  static void Main()
  {

    // Given Input
    int n = 6;

    // Append 0 to consider
    // 1-based indexing
    int[] p = { 0, 2, 5, 3, 1, 4, 6 };

    // Function Call
    sortArray(p, n);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to swap integers
// in an operation
function Swap(x, y, p, posOfCurrNum)
{
    let temp = posOfCurrNum[p[x]];
    posOfCurrNum[p[x]] = posOfCurrNum[p[y]];
    posOfCurrNum[p[y]] = temp;

     temp = p[x];
    p[x] = p[y];
    p[y] = temp;
}

// Function to sort permutation
// using given operations
function sortArray(p, n)
{
    // Store the position of the
    // array elements
    let posOfCurrNum = new Array(n + 1);
    for (let i = 1; i <= n; i++) {
        posOfCurrNum[p[i]] = i;
    }

    // Store the result
    let ans = [];

    // Traverse the given array, p[]
    for (let i = 1; i <= n; i++) {

        // If current number is already
        // present at the right position
        if (p[i] == i) {
            continue;
        }

        // Store the current position of
        // the number 'i'
        let j = posOfCurrNum[i];

        // Case 1: If both the indices
        // satisfies the given condition
        if (Math.abs(i - j) * 2 >= n) {

            Swap(i, j, p, posOfCurrNum);

            ans.push([ i, j ]);
        }

        // Case 2: If the current number
        // 'i' is present at right side
        // of half of the given array
        else if (n / 2 <= i - 1) {

            Swap(1, i, p, posOfCurrNum);
            ans.push([ i, 1 ]);

            Swap(1, j, p, posOfCurrNum);
            ans.push([ 1, j ]);

            Swap(i, 1, p, posOfCurrNum);
            ans.push([ i, 1 ]);
        }

        // Case 3: If the position of the
        // current number 'i' is left side
        // of half of the given array
        else if (n - j >= n / 2) {

            Swap(i, n, p, posOfCurrNum);
            ans.push([ i, n ]);

            Swap(j, n, p, posOfCurrNum);
            ans.push([ j, n ]);

            Swap(i, n, p, posOfCurrNum);
            ans.push([ i, n ]);
        }

        // Case 4: For all other cases
        else {
            Swap(i, n, p, posOfCurrNum);
            ans.push([ i, n ]);

            Swap(n, 1, p, posOfCurrNum);
            ans.push([ n, 1 ]);

            Swap(1, j, p, posOfCurrNum);
            ans.push([ 1, j ]);

            Swap(1, n, p, posOfCurrNum);
            ans.push([ 1, n ]);

            Swap(i, n, p, posOfCurrNum);
            ans.push([ i, n ]);
        }
    }

    // Print the number of operations
    document.write(ans.length + '<br>');

    // Print the steps
    for (let p of ans)
        document.write(p[0] + " " + p[1] + '<br>');
}

// Driver Code

    // Given Input
    let n = 6;

    // Append 0 to consider
    // 1-based indexing
    let p = [ 0, 2, 5, 3, 1, 4, 6 ];

    // Function Call
    sortArray(p, n);

    // This code is contributed by gfgking.
</script>
```

**Output:** 

```
9
1 4
2 6
6 1
1 4
1 6
2 6
4 1
1 5
4 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)