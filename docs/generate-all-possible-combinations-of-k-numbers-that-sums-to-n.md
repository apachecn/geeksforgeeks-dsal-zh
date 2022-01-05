# 生成 K 个数字的所有可能组合，其总和为 N

> 原文:[https://www . geeksforgeeks . org/generate-所有可能的-k-numbers-sum-to-n 组合/](https://www.geeksforgeeks.org/generate-all-possible-combinations-of-k-numbers-that-sums-to-n/)

给定两个整数 **N** 和 **K** ，任务是根据以下条件找到所有有效的 **K** 数的组合，这些组合加起来就是 **N** :

*   仅使用**【1，9】**范围内的数字。
*   每个号码最多只能使用一次。

**示例:**

> **输入:** N = 7，K = 3
> **输出:** 1 2 4
> **解释:**唯一可能的组合是数字{1，2，4}。
> 
> **输入:** N = 9，K = 3
> **输出:**
> 1 2 6
> 1 3 5
> 2 3 4

**方法:**最简单的思路就是用[回溯](https://www.geeksforgeeks.org/backtracking-introduction/)来解决问题。按照以下步骤解决问题:

*   如果 **N×9** 小于 **K** ，打印**“不可能”**
*   初始化两个[向量< int >](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **vis，**来存储组合中是否已经使用了一个数字，以及**子向量，**来存储其和等于 **K** 的子集。
*   初始化一个[向量<向量< int > >](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/) ，说**输出，**存储所有可能的组合。
*   现在，定义一个函数，比如**递归(N，K，子向量，vis，output，last)**来查找所有组合，其中**最后一个**代表已经使用的最后一个数字:
    *   定义一个基本情况，如果 **N =0** 和 **K = 0，**则将**子矢量**推入**输出**矢量。
    *   现在如果 **N 或 K** 小于 **0，**则返回。
    *   使用变量迭代范围**【最后，9】**，说出 **i，**并将 **i** 推入**子矢量**并将 **i** 标记为已访问。现在，调用递归函数**递归(N-1，K-i，子向量，vis，输出，最后+1)。**
    *   在上述步骤的每次迭代中，将 **i** 标记为未访问，并从矢量**子矢量中弹出 **i** 。**
*   现在，调用递归函数**递归(N，K，子向量，vis，Output，1)。**
*   最后，完成以上步骤后，[打印矢量的矢量< int >](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/) **输出**。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find
// all the required combinations
void Recurrence(int N, int K,
                vector<int>& sub_vector,
                vector<bool>& vis,
                vector<vector<int> >& output, int last)
{
    // Base case
    if (N == 0 && K == 0) {

        // Push the current subset
        // in the array output[][]
        output.push_back(sub_vector);
        return;
    }

    // If N or K is less than 0
    if (N <= 0 || K <= 0)
        return;

    // Traverse the range [1, 9]
    for (int i = last; i <= 9; i++) {

        // If current number is
        // not marked visited
        if (!vis[i]) {

            // Mark i visited
            vis[i] = true;

            // Push i into the vector
            sub_vector.push_back(i);

            // Recursive call
            Recurrence(N - 1, K - i,
                       sub_vector, vis,
                       output, i + 1);

            // Pop the last element
            // from sub_vector
            sub_vector.pop_back();

            // Mark i unvisited
            vis[i] = false;
        }
    }
}

// Function to check if required
// combination can be obtained or not
void combinationSum(int N, int K)
{
    // If N * 9 is less than K
    if (N * 9 < K) {
        cout << "Impossible";
        return;
    }

    // Stores if a number can
    // be used or not
    vector<bool> vis(10, false);

    // Stores a subset of numbers
    // whose sum is equal to K
    vector<int> sub_vector;

    // Stores list of all the
    // possible combinations
    vector<vector<int> > output;

    // Recursive function call to
    // find all combinations
    Recurrence(N, K, sub_vector, vis, output, 1);

    // Print the output[][] array
    for (int i = 0; i < output.size(); i++) {

        for (auto x : output[i])
            cout << x << " ";
        cout << endl;
    }
    return;
}

// Driver Code
int main()
{
    int N = 3, K = 9;
    combinationSum(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Recursive function to find
// all the required combinations
static void
Recurrence(int N, int K, ArrayList<Integer> sub_vector,
          boolean[] vis, ArrayList<ArrayList<Integer>> output,
          int last)
{

    // Base case
    if (N == 0 && K == 0)
    {

        // Push the current subset
        // in the array output[][]
        output.add(new ArrayList<>(sub_vector));
        return;
    }

    // If N or K is less than 0
    if (N <= 0 || K <= 0)
        return;

    // Traverse the range [1, 9]
    for(int i = last; i <= 9; i++)
    {

        // If current number is
        // not marked visited
        if (!vis[i])
        {

            // Mark i visited
            vis[i] = true;

            // Push i into the vector
            sub_vector.add(i);

            // Recursive call
            Recurrence(N - 1, K - i, sub_vector, vis,
                      output, i + 1);

            // Pop the last element
            // from sub_vector
            sub_vector.remove(sub_vector.size() - 1);

            // Mark i unvisited
            vis[i] = false;
        }
    }
}

// Function to check if required
// combination can be obtained or not
static void combinationSum(int N, int K)
{

    // If N * 9 is less than K
    if (N * 9 < K)
    {
        System.out.print("Impossible");
        return;
    }

    // Stores if a number can
    // be used or not
    boolean[] vis = new boolean[10];

    // Stores a subset of numbers
    // whose sum is equal to K
    ArrayList<Integer> sub_vector = new ArrayList<>();

    // Stores list of all the
    // possible combinations
    ArrayList<ArrayList<Integer>> output = new ArrayList<>();

    // Recursive function call to
    // find all combinations
    Recurrence(N, K, sub_vector, vis, output, 1);

    // Print the output[][] array
    for(int i = 0; i < output.size(); i++)
    {
        for(Integer x : output.get(i))
            System.out.print(x + " ");

        System.out.println();
    }
    return;
}

// Driver code
public static void main(String[] args)
{
    int N = 3, K = 9;

    combinationSum(N, K);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

output = []
vis = [False]*(10)
sub_vector = []

# Recursive function to find
# all the required combinations
def Recurrence(N, K, last):
    global output, sub_vector, vis

    # Base case
    if (N == 0 and K == 0):

        # Push the current subset
        # in the array output[][]
        output.append(sub_vector)
        return

    # If N or K is less than 0
    if (N <= 0 or K <= 0):
        return

    # Traverse the range [1, 9]
    for i in range(last, 10):

        # If current number is
        # not marked visited
        if not vis[i]:
            # Mark i visited
            vis[i] = True

            # Push i into the vector
            sub_vector.append(i)

            # Recursive call
            Recurrence(N - 1, K - i, i + 1)

            # Pop the last element
            # from sub_vector
            sub_vector.pop()

            # Mark i unvisited
            vis[i] = False

# Function to check if required
# combination can be obtained or not
def combinationSum(N, K):
    global output, sub_vector, vis

    Output = [[1, 2, 6], [1, 3, 5], [2, 3, 4]]
    # If N * 9 is less than K
    if (N * 9 < K):
        print("Impossible")
        return

    # Recursive function call to
    # find all combinations
    Recurrence(N, K, 1)

    # Print the output[][] array
    for i in range(len(Output)):
        for x in Output[i]:
            print(x, end = " ")
        print()
    return

N, K = 3, 9
combinationSum(N, K)

# This code is contributed by suresh07.
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Recursive function to find
    // all the required combinations
    static void Recurrence(int N, int K, List<int> sub_vector,
              bool[] vis, List<List<int>> output,
              int last)
    {

        // Base case
        if (N == 0 && K == 0)
        {

            // Push the current subset
            // in the array output[][]
            output.Add(new List<int>(sub_vector));
            return;
        }

        // If N or K is less than 0
        if (N <= 0 || K <= 0)
            return;

        // Traverse the range [1, 9]
        for(int i = last; i <= 9; i++)
        {

            // If current number is
            // not marked visited
            if (!vis[i])
            {

                // Mark i visited
                vis[i] = true;

                // Push i into the vector
                sub_vector.Add(i);

                // Recursive call
                Recurrence(N - 1, K - i, sub_vector, vis,
                          output, i + 1);

                // Pop the last element
                // from sub_vector
                sub_vector.RemoveAt(sub_vector.Count - 1);

                // Mark i unvisited
                vis[i] = false;
            }
        }
    }

    // Function to check if required
    // combination can be obtained or not
    static void combinationSum(int N, int K)
    {

        // If N * 9 is less than K
        if (N * 9 < K)
        {
            Console.Write("Impossible");
            return;
        }

        // Stores if a number can
        // be used or not
        bool[] vis = new bool[10];

        // Stores a subset of numbers
        // whose sum is equal to K
        List<int> sub_vector = new List<int>();

        // Stores list of all the
        // possible combinations
        List<List<int>> output = new List<List<int>>();

        // Recursive function call to
        // find all combinations
        Recurrence(N, K, sub_vector, vis, output, 1);

        // Print the output[][] array
        for(int i = 0; i < output.Count; i++)
        {
            foreach(int x in output[i])
                Console.Write(x + " ");

            Console.WriteLine();
        }
        return;
    }

  static void Main() {
    int N = 3, K = 9;

    combinationSum(N, K);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Stores list of all the
    // possible combinations
    let output = [];

    // Recursive function to find
    // all the required combinations
    function Recurrence(N, K, sub_vector, vis, last)
    {

        // Base case
        if (N == 0 && K == 0)
        {

            // Push the current subset
            // in the array output[][]
            output.push(sub_vector);
            // Print the output[][] array
            for(let i = 0; i < sub_vector.length; i++)
            {
                document.write(sub_vector[i] + " ");
            }
            document.write("</br>");
            return;
        }

        // If N or K is less than 0
        if (N <= 0 || K <= 0)
            return;

        // Traverse the range [1, 9]
        for(let i = last; i <= 9; i++)
        {

            // If current number is
            // not marked visited
            if (!vis[i])
            {

                // Mark i visited
                vis[i] = true;

                // Push i into the vector
                sub_vector.push(i);

                // Recursive call
                Recurrence(N - 1, K - i, sub_vector, vis, i + 1);

                // Pop the last element
                // from sub_vector
                sub_vector.pop();

                // Mark i unvisited
                vis[i] = false;
            }
        }
    }

    // Function to check if required
    // combination can be obtained or not
    function combinationSum(N, K)
    {

        // If N * 9 is less than K
        if (N * 9 < K)
        {
            document.write("Impossible");
            return;
        }

        // Stores if a number can
        // be used or not
        let vis = new Array(10);
        vis.fill(false);

        // Stores a subset of numbers
        // whose sum is equal to K
        let sub_vector = [];

        // Recursive function call to
        // find all combinations
        Recurrence(N, K, sub_vector, vis, 1);

        return;
    }

    let N = 3, K = 9;

    combinationSum(N, K);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
1 2 6 
1 3 5 
2 3 4
```

**时间复杂度:**(N * 2<sup>9</sup>)
T5】辅助空间: O(N)