# 打印所有可能的方式将数组拆分成 K 个子集

> 原文:[https://www . geeksforgeeks . org/print-所有可能的方法-将数组拆分为 k 个子集/](https://www.geeksforgeeks.org/print-all-possible-ways-to-split-an-array-into-k-subsets/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是打印所有可能的方式将给定数组拆分为 **K** 子集。

**示例:**

> **输入:** arr[] = { 1，2，3 }，K = 2
> **输出:** { {{ 1，2 }，{ 3 }}，{{ 1，3 }，{ 2 }}，{{ 1 }，{ 2，3 }}。
> 
> **输入:** arr[] = { 1，2，3，4 }，K = 2
> **输出:**{{ 1，2，3 }，{ 4 }}，{{ 1，2，4 }，{ 3 }，{{ 1，2 }，{ 3，4 }}，{{ 1，3，4 }，{ 2 }，{{ 1，3 }，{ 2，4 }}，{ { 1，4 }，{ 2，3 }}，{{ 1 }，{ 2 }

**方法:**使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)生成并打印所有子集可以解决问题。按照以下步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并使用以下递归关系将元素插入任意一个 **K** 子集:

> 分区 ub(i，k，n)
> 
> {
> 
> for(j = 0；j < K；j++){ 0
> 
> sub[j]。推回(arr[i])
> 
> 分区 ub(i + 1，k，n)
> 
> sub[j]。pop_back()
> 
> }
> 
> }

2.  如果 **K** 等于 **0** 或 **K > N** ，则不能生成子集。
3.  如果插入到 **K** 子集中的数组元素个数等于 **N** ，则打印该子集中的元素。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// arr: Store input array
// i: Stores current index of arr
// N: Stores length of arr
// K: Stores count of subsets
// nos: Stores count of feasible subsets formed
// v: Store K subsets of the given array

// Utility function to find all possible
// ways to split array into K subsets
void PartitionSub(int arr[], int i,
                int N, int K, int nos,
                vector<vector<int> >& v)
{

    // If count of elements in K subsets
    // are greater than or equal to N
    if (i >= N) {

        // If count of subsets
        // formed is equal to K
        if (nos == K) {

            // Print K subsets by splitting
            // array into K subsets
            for (int x = 0; x < v.size(); x++) {

                cout << "{ ";

                // Print current subset
                for (int y = 0; y < v[x].size(); y++) {
                    cout << v[x][y];

                    // If current element is the last
                    // element of the subset
                    if (y == v[x].size() - 1) {

                        cout << " ";
                    }

                    // Otherwise
                    else {

                        cout << ", ";
                    }
                }

                if (x == v.size() - 1) {

                    cout << "}";
                }
                else {

                    cout << "}, ";
                }
            }
            cout << endl;
        }

        return;
    }

    for (int j = 0; j < K; j++) {

        // If any subset is occupied,
        // then push the element
        // in that first
        if (v[j].size() > 0) {
            v[j].push_back(arr[i]);

            // Recursively do the same
            // for remaining elements
            PartitionSub(arr, i + 1, N, K, nos, v);

            // Backtrack
            v[j].pop_back();
        }

        // Otherwise, push it in an empty
        // subset and increase the
        // subset count by 1
        else {

            v[j].push_back(arr[i]);
            PartitionSub(arr, i + 1, N, K, nos + 1, v);
            v[j].pop_back();

            // Break to avoid the case of going in
            // other empty subsets, if available,
            // and forming the same combination
            break;
        }
    }
}

// Function to to find all possible ways to
// split array into K subsets
void partKSubsets(int arr[], int N, int K)
{

    // Stores K subset by splitting array
    // into K subsets
    vector<vector<int> > v(K);

    // Size of each subset must
    // be less than the number of elements
    if (K == 0 || K > N) {

        cout << "Not Possible" << endl;
    }
    else {

        cout << "The Subset Combinations are: " << endl;
        PartitionSub(arr, 0, N, K, 0, v);
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Given K
    int K = 2;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Prints all possible
    // splits into subsets
    partKSubsets(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class Gfg
{

  // arr: Store input array
  // i: Stores current index of arr
  // N: Stores length of arr
  // K: Stores count of subsets
  // nos: Stores count of feasible subsets formed
  // v: Store K subsets of the given array

  // Utility function to find all possible
  // ways to split array into K subsets
  static void PartitionSub(int arr[], int i,
                           int N, int K, int nos,
                           ArrayList<ArrayList<Integer>> v)
  {

    // If count of elements in K subsets
    // are greater than or equal to N
    if (i >= N)
    {

      // If count of subsets
      // formed is equal to K
      if (nos == K)
      {

        // Print K subsets by splitting
        // array into K subsets
        for (int x = 0; x < v.size(); x++)
        {

          System.out.print("{ ");

          // Print current subset
          for (int y = 0; y < v.get(x).size(); y++)
          {
            System.out.print(v.get(x).get(y));

            // If current element is the last
            // element of the subset
            if (y == v.get(x).size() - 1)
            {
              System.out.print(" ");
            }

            // Otherwise
            else
            {
              System.out.print(", ");
            }
          }

          if (x == v.size() - 1)
          {
            System.out.print("}");
          }
          else
          {
            System.out.print("}, ");
          }
        }
        System.out.println();;
      }
      return;
    }

    for (int j = 0; j < K; j++)
    {

      // If any subset is occupied,
      // then push the element
      // in that first
      if (v.get(j).size() > 0)
      {
        v.get(j).add(arr[i]);

        // Recursively do the same
        // for remaining elements
        PartitionSub(arr, i + 1, N, K, nos, v);

        // Backtrack
        v.get(j).remove(v.get(j).size()-1);
      }

      // Otherwise, push it in an empty
      // subset and increase the
      // subset count by 1
      else
      {

        v.get(j).add(arr[i]);
        PartitionSub(arr, i + 1, N, K, nos + 1, v);
        v.get(j).remove(v.get(j).size()-1);

        // Break to avoid the case of going in
        // other empty subsets, if available,
        // and forming the same combination
        break;
      }
    }
  }

  // Function to to find all possible ways to
  // split array into K subsets
  static void partKSubsets(int arr[], int N, int K)
  {

    // Stores K subset by splitting array
    // into K subsets
    ArrayList<ArrayList<Integer>> v = new ArrayList<>();

    for(int i = 0; i < K; i++)
      v.add(new ArrayList<>());

    // Size of each subset must
    // be less than the number of elements
    if (K == 0 || K > N)
    {
      System.out.println("Not Possible");
    }
    else
    {
      System.out.println("The Subset Combinations are: ");
      PartitionSub(arr, 0, N, K, 0, v);
    }
  }

  // Driver function
  public static void main (String[] args)
  {

    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Given K
    int K = 2;

    // Size of the array
    int N = arr.length;

    // Prints all possible
    // splits into subsets
    partKSubsets(arr, N, K);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# arr: Store input array
# i: Stores current index of arr
# N: Stores length of arr
# K: Stores count of subsets
# nos: Stores count of feasible subsets formed
# v: Store K subsets of the given array

# Utility function to find all possible
# ways to split array into K subsets
def PartitionSub(arr, i, N, K, nos, v):

    # If count of elements in K subsets
    # are greater than or equal to N
    if (i >= N):

        # If count of subsets
        # formed is equal to K
        if (nos == K):

            # Print K subsets by splitting
            # array into K subsets
            for x in range(len(v)):
                print("{ ", end = "")

                # Print current subset
                for y in range(len(v[x])):
                    print(v[x][y], end = "")

                    # If current element is the last
                    # element of the subset
                    if (y == len(v[x]) - 1):
                        print(" ", end = "")

                    # Otherwise
                    else:
                        print(", ", end = "")

                if (x == len(v) - 1):
                    print("}", end = "")

                else:
                    print("}, ", end = "")
            print("\n", end = "")
        return
    for j in range(K):

        # If any subset is occupied,
        # then push the element
        # in that first
        if (len(v[j]) > 0):
            v[j].append(arr[i])

            # Recursively do the same
            # for remaining elements
            PartitionSub(arr, i + 1, N, K, nos, v)

            # Backtrack
            v[j].remove(v[j][len(v[j]) - 1])

        # Otherwise, push it in an empty
        # subset and increase the
        # subset count by 1
        else:
            v[j].append(arr[i])
            PartitionSub(arr, i + 1, N, K, nos + 1, v)
            v[j].remove(v[j][len(v[j]) - 1])

            # Break to avoid the case of going in
            # other empty subsets, if available,
            # and forming the same combination
            break

# Function to to find all possible ways to
# split array into K subsets
def partKSubsets(arr, N, K):

    # Stores K subset by splitting array
    # into K subsets
    v = [[] for i in range(K)]

    # Size of each subset must
    # be less than the number of elements
    if (K == 0 or K > N):
        print("Not Possible", end = "")
    else:
        print("The Subset Combinations are: ")
        PartitionSub(arr, 0, N, K, 0, v)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr =  [1, 2, 3, 4]

    # Given K
    K = 2

    # Size of the array
    N = len(arr)

    # Prints all possible
    # splits into subsets
    partKSubsets(arr, N, K)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // arr: Store input array
  // i: Stores current index of arr
  // N: Stores length of arr
  // K: Stores count of subsets
  // nos: Stores count of feasible subsets formed
  // v: Store K subsets of the given array

  // Utility function to find all possible
  // ways to split array into K subsets
  static void PartitionSub(int []arr, int i,
                           int N, int K, int nos,
                           List<List<int>>v)
{

  // If count of elements in K subsets
  // are greater than or equal to N
  if (i >= N) {

    // If count of subsets
    // formed is equal to K
    if (nos == K) {

      // Print K subsets by splitting
      // array into K subsets
      for (int x = 0; x < v.Count; x++) {

        Console.Write("{ ");

        // Print current subset
        for (int y = 0; y < v[x].Count; y++) {
          Console.Write(v[x][y]);

          // If current element is the last
          // element of the subset
          if (y == v[x].Count - 1) {

            Console.Write(" ");
          }

          // Otherwise
          else {

            Console.Write(", ");
          }
        }

        if (x == v.Count - 1) {

          Console.Write("}");
        }
        else {

          Console.Write("}, ");
        }
      }
      Console.Write("\n");
    }

    return;
  }

  for (int j = 0; j < K; j++) {

    // If any subset is occupied,
    // then push the element
    // in that first
    if (v[j].Count > 0) {
      v[j].Add(arr[i]);

      // Recursively do the same
      // for remaining elements
      PartitionSub(arr, i + 1, N, K, nos, v);

      // Backtrack
      v[j].RemoveAt(v[j].Count - 1);
    }

    // Otherwise, push it in an empty
    // subset and increase the
    // subset count by 1
    else {

      v[j].Add(arr[i]);
      PartitionSub(arr, i + 1, N, K, nos + 1, v);
      v[j].RemoveAt(v[j].Count - 1);

      // Break to avoid the case of going in
      // other empty subsets, if available,
      // and forming the same combination
      break;
    }
  }
}

 // Function to to find all possible ways to
 // split array into K subsets
 static void partKSubsets(int []arr, int N, int K)
 {

   // Stores K subset by splitting array
   // into K subsets
   List<List<int> > v = new List<List<int>>();
   for(int i=0;i<K;i++)
     v.Add(new List<int>());

   // Size of each subset must
   // be less than the number of elements
   if (K == 0 || K > N) {

     Console.WriteLine("Not Possible");
   }
   else {

     Console.WriteLine("The Subset Combinations are: ");
     PartitionSub(arr, 0, N, K, 0, v);
   }
 }

 // Driver Code
 public static void Main()
 {

   // Given array
   int []arr = {1, 2, 3, 4};

   // Given K
   int K = 2;

   // Size of the array
   int N = arr.Length;

   // Prints all possible
   // splits into subsets
   partKSubsets(arr, N, K);
 }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // Javascript program for above approach

    // arr: Store input array
    // i: Stores current index of arr
    // N: Stores length of arr
    // K: Stores count of subsets
    // nos: Stores count of feasible subsets formed
    // v: Store K subsets of the given array

    // Utility function to find all possible
    // ways to split array into K subsets
    function PartitionSub(arr, i, N, K, nos, v)
    {

      // If count of elements in K subsets
      // are greater than or equal to N
      if (i >= N)
      {

        // If count of subsets
        // formed is equal to K
        if (nos == K)
        {

          // Print K subsets by splitting
          // array into K subsets
          for (let x = 0; x < v.length; x++)
          {

            document.write("{ ");

            // Print current subset
            for (let y = 0; y < v[x].length; y++)
            {
              document.write(v[x][y]);

              // If current element is the last
              // element of the subset
              if (y == v[x].length - 1)
              {
                document.write(" ");
              }

              // Otherwise
              else
              {
                document.write(", ");
              }
            }

            if (x == v.length - 1)
            {
              document.write("}");
            }
            else
            {
              document.write("}, ");
            }
          }
          document.write("</br>");
        }
        return;
      }

      for (let j = 0; j < K; j++)
      {

        // If any subset is occupied,
        // then push the element
        // in that first
        if (v[j].length > 0)
        {
          v[j].push(arr[i]);

          // Recursively do the same
          // for remaining elements
          PartitionSub(arr, i + 1, N, K, nos, v);

          // Backtrack
          v[j].pop();
        }

        // Otherwise, push it in an empty
        // subset and increase the
        // subset count by 1
        else
        {

          v[j].push(arr[i]);
          PartitionSub(arr, i + 1, N, K, nos + 1, v);
          v[j].pop();

          // Break to avoid the case of going in
          // other empty subsets, if available,
          // and forming the same combination
          break;
        }
      }
    }

    // Function to to find all possible ways to
    // split array into K subsets
    function partKSubsets(arr, N, K)
    {

      // Stores K subset by splitting array
      // into K subsets
      let v = [];

      for(let i = 0; i < K; i++)
        v.push([]);

      // Size of each subset must
      // be less than the number of elements
      if (K == 0 || K > N)
      {
        document.write("Not Possible" + "</br>");
      }
      else
      {
        document.write("The Subset Combinations are: " + "</br>");
        PartitionSub(arr, 0, N, K, 0, v);
      }
    }

    // Given array
    let arr = [ 1, 2, 3, 4 ];

    // Given K
    let K = 2;

    // Size of the array
    let N = arr.length;

    // Prints all possible
    // splits into subsets
    partKSubsets(arr, N, K);

// This code is contributed by decode2207.
</script>
```

**Output**

```
The Subset Combinations are: 
{ 1, 2, 3 }, { 4 }
{ 1, 2, 4 }, { 3 }
{ 1, 2 }, { 3, 4 }
{ 1, 3, 4 }, { 2 }
{ 1, 3 }, { 2, 4 }
{ 1, 4 }, { 2, 3 }
{ 1 }, { 2, 3, 4 }
```