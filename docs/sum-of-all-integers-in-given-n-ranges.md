# 给定 N 个范围内所有整数之和

> 原文:[https://www . geesforgeks . org/给定 n 范围内所有整数之和/](https://www.geeksforgeeks.org/sum-of-all-integers-in-given-n-ranges/)

给定形式为**【L，R】**的 **N** 范围，任务是找出位于任何给定范围内的所有整数的和。

**示例**:

> **输入** : arr[] = {{1，5}，{3，7}}，N = 2
> **输出** : 28
> **说明:**存在于一个或多个范围内的整数集合为{1，2，3，4，5，6，7}。因此总和是 28。
> 
> **输入**:范围[]= {-12，15}、{3，9}、{-5，-2}、{20，25}、{16，20}}
> 输出 : 247

**方法:**给定的问题可以通过类似于[合并重叠区间](https://www.geeksforgeeks.org/merging-intervals/)问题的方法来解决。以下是要遵循的步骤:

*   [根据 **L** 的递增顺序对](https://www.geeksforgeeks.org/sorting-algorithms/)区间进行排序。
*   将第一个间隔推到一个[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)上，并对每个间隔执行以下操作:
    *   如果当前间隔与堆栈顶部不重叠，请按下它。
    *   如果当前间隔与堆栈顶部重叠，并且当前间隔的右端大于堆栈顶部，则使用当前间隔右端的值更新堆栈顶部。
*   遍历所有区间后，剩余的栈包含合并的区间。合并区间的和可以用公式计算[一个等差数列的和](https://www.geeksforgeeks.org/program-sum-arithmetic-series/)作为范围**【L，R】**形成一个 AP，共同的区别为 **1** 和元素个数为**R–L+1**。总和为 **((L + R)*(R-L+1))/2。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function to find the sum of all
// integers numbers in range [L, R]
ll sumInRange(long L, long R)
{
    ll Sum = ((R - L + 1) / 2)
      * (2 * L + (R - L));
    return Sum;
}

// Function to find sum of all integers
// that lie in any of the given ranges
ll calcSum(vector<pair<long, long> > data,
           int n)
{

    // Sort intervals in increasing order
    // according to their first element
    sort(data.begin(), data.end());

    // Merging the overlaping intervals
    int i, idx = 0;

    // Loop to iterate through the array
    for (i = 1; i < n; i++) {

        // If current interval overlaps
        // with the previous intervals
        if ((data[idx].second >=
             data[i].first)
            || (data[i].first ==
                data[idx].second + 1)) {

            // Merge the previou and the
            // current interval
            data[idx].second
                = max(data[idx].second,
                      data[i].second);
        }
        else {
            idx++;
            data[idx].second = data[i].second;
            data[idx].first = data[i].first;
        }
    }

    // Stores the required sum
    ll Sum = 0;

    // Loop to calculate the sum of all
    // the remaining merged intervals
    for (i = 0; i <= idx; i++) {

        // Add sum of integers
        // in current range
        Sum += sumInRange(data[i].first,
                          data[i].second);
    }

    // Return the total Sum
    return Sum;
}

// Driver Code
int main()
{
    vector<pair<long, long> > vec
      = { { -12, 15 },
         { 3, 9 },
         { -5, -2 },
         { 20, 25 },
         { 16, 20 } };

    cout << calcSum(vec, vec.size());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the sum of all
// integers numbers in range [L, R]
static int sumInRange(int L, int R)
{
    int Sum = ((R - L + 1) / 2)
      * (2 * L + (R - L));
    return Sum;
}

// Function to find sum of all integers
// that lie in any of the given ranges
static int calcSum(int [][]data,
           int n)
{

    // Sort intervals in increasing order
    // according to their first element
    Arrays.sort(data,(a,b)->{
        return a[0]-b[0];
    });

    // Merging the overlaping intervals
    int i, idx = 0;

    // Loop to iterate through the array
    for (i = 1; i < n; i++) {

        // If current interval overlaps
        // with the previous intervals
        if ((data[idx][1] >=
             data[i][0])
            || (data[i][0] ==
                data[idx][1] + 1)) {

            // Merge the previou and the
            // current interval
            data[idx][1]
                = Math.max(data[idx][1],
                      data[i][1]);
        }
        else {
            idx++;
            data[idx][1] = data[i][1];
            data[idx][0] = data[i][0];
        }
    }

    // Stores the required sum
    int Sum = 0;

    // Loop to calculate the sum of all
    // the remaining merged intervals
    for (i = 0; i <= idx; i++) {

        // Add sum of integers
        // in current range
        Sum += sumInRange(data[i][0],
                          data[i][1]);
    }

    // Return the total Sum
    return Sum;
}

// Driver Code
public static void main(String[] args)
{
    int [][]vec
      = { { -12, 15 },
         { 3, 9 },
         { -5, -2 },
         { 20, 25 },
         { 16, 20 } };

    System.out.print(calcSum(vec, vec.length));

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the sum of all
# integers numbers in range [L, R]
def sumInRange(L, R):

    Sum = ((R - L + 1) // 2) * (2 * L + (R - L))
    return Sum

# Function to find sum of all integers
# that lie in any of the given ranges
def calcSum(data,
            n):

    # Sort intervals in increasing order
    # according to their first element
    data.sort()

    # Merging the overlaping intervals
    idx = 0

    # Loop to iterate through the array
    for i in range(1, n):

        # If current interval overlaps
        # with the previous intervals
        if ((data[idx][1] >=
             data[i][0])
            or (data[i][0] ==
                data[idx][1] + 1)):

            # Merge the previou and the
            # current interval
            data[idx][1] = max(data[idx][1],
                               data[i][1])

        else:
            idx += 1
            data[idx][1] = data[i][1]
            data[idx][0] = data[i][0]
    # Stores the required sum
    Sum = 0

    # Loop to calculate the sum of all
    # the remaining merged intervals
    for i in range(idx+1):

        # Add sum of integers
        # in current range
        Sum += sumInRange(data[i][0],
                          data[i][1])

    # Return the total Sum
    return Sum

# Driver Code
if __name__ == "__main__":

    vec = [[-12, 15],
           [3, 9],
           [-5, -2],
           [20, 25],
           [16, 20]]

    print(calcSum(vec, len(vec)))

    # This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find the sum of all
       // integers numbers in range [L, R]
       function sumInRange(L, R) {
           let Sum = ((R - L + 1) / 2)
               * (2 * L + (R - L));
           return Sum;
       }

       // Function to find sum of all integers
       // that lie in any of the given ranges
       function calcSum(data, n) {

           // Sort intervals in increasing order
           // according to their first element
           data.sort(function (a, b) { return a.first - b.first })

           // Merging the overlaping intervals
           let i, idx = 0;

           // Loop to iterate through the array
           for (i = 1; i < n; i++) {

               // If current interval overlaps
               // with the previous intervals
               if ((data[idx].second >=
                   data[i].first)
                   || (data[i].first ==
                       data[idx].second + 1)) {

                   // Merge the previou and the
                   // current interval
                   data[idx].second
                       = Math.max(data[idx].second,
                           data[i].second);
               }
               else {
                   idx++;
                   data[idx].second = data[i].second;
                   data[idx].first = data[i].first;
               }
           }

           // Stores the required sum
           let Sum = 0;

           // Loop to calculate the sum of all
           // the remaining merged intervals
           for (i = 0; i <= idx; i++) {

               // Add sum of integers
               // in current range
               Sum += sumInRange(data[i].first,
                   data[i].second);
           }

           // Return the total Sum
           return Sum;
       }

       // Driver Code

       let vec
           = [{ first: -12, second: 15 },
           { first: 3, second: 9 },
           { first: -5, second: -2 },
           { first: 20, second: 25 },
           { first: 16, second: 20 }];

       document.write(calcSum(vec, vec.length));

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
247
```

***时间** **复杂度:** O(N*log N)*
***辅助空间:** O(1)*