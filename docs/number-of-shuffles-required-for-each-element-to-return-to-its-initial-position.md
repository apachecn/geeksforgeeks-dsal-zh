# 每个元素返回其初始位置所需的洗牌次数

> 原文:[https://www . geesforgeks . org/每个元素返回初始位置所需的洗牌次数/](https://www.geeksforgeeks.org/number-of-shuffles-required-for-each-element-to-return-to-its-initial-position/)

给定一个整数数组 **arr[]** ，该数组包含从 **1** 到 **N** 的整数排列。让 **K[]** 成为某种任意数组。数组 arr[i]中的每个元素都表示元素的索引，该元素最初位于数组 K[]中的位置“I”。任务是找到需要在 K[]上执行的洗牌次数，以使元素回到初始位置。
**注:**给出了必须对 **K[]** (即)进行至少 1 次混洗，对于数组 K[]中的所有元素，必须将最初位于数组 **K[]** 中“I”位置的元素放入索引**arr【I】**中至少一次。
**举例:**

> **输入:** arr[] = {3，4，1，2}
> **输出:** 2 2 2 2
> **解释:**
> 让初始数组 B[] = {5，6，7，8}。因此:
> 第一次洗牌后:第一个元素会去第三个位置，第二个元素会去第四个位置。因此，B[] = {7，8，5，6}。
> 第二次洗牌后:第一个元素会到第三个位置，第二个元素会到第四个位置。因此，B[] = {5，6，7，8}。
> 因此，所有元素回到同一初始位置的洗牌次数为 2。
> **输入:** arr[] = {4，6，2，1，5，3}
> **输出:**2 3 2 1 3

**天真方法:**这个问题的天真方法是计算每个元素所需的洗牌次数。这种方法的时间复杂度是 **O(N <sup>2</sup> )** 。
**有效方法:**解决这个问题的有效方法是首先计算问题中的循环数。同一周期中的元素具有相同数量的洗牌。例如，在给定的数组 arr[]中= {3，4，1，2}:

*   每次洗牌时，第一个元素总是排在第三位，第三个元素总是排在第一位。
*   因此，可以得出结论，这两个元素都处于一个循环中。因此，无论数组**是什么，两个元素的混洗次数都是 2。**
*   因此，想法是找到数组中这种循环的数量，并跳过这些元素。

以下是上述方法的实现:

## C++

```
// C++ program to find the number of
// shuffles required for each element
// to return to its initial position

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// shuffles required for each element
// to return to its initial position
void countShuffles(int* A, int N)
{
    // Initialize array to store
    // the counts
    int count[N];

    // Initialize visited array to
    // check if visited before or not
    bool vis[N];
    memset(vis, false, sizeof(vis));

    // Making the array 0-indexed
    for (int i = 0; i < N; i++)
        A[i]--;

    for (int i = 0; i < N; i++) {
        if (!vis[i]) {

            // Initialize vector to store the
            // elements in the same cycle
            vector<int> cur;

            // Initialize variable to store
            // the current element
            int pos = i;

            // Count number of shuffles
            // for current element
            while (!vis[pos]) {

                // Store the elements in
                // the same cycle
                cur.push_back(pos);

                // Mark visited
                vis[pos] = true;

                // Make the shuffle
                pos = A[pos];
            }

            // Store the result for all the
            // elements in the same cycle
            for (auto el : cur)
                count[el] = cur.size();
        }
    }

    // Print the result
    for (int i = 0; i < N; i++)
        cout << count[i] << " ";
    cout << endl;
}

// Driver code
int main()
{
    int arr[] = { 4, 6, 2, 1, 5, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    countShuffles(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of
// shuffles required for each element
// to return to its initial position
import java.util.*;

class GFG {

// Function to count the number of
// shuffles required for each element
// to return to its initial position
static void countShuffles(int[] A, int N)
{

    // Initialize array to store
    // the counts
    int[] count = new int[N];

    // Initialize visited array to
    // check if visited before or not
    boolean[] vis = new boolean[N];

    // Making the array 0-indexed
    for(int i = 0; i < N; i++)
       A[i]--;

    for(int i = 0; i < N; i++)
    {
       if (!vis[i])
       {

           // Initialize vector to store the
           // elements in the same cycle
           Vector<Integer> cur = new Vector<>(); 

           // Initialize variable to store
           // the current element
           int pos = i;

           // Count number of shuffles
           // for current element
           while (!vis[pos])
           {

               // Store the elements in
               // the same cycle
               cur.add(pos);

               // Mark visited
               vis[pos] = true;

               // Make the shuffle
               pos = A[pos];
            }

            // Store the result for all the
            // elements in the same cycle
            for(int k = 0; k < cur.size(); k++)
               count[cur.get(k)] = cur.size();
       }
    }

    // Print the result
    for(int k = 0; k < N; k++)
       System.out.print(count[k] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 2, 1, 5, 3 };
    int N = arr.length;

    countShuffles(arr, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the number of
# shuffles required for each element
# to return to its initial position

# Function to count the number of
# shuffles required for each element
# to return to its initial position
def countShuffles(A, N):

    # Initialize array to store
    # the counts
    count = [0] * N

    # Initialize visited array to
    # check if visited before or not
    vis = [False] * N

    # Making the array 0-indexed
    for i in range(N):
        A[i] -= 1

    for i in range(N):
        if (not vis[i]):

            # Initialize vector to store the
            # elements in the same cycle
            cur = []

            # Initialize variable to store
            # the current element
            pos = i

            # Count number of shuffles
            # for current element
            while (not vis[pos]):

                # Store the elements in
                # the same cycle
                cur.append(pos)

                # Mark visited
                vis[pos] = True

                # Make the shuffle
                pos = A[pos]

            # Store the result for all the
            # elements in the same cycle
            for el in cur:
                count[el] = len(cur)

    # Print the result
    for i in range(N):
        print(count[i], end = " ")
    print()

# Driver code
if __name__ == "__main__":

    arr = [ 4, 6, 2, 1, 5, 3 ]
    N = len(arr)
    countShuffles(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the number of
// shuffles required for each element
// to return to its initial position
using System;
using System.Collections;

class GFG{

// Function to count the number of
// shuffles required for each element
// to return to its initial position
static void countShuffles(int[] A, int N)
{

    // Initialize array to store
    // the counts
    int[] count = new int[N];

    // Initialize visited array to
    // check if visited before or not
    bool[] vis = new bool[N];

    // Making the array 0-indexed
    for(int i = 0; i < N; i++)
        A[i]--;

    for(int i = 0; i < N; i++)
    {
        if (!vis[i])
        {

            // Initialize vector to store the
            // elements in the same cycle
            ArrayList cur = new ArrayList();

            // Initialize variable to store
            // the current element
            int pos = i;

            // Count number of shuffles
            // for current element
            while (!vis[pos])
            {

                // Store the elements in
                // the same cycle
                cur.Add(pos);

                // Mark visited
                vis[pos] = true;

                // Make the shuffle
                pos = A[pos];
            }

            // Store the result for all the
            // elements in the same cycle
            for(int k = 0; k < cur.Count; k++)
                count[(int)cur[k]] = cur.Count;
        }
    }

    // Print the result
    for(int k = 0; k < N; k++)
        Console.Write(count[k] + " ");
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 4, 6, 2, 1, 5, 3 };
    int N = arr.Length;

    countShuffles(arr, N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to find the number of
// shuffles required for each element
// to return to its initial position

// Function to count the number of
// shuffles required for each element
// to return to its initial position
function countShuffles(A, N)
{

    // Initialize array to store
    // the counts
    var count = Array(N);

    // Initialize visited array to
    // check if visited before or not
    var vis = Array(N).fill(false);

    // Making the array 0-indexed
    for (var i = 0; i < N; i++)
        A[i]--;

    for (var i = 0; i < N; i++) {
        if (!vis[i]) {

            // Initialize vector to store the
            // elements in the same cycle
            var cur = [];

            // Initialize variable to store
            // the current element
            var pos = i;

            // Count number of shuffles
            // for current element
            while (!vis[pos]) {

                // Store the elements in
                // the same cycle
                cur.push(pos);

                // Mark visited
                vis[pos] = true;

                // Make the shuffle
                pos = A[pos];
            }

            // Store the result for all the
            // elements in the same cycle
            for( var e1 = 0; e1<cur.length; e1++)
            {
                count[cur[e1]]=cur.length;
            }

        }
    }

    // Print the result
    for (var i = 0; i < N; i++)
        document.write( count[i] + " ");
    document.write("<br>");
}

// Driver code
var arr = [ 4, 6, 2, 1, 5, 3 ];
var N = arr.length;
countShuffles(arr, N);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2 3 3 2 1 3
```

**时间复杂度:** *O(N)* ，其中 N 是数组的大小。