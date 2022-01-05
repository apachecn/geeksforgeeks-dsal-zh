# 找到 GCD 等于 1 的移除数组元素游戏的赢家

> 原文:[https://www . geesforgeks . org/find-移除数组元素游戏的赢家-拥有-gcd-等于-1/](https://www.geeksforgeeks.org/find-the-winner-of-game-of-removing-array-elements-having-gcd-equal-to-1/)

给定一个大小为 **N** 的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是当两个玩家按照以下规则进行最佳游戏时，找到游戏的赢家:

*   **玩家 1** 开始游戏。
*   在每一回合中，玩家从数组中移除一个元素。
*   **只有当**玩家 1** 移除的所有元素中的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 变为等于 **1** 时，玩家 2** 才会赢得游戏。

**示例:**

> **输入:** arr[] = { 2，4，8 }
> **输出:**玩家 1
> **解释:**
> **回合 1:** 玩家 1 移除 arr[0]。因此，玩家 1 移除的元素 GCD = 2
> **转 2:** 因为玩家 1 移除的元素 GCD 不等于 1。因此，玩家 2 移除 arr[1]。
> **第三回合:**玩家 1 移除 arr[2]。因此，玩家 1 移除的元素 GCD = GCD(2，8) = 2
> 由于玩家 1 移除的元素 GCD 不等于 1，所以玩家 1 赢得游戏。
> 
> **输入:** arr[] = { 2，1，1，1，1，1 }
> **输出:**:玩家 2
> **回合 1:** 玩家 1 移除 arr[0]。因此，玩家 1 移除的元素 GCD = 2
> **回合 2:** 由于玩家 1 移除的元素 GCD 不等于 1，玩家 2 移除 arr[1]。
> **第三回合:**玩家 1 移除 arr[2]。因此，玩家 1 移除的元素 GCD = GCD(2，1) = 1
> 由于玩家 1 移除的元素 GCD 为 1，所以玩家 2 赢得游戏。

**方法:**玩家 1 和玩家 2 的最佳方式是总是移除在大多数数组元素中至少有一个公共[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的数组元素。按照以下步骤解决问题:

*   [初始化一个映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如说 **mp** ，这样**MP【I】**存储其[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)为 **i** 的数组元素的计数
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)找到**地图**中存在的最大值，说 **maxCnt** 。
*   如果 [N 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)**maxCnt**等于 **N** 或者如果 [N 为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)**maxCnt≥N–1**，则**玩家 1** 获胜。
*   否则**玩家 2** 获胜。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the winner of the game by
// removing array elements whose GCD is 1
void findWinnerGameRemoveGCD(int arr[], int n)
{

    // mp[i]: Stores count of array
    // elements whose prime factor is i
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Calculate the prime factors
        // of arr[i]
        for (int j = 2; j * j <= arr[i];
             j++) {

            // If arr[i] is divisible by j
            if (arr[i] % j == 0) {

                // Update mp[j]
                mp[j]++;

                while (arr[i] % j == 0) {

                    // Update arr[i]
                    arr[i] = arr[i] / j;
                }
            }
        }

        // If arr[i] exceeds 1
        if (arr[i] > 1) {
            mp[arr[i]]++;
        }
    }

    // Stores maximum value
    // present in the Map
    int maxCnt = 0;

    // Traverse the map
    for (auto i : mp) {

        // Update maxCnt
        maxCnt = max(maxCnt,
                     i.second);
    }

    // If n is an even number
    if (n % 2 == 0) {

        // If maxCnt is greater
        // than or equal to n-1
        if (maxCnt >= n - 1) {

            // Player 1 wins
            cout << "Player 1";
        }
        else {

            // Player 2 wins
            cout << "Player 2";
        }
    }
    else {

        // If maxCnt equal to n
        if (maxCnt == n) {

            // Player 1 wins
            cout << "Player 1";
        }
        else {

            // Player 2 wins
            cout << "Player 2";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 8 };
    int N = sizeof(arr)
            / sizeof(arr[0]);

    findWinnerGameRemoveGCD(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

  // Function to find the winner of the game by
  // removing array elements whose GCD is 1
  static void findWinnerGameRemoveGCD(int arr[], int n)
  {

    // mp[i]: Stores count of array
    // elements whose prime factor is i
    HashMap<Integer,
    Integer> mp = new HashMap<Integer,
    Integer>();

    // Traverse the array
    for (int i = 0; i < n; i++) {

      // Calculate the prime factors
      // of arr[i]
      for (int j = 2; j * j <= arr[i];
           j++) {

        // If arr[i] is divisible by j
        if (arr[i] % j == 0) {

          // Update mp[j]
          if (mp.containsKey(j))
          {
            mp.put(j, mp.get(j) + 1);
          }
          else
          {
            mp.put(j, 1);
          }

          while (arr[i] % j == 0) {

            // Update arr[i]
            arr[i] = arr[i] / j;
          }
        }
      }

      // If arr[i] exceeds 1
      if (arr[i] > 1) {
        if(mp.containsKey(arr[i]))
        {
          mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
          mp.put(arr[i], 1);
        }
      }
    }

    // Stores maximum value
    // present in the Map
    int maxCnt = 0;

    // Traverse the map
    for (Map.Entry<Integer,
         Integer> i : mp.entrySet()) {

      // Update maxCnt
      maxCnt = Math.max(maxCnt, i.getValue());
    }

    // If n is an even number
    if (n % 2 == 0) {

      // If maxCnt is greater
      // than or equal to n-1
      if (maxCnt >= n - 1) {

        // Player 1 wins
        System.out.print("Player 1");
      }
      else {

        // Player 2 wins
        System.out.print("Player 2");
      }
    }
    else {

      // If maxCnt equal to n
      if (maxCnt == n) {

        // Player 1 wins
        System.out.print("Player 1");
      }
      else {

        // Player 2 wins
        System.out.print("Player 2");
      }
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 2, 4, 8 };
    int N = arr.length;

    findWinnerGameRemoveGCD(arr, N);
  }
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the winner of the game by
# removing array elements whose GCD is 1
def findWinnerGameRemoveGCD(arr, n) :

    # mp[i]: Stores count of array
    # elements whose prime factor is i
    mp = dict.fromkeys(arr, 0);

    # Traverse the array
    for i in range(n) :

        # Calculate the prime factors
        # of arr[i]
        for j in range(2, int(arr[i] * (1/2)) + 1) :

            # If arr[i] is divisible by j
            if (arr[i] % j == 0) :

                # Update mp[j]
                mp[j] += 1;

                while (arr[i] % j == 0) :

                    # Update arr[i]
                    arr[i] = arr[i] // j;

        # If arr[i] exceeds 1
        if (arr[i] > 1) :
            mp[arr[i]] += 1;

    # Stores maximum value
    # present in the Map
    maxCnt = 0;

    # Traverse the map
    for i in mp:

        # Update maxCnt
        maxCnt = max(maxCnt,mp[i]);

    # If n is an even number
    if (n % 2 == 0) :

        # If maxCnt is greater
        # than or equal to n-1
        if (maxCnt >= n - 1) :

            # Player 1 wins
            print("Player 1",end="");

        else :

            # Player 2 wins
            print("Player 2",end="");

    else :

        # If maxCnt equal to n
        if (maxCnt == n) :

            # Player 1 wins
            print("Player 1",end="");

        else :

            # Player 2 wins
            print("Player 2",end="");

# Driver Code
if __name__ == "__main__" :
    arr = [ 2, 4, 8 ];
    N = len(arr);

    findWinnerGameRemoveGCD(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to find the winner of the game by
  // removing array elements whose GCD is 1
  static void findWinnerGameRemoveGCD(int []arr, int n)
  {

    // mp[i]: Stores count of array
    // elements whose prime factor is i
    Dictionary<int,
    int> mp = new Dictionary<int,
    int>();

    // Traverse the array
    for (int i = 0; i < n; i++) {

      // Calculate the prime factors
      // of arr[i]
      for (int j = 2; j * j <= arr[i];
           j++) {

        // If arr[i] is divisible by j
        if (arr[i] % j == 0)
        {

          // Update mp[j]
          if (mp.ContainsKey(j))
          {
            mp[j] = mp[j] + 1;
          }
          else
          {
            mp.Add(j, 1);
          }

          while (arr[i] % j == 0)
          {

            // Update arr[i]
            arr[i] = arr[i] / j;
          }
        }
      }

      // If arr[i] exceeds 1
      if (arr[i] > 1)
      {
        if(mp.ContainsKey(arr[i]))
        {
          mp[arr[i]] =  mp[arr[i]] + 1;
        }
        else
        {
          mp.Add(arr[i], 1);
        }
      }
    }

    // Stores maximum value
    // present in the Map
    int maxCnt = 0;

    // Traverse the map
    foreach (KeyValuePair<int,
             int> i in mp)
    {

      // Update maxCnt
      maxCnt = Math.Max(maxCnt, i.Value);
    }

    // If n is an even number
    if (n % 2 == 0)
    {

      // If maxCnt is greater
      // than or equal to n-1
      if (maxCnt >= n - 1)
      {

        // Player 1 wins
        Console.Write("Player 1");
      }
      else
      {

        // Player 2 wins
        Console.Write("Player 2");
      }
    }
    else
    {

      // If maxCnt equal to n
      if (maxCnt == n)
      {

        // Player 1 wins
        Console.Write("Player 1");
      }
      else
      {

        // Player 2 wins
        Console.Write("Player 2");
      }
    }
  }

  // Driver code
  public static void Main(String[] args)
  {
    int []arr = { 2, 4, 8 };
    int N = arr.Length;

    findWinnerGameRemoveGCD(arr, N);
  }
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
Player 1
```

***时间复杂度:** (N * sqrt(X))，其中 **X** 为阵中最大元素*
***辅助空间:** O(N)*