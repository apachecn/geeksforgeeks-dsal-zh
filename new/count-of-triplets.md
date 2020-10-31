# 三元组计数

> 原文：[https://www.geeksforgeeks.org/count-of-triplets/](https://www.geeksforgeeks.org/count-of-triplets/)

给定平面中`N`个点，以 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的形式，以使每一行都包含两个整数`L`和`R`，`L`属于`x`坐标，`R`属于`y`坐标。 任务是计算点的三元组（例如`a, b, c`），以使`a, b`之间的距离等于`a, c`之间的距离。

**注意**：三元组的顺序很重要。

**示例**：

> **输入**：`arr[] = {{0, 0}, {1, 0}, {2, 0}}`
>
> **输出**：2
>
> **说明**：
>
> 可能的三元组为：`{{1, 0}, {0, 0}, {2, 0}}`和`{{1, 0}, {2, 0}, {0, 0}}`
> 
> **输入**：`arr[] = {{1, 0}, {1, -1}, {2, 3}, {4, 3}, {4, 4}}`
>
> **输出**：0
>
> **说明**：
>
> 不存在这样的三元组。

**方法**：

1.  为每个点计算到其他所有点的距离。

2.  在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中存储点到其他点的中间距离（例如 **d** ）。

3.  如果映射已经具有相同的距离，则三元组的数量是映射中为`d`存储的值的两倍。

4.  更新映射中当前距离的计数。

下面是上述的实现：

## C++

```cpp

// C++ program for the above appproach
#include <bits/stdc++.h>
using namespace std;

// Function to count the triplets
int countTriplets(vector<vector<int> >& p)
{

    // Intialise count
    int count = 0;

    // Traverse the arr[]
    for (int i = 0; i < p.size(); i++) {

        // Map to store the distance between
        // every pairs p[i] and p[j]
        unordered_map<int, int> d;

        for (int j = 0; j < p.size(); j++) {

            // Find the distance
            int dist = pow(p[j][1] - p[i][1], 2)
                       + pow(p[j][0] - p[i][0], 2);

            // If count of distance is greater
            // than 0, then find the count
            if (d[dist] > 0) {
                count += 2 * d[dist];
            }

            // Update the current count of the
            // distance
            d[dist]++;
        }
    }

    // Return the count of triplets
    return count;
}

// Driver Code
int main()
{

    // Set of points in plane
    vector<vector<int> > arr = { { 0, 0 },
                                 { 1, 0 },
                                 { 2, 0 } };

    // Function call
    cout << countTriplets(arr);
    return 0;
}

```

## Java

```java

// Java program for the above appproach
import java.util.*;
class GFG{

    // Function to count the triplets
    static int countTriplets(int p[][])
    {

        // Intialise count
        int count = 0;

        // Traverse the arr[]
        for (int i = 0; i < p.length; i++) {

            // Map to store the distance between
            // every pairs p[i] and p[j]
            HashMap<Integer, Integer> d = new HashMap<Integer,Integer>();

            for (int j = 0; j < p.length; j++) {

                // Find the distance
                int dist = (int)(Math.pow(p[j][1] - p[i][1], 2)+ Math.pow(p[j][0] - p[i][0], 2));

                // If count of distance is greater
                // than 0, then find the count

                if (d.containsKey(dist) && d.get(dist) > 0) {
                    count += 2 * d.get(dist);
                }

                // Update the current count of the
                // distance
                if (d.containsKey(dist)){
                    d.put(dist,d.get(dist)+1);
                }
                else
                    d.put(dist,1);
            }
        }

        // Return the count of triplets
        return count;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Set of points in plane
        int arr[][] = { { 0, 0 },
                                    { 1, 0 },
                                    { 2, 0 } };

        // Function call
        System.out.println(countTriplets(arr));

    }
}

// This code is contributed by AbhiThakur

```

## Python3

```py

# Python3 program for the above appproach

# Function to count the triplets
def countTriplets(p) :

    # Intialise count
    count = 0;

    # Traverse the arr[]
    for i in range(len(p)) :

        # Map to store the distance between
        # every pairs p[i] and p[j]
        d = {};

        for j in range(len(p)) :

            # Find the distance
            dist = pow(p[j][1] - p[i][1], 2) + \
                    pow(p[j][0] - p[i][0], 2);

            if dist not in d :
                d[dist] = 0;

            # If count of distance is greater
            # than 0, then find the count
            if (d[dist] > 0) :
                count += 2 * d[dist];

            # Update the current count of the
            # distance
            d[dist] += 1;

    # Return the count of triplets
    return count;

# Driver Code
if __name__ == "__main__" :

    # Set of points in plane
    arr = [ [ 0, 0 ],
            [ 1, 0 ],
            [ 2, 0 ] ];

    # Function call
    print(countTriplets(arr));

# This code is contributed by Yash_R

```

## C#

```cs

// C# program for the above appproach  
using System;
using System.Collections.Generic;

class GFG{

// Function to count the triplets 
static int countTriplets(int[,] p) 
{ 

    // Intialise count 
    int count = 0; 

    // Traverse the arr[] 
    for(int i = 0; i < p.GetLength(0); i++)
    { 

        // Map to store the distance between 
        // every pairs p[i] and p[j] 
        Dictionary<int, 
                   int> d = new Dictionary<int,
                                           int>();

        for(int j = 0; j < p.GetLength(0); j++)
        { 

            // Find the distance 
            int dist = (int)(Math.Pow(p[j, 1] - 
                                      p[i, 1], 2) + 
                             Math.Pow(p[j, 0] - 
                                      p[i, 0], 2)); 

            // If count of distance is greater 
            // than 0, then find the count 
            if (d.ContainsKey(dist) && d[dist] > 0) 
            { 
                count += 2 * d[dist]; 
            } 

            // Update the current count of the 
            // distance 
            if (d.ContainsKey(dist))
            { 
                d[dist]++; 
            } 
            else
                d.Add(dist, 1); 
        } 
    } 

    // Return the count of triplets 
    return count; 
} 

// Driver code
static void Main() 
{

    // Set of points in plane 
    int[,] arr = new int [3, 2]{ { 0, 0 }, 
                                 { 1, 0 }, 
                                 { 2, 0 } }; 

    // Function call 
    Console.WriteLine(countTriplets(arr));
}
}

// This code is contributed by divyeshrabadiya07

```

**Output:** 

```
2

```



* * *

* * *



