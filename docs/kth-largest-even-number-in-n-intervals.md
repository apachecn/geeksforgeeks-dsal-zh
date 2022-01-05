# N 个区间中第 k 个最大偶数

> 原文:[https://www . geesforgeks . org/kth-最大偶数 n 进制间隔/](https://www.geeksforgeeks.org/kth-largest-even-number-in-n-intervals/)

给定一个 **N** 范围的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**arr【】**，表示从 **L** 到 **R** 的整数间隔，以及一个数字 **K** ，任务是找到第 K 个最大的偶数。

**示例**:

> **输入** : arr = {{12，15}、{3，9}、{2，5}、{20，25}、{16，20}}，K = 9
> **输出** : 6
> **解释**:合并后，范围变为{{2，9}、{12，25}}范围内出现的偶数为{2，4，6，8，12，14，16，18，20
> 
> **输入** : arr = {{2，4}，{8，12}}，K = 4
> T3】输出 : 4

**逼近**:给定的问题可以通过[合并重叠区间的方法来解决。](https://www.geeksforgeeks.org/merging-intervals/)想法是[根据范围的下限对间隔](https://www.geeksforgeeks.org/insert-in-sorted-and-non-overlapping-interval-array/)进行排序，并将它们合并以消除整数的重复。那么可以按照以下步骤来解决问题:

*   如果 **K < =0** 或 **N=0** ，则返回-1
*   初始化， **L = arr[i]。首先**和 **R = arr[i]。第二**
*   初始化一个变量**范围，**存储该范围内的偶数
*   [从 **idx** 到 0 循环迭代](https://www.geeksforgeeks.org/for-each-loop-in-java/)
    *   如果 **R** 是奇数
        *   **范围** =楼层((R–L+1)/2)
        *   如果， **K >范围**K = K–范围
        *   否则返回**R–2 * K+1**
    *   如果 **R** 为偶数
        *   **范围** =上限((浮动)(R–L+1)/2)
        *   如果， **K >范围**K = K–范围
        *   否则，**R–2 * K+2**
*   返回-1

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
#include <cmath>
using namespace std;

// Function to merge overlapping intervals
// and return the Kth largest even number
int calcEven(vector<pair<int, int> > V,
             int N, int k)
{

    // Base Case
    if (k <= 0 || N == 0)
        return -1;

    // Sort the intervals in increasing order
    // according to their first element
    sort(V.begin(), V.end());

    int i, idx = 0;

    // Merging the overlaping intervals
    for (i = 1; i < N; i++) {

        // If it overlaps with
        // the previous intervals
        if ((V[idx].second >= V[i].first)
            || (V[i].first == V[idx].second + 1)) {

            // Merge previous and current intervals
            V[idx].second = max(V[idx].second,
                                V[i].second);
        }
        else {

            // Increment the index
            idx++;

            V[idx].second = V[i].second;
            V[idx].first = V[i].first;
        }
    }

    // Find Kth largest even number
    for (i = idx; i >= 0; i--) {

        // Initialize L and R
        int L = V[i].first;
        int R = V[i].second;

        // If R is odd
        if (R & 1) {

            // Calculate number of even
            // numbers within the range
            int range = (R - L + 1) / 2;

            // if k > range then kth largest
            // even number is not in this range
            if (k > range) {

                k -= range;
            }
            else
                return (R - 2 * k + 1);
        }
        else {

            // Calculate number of even
            // numbers within the range
            int range = ceil((float)(R - L + 1) / 2);

            // if k > range then kth largest
            // even number is not in this range
            if (k > range) {

                k -= range;
            }
            else
                return (R - 2 * k + 2);
        }
    }

    // No Kth even number in the range
    // so return -1
    return -1;
}

// Driver Code
int main()
{

    // Initialize the ranges
    vector<pair<int, int> > vec = { { 12, 15 },
                                    { 3, 9 },
                                    { 2, 5 },
                                    { 20, 25 },
                                    { 16, 20 } };

    int N = vec.size();

    // Initialize K
    int K = 9;

    // Print the answer
    cout << calcEven(vec, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class GFG {

  static class Pair {
    int first = 0;
    int second = 0;

    public Pair(int first, int second) {
      this.first = first;
      this.second = second;
    }
  }

  // Function to merge overlapping intervals
  // and return the Kth largest even number
  public static int calcEven(ArrayList<Pair> V, int N, int k) {

    // Base Case
    if (k <= 0 || N == 0)
      return -1;

    // Sort the intervals in increasing order
    // according to their first element
    Collections.sort(V, new Comparator<Pair>() {
      @Override
      public int compare(Pair p1, Pair p2) {
        return p1.first - p2.first;
      }
    });

    int i, idx = 0;

    // Merging the overlaping intervals
    for (i = 1; i < N; i++) {

      // If it overlaps with
      // the previous intervals
      if ((V.get(idx).second >= V.get(i).first) || (V.get(i).first == V.get(idx).second + 1)) {

        // Merge previous and current intervals
        V.get(idx).second = Math.max(V.get(idx).second, V.get(i).second);
      } else {

        // Increment the index
        idx++;

        V.get(idx).second = V.get(i).second;
        V.get(idx).first = V.get(i).first;
      }
    }

    // Find Kth largest even number
    for (i = idx; i >= 0; i--) {

      // Initialize L and R
      int L = V.get(i).first;
      int R = V.get(i).second;

      // If R is odd
      if ((R & 1) > 0) {

        // Calculate number of even
        // numbers within the range
        int range = (R - L + 1) / 2;

        // if k > range then kth largest
        // even number is not in this range
        if (k > range) {

          k -= range;
        } else
          return (R - 2 * k + 1);
      } else {

        // Calculate number of even
        // numbers within the range
        int range = (int) Math.ceil((R - L + 1) / 2);

        // if k > range then kth largest
        // even number is not in this range
        if (k > range) {

          k -= range;
        } else
          return (R - 2 * k + 2);
      }
    }

    // No Kth even number in the range
    // so return -1
    return -1;
  }

  // Driver Code
  public static void main(String args[]) {

    // Initialize the ranges
    ArrayList<Pair> vec = new ArrayList<Pair>();

    vec.add(new Pair(12, 15));
    vec.add(new Pair(3, 9));
    vec.add(new Pair(2, 5));
    vec.add(new Pair(20, 25));
    vec.add(new Pair(16, 20));

    int N = vec.size();

    // Initialize K
    int K = 9;

    // Print the answer
    System.out.println(calcEven(vec, N, K));
  }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python implementation for the above approach
import math

# Function to merge overlapping intervals
# and return the Kth largest even number
def calcEven(V, N, k):

    # Base Case
    if (k <= 0 or N == 0):
        return -1

    # Sort the intervals in increasing order
    # according to their first element
    V.sort()

    idx = 0

    # Merging the overlaping intervals
    for i in range(1, N):

        # If it overlaps with
        # the previous intervals
        if ((V[idx][1] >= V[i][0]) or (V[i][0] == V[idx][1] + 1)):

            # Merge previous and current intervals
            V[idx][1] = max(V[idx][1], V[i][1])

        else:

           # Increment the index
            idx += 1

            V[idx][1] = V[i][1]
            V[idx][0] = V[i][0]

        # Find Kth largest even number
    for i in range(idx, -1, -1):

        # Initialize L and R
        L = V[i][0]
        R = V[i][1]

        # If R is odd
        if (R & 1):

            # Calculate number of even
            # numbers within the rng
            rng = (R - L + 1) // 2

            # if k > rng then kth largest
            # even number is not in this rng
            if (k > rng):
                k -= rng

            else:
                return (R - 2 * k + 1)

        else:

            # Calculate number of even
            # numbers within the rng
            rng = math.ceil((R - L + 1) / 2)

            # if k > rng then kth largest
            # even number is not in this rng
            if (k > rng):
                k -= rng

            else:
                return (R - 2 * k + 2)

        # No Kth even number in the rng
        # so return -1
    return -1

# Driver Code
if __name__ == "__main__":

   # Initialize the ranges
    vec = [[12, 15], [3, 9], [2, 5], [20, 25], [16, 20]]

    N = len(vec)

    # Initialize K
    K = 9

    # Print the answer
    print(calcEven(vec, N, K))

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to merge overlapping intervals
       // and return the Kth largest even number
       function calcEven(V, N, k)
       {

           // Base Case
           if (k <= 0 || N == 0)
               return -1;

           // Sort the intervals in increasing order
           // according to their first element
           V.sort(function (a, b) { return a.first - b.first })

           let i, idx = 0;

           // Merging the overlaping intervals
           for (i = 1; i < N; i++) {

               // If it overlaps with
               // the previous intervals
               if ((V[idx].second >= V[i].first)
                   || (V[i].first == V[idx].second + 1)) {

                   // Merge previous and current intervals
                   V[idx].second = Math.max(V[idx].second,
                       V[i].second);
               }
               else {

                   // Increment the index
                   idx++;

                   V[idx].second = V[i].second;
                   V[idx].first = V[i].first;
               }
           }

           // Find Kth largest even number
           for (i = idx; i >= 0; i--) {

               // Initialize L and R
               let L = V[i].first;
               let R = V[i].second;

               // If R is odd
               if (R & 1) {

                   // Calculate number of even
                   // numbers within the range
                   let range = (R - L + 1) / 2;

                   // if k > range then kth largest
                   // even number is not in this range
                   if (k > range) {

                       k -= range;
                   }
                   else
                       return (R - 2 * k + 1);
               }
               else {

                   // Calculate number of even
                   // numbers within the range
                   let range = Math.ceil((R - L + 1) / 2);

                   // if k > range then kth largest
                   // even number is not in this range
                   if (k > range) {

                       k -= range;
                   }
                   else
                       return (R - 2 * k + 2);
               }
           }

           // No Kth even number in the range
           // so return -1
           return -1;
       }

       // Driver Code

       // Initialize the ranges
       let vec = [{ first: 12, second: 15 },
       { first: 3, second: 9 },
       { first: 2, second: 5 },
       { first: 20, second: 25 },
       { first: 16, second: 20 }];

       let N = vec.length;

       // Initialize K
       let K = 9;

       // Print the answer
       document.write(calcEven(vec, N, K));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
6
```

**时间** **复杂度**:O(N * log N)
T5】辅助 T7】空间 : O(1)