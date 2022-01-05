# 打印每个数组元素左侧出现的更大元素

> 原文:[https://www . geeksforgeeks . org/print-elements-elements-present-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on-on](https://www.geeksforgeeks.org/print-greater-elements-present-on-the-left-side-of-each-array-element/)

给定一个由 **N** 个不同整数组成的 [<u>数组</u>](https://www.geeksforgeeks.org/introduction-to-arrays/)**【arr】**，任务是为每个数组元素打印其左侧所有**个更大的元素**。

**示例:**

> **输入:** arr[] = {5，3，9，0，16，12}
> **输出:**
> 5:
> 3:5
> 9:
> 0:9 5 3
> 16:
> 12:16
> 
> **输入:** arr[] = {1，2，0}
> **输出:**
> 1:
> 2:
> 0: 2 1

**天真方法:**解决这个问题最简单的方法是遍历数组，对于每个数组元素，遍历它前面的所有元素，打印大于当前元素的元素。

## C++

```
// C++ program for Naive approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all greater elements on the left of each array element
void printGreater(vector<int>& arr)
{
    // store the size of array in variable n
    int n = arr.size();
    for (int i = 0; i < n; i++)
    {
        // result is used to store elements which are greater than current element present left side of current element
        vector<int> result;

        // traversing all the elements which are left of current element arr[i]

        for (int j = i - 1; j >= 0; j--)
        {
            //checking whether arr[j] (left element) is greater than current element or not
            // if yes then insert the element to the result vector
            if (arr[j] > arr[i])
            {
                result.push_back(arr[j]);
            }
        }
        cout << arr[i] << ": ";

        //printing all the elements present in result vector
        for (int k = 0; k < result.size(); k++)
        {
            cout << result[k] << " ";
        }
        cout << endl;
    }
}

//Driver Code
int main()
{
    vector<int> arr{5, 3, 9, 0, 16, 12};
    printGreater(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for Naive approach
import java.util.*;

class GFG{

  // Function to print all greater elements on the left of each array element
  static void printGreater(ArrayList<Integer> arr)
  {
    // store the size of array in variable n
    int n = arr.size();
    for (int i = 0; i < n; i++)
    {

      // result is used to store elements which
      // are greater than current element present
      // left side of current element
      ArrayList<Integer> result
        = new ArrayList<Integer>();

      // traversing all the elements which
      // are left of current element arr[i]

      for (int j = i - 1; j >= 0; j--)
      {
        // checking whether arr[j] (left element) is
        // greater than current element or not
        // if yes then insert the element to the result vector
        if (arr.get(j) > arr.get(i))
        {
          result.add(arr.get(j));
        }
      }
      System.out.print(arr.get(i) + ": ");

      // printing all the elements present in result vector
      for (int k = 0; k < result.size(); k++)
      {
        System.out.print(result.get(k) +" ");
      }
      System.out.println();
    }
  }

  // Driver Code
  public static void main(String args[])
  {
    ArrayList<Integer> arr = new ArrayList<Integer>(Arrays.asList(5, 3, 9, 0, 16, 12));
    printGreater(arr);
  }
}

// This code is contributed by bgangwar59.
```

## 蟒蛇 3

```
# Python3 program for Naive approach

# Function to print all greater
# elements on the left of each
# array element
def printGreater(arr):

    # Store the size of array
    # in variable n
    n = len(arr)

    for i in range(n):

        # Result is used to store elements
        # which are greater than current
        # element present left side of
        # current element
        result = []

        # Traversing all the elements
        # which are left of current
        # element arr[i]
        j = i - 1

        while(j >= 0):

            # Checking whether arr[j] (left element)
            # is greater than current element or not
            # if yes then insert the element to the
            # result vector
            if (arr[j] > arr[i]):
                result.append(arr[j])

            j -= 1

        print(arr[i], end = ": ")

        # Printing all the elements present
        # in result vector
        for k in range(len(result)):
            print(result[k], end = " ")

        print("\n", end = "")

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 3, 9, 0, 16, 12 ]

    printGreater(arr)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for Naive approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to print all greater elements on the left of
    // each array element
    static void printGreater(int[] arr)
    {

        // store the size of array in variable n
        int n = arr.Length;
        for (int i = 0; i < n; i++)
        {

            // result is used to store elements which are
            // greater than current element present left
            // side of current element
            List<int> result = new List<int>();

            // traversing all the elements which are left of
            // current element arr[i]

            for (int j = i - 1; j >= 0; j--)
            {

                // checking whether arr[j] (left element) is
                // greater than current element or not
                // if yes then insert the element to the
                // result vector
                if (arr[j] > arr[i]) {
                    result.Add(arr[j]);
                }
            }
            Console.Write(arr[i] + ": ");

            // printing all the elements present in result
            // vector
            for (int k = 0; k < result.Count; k++) {
                Console.Write(result[k] + " ");
            }
            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 5, 3, 9, 0, 16, 12 };
        printGreater(arr);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // Javascript program for Naive approach

    // Function to print all greater elements on the left of
    // each array element
    function printGreater(arr)
    {

        // store the size of array in variable n
        let n = arr.length;
        for (let i = 0; i < n; i++)
        {

            // result is used to store elements which are
            // greater than current element present left
            // side of current element
            let result = [];

            // traversing all the elements which are left of
            // current element arr[i]

            for (let j = i - 1; j >= 0; j--)
            {

                // checking whether arr[j] (left element) is
                // greater than current element or not
                // if yes then insert the element to the
                // result vector
                if (arr[j] > arr[i]) {
                    result.push(arr[j]);
                }
            }
            document.write(arr[i] + ": ");

            // printing all the elements present in result
            // vector
            for (let k = 0; k < result.length; k++) {
                document.write(result[k] + " ");
            }
            document.write("</br>");
        }
    }

    let arr = [ 5, 3, 9, 0, 16, 12 ];
      printGreater(arr);

    // This code is contributed by mukesh07.
</script>
```

**Output**

```
5: 
3: 5 
9: 
0: 9 3 5 
16: 
12: 16 
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)

**高效方法:**为了优化上述方法，想法是利用一个[自平衡二分搜索法树](https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/)。[c++中的 Set](https://www.geeksforgeeks.org/set-in-cpp-stl/)是使用自平衡 BST 实现的，可以用来解决这个问题。按照以下步骤解决问题:

*   初始化一个[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)和**集**，以非递减顺序存储元素。
*   [在索引 **0** 到**N–1**上遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下操作:
    *   [将**arr【I】**插入到集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)T4 中。
    *   [从集合](https://www.geeksforgeeks.org/setbegin-setend-c-stl/)开始迭代到 **p** 并打印集合中的元素。

**以下是上述方法的实现:**

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all greater elements
// on the left of each array element
void printGreater(vector<int>& arr)
{
    int n = arr.size();

    // Set to implement
    // self-balancing BSTs
    set<int, greater<int> > s;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Insert the current
        // element into the set
        auto p = s.insert(arr[i]);
        auto j = s.begin();

        cout << arr[i] << ": ";

        // Iterate through the set
        while (j != p.first) {

            // Print the element
            cout << *j << " ";
            j++;
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    vector<int> arr{ 5, 3, 9, 0, 16, 12 };
    printGreater(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to print all greater elements
// on the left of each array element
static void printGreater(int arr[])
{
    int n = arr.length;

    // Set to implement
    // self-balancing BSTs
    TreeSet<Integer> s = new TreeSet<>(
        Collections.reverseOrder());

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Insert the current
        // element into the set
        s.add(arr[i]);

        System.out.print(arr[i] + ": ");

        // Iterate through the set
        for(int v : s)
        {
            if (v == arr[i])
                break;

            // Print the element
            System.out.print(v + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 3, 9, 0, 16, 12 };
    printGreater(arr);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print all greater elements
# on the left of each array element
def printGreater(arr):
    n = len(arr)

    # Set to implement
    # self-balancing BSTs
    s = set([])

    # Traverse the array
    for i in range(n):

        # Insert the current
        # element into the set
        s.add(arr[i])

        print(arr[i], ": ", sep = "", end = "")
        temp = list(s)
        temp.sort()
        temp.reverse()

        # Iterate through the set
        for v in range(len(temp)):
            if (temp[v] == arr[i]):
                break

            # Print the element
            print(temp[v], end = " ")
        print()

arr = [5, 3, 9, 0, 16, 12]
printGreater(arr)

# This code is contributed by divyesh072019.
```

## C#

```
// C# Program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to print all greater elements
    // on the left of each array element
    static void printGreater(int[] arr)
    {
        int n = arr.Length;

        // Set to implement
        // self-balancing BSTs
        HashSet<int> s = new HashSet<int>();

        // Traverse the array
        for(int i = 0; i < n; i++)
        {

            // Insert the current
            // element into the set
            s.Add(arr[i]);

            Console.Write(arr[i] + ": ");
            List<int> temp = new List<int>();
            // Iterate through the set
            foreach(int v in s)
            {
                temp.Add(v);
            }
            temp.Sort();
            temp.Reverse();

            // Iterate through the set
            for(int v = 0; v < temp.Count; v++)
            {
                if (temp[v] == arr[i])
                {
                    break;
                }

                // Print the element
                Console.Write(temp[v] + " ");
            }
            Console.WriteLine();
        }
    }

  // Driver code
  static void Main() {
    int[] arr = { 5, 3, 9, 0, 16, 12 };
    printGreater(arr);
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print all greater elements
// on the left of each array element
function printGreater(arr)
{
    let n = arr.length;

    // Set to implement
    // self-balancing BSTs
    let s = new Set();

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

        // Insert the current
        // element into the set
        s.add(arr[i]);

        document.write(arr[i] + ": ");
         let temp=Array.from(s).sort(function(a,b){return b-a;});

        // Iterate through the set
        for(let v=0;v< temp.length;v++)
        {
            if (temp[v] == arr[i])
                break;

            // Print the element
            document.write(temp[v] + " ");
        }
        document.write("<br>");
    }
}

// Driver Code
let arr=[5, 3, 9, 0, 16, 12];
printGreater(arr);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
5: 
3: 5 
9: 
0: 9 5 3 
16: 
12: 16 
```

***时间复杂度**:O(N<sup>2</sup>)*
***辅助空间:** O(N)*