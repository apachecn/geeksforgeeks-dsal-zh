# 在一个数组中找到两个和相等的非重叠对

> 原文:[https://www . geeksforgeeks . org/find-两个非重叠对-具有相等的阵列总和/](https://www.geeksforgeeks.org/find-two-non-overlapping-pairs-having-equal-sum-in-an-array/)

给定一个未排序的整数数组。任务是找到任意两个和相等的非重叠对。
如果两对的所有元素都在不同的索引处，则称这两对是不重叠的。即配对 **(A <sub>i</sub> 、A <sub>j</sub> )** 和配对 **(A <sub>m</sub> 、A <sub>n</sub> )** 如果 **i ≠ j ≠ m ≠ n** 则称不重叠。

**示例**:

```
Input: arr[] = {8, 4, 7, 8, 4}
Output: Pair First(4, 8)
        Pair Second (8, 4)

Input: arr[] = {8, 4, 7, 4}
Output: No such non-overlapping pairs present.
Note: (8, 4) and (8, 4) forms overlapping pair
as index of 8 is same in both pairs.

```

其思想是使用键值对的映射来存储总和的所有出现。映射中的键将存储总和，相应的值将是具有该总和的一对索引(I，j)的列表。

*   其思想是遍历数组并生成所有可能的对。
*   如果找到一个新的和，将其直接插入到映射中，否则检查之前遇到的具有该和的任何对是否与当前对不重叠。
*   如果没有，打印两对。

下面是上述方法的实现:

## C++

```
// C++ programs to find two non-overlapping
// pairs having equal sum in an Array

#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

typedef pair<int, int> Pair;

// Function to find two non-overlapping
// with same sum in an array
void findPairs(int arr[], int n)
{
    // first create an empty map
    // key -> which is sum of a pair of
    // elements in the array
    // value -> vector storing index of
    // every pair having that sum
    unordered_map<int, vector<Pair> > map;

    // consider every pair (arr[i], arr[j])
    // and where (j > i)
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // calculate sum of current pair
            int sum = arr[i] + arr[j];

            // if sum is already present in the map
            if (map.find(sum) != map.end()) {

                // check every pair having equal sum
                for (auto pair : map.find(sum)->second) {
                    int m = pair.first, n = pair.second;

                    // if pairs don't overlap,
                    // print them and return
                    if ((m != i && m != j) && (n != i && n != j)) {
                        cout << "Pair First(" << arr[i] << ", "
                             << arr[j] << ")\nPair Second ("
                             << arr[m] << ", " << arr[n] << ")";
                        return;
                    }
                }
            }

            // Insert current pair into the map
            map[sum].push_back({ i, j });
        }
    }

    // If no such pair found
    cout << "No such non-overlapping pairs present";
}

// Driver Code
int main()
{
    int arr[] = { 8, 4, 7, 8, 4 };
    int size = sizeof(arr) / sizeof(arr[0]);

    findPairs(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find two non-overlapping
// pairs having equal sum in an Array

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

// Declare a pair
class Pair {
    public int x, y;

    Pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class GFG {
    // Function to find two non-overlapping
    // pairs with same sum in an array
    public static void findPairs(int[] A)
    {
        // first create an empty map
        // key -> which is sum of a pair
        // of elements in the array
        // value -> list storing index of
        // every pair having that sum
        Map<Integer, List<Pair> > map = new HashMap<>();

        // consider every pair (A[i], A[j]) where (j > i)
        for (int i = 0; i < A.length - 1; i++) {
            for (int j = i + 1; j < A.length; j++) {

                // calculate sum of current pair
                int sum = A[i] + A[j];

                // if sum is already present in the map
                if (map.containsKey(sum)) {

                    // check every pair having desired sum
                    for (Pair pair : map.get(sum)) {
                        int x = pair.x;
                        int y = pair.y;

                        // if pairs don't overlap, print
                        // them and return
                        if ((x != i && x != j) && (y != i && y != j)) {
                            System.out.println("Pair First(" + A[i] + ", "
                                               + A[j] + ")");

                            System.out.println("Pair Second (" + A[x] + ", "
                                               + A[y] + ")");

                            return;
                        }
                    }
                }

                // Insert current pair into the map
                map.putIfAbsent(sum, new ArrayList<>());
                map.get(sum).add(new Pair(i, j));
            }
        }

        System.out.print("No such non-overlapping pairs present");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] A = { 8, 4, 7, 8, 4 };

        findPairs(A);
    }
}
```

## 蟒蛇 3

```
# Python3 programs to find two non-overlapping
# pairs having equal Sum in an Array

# Function to find two non-overlapping
# with same Sum in an array
def findPairs(arr, size):

    # first create an empty Map
    # key -> which is Sum of a pair of
    # elements in the array
    # value -> vector storing index of
    # every pair having that Sum
    Map = {}

    # consider every pair (arr[i], arr[j])
    # and where (j > i)
    for i in range(0, size - 1):
        for j in range(i + 1, size):

            # calculate Sum of current pair
            Sum = arr[i] + arr[j]

            # if Sum is already present in the Map
            if Sum in Map:

                # check every pair having equal Sum
                for pair in Map[Sum]:
                    m, n = pair

                    # if pairs don't overlap,
                    # print them and return
                    if ((m != i and m != j) and
                        (n != i and n != j)):

                        print("Pair First ({}, {})".
                               format(arr[i], arr[j]))
                        print("Pair Second ({}, {})".
                               format(arr[m], arr[n]))
                        return

            # Insert current pair into the Map
            if Sum not in Map:
                Map[Sum] = []
            Map[Sum].append((i, j))

    # If no such pair found
    print("No such non-overlapping pairs present")

# Driver Code
if __name__ == "__main__":

    arr = [8, 4, 7, 8, 4]
    size = len(arr)

    findPairs(arr, size)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find two non-overlapping
// pairs having equal sum in an Array
using System;
using System.Collections.Generic;

// Declare a pair
class Pair
{
    public int x, y;

    public Pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class GFG{

// Function to find two non-overlapping
// pairs with same sum in an array
public static void findPairs(int[] A)
{

    // First create an empty map
    // key -> which is sum of a pair
    // of elements in the array
    // value -> list storing index of
    // every pair having that sum
    Dictionary<int,
               List<Pair>> map = new Dictionary<int,
                                                List<Pair>>();

    // Consider every pair (A[i], A[j])
    // where (j > i)
    for(int i = 0; i < A.Length - 1; i++)
    {
        for(int j = i + 1; j < A.Length; j++)
        {

            // Calculate sum of current pair
            int sum = A[i] + A[j];

            // If sum is already present in the map
            if (map.ContainsKey(sum))
            {

                // Check every pair having desired sum
                foreach(Pair pair in map[sum])
                {
                    int x = pair.x;
                    int y = pair.y;

                    // If pairs don't overlap, print
                    // them and return
                    if ((x != i && x != j) &&
                        (y != i && y != j))
                    {
                        Console.WriteLine("Pair First(" + A[i] +
                                          ", " + A[j] + ")");

                        Console.WriteLine("Pair Second (" + A[x] +
                                          ", " + A[y] + ")");

                        return;
                    }
                }
            }

            // Insert current pair into the map
            map[sum] = new List<Pair>();
            map[sum].Add(new Pair(i, j));
        }
    }

    Console.Write("No such non-overlapping pairs present");
}

// Driver Code
public static void Main(String[] args)
{
    int[] A = { 8, 4, 7, 8, 4 };

    findPairs(A);
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
Pair First(4, 8)
Pair Second (8, 4)

```