# 在面积增加的基础上对三角形的边进行排序

> 原文:[https://www . geeksforgeeks . org/按面积递增对三角形的边进行排序/](https://www.geeksforgeeks.org/sort-the-sides-of-triangle-on-the-basis-of-increasing-area/)

给定一个由 **N** 个三角形的边组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是根据面积的递增顺序对三角形的给定边进行排序。

**示例:**

> **输入:** arr[] = {{5，3，7}，{15，20，4}，{4，9，6}，{8，4，5}}
> **输出:** {{5，3，7}，{8，4，5}，{4，9，6}，{15，20，17}}
> **解释:**
> 以下是三角形的区域:
> 
> *   第一个三角形(5，3，7)的面积是 6.4。
> *   第二个三角形(15，20，4)的面积是 124.2。
> *   第三个三角形(4，9，6)的面积是 9.5。
> *   第四个三角形(8，4，5)的面积是 8.1。
> 
> 因此，按照区域的递增顺序对它们进行排序会将给定的数组修改为 6.4 {5，3，7}、8.1 {8，4，5}、9.5 {4，9，6}、124.2 {15，20，4}。
> 
> **输入:** arr[] = {{7，24，25}，{5，12，13}，{3，4，5}}
> **输出:** {{3，4，5}，{5，12，13}，{7，24，25}

**方法:**给定的可以通过将三角形的[区域的边存储在另一个数组中，然后](https://www.geeksforgeeks.org/c-program-find-area-triangle/)[按照存储区域的递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组进行排序，然后打印存储在另一个数组中的边作为结果来解决。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the sides of
// triangle in increasing order of area
void rearrangeTriangle(
    vector<vector<int> > arr, int N)
{
    // Stores the area of triangles with
    // their corresponding indices
    vector<pair<float, int> > area;

    for (int i = 0; i < N; i++) {

        // Find the area
        float a = (arr[i][0]
                   + arr[i][1]
                   + arr[i][2])
                  / 2.0;
        float Area = sqrt(abs(a * (a - arr[i][0])
                              * (a - arr[i][1])
                              * (a - arr[i][2])));

        area.push_back({ Area, i });
    }

    // Sort the area vector
    sort(area.begin(), area.end());

    // Resultant sides
    for (int i = 0; i < area.size(); i++) {
        cout << arr[area[i].second][0]
             << " "
             << arr[area[i].second][1]
             << " "
             << arr[area[i].second][2]
             << '\n';
    }
}

// Driver Code
int main()
{
    vector<vector<int> > arr = {
        { 5, 3, 7 }, { 15, 20, 4 }, { 4, 9, 6 }, { 8, 4, 5 }
    };
    int N = arr.size();

    rearrangeTriangle(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function to rearrange the sides of
# triangle in increasing order of area
def rearrangeTriangle(arr, N):

        # Stores the area of triangles with
        # their corresponding indices
    area = []

    for i in range(0, N):

                # Find the area
        a = (arr[i][0] + arr[i][1] + arr[i][2]) / 2.0
        Area = math.sqrt(
            abs(a * (a - arr[i][0]) * (a - arr[i][1]) * (a - arr[i][2])))

        area.append([Area, i])

        # Sort the area vector
    area.sort()

    # Resultant sides
    for i in range(0, len(area)):
        print(arr[area[i][1]][0], end=" ")
        print(arr[area[i][1]][1], end=" ")
        print(arr[area[i][1]][2])

# Driver Code
if __name__ == "__main__":

    arr = [
        [5, 3, 7], [15, 20, 4], [4, 9, 6], [8, 4, 5]
    ]
    N = len(arr)

    rearrangeTriangle(arr, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG {

  // Function to rearrange the sides of
  // triangle in increasing order of area
  static void rearrangeTriangle(
    List<List<int> > arr, int N)
  {

    // Stores the area of triangles with
    // their corresponding indices
    List<KeyValuePair<float, int> > area = new List<KeyValuePair<float, int> >();

    for (int i = 0; i < N; i++) {

      // Find the area
      float a = (float)(arr[i][0]
                        + arr[i][1]
                        + arr[i][2])
        / 2;
      float Area = (float)Math.Sqrt(Math.Abs(a * (a - arr[i][0])
                                             * (a - arr[i][1])
                                             * (a - arr[i][2])));

      area.Add(new KeyValuePair <float, int>(Area, i ));
    }

    // Sort the area List
    area.Sort((x, y) => x.Key.CompareTo(y.Key));

    // Resultant sides
    for (int i = 0; i < area.Count; i++) {
      Console.WriteLine(arr[area[i].Value][0] + " "
                        + arr[area[i].Value][1]
                        + " "
                        + arr[area[i].Value][2]);
    }
  }

  // Driver Code
  static public void Main ()
  {
    List<List<int> > arr = new List<List<int> >(){
      new List<int>(){ 5, 3, 7 },
      new List<int>(){ 15, 20, 4 },
      new List<int>(){ 4, 9, 6 },
      new List<int>(){ 8, 4, 5 }
    };
    int N = arr.Count;

    rearrangeTriangle(arr, N);
  }
}

// This code is contributed
// by Shubham Singh
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to rearrange the sides of
        // triangle in increasing order of area
        function rearrangeTriangle(
            arr, N)
        {

            // Stores the area of triangles with
            // their corresponding indices
            let area = [];

            for (let i = 0; i < N; i++) {

                // Find the area
                let a = (arr[i][0]
                    + arr[i][1]
                    + arr[i][2])
                    / 2.0;
                let Area = Math.sqrt(Math.abs(a * (a - arr[i][0])
                    * (a - arr[i][1])
                    * (a - arr[i][2])));

                area.push({ first: parseInt(Area), second: parseInt(i) });
            }

            // Sort the area vector
            area.sort(function (a, b) {
                return a.first - b.first;
            })

            // Resultant sides
            for (let i = 0; i < area.length; i++) {
                document.write(arr[area[i].second][0]
                    + " "
                    + arr[area[i].second][1]
                    + " "
                    + arr[area[i].second][2]
                    + '<br>'
                )
            }
        }

        // Driver Code
        let arr = [
            [5, 3, 7], [15, 20, 4], [4, 9, 6], [8, 4, 5]
        ];
        let N = arr.length;
        rearrangeTriangle(arr, N);

       // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
5 3 7
8 4 5
4 9 6
15 20 4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*

**空间优化方法:**上述方法也可以在空间方面进行优化，思路是利用[比较器功能](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)对给定数组按照面积递增顺序进行排序。下面是使用的比较器功能:

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the area of sides
// of triangle stored in arr[]
float findArea(vector<int>& arr)
{

    // Find the semi perimeter
    float a = (arr[0]
               + arr[1]
               + arr[2])
              / 2.0;

    // Find area using Heron's Formula
    float Area = sqrt(abs(a * (a - arr[0])
                          * (a - arr[1])
                          * (a - arr[2])));

    // Return the area
    return Area;
}

// Comparator function to sort the given
// array of sides of triangles in
// increasing order of area
bool cmp(vector<int>& A, vector<int>& B)
{
    return findArea(A) <= findArea(B);
}

// Function to rearrange the sides of
// triangle in increasing order of area
void rearrangeTriangle(
    vector<vector<int> > arr, int N)
{
    // Sort the array arr[] in increasing
    // order of area
    sort(arr.begin(), arr.end(), cmp);

    // Resultant sides
    for (int i = 0; i < N; i++) {
        cout << arr[i][0] << " " << arr[i][1] << " "
             << arr[i][2] << '\n';
    }
}

// Driver Code
int main()
{
    vector<vector<int> > arr = {
        { 5, 3, 7 }, { 15, 20, 4 }, { 4, 9, 6 }, { 8, 4, 5 }
    };
    int N = arr.size();

    rearrangeTriangle(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to find the area of sides
# of triangle stored in arr[]
def findArea(arr):

    # Find the semi perimeter
    a = (arr[0] + arr[1] + arr[2]) / 2.0

    # Find area using Heron's Formula
    Area = math.sqrt(abs(a * (a - arr[0]) * (a - arr[1]) * (a - arr[2])))

    # Return the area
    return Area

# Function to rearrange the sides of
# triangle in increasing order of area
def rearrangeTriangle(arr , N):

  # Sort the array arr[] in increasing
  # order of area
  arr.sort(key = lambda x: (findArea(x)))

  # Resultant sides
  for i in range(0,N):
    print(arr[i][0], arr[i][1], arr[i][2])

# Driver Code
if __name__ == "__main__":

    arr = [[5 , 3 , 7], [15 , 20 , 4], [4 , 9 , 6], [8 , 4 , 5]]
    N = len(arr)

    rearrangeTriangle(arr, N)

    # This code is contributed by bhupenderyadav18.
```

**Output:** 

```
5 3 7
8 4 5
4 9 6
15 20 4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*