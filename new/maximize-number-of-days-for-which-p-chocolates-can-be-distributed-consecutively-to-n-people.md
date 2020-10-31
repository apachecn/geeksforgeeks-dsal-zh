# 最大限度地增加 P 巧克力可以连续分配给 N 个人的天数

> 原文：[https://www.geeksforgeeks.org/maximize-number-of-days-for-which-p-chocolates-can-be-distributed-consecutively-to-n-people/](https://www.geeksforgeeks.org/maximize-number-of-days-for-which-p-chocolates-can-be-distributed-consecutively-to-n-people/)

给定一个整数，表示巧克力数量的 **P** 和数组 **a []** ，其中 <sub>i</sub> 表示 **i <sup>th [</sup>** 巧克力。 **N** 人每天都想吃巧克力。 考虑以下条件，找出 **N** 人可以吃巧克力的最大连续天数：

1.  每个 **N** 人在特定的一天必须只吃一种巧克力。

2.  一个人只能整天吃同一类型的巧克力。

**示例**：

> **输入**：N = 4，P = 10，arr [] = {1、5、2、1、1、1、2、5、7、2}
> **输出**：2
> **说明**：巧克力的分配方式如下：
> **人物 1**：类型 1
> **人物 2**：类型 1
> **人 3**：类型 2
> **人 4**：类型 5
> 这样，每个人都有足够的巧克力，可以连续吃两个巧克力 天。 没有其他可能的巧克力分配方式可以使人们食用巧克力超过 2 天。
> 
> **输入**：N = 3，P = 10，arr [] = {1、2、2、1、1、3、3、3、2、4}
> **输出**：3
> **说明**：巧克力可以通过以下方式分配：
> **人 1**：类型 1
> **人 2**：类型 2
> **人 3**：3 型
> 这样，三个人都可以在三天内吃各自分配的巧克力。

**方法**：请按照以下步骤解决问题：

*   可以分配巧克力的最小天数为 **0** ，最大天数为 **P** 。

*   因此，对于此范围内的每个 *X* ，请检查是否有可能在 *X* 天之内向每个人分发巧克力。

*   对于所有这样的 X，找到最大值。

*   现在，使用[二分搜索](https://www.geeksforgeeks.org/binary-search/)检查范围 0 到 P 中的所有数字。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the frequency of
// each type of chocolate
map<int, int> mp;

int N, P;

// Function to check if chocolates
// can be eaten for 'mid' no. of days
bool helper(int mid)
{

    int cnt = 0;
    for (auto i : mp) {
        int temp = i.second;

        while (temp >= mid) {
            temp -= mid;
            cnt++;
        }
    }

    // If cnt exceeds N,
    // return true
    return cnt >= N;
}

// Function to find the maximum
// number of days for which
// chocolates can be eaten
int findMaximumDays(int arr[])
{

    // Store the frequency
    // of each type of chocolate
    for (int i = 0; i < P; i++) {
        mp[arr[i]]++;
    }

    // Initialize start and end
    // with 0 and P respectively
    int start = 0, end = P, ans = 0;
    while (start <= end) {

        // Calculate mid
        int mid = start
                  + ((end - start) / 2);

        // Check if chocolates can be
        // distributed for mid days
        if (mid != 0 and helper(mid)) {

            ans = mid;

            // Check if chocolates can
            // be distributed for more
            // than mid consecutive days
            start = mid + 1;
        }
        else if (mid == 0) {
            start = mid + 1;
        }
        else {
            end = mid - 1;
        }
    }

    return ans;
}

// Driver code
int main()
{

    N = 3, P = 10;
    int arr[] = { 1, 2, 2, 1, 1,
                  3, 3, 3, 2, 4 };

    // Function call
    cout << findMaximumDays(arr);

    return 0;
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Stores the frequency of
// each type of chocolate
static HashMap<Integer,
               Integer> mp = new HashMap<Integer,
                                         Integer>();

static int N, P;

// Function to check if chocolates
// can be eaten for 'mid' no. of days
static boolean helper(int mid)
{
    int cnt = 0;
    for(Map.Entry<Integer, Integer> i : mp.entrySet())
    {
        int temp = i.getValue();

        while (temp >= mid) 
        {
            temp -= mid;
            cnt++;
        }
    }

    // If cnt exceeds N,
    // return true
    return cnt >= N;
}

// Function to find the maximum
// number of days for which
// chocolates can be eaten
static int findMaximumDays(int arr[])
{

    // Store the frequency
    // of each type of chocolate
    for(int i = 0; i < P; i++) 
    {
        if (mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    // Initialize start and end
    // with 0 and P respectively
    int start = 0, end = P, ans = 0;
    while (start <= end)
    {

        // Calculate mid
        int mid = start + 
                  ((end - start) / 2);

        // Check if chocolates can be
        // distributed for mid days
        if (mid != 0 && helper(mid))
        {
            ans = mid;

            // Check if chocolates can
            // be distributed for more
            // than mid consecutive days
            start = mid + 1;
        }
        else if (mid == 0) 
        {
            start = mid + 1;
        }
        else
        {
            end = mid - 1;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{

    N = 3;
    P = 10;
    int arr[] = { 1, 2, 2, 1, 1,
                  3, 3, 3, 2, 4 };

    // Function call
    System.out.print(findMaximumDays(arr));
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program to implement
# the above approach

# Stores the frequency of
# each type of chocolate
mp = {}

N, P = 0, 0

# Function to check if chocolates
# can be eaten for 'mid' no. of days
def helper(mid):

    cnt = 0;
    for i in mp:
        temp = mp[i]

        while (temp >= mid):
            temp -= mid
            cnt += 1

    # If cnt exceeds N,
    # return true
    return cnt >= N

# Function to find the maximum
# number of days for which
# chocolates can be eaten
def findMaximumDays(arr):

    # Store the frequency
    # of each type of chocolate
    for i in range(P):
        mp[arr[i]] = mp.get(arr[i], 0) + 1

    # Initialize start and end
    # with 0 and P respectively
    start = 0
    end = P
    ans = 0

    while (start <= end):

        # Calculate mid
        mid = start + ((end - start) // 2)

        # Check if chocolates can be
        # distributed for mid days
        if (mid != 0 and helper(mid)):
            ans = mid

            # Check if chocolates can
            # be distributed for more
            # than mid consecutive days
            start = mid + 1
        elif (mid == 0):
            start = mid + 1
        else:
            end = mid - 1

    return ans

# Driver code
if __name__ == '__main__':

    N = 3
    P = 10

    arr = [ 1, 2, 2, 1, 1, 
            3, 3, 3, 2, 4 ]

    # Function call
    print(findMaximumDays(arr))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Stores the frequency of
// each type of chocolate
static Dictionary<int,
                  int> mp = new Dictionary<int,
                                           int>();                                         
static int N, P;

// Function to check if 
// chocolates can be eaten 
// for 'mid' no. of days
static bool helper(int mid)
{
  int cnt = 0;
  foreach(KeyValuePair<int, 
                       int> i in mp)
  {
    int temp = i.Value;

    while (temp >= mid) 
    {
      temp -= mid;
      cnt++;
    }
  }

  // If cnt exceeds N,
  // return true
  return cnt >= N;
}

// Function to find the maximum
// number of days for which
// chocolates can be eaten
static int findMaximumDays(int []arr)
{
  // Store the frequency
  // of each type of chocolate
  for(int i = 0; i < P; i++) 
  {
    if (mp.ContainsKey(arr[i]))
    {
      mp[arr[i]] =  mp[arr[i]] + 1;
    }
    else
    {
      mp.Add(arr[i], 1);
    }
  }

  // Initialize start and end
  // with 0 and P respectively
  int start = 0, end = P, ans = 0;
  while (start <= end)
  {
    // Calculate mid
    int mid = start + 
              ((end - start) / 2);

    // Check if chocolates can be
    // distributed for mid days
    if (mid != 0 && helper(mid))
    {
      ans = mid;

      // Check if chocolates can
      // be distributed for more
      // than mid consecutive days
      start = mid + 1;
    }
    else if (mid == 0) 
    {
      start = mid + 1;
    }
    else
    {
      end = mid - 1;
    }
  }
  return ans;
}

// Driver code
public static void Main(String[] args)
{
  N = 3;
  P = 10;
  int []arr = {1, 2, 2, 1, 1,
               3, 3, 3, 2, 4};

  // Function call
  Console.Write(findMaximumDays(arr));
}
}

// This code is contributed by 29AjayKumar

```

**Output**

```
3

```

**时间复杂度**：`O(N * log N)`

**辅助空间**：`O(n)`



* * *

* * *



