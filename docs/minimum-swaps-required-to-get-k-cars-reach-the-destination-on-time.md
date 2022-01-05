# 让 K 辆车准时到达目的地所需的最少换车次数

> 原文:[https://www . geesforgeks . org/minimum-swaps-required-to-get-k-cars-准时到达目的地/](https://www.geeksforgeeks.org/minimum-swaps-required-to-get-k-cars-reach-the-destination-on-time/)

给定 **N** 辆数和一个整数 **D** 即**T5】到目的地的距离。所有的汽车都从同一个起点出发，朝着同一个目的地前进。每辆车的速度由阵列**速度[]** 给出，并且它们在**递增**顺序中各自的**位置**以阵列**位置[]给出。**一辆车以比前一辆车慢的速度行驶被认为是另一辆车的**障碍**。任务是让 **K** 数量的车在给定时间内以**最小**数量的**交换****t**一辆车只能和后面的车交换，这只能用一辆车来完成。
同时进行多项互换，但每项互换均应计为单独互换。如果 **K** 辆车在给定时间内无法到达目的地，则返回-1**

**示例**:

> **输入** : N = 5，K= 3，D = 10，T = 5，位置[] = {0，2，5，6，7}，速度[] = {1，1，1，1，4}
> **输出** : 0
> **说明**:由于所有车的速度都是递增的，最后 3 辆车可以很容易的及时到达目的地 T
> 
> **输入** : N = 5，K = 3，D = 10，T = 5，位置[] = {0，2，3，5，7}，速度[] = {2，1，1，1，4}
> **输出** : 2
> **说明**:已经走完 0 段距离即第(0 次指标)的车与第 1 次、第 2 次指标的车对调，因为都不能按时到达目的地。交换后，至少有 3 辆车可以准时到达目的地。
> 
> **输入** : N = 5，K = 3，D = 10，T = 5，位置[] = {0，2，3，4，7}，速度[] = {2，1，1，1，4}
> **输出** : -1
> **解释**:通过任意数量的互换，K 辆车无法按时到达目的地。

**进场**:使用[贪婪](https://www.geeksforgeeks.org/greedy-algorithms/)进场可以解决任务。由于每辆车的位置都是以**递增**的顺序给出的，所以最好的方法是开始遍历最后一辆**车，对于能及时到达目的地的车保留一个计数器**可达**，对于不能及时到达目的地的车保留一个计数器**障碍**。如果一辆车能够及时到达，那么在**交换的数量上加上障碍物的数量。**
以下是上述方法的实施:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get minimum
// number of swaps and returns
// number of cars that
// car reach there in time.
int reachables(int x[], int v[], int n,
               int& swaps, int d,
               int t, int k)
{

    // Counter for number of cars that
    // can reach in time
    int reachable = 0;

    // Counter for cars that cannot reach
    // destination in time.
    int obstacle = 0;

    int i = n - 1;
    while (i >= 0) {

        int temp = d - x[i];
        if (v[i] * t >= temp) {
            // If a car can reach in
            // time then increase the
            // reachable counter
            reachable++;

            // Adding the number of cars
            // that need to be swapped
            swaps += obstacle;
        }
        else {
            // If a car cannot reach
            // in time then increase
            // the obstacle counter
            obstacle++;
        }

        if (reachable >= k) {
            break;
        }

        i--;
    }
    // Return the swaps
    if (reachable >= k)
        return swaps;
    else
        return -1;
}
// Driver Code
int main()
{
    int n = 5, k = 3, d = 10, t = 5;
    int x[] = { 0, 2, 3, 5, 7 };
    int v[] = { 2, 1, 1, 1, 4 };
    int swaps = 0;

    cout << reachables(x, v, n, swaps, d, t, k);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
class GFG
{
  // Function to get minimum
  // number of swaps and returns
  // number of cars that
  // car reach there in time.
  static int reachables(int x[], int v[], int n,
                 int swaps, int d,
                 int t, int k)
  {

      // Counter for number of cars that
      // can reach in time
      int reachable = 0;

      // Counter for cars that cannot reach
      // destination in time.
      int obstacle = 0;

      int i = n - 1;
      while (i >= 0) {

          int temp = d - x[i];
          if (v[i] * t >= temp) {
              // If a car can reach in
              // time then increase the
              // reachable counter
              reachable++;

              // Adding the number of cars
              // that need to be swapped
              swaps += obstacle;
          }
          else {
              // If a car cannot reach
              // in time then increase
              // the obstacle counter
              obstacle++;
          }

          if (reachable >= k) {
              break;
          }

          i--;
      }
      // Return the swaps
      if (reachable >= k)
          return swaps;
      else
          return -1;
  }

  // Driver Code
  public static void main(String [] args)
  {
      int n = 5, k = 3, d = 10, t = 5;
      int x[] = { 0, 2, 3, 5, 7 };
      int v[] = { 2, 1, 1, 1, 4 };
      int swaps = 0;

      System.out.println(reachables(x, v, n, swaps, d, t, k));

  }

}

// This code is contributed by AR_Gaurav
```

## **C#**

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to get minimum
  // number of swaps and returns
  // number of cars that
  // car reach there in time.
  static int reachables(int []x, int []v, int n,
                 int swaps, int d,
                 int t, int k)
  {

      // Counter for number of cars that
      // can reach in time
      int reachable = 0;

      // Counter for cars that cannot reach
      // destination in time.
      int obstacle = 0;

      int i = n - 1;
      while (i >= 0) {

          int temp = d - x[i];
          if (v[i] * t >= temp) {
              // If a car can reach in
              // time then increase the
              // reachable counter
              reachable++;

              // Adding the number of cars
              // that need to be swapped
              swaps += obstacle;
          }
          else {
              // If a car cannot reach
              // in time then increase
              // the obstacle counter
              obstacle++;
          }

          if (reachable >= k) {
              break;
          }

          i--;
      }
      // Return the swaps
      if (reachable >= k)
          return swaps;
      else
          return -1;
  }

  // Driver Code
  public static void Main(string [] args)
  {
      int n = 5, k = 3, d = 10, t = 5;
      int []x = { 0, 2, 3, 5, 7 };
      int []v = { 2, 1, 1, 1, 4 };
      int swaps = 0;

      Console.WriteLine(reachables(x, v, n, swaps, d, t, k));
  }
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to get minimum
# number of swaps and returns
# number of cars that
# car reach there in time.
def reachables(x, v, n,swaps, d, t, k) :

    # Counter for number of cars that
    # can reach in time
    reachable = 0;

    # Counter for cars that cannot reach
    # destination in time.
    obstacle = 0;

    i = n - 1;
    while (i >= 0) :

        temp = d - x[i];
        if (v[i] * t >= temp) :
            # If a car can reach in
            # time then increase the
            # reachable counter
            reachable += 1;

            # Adding the number of cars
            # that need to be swapped
            swaps += obstacle;

        else :
            # If a car cannot reach
            # in time then increase
            # the obstacle counter
            obstacle += 1;

        if (reachable >= k) :
            break;

        i -= 1;

    # Return the swaps
    if (reachable >= k) :
        return swaps;
    else :
        return -1;

# Driver Code
if __name__ == "__main__" :

    n = 5; k = 3; d = 10; t = 5;
    x = [ 0, 2, 3, 5, 7 ];
    v = [ 2, 1, 1, 1, 4 ];
    swaps = 0;

    print(reachables(x, v, n, swaps, d, t, k));

    # This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to get minimum
// number of swaps and returns
// number of cars that
// car reach there in time.
function reachables(x, v, n, swaps, d, t, k) {
  // Counter for number of cars that
  // can reach in time
  let reachable = 0;

  // Counter for cars that cannot reach
  // destination in time.
  let obstacle = 0;

  let i = n - 1;
  while (i >= 0) {
    let temp = d - x[i];
    if (v[i] * t >= temp) {
      // If a car can reach in
      // time then increase the
      // reachable counter
      reachable++;

      // Adding the number of cars
      // that need to be swapped
      swaps += obstacle;
    } else {
      // If a car cannot reach
      // in time then increase
      // the obstacle counter
      obstacle++;
    }

    if (reachable >= k) {
      break;
    }

    i--;
  }
  // Return the swaps
  if (reachable >= k) return swaps;
  else return -1;
}
// Driver Code

let n = 5,
  k = 3,
  d = 10,
  t = 5;
let x = [0, 2, 3, 5, 7];
let v = [2, 1, 1, 1, 4];
let swaps = 0;

document.write(reachables(x, v, n, swaps, d, t, k));

// This code is contributed by saurabh_jaiswal.
</script>
```

****Output**

```
2
```** 

*****时间复杂度*** : O(N)
***辅助空间*** : O(1)**