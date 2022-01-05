# 使用回溯生成数组的所有不同子序列

> 原文:[https://www . geeksforgeeks . org/generate-all-distinct-subseries-of-array-use-backtrack/](https://www.geeksforgeeks.org/generate-all-distinct-subsequences-of-array-using-backtracking/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是生成数组的所有不同[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)。

**示例:**

> **输入:** arr[] = {1，2，2}
> **输出:** {} {1} {1，2} {1，2，2} {2} {2，2}
> **解释:**
> 给定数组的总子序列为{}、{1}、{2}、{2}、{2}、{1，2}、{1，2}、{2，2}、{1，2，2}。
> 由于{2}和{1，2}重复两次，打印数组的所有剩余子序列。
> 
> **输入:** arr[] = {1，2，3，3}
> **输出:** {} {1} {1，2} {1，2，3} {1，2，3，3} {1，3} {1，3，3} {2} {2，3} {2，3} {3}，{3，3}

**方法:**按照以下步骤解决问题:

1.  [给定数组排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
2.  初始化向量的[向量](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)来存储所有不同的子序列。
3.  [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并考虑每个数组元素的两个选择，将其包含在子序列中还是不包含。
4.  如果发现重复，忽略它们并检查剩余的元素。否则，将当前数组元素添加到当前子序列，并遍历其余元素以生成子序列。
5.  生成子序列后，移除当前数组元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate all distinct
// subsequences of the array using backtracking
void backtrack(vector<int>& nums, int start,
               vector<vector<int> >& resultset,
               vector<int> curr_set)
{
    resultset.push_back(curr_set);

    for (int i = start; i < nums.size(); i++) {

        // If the current element is repeating
        if (i > start
            && nums[i] == nums[i - 1]) {
            continue;
        }

        // Include current element
        // into the subsequence
        curr_set.push_back(nums[i]);

        // Proceed to the remaining array
        // to generate subsequences
        // including current array element
        backtrack(nums, i + 1, resultset,
                  curr_set);

        // Remove current element
        // from the subsequence
        curr_set.pop_back();
    }
}

// Function to sort the array and generate
// subsequences using Backtracking
vector<vector<int> > AllSubsets(
    vector<int> nums)
{
    // Stores the subsequences
    vector<vector<int> > resultset;

    // Stores the current
    // subsequence
    vector<int> curr_set;

    // Sort the vector
    sort(nums.begin(), nums.end());

    // Backtrack function to
    // generate subsequences
    backtrack(nums, 0, resultset,
              curr_set);

    // Return the result
    return resultset;
}

// Function to print all subsequences
void print(vector<vector<int> > result)
{
    for (int i = 0; i < result.size();
         i++) {

        cout << "{";
        for (int j = 0; j < result[i].size();
             j++) {

            cout << result[i][j];
            if (j < result[i].size() - 1) {

                cout << ", ";
            }
        }
        cout << "} ";
    }
}

// Driver Code
int main()
{
    vector<int> v{ 1, 2, 2 };

    // Function call
    vector<vector<int> > result
        = AllSubsets(v);

    // Print function
    print(result);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to generate all distinct
// subsequences of the array using backtracking
public static void backtrack(ArrayList<Integer> nums,
                             int start,
                             ArrayList<Integer> curr_set)
{
    System.out.print(curr_set + " ");

    for(int i = start; i < nums.size(); i++)
    {

        // If the current element is repeating
        if (i > start &&
            nums.get(i) == nums.get(i - 1))
        {
            continue;
        }

        // Include current element
        // into the subsequence
        curr_set.add(nums.get(i));

        // Proceed to the remaining array
        // to generate subsequences
        // including current array element
        backtrack(nums, i + 1, curr_set);

        // Remove current element
        // from the subsequence
        curr_set.remove(curr_set.size() - 1);
    }
}

// Function to sort the array and generate
// subsequences using Backtracking
public static void AllSubsets(ArrayList<Integer> nums)
{

    // Stores the current
    // subsequence
    ArrayList<Integer> curr_set = new ArrayList<>();

    // Sort the vector
    Collections.sort(nums);

    // Backtrack function to
    // generate subsequences
    backtrack(nums, 0, curr_set);
}

// Driver Code
public static void main(String[] args)
{
    ArrayList<Integer> v = new ArrayList<>();
    v.add(1);
    v.add(2);
    v.add(2);

    // Function call
    AllSubsets(v);
}
}

// This code is contributed by hemanthswarna1506
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
result = []

# Function to generate all distinct
# subsequences of the array
# using backtracking
def backtrack(nums, start, curr_set):

    # Global result
    result.append(list(curr_set))

    for i in range(start, len(nums)):

        # If the current element is repeating
        if (i > start and nums[i] == nums[i - 1]):
            continue

        # Include current element
        # into the subsequence
        curr_set.append(nums[i])

        # Proceed to the remaining array
        # to generate subsequences
        # including current array element
        backtrack(nums, i + 1, curr_set)

        # Remove current element
        # from the subsequence
        curr_set.pop()

# Function to sort the array and generate
# subsequences using Backtracking
def AllSubsets(nums):

    # Stores the current
    # subsequence
    curr_set = []

    # Sort the vector
    nums.sort()

    # Backtrack function to
    # generate subsequences
    backtrack(nums, 0, curr_set)

# Function to prints all subsequences
def prints():

    global result

    for i in range(len(result)):
        print('{', end = '')

        for j in range(len(result[i])):
            print(result[i][j], end = '')

            if (j < len(result[i]) - 1):
                print(',', end = ' ')

        print('} ', end = '')

# Driver Code
if __name__=='__main__':

    v = [ 1, 2, 2 ]

    # Function call
    AllSubsets(v)

    # Print function
    prints()

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to generate all distinct
// subsequences of the array using
// backtracking
public static void backtrack(List<int> nums,
                             int start,
                             List<int> curr_set)
{
  Console.Write(" {");

  foreach(int i in curr_set)
  {
    Console.Write(i);
    Console.Write(", ");
  }

  Console.Write("}");

  for(int i = start;
          i < nums.Count; i++)
  {
    // If the current element
    // is repeating
    if (i > start &&
        nums[i] == nums[i - 1])
    {
      continue;
    }

    // Include current element
    // into the subsequence
    curr_set.Add(nums[i]);

    // Proceed to the remaining array
    // to generate subsequences
    // including current array element
    backtrack(nums, i + 1, curr_set);

    // Remove current element
    // from the subsequence
    curr_set.Remove(curr_set.Count - 1);
  }
}

// Function to sort the array and generate
// subsequences using Backtracking
public static void AllSubsets(List<int> nums)
{
  // Stores the current
  // subsequence
  List<int> curr_set = new List<int>();

  // Sort the vector
  nums.Sort();

  // Backtrack function to
  // generate subsequences
  backtrack(nums, 0, curr_set);
}

// Driver Code
public static void Main(String[] args)
{
  List<int> v = new List<int>();
  v.Add(1);
  v.Add(2);
  v.Add(2);

  // Function call
  AllSubsets(v);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to generate all distinct
    // subsequences of the array using
    // backtracking
    function backtrack(nums, start, curr_set)
    {
      document.write(" {");

      for(let i = 0; i < curr_set.length - 1; i++)
      {
        document.write(curr_set[i]);
        document.write(", ");
      }

      if(curr_set.length >= 1)
      {
          document.write(curr_set[curr_set.length - 1]);
          document.write("}");
      }
      else
      {
          document.write("}");
      }

      for(let i = start; i < nums.length; i++)
      {
        // If the current element
        // is repeating
        if (i > start && nums[i] == nums[i - 1])
        {
          continue;
        }

        // Include current element
        // into the subsequence
        curr_set.push(nums[i]);

        // Proceed to the remaining array
        // to generate subsequences
        // including current array element
        backtrack(nums, i + 1, curr_set);

        // Remove current element
        // from the subsequence
        curr_set.pop();
      }
    }

    // Function to sort the array and generate
    // subsequences using Backtracking
    function AllSubsets(nums)
    {
      // Stores the current
      // subsequence
      let curr_set = [];

      // Sort the vector
      nums.sort();

      // Backtrack function to
      // generate subsequences
      backtrack(nums, 0, curr_set);
    }

    let v = [];
    v.push(1);
    v.push(2);
    v.push(2);

    // Function call
    AllSubsets(v);

// This code is contributed by mukesh07.
</script>
```

**Output**

```
{} {1} {1, 2} {1, 2, 2} {2} {2, 2}
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*