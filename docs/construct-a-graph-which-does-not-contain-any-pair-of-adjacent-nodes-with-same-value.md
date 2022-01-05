# 构建一个不包含任何一对具有相同值的相邻节点的图

> 原文:[https://www . geesforgeks . org/construct-a-graph-其中不包含任何一对具有相同值的相邻节点/](https://www.geeksforgeeks.org/construct-a-graph-which-does-not-contain-any-pair-of-adjacent-nodes-with-same-value/)

给定一个由 **N** 个字符组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是生成 **N** 个节点和**(N–1)**条边的[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，使得每个节点 **i** 与字符**arr【I】**相关联，并且没有两个相邻节点具有相同的值。如果可以做出这样的图形，那么用成对的边打印**“可能”**。否则，打印**“不可能”**。

**示例:**

> **输入:** N = 5，arr[] = {'a '，' b '，' a '，' b '，' c'}
> **输出:**“可能的”
> 1–2
> 1–4
> 1–5
> 5–3
> **解释:**
> 一个可以构造满足给定条件的可能图形如下:
> 
> ![](img/46aba9370c10c4a45a7ee135be648621.png)
> 
> **输入:** N = 3，arr[] = {'z '，' z '，' z'}
> **输出:**“不可能”

**方法:**为了构建一个图，使得没有相邻的节点具有相同的值，想法是检查是否至少有**两个唯一的值**存在。如果发现是真的，就可以构造这样一个图。请遵循以下步骤:

*   检查每个节点上存在的所有值，如果所有节点值都是相同的**，则**不可能**构建图形。**
*   **如果任意两个值**不同**，总会有办法构造这样的图。**
*   **现在，选择任意两个唯一值，将所有其他值的出现连接到除值本身之外的第一个唯一值。**
*   **存储第一个唯一值出现的**索引**，除了它的第一次出现，并将所有这些索引连接到第二个唯一值。**
*   **这样总会有办法构造出这样一个有**(N–1)**条边的图。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that prints the edges of
// the generated graph
void printConnections(
    vector<pair<int, int> > store,
    vector<int> ind, int ind1)
{
    // First print connections
    // stored in store[]
    for (auto pr : store) {
        cout << pr.first << " "
             << pr.second << "\n";
    }

    // Check if there is more than one
    // occurrence of 1st unique element
    if (ind.size() != 0) {

        // Print all other occurrence
        // of 1st unique element with
        // second unique element
        for (auto x : ind) {
            cout << ind1 << " "
                 << x + 1 << "\n";
        }
    }
}

// Function to construct the graph such
// that the every adjacent nodes have
// different value
void constructGraph(char arr[], int N)
{
    vector<int> ind;

    // Stores pair of edges formed
    vector<pair<int, int> > store;

    // Stores first unique occurrence
    char x = arr[0];

    int count = 0, ind1;

    for (int i = 1; i <= N - 1; ++i) {

        // Check for the second
        // unique occurrence
        if (arr[i] != x) {

            // Store indices of 2nd
            // unique occurrence
            ind1 = i + 1;

            // To check if arr has only
            // 1 unique element or not
            count++;

            // Store the connections of all
            // unique elements with Node 1
            store.push_back({ 1, i + 1 });
        }

        // If value at node (i + 1) is
        // same as value at Node 1 then
        // store its indices
        else {
            ind.push_back(i);
        }
    }

    // If count is zero then it's not
    // possible to construct the graph
    if (count == 0) {
        cout << "Not Possible";
    }

    // If more than 1 unique
    // element is present
    else {
        cout << "Possible"
             << "\n";

        // Print the edges
        printConnections(store, ind, ind1);
    }
}

// Driver Code
int main()
{
    int N = 5;

    // Given array having node values
    char arr[] = { 'a', 'b', 'a', 'b', 'c' };

    // Function Call
    constructGraph(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static class pair
{
  int first, second;
  public pair(int first,
              int second) 
  {
    this.first = first;
    this.second = second;
  }   
}

// Function that prints the edges of
// the generated graph
static void printConnections(Vector<pair > store,
                             Vector<Integer> ind,
                             int ind1)
{
  // First print connections
  // stored in store[]
  for (pair pr : store)
  {
    System.out.print(pr.first + " " +
                     pr.second + "\n");
  }

  // Check if there is more than one
  // occurrence of 1st unique element
  if (ind.size() != 0)
  {
    // Print all other occurrence
    // of 1st unique element with
    // second unique element
    for (int x : ind)
    {
      System.out.print(ind1 + " " +
                      (x + 1) + "\n");
    }
  }
}

// Function to construct the graph such
// that the every adjacent nodes have
// different value
static void constructGraph(char arr[],
                           int N)
{
  Vector<Integer> ind = new Vector<>();

  // Stores pair of edges formed
  Vector<pair > store = new Vector<>();

  // Stores first unique occurrence
  char x = arr[0];

  int count = 0;
  int ind1=-1;

  for (int i = 1; i <= N - 1; ++i)
  {
    // Check for the second
    // unique occurrence
    if (arr[i] != x)
    {
      // Store indices of 2nd
      // unique occurrence
      ind1 = i + 1;

      // To check if arr has only
      // 1 unique element or not
      count++;

      // Store the connections of all
      // unique elements with Node 1
      store.add(new pair(1, i + 1 ));
    }

    // If value at node (i + 1) is
    // same as value at Node 1 then
    // store its indices
    else
    {
      ind.add(i);
    }
  }

  // If count is zero then it's not
  // possible to construct the graph
  if (count == 0)
  {
    System.out.print("Not Possible");
  }

  // If more than 1 unique
  // element is present
  else
  {
    System.out.print("Possible" +
                     "\n");

    // Print the edges
    printConnections(store,
                     ind, ind1);
  }
}

// Driver Code
public static void main(String[] args)
{
  int N = 5;

  // Given array having
  // node values
  char arr[] = {'a', 'b',
                'a', 'b', 'c'};

  // Function Call
  constructGraph(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function that prints the edges of
# the generated graph
def printConnections(store, ind, ind1):

    # First print connections
    # stored in store[]
    for pr in store:
        print(pr[0], pr[1])

    # Check if there is more than one
    # occurrence of 1st unique element
    if (len(ind) != 0):

        # Print all other occurrence
        # of 1st unique element with
        # second unique element
        for x in ind:
            print(ind1, x + 1)

# Function to construct the graph such
# that the every adjacent nodes have
# different value
def constructGraph(arr, N):

    ind = []

    # Stores pair of edges formed
    store = []

    # Stores first unique occurrence
    x = arr[0]

    count, ind1 = 0, 0

    for i in range(1, N):

        # Check for the second
        # unique occurrence
        if (arr[i] != x):

            # Store indices of 2nd
            # unique occurrence
            ind1 = i + 1

            # To check if arr has only
            # 1 unique element or not
            count += 1

            # Store the connections of all
            # unique elements with Node 1
            store.append([1, i + 1])

            # If value at node (i + 1) is
            # same as value at Node 1 then
            # store its indices
        else:
            ind.append(i)

    # If count is zero then it's not
    # possible to construct the graph
    if count == 0:
        print("Not Possible")
    else:

        # If more than 1 unique
        # element is present
        print("Possible")

        # Print the edges
        printConnections(store, ind, ind1)

# Driver Code
if __name__ == '__main__':

    N = 5

    # Given array having node values
    arr = [ 'a', 'b', 'a', 'b', 'c' ]

    # Function Call
    constructGraph(arr, N)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

public class pair
{
  public int first,
  second;
  public pair(int first,
              int second) 
  {
    this.first = first;
    this.second = second;
  }   
}

// Function that prints the edges of
// the generated graph
static void printConnections(List<pair > store,
                             List<int> ind,
                             int ind1)
{
  // First print connections
  // stored in store[]
  foreach (pair pr in store)
  {
    Console.Write(pr.first + " " +
                  pr.second + "\n");
  }

  // Check if there is more than one
  // occurrence of 1st unique element
  if (ind.Count != 0)
  {
    // Print all other occurrence
    // of 1st unique element with
    // second unique element
    foreach (int x in ind)
    {
      Console.Write(ind1 + " " +
                   (x + 1) + "\n");
    }
  }
}

// Function to construct the graph such
// that the every adjacent nodes have
// different value
static void constructGraph(char []arr,
                           int N)
{
  List<int> ind = new List<int>();

  // Stores pair of edges formed
  List<pair > store = new List<pair>();

  // Stores first unique occurrence
  char x = arr[0];

  int count = 0;
  int ind1=-1;

  for (int i = 1; i <= N - 1; ++i)
  {
    // Check for the second
    // unique occurrence
    if (arr[i] != x)
    {
      // Store indices of 2nd
      // unique occurrence
      ind1 = i + 1;

      // To check if arr has only
      // 1 unique element or not
      count++;

      // Store the connections of all
      // unique elements with Node 1
      store.Add(new pair(1, i + 1 ));
    }

    // If value at node (i + 1) is
    // same as value at Node 1 then
    // store its indices
    else
    {
      ind.Add(i);
    }
  }

  // If count is zero then it's not
  // possible to construct the graph
  if (count == 0)
  {
    Console.Write("Not Possible");
  }

  // If more than 1 unique
  // element is present
  else
  {
    Console.Write("Possible" +
                     "\n");

    // Print the edges
    printConnections(store,
                     ind, ind1);
  }
}

// Driver Code
public static void Main(String[] args)
{
  int N = 5;

  // Given array having
  // node values
  char []arr = {'a', 'b',
                'a', 'b', 'c'};

  // Function Call
  constructGraph(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## **java 描述语言**

```
<script>

// Javascript program for the
// above approach

// Function that prints the edges of
// the generated graph
function printConnections(store, ind, ind1)
{

    // First print connections
    // stored in store[]
    for(let pr = 0; pr < store.length; pr++)
    {
        document.write(store[pr][0] + " " +
                       store[pr][1] + "<br>");
    }

    // Check if there is more than one
    // occurrence of 1st unique element
    if (ind.length != 0)
    {

        // Print all other occurrence
        // of 1st unique element with
        // second unique element
        for(let x = 0; x < ind.length; x++)
        {
            document.write(ind1 + " " +
                        (ind[x] + 1) + "<br>");
        }
    }
}

// Function to construct the graph such
// that the every adjacent nodes have
// different value
function constructGraph(arr, N)
{
    let ind = [];

    // Stores pair of edges formed
    let store = [];

    // Stores first unique occurrence
    let x = arr[0];

    let count = 0;
    let ind1 = -1;

    for(let i = 1; i <= N - 1; ++i)
    {

        // Check for the second
        // unique occurrence
        if (arr[i] != x)
        {

            // Store indices of 2nd
            // unique occurrence
            ind1 = i + 1;

            // To check if arr has only
            // 1 unique element or not
            count++;

            // Store the connections of all
            // unique elements with Node 1
            store.push([1, i + 1]);
        }

        // If value at node (i + 1) is
        // same as value at Node 1 then
        // store its indices
        else
        {
            ind.push(i);
        }
    }

    // If count is zero then it's not
    // possible to construct the graph
    if (count == 0)
    {
        document.write("Not Possible");
    }

    // If more than 1 unique
    // element is present
    else
    {
        document.write("Possible" + "<br>");

        // Print the edges
        printConnections(store, ind, ind1);
    }
}

// Driver Code
let N = 5;

// Given array having
// node values
let arr = [ 'a', 'b', 'a', 'b', 'c' ];

// Function Call
constructGraph(arr, N);

// This code is contributed by unknown2108

</script>
```

****Output:** 

```
Possible
1 2
1 4
1 5
5 3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**