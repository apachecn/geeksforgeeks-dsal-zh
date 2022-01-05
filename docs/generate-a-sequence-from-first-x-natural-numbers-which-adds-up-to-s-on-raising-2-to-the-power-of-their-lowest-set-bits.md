# 根据前 X 个自然数生成一个序列，将它们的最低位的 2 次方

加起来就是 S

> 原文:[https://www . geesforgeks . org/generate-a-sequence-from-first-x-natural-numbers-and-up-s-on-raising-2-其最低设置位的幂/](https://www.geeksforgeeks.org/generate-a-sequence-from-first-x-natural-numbers-which-adds-up-to-s-on-raising-2-to-the-power-of-their-lowest-set-bits/)

给定两个整数 **X** 和 **S** ，任务是从范围**【1，X】**中构造不同整数的序列，使得值**2<sup>K</sup>T9】的和等于 **S** ，其中 **K** 是从[的末端](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/) ( 0- *基于索引*)开始的第一组位的[位置](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)**

**示例:**

> **输入:** X = 3，S = 4
> **输出:** 2 3 1
> **解释:**
> 集合中每个元素的 2 <sup>K</sup> 之和如下:
> 为 2，则为 2^1 = 2。
> 对于 3，它是 2^0 = 1。
> 对于 1，它是 2^0 = 1。
> 因此，要求的和= 2 + 1 + 1 = 4，等于 s。
> 
> **输入:** X = 1，S = 5
> **输出:** -1

**方法:**问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:

*   初始化一个变量，说 **lowBit，**存储任意数字的**2<sup>K</sup>T5 的值，其中 **K** 是从每个元素[二进制表示的末尾](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)开始的第一个设置位的[位置。](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)**
*   将范围**【1，X】**中所有数字的**低位**的所有值插入到[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **V** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，以将这些数字与其**低位**值配对。 **lowBit(X)** 的值可以通过 **log2(N & -N) + 1** 得到。
*   [按照相反的顺序](https://www.geeksforgeeks.org/how-to-sort-a-vector-in-descending-order-using-stl-in-c/)排序向量，首先得到最大值**低位**。
*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说**ans【】**，存储所需的集合和一个整数，比如说 **ansSum，**存储**低位**值的当前总和。
*   [遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **V** 并执行以下步骤:
    *   检查 **(ansSum+v[i]。首先)< = S** ，然后加上**v【I】的值。第二次**到阵 **ans[]** 和更新 **ansSum** 。
    *   如果 **ansSum** 等于给定的和 **S，**则[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)并打印结果数组 **ans[]** 。
*   如果发现 **ansSum** 不等于 **S，**则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the lowest
// set bit of any number N
int lowBit(int N)
{
    return log2(N & -N) + 1;
}

// Function to generate the sequence
// which adds up to sum on raising 2
// to the power of lowest set bit
// of all integers from the sequence
void find_set(int X, int sum)
{
    // Stores the lowBit value
    vector<pair<int, int> > v;

    // Traverse through 1 to X and
    // insert all the lowBit value
    for (int i = 1; i <= X; i++) {
        pair<int, int> aux;
        aux.first = lowBit(i);
        aux.second = i;
        v.push_back(aux);
    }

    // Sort vector in reverse manner
    sort(v.rbegin(), v.rend());

    bool check = false;

    // Store all our set values
    vector<int> ans;

    // Stores the current
    // summation of lowBit
    int ansSum = 0;

    // Traverse vector v
    for (int i = 0; i < v.size(); i++) {

        // Check if ansSum+v[i].first
        // is at most sum
        if (ansSum + v[i].first <= sum) {

            // Add to the ansSum
            ansSum += v[i].first;
            ans.push_back(v[i].second);
        }

        // If ansSum is same as the sum,
        // then break from loop
        if (ansSum == sum) {
            check = true;
            break;
        }
    }

    // If check is false, no such
    // sequence can be obtained
    if (!check) {
        cout << "-1";
        return;
    }

    // Otherwise, print the sequence
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    int X = 3, S = 4;

    // Generate and print
    // the required sequence
    find_set(X, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

// User defined Pair class
class Pair {
  int x;
  int y;

  // Constructor
  public Pair(int x, int y)
  {
    this.x = x;
    this.y = y;
  }
}

// class to define user defined conparator
class Compare
{
  static void compare(Pair arr[], int n)
  {

    // Comparator to sort the pair according to second element
    Arrays.sort(arr, new Comparator<Pair>() {
      @Override public int compare(Pair p1, Pair p2)
      {
        return p1.x - p2.x;
      }
    });
  }
}

// Driver class
class GFG
{

  // Function to calculate the lowest
  // set bit of any number N
  static int lowBit(int N)
  {
    return (int)(Math.log(N & -N) / Math.log(2)) + 1;
  }

  // Function to generate the sequence
  // which adds up to sum on raising 2
  // to the power of lowest set bit
  // of all integers from the sequence
  static void find_set(int X, int sum)
  {
    // Stores the lowBit value
    Pair v[] = new Pair[X];

    // Traverse through 1 to X and
    // insert all the lowBit value
    for (int i = 0; i < X; i++)
    {
      Pair aux = new Pair(lowBit(i + 1), i + 1);
      v[i] = aux;
    }

    // Sort vector in reverse manner
    Compare obj = new Compare();
    obj.compare(v, X);
    int j = X - 1;
    for(int i = 0; i < X / 2; i++)
    {
      Pair temp = v[i];
      v[i] = v[j];
      v[j] = temp;
      j--;
    }

    boolean check = false;

    // Store all our set values
    Vector<Integer> ans = new Vector<Integer>();

    // Stores the current
    // summation of lowBit
    int ansSum = 0;

    // Traverse vector v
    for (int i = 0; i < X; i++) {

      // Check if ansSum+v[i].first
      // is at most sum
      if (ansSum + v[i].x <= sum) {

        // Add to the ansSum
        ansSum += v[i].x;
        ans.add(v[i].y);
      }

      // If ansSum is same as the sum,
      // then break from loop
      if (ansSum == sum) {
        check = true;
        break;
      }
    }

    // If check is false, no such
    // sequence can be obtained
    if (!check)
    {
      System.out.println("-1");
      return;
    }

    // Otherwise, print the sequence
    for (int i = 0; i < ans.size(); i++)
    {
      System.out.print(ans.get(i) + " ");
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    int X = 3, S = 4;

    // Generate and print
    // the required sequence
    find_set(X, S);
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2, ceil, floor

# Function to calculate the lowest
# set bit of any number N
def lowBit(N):

    return log2(N & -N) + 1

# Function to generate the sequence
# which adds up to sum on raising 2
# to the power of lowest set bit
# of all integers from the sequence
def find_set(X, sum):

    # Stores the lowBit value
    v = []

    # Traverse through 1 to X and
    # insert all the lowBit value
    for i in range(1, X + 1):
        aux = [0, 0]
        aux[0] = lowBit(i)
        aux[1] = i
        v.append(aux)

    # Sort vector in reverse manner
    v = sorted(v)[::-1]

    check = False

    # Store all our set values
    ans = []

    # Stores the current
    # summation of lowBit
    ansSum = 0

    # Traverse vector v
    for i in range(len(v)):

        # Check if ansSum+v[i][0]
        # is at most sum
        if (ansSum + v[i][0] <= sum):

            # Add to the ansSum
            ansSum += v[i][0]
            ans.append(v[i][1])

        # If ansSum is same as the sum,
        # then break from loop
        if (ansSum == sum):
            check = True
            break

    # If check is false, no such
    # sequence can be obtained
    if (not check):
        print("-1")
        return

    # Otherwise, print the sequence
    for i in range(len(ans)):
        print(ans[i], end = " ")

# Driver Code
if __name__ == '__main__':

    X, S = 3, 4

    # Generate and pr
    # the required sequence
    find_set(X, S)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to calculate the lowest
    // set bit of any number N
    static int lowBit(int N)
    {
        return (int)(Math.Log(N & -N, 2)) + 1;
    }

    // Function to generate the sequence
    // which adds up to sum on raising 2
    // to the power of lowest set bit
    // of all integers from the sequence
    static void find_set(int X, int sum)
    {
        // Stores the lowBit value
        List<Tuple<int, int>> v = new List<Tuple<int, int>>();

        // Traverse through 1 to X and
        // insert all the lowBit value
        for (int i = 1; i <= X; i++) {
            Tuple<int, int> aux = new Tuple<int, int>(lowBit(i), i);
            v.Add(aux);
        }

        // Sort vector in reverse manner
        v.Sort();
        v.Reverse(); 

        bool check = false;

        // Store all our set values
        List<int> ans = new List<int>();

        // Stores the current
        // summation of lowBit
        int ansSum = 0;

        // Traverse vector v
        for (int i = 0; i < v.Count; i++) {

            // Check if ansSum+v[i].first
            // is at most sum
            if (ansSum + v[i].Item1 <= sum) {

                // Add to the ansSum
                ansSum += v[i].Item1;
                ans.Add(v[i].Item2);
            }

            // If ansSum is same as the sum,
            // then break from loop
            if (ansSum == sum) {
                check = true;
                break;
            }
        }

        // If check is false, no such
        // sequence can be obtained
        if (!check) {
            Console.Write("-1");
            return;
        }

        // Otherwise, print the sequence
        for (int i = 0; i < ans.Count; i++) {
            Console.Write(ans[i] + " ");
        }
    }

  // Driver code
  static void Main()
  {    
    int X = 3, S = 4;

    // Generate and print
    // the required sequence
    find_set(X, S);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate the lowest
// set bit of any number N
function lowBit(N) {
    return Math.log2(N & -N) + 1;
}

// Function to generate the sequence
// which adds up to sum on raising 2
// to the power of lowest set bit
// of all integers from the sequence
function find_set(X, sum) {
    // Stores the lowBit value
    let v = [];

    // Traverse through 1 to X and
    // insert all the lowBit value
    for (let i = 1; i <= X; i++) {
        let aux = [];
        aux[0] = lowBit(i);
        aux[1] = i;
        v.push(aux);
    }

    // Sort vector in reverse manner
    v.sort((a, b) => a[0] - b[0]).reverse();

    let check = false;

    // Store all our set values
    let ans = [];

    // Stores the current
    // summation of lowBit
    let ansSum = 0;

    // Traverse vector v
    for (let i = 0; i < v.length; i++) {

        // Check if ansSum+v[i][0]
        // is at most sum
        if (ansSum + v[i][0] <= sum) {

            // Add to the ansSum
            ansSum += v[i][0];
            ans.push(v[i][1]);
        }

        // If ansSum is same as the sum,
        // then break from loop
        if (ansSum == sum) {
            check = true;
            break;
        }
    }

    // If check is false, no such
    // sequence can be obtained
    if (!check) {
        document.write("-1");
        return;
    }

    // Otherwise, print the sequence
    for (let i = 0; i < ans.length; i++) {
        document.write(ans[i] + " ");
    }
}

// Driver Code

let X = 3, S = 4;

// Generate and print
// the required sequence
find_set(X, S);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2 3 1
```

***时间复杂度:**O(X)*
T5**辅助空间:** O(X)