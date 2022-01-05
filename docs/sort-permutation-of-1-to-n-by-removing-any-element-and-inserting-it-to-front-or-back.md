# 通过移除任何元素并将其插入到前面或后面来对 1 到 N 的排列进行排序

> 原文:[https://www . geeksforgeeks . org/sort-1 到 n 的排列-通过移除任意元素并将其插入到前面或后面/](https://www.geeksforgeeks.org/sort-permutation-of-1-to-n-by-removing-any-element-and-inserting-it-to-front-or-back/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**，该数组具有从 **1** 到 **N、**的**个不同的整数，任务是通过移除任何元素并将其插入到数组的**前**或**后**来计算[按升序对数组](https://www.geeksforgeeks.org/sorting-algorithms/)排序所需的**最小步骤数。****

**示例:**

> **输入:** arr[ ] = {4，1，3，2}
> **输出:** 2
> **解释:**
> 给定数组可以通过以下两个操作按递增顺序排序:
> 操作 1:移除 3，并将其添加到数组后面。{4，1， **3** ，2} - > {4，1，2， **3** }
> 操作 2:去掉 4，添加到数组后面。{ **4** ，1，2，3} - > {1，2，3， **4**
> 
> **输入:** arr[ ] = {4，1，2，5，3}
> **输出:** 2

**方法:**利用以下事实可以解决这个问题:要使数组以**最小**步数排序，必须将最小数量的元素移到**前面**或**后面**。此外，必须改变位置的元素最初不会按照**增加**的顺序排列。因此，问题简化为[寻找最长的递增子阵列](https://www.geeksforgeeks.org/longest-increasing-subarray/)，因为只有阵列中的那些元素不会被移动。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum steps
// to sort the array
void findMinStepstoSort(int arr[], int N){

  // Storing the positions of elements
  map<int,int> pos;
  for(int i = 0; i < N; i++)
    pos[arr[i]] = i;

  // Intitalize answer
  int ans = N-1;
  int prev = -1;
  int count = 0;

  // Traversing the array
  for(int i = 1; i < N + 1; i++){

    // If current is greater than
    // previous
    if(pos[i] > prev)
      count += 1;

    // else if current is less than
    // previous
    else
      count = 1;

    // Updating previous
    prev = pos[i];

    // Updating ans
    ans = min(ans, N - count);
   }
  cout<<ans;
}

// Driver Code
int main(){

  int N = 5;
  int arr[] = {4, 1, 2, 5, 3};

  findMinStepstoSort(arr, N);

}

// This code is contributed by SURENDRA_GANGWAR.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum steps
// to sort the array
static void findMinStepstoSort(int arr[], int N){

  // Storing the positions of elements
  HashMap<Integer,Integer> pos = new HashMap<>();
  for(int i = 0; i < N; i++)
    pos.put(arr[i], i);

  // Intitalize answer
  int ans = N - 1;
  int prev = -1;
  int count = 0;

  // Traversing the array
  for(int i = 1; i < N + 1; i++){

    // If current is greater than
    // previous
    if(pos.get(i) > prev)
      count += 1;

    // else if current is less than
    // previous
    else
      count = 1;

    // Updating previous
    prev = pos.get(i);

    // Updating ans
    ans = Math.min(ans, N - count);
   }
  System.out.print(ans);
}

// Driver Code
public static void main(String[] args){

  int N = 5;
  int arr[] = {4, 1, 2, 5, 3};

  findMinStepstoSort(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum steps
# to sort the array
def findMinStepstoSort(arr, N):

  # Storing the positions of elements
  pos = {arr[i]:i for i in range(N)}

  # Intitalize answer
  ans = N-1
  prev = -1;count = 0

  # Traversing the array
  for i in range(1, N + 1):

    # If current is greater than
    # previous
    if pos[i] > prev:
      count += 1

    # else if current is less than
    # previous
    else:
      count = 1

    # Updating previous
    prev = pos[i]

    # Updating ans
    ans = min(ans, N - count)
  print(ans)

# Driver Code
if __name__ == '__main__':
  N = 5
  arr = [4, 1, 2, 5, 3]

  findMinStepstoSort(arr, N)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find the minimum steps
// to sort the array
static void findMinStepstoSort(int[] arr, int N){

  // Storing the positions of elements
  Dictionary<int, int> pos = new
                Dictionary<int, int>();
  for(int i = 0; i < N; i++)
    pos[arr[i]] = i;

  // Intitalize answer
  int ans = N - 1;
  int prev = -1;
  int count = 0;

  // Traversing the array
  for(int i = 1; i < N + 1; i++){

    // If current is greater than
    // previous
    if(pos[i] > prev)
      count += 1;

    // else if current is less than
    // previous
    else
      count = 1;

    // Updating previous
    prev = pos[i];

    // Updating ans
    ans = Math.Min(ans, N - count);
   }
  Console.WriteLine(ans);
}

    // Driver Code
    public static void Main (string[] args)
    {
        int N = 5;
        int[] arr = {4, 1, 2, 5, 3};

        findMinStepstoSort(arr, N);
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum steps
        // to sort the array
        function findMinStepstoSort(arr, N) {

            // Storing the positions of elements
            let pos = new Array(N);

            for (let i = 0; i < N; i++) {
                pos[i] = arr[i];
            }

            // Intitalize answer
            ans = N - 1
            prev = -1; count = 0

            // Traversing the array
            for (let i = 1; i < N + 1; i++) {

                // If current is greater than
                // previous
                if (pos[i] > prev)
                    count += 1

                // else if current is less than
                // previous
                else
                    count = 1

                // Updating previous
                prev = pos[i]

                // Updating ans
                ans = Math.min(ans, N - count)
            }
            document.write(ans)

        }

        let N = 5
        let arr = [4, 1, 2, 5, 3]

        findMinStepstoSort(arr, N)

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)