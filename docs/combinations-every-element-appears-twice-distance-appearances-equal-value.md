# 每个元素出现两次且外观之间的距离等于值

的组合

> 原文:[https://www . geesforgeks . org/combinations-每个元素-出现-两次-距离-出现-等值/](https://www.geeksforgeeks.org/combinations-every-element-appears-twice-distance-appearances-equal-value/)

给定一个正数 n，我们需要找到 2*n 个元素的所有组合，使得从 1 到 n 的每个元素恰好出现两次，并且其外观之间的距离恰好等于元素的值。

示例:

```
Input :  n = 3
Output : 3 1 2 1 3 2
         2 3 1 2 1 3
All elements from 1 to 3 appear
twice and distance between two
appearances is equal to value
of the element.

Input :  n = 4
Output : 4 1 3 1 2 4 3 2
         2 3 4 2 1 3 1 4

```

**解释**
我们可以用回溯法来解决这个问题。这个想法是对第一个元素的所有可能的组合进行递归探索，以检查它们是否会导致解决方案。如果当前的配置没有导致解决方案，我们会回溯。请注意，元素 k 可以放置在输出数组 I 中的位置 I 和(I+k+1)>= 0 和(i+k+1) < 2*n。

注意，对于像 2、5、6 等一些 n 值，元素的组合是不可能的。

## C++

```
// C++ program to find all combinations where every
// element appears twice and distance between
// appearances is equal to the value
#include <bits/stdc++.h>
using namespace std;

// Find all combinations that satisfies given constraints
void allCombinationsRec(vector<int> &arr, int elem, int n)
{
    // if all elements are filled, print the solution
    if (elem > n)
    {
        for (int i : arr)
            cout << i << " ";
        cout << endl;

        return;
    }

    // try all possible combinations for element elem
    for (int i = 0; i < 2*n; i++)
    {
        // if position i and (i+elem+1) are not occupied
        // in the vector
        if (arr[i] == -1 && (i + elem + 1) < 2*n &&
                arr[i + elem + 1] == -1)
        {
            // place elem at position i and (i+elem+1)
            arr[i] = elem;
            arr[i + elem + 1] = elem;

            // recurse for next element
            allCombinationsRec(arr, elem + 1, n);

            // backtrack (remove elem from position i and (i+elem+1) )
            arr[i] = -1;
            arr[i + elem + 1] = -1;
        }
    }
}

void allCombinations(int n)
{
    // create a vector of double the size of given number with
    vector<int> arr(2*n, -1);

    // all its elements initialized by 1
    int elem = 1;

    // start from element 1
    allCombinationsRec(arr, elem, n);
}

// Driver code
int main()
{
    // given number
    int n = 3;
    allCombinations(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all combinations where every
// element appears twice and distance between
// appearances is equal to the value

import java.util.Vector;

class Test
{
    // Find all combinations that satisfies given constraints
    static void allCombinationsRec(Vector<Integer> arr, int elem, int n)
    {
        // if all elements are filled, print the solution
        if (elem > n)
        {
            for (int i : arr)
                System.out.print(i + " ");
            System.out.println();

            return;
        }

        // try all possible combinations for element elem
        for (int i = 0; i < 2*n; i++)
        {
            // if position i and (i+elem+1) are not occupied
            // in the vector
            if (arr.get(i) == -1 && (i + elem + 1) < 2*n &&
                    arr.get(i + elem + 1) == -1)
            {
                // place elem at position i and (i+elem+1)
                arr.set(i, elem);
                arr.set(i + elem + 1, elem);

                // recurse for next element
                allCombinationsRec(arr, elem + 1, n);

                // backtrack (remove elem from position i and (i+elem+1) )
                arr.set(i, -1);
                arr.set(i + elem + 1, -1);
            }
        }
    }

    static void allCombinations(int n)
    {

        // create a vector of double the size of given number with
        Vector<Integer> arr = new Vector<>();

        for (int i = 0; i < 2*n; i++) {
            arr.add(-1);
        }

        // all its elements initialized by 1
        int elem = 1;

        // start from element 1
        allCombinationsRec(arr, elem, n);
    }

    // Driver method
    public static void main(String[] args)
    {
        // given number
        int n = 3;
        allCombinations(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find all combinations
# where every element appears twice and distance
# between appearances is equal to the value

# Find all combinations that
# satisfies given constraints
def allCombinationsRec(arr, elem, n):

    # if all elements are filled,
    # print the solution
    if (elem > n):

        for i in (arr):
            print(i, end = " ")

        print("")
        return

    # Try all possible combinations
    # for element elem
    for i in range(0, 2 * n):

        # if position i and (i+elem+1) are 
        # not occupied in the vector
        if (arr[i] == -1 and
           (i + elem + 1) < 2*n and
           arr[i + elem + 1] == -1):

            # place elem at position
            # i and (i+elem+1)
            arr[i] = elem
            arr[i + elem + 1] = elem

            # recurse for next element
            allCombinationsRec(arr, elem + 1, n)

            # backtrack (remove elem from
            # position i and (i+elem+1) )
            arr[i] = -1
            arr[i + elem + 1] = -1

def allCombinations(n):

    # create a vector of double
    # the size of given number with
    arr = [-1] * (2 * n)

    # all its elements initialized by 1
    elem = 1

    # start from element 1
    allCombinationsRec(arr, elem, n)

# Driver code
n = 3
allCombinations(n)

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find all combinations where every
// element appears twice and distance between
// appearances is equal to the value
using System;
using System.Collections.Generic;

class Test{

// Find all combinations that satisfies given
// constraints
static void allCombinationsRec(List<int> arr, int elem,
                               int n)
{

    // If all elements are filled, print the solution
    if (elem > n)
    {
        foreach(int i in arr)
            Console.Write(i + " ");

        Console.WriteLine();

        return;
    }

    // Try all possible combinations for element elem
    for(int i = 0; i < 2 * n; i++)
    {

        // If position i and (i+elem+1) are not
        // occupied in the vector
        if (arr[i] == -1 && (i + elem + 1) < 2 * n &&
                         arr[i + elem + 1] == -1)
        {

            // Place elem at position i and (i+elem+1)
            arr[i] = elem;
            arr[i + elem + 1] = elem;

            // Recurse for next element
            allCombinationsRec(arr, elem + 1, n);

            // Backtrack (remove elem from position i
            // and (i+elem+1) )
            arr[i] = -1;
            arr[i + elem + 1] = -1;
        }
    }
}

static void allCombinations(int n)
{

    // Create a vector of double the size of given
    // number with
    List<int> arr = new List<int>();

    for(int i = 0; i < 2 * n; i++)
    {
        arr.Add(-1);
    }

    // All its elements initialized by 1
    int elem = 1;

    // Start from element 1
    allCombinationsRec(arr, elem, n);
}

// Driver Code
public static void Main(string[] args)
{

    // Given number
    int n = 3;

    allCombinations(n);
}
}

// This code is contributed by ukasp
```

**输出:**

```
 3 1 2 1 3 2 
 2 3 1 2 1 3 
```

本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。