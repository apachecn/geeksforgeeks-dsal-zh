# 找到具有相同数字和的最大和对

> 原文:[https://www . geeksforgeeks . org/find-最大和对同位数和/](https://www.geeksforgeeks.org/find-maximum-sum-pair-with-same-digit-sum/)

给定一个具有 **N** 个整数的数组 **arr** ，任务是找到一个具有最大和且具有相同位数和的对。打印该对的总和(如果存在)。否则，打印 **-1** 。

**示例:**

> **输入:** arr[]={55，23，32，46，88}
> **输出:** 46 55 101
> **解释:** Pair {55，46}将给出 55 + 46 = 101 的和
> 
> **输入:** arr[]={18，19，23，15}
> **输出:** -1

**方法:**按照以下步骤解决这个问题:

1.  创建一个地图，比如 **mp** 来存储一个数字中的数字总和作为关键字，以及具有该数字总和的最大数字作为值。
2.  现在创建一个全局变量**和**来存储这个问题的答案。
3.  现在开始遍历数组，在每次迭代中:
    *   检查其数字的总和是否已经出现在地图中。如果是，那么用 ans 的最大值和两个数之和来改变 **ans** 。
    *   如果地图中没有这些数字的总和。为它创建一个新的密钥并存储它的值。否则，如果地图中的数字大于现有数字，请更新该数字。
4.  返回 **ans** 作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find sum of digits
int digitSum(long n)
{
    long sum = 0;
    while (n) {
        sum += (n % 10);
        n /= 10;
    }
    return sum;
}

// Function to find maximum sum pair
// having the same sum of digits
void findMax(vector<int> arr, int n)
{
    // Map to store the sum of digits
    // in a number as the key and
    // the maximum number having
    // that sum of digits as the value
    unordered_map<int, int> mp;
    int ans = -1, pairi = 0, pairj = 0;
    for (int i = 0; i < n; i++) {

        // Store the current sum of digits
        // of the number in temp
        int temp = digitSum(arr[i]);

        // If temp is already present
        // in the map then update
        // ans if the sum is greater
        // than the existing value
        if (mp[temp] != 0) {
            if (arr[i] + mp[temp] > ans) {
                pairi = arr[i];
                pairj = mp[temp];
                ans = pairi + pairj;
            }
        }

        // Change the value in the map
        mp[temp] = max(arr[i], mp[temp]);
    }

    cout << pairi << " " << pairj
         << " " << ans << endl;
}

// Driver Code Starts.
int main()
{
    vector<int> arr = { 55, 23, 32, 46, 88 };
    int n = arr.size();
    findMax(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find sum of digits
static int digitSum(long n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += (n % 10);
        n /= 10;
    }
    return sum;
}

// Function to find maximum sum pair
// having the same sum of digits
static void findMax(int []arr, int n)
{

    // Map to store the sum of digits
    // in a number as the key and
    // the maximum number having
    // that sum of digits as the value
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();
    int ans = -1, pairi = 0, pairj = 0;
    for (int i = 0; i < n; i++) {

        // Store the current sum of digits
        // of the number in temp
        int temp = digitSum(arr[i]);

        // If temp is already present
        // in the map then update
        // ans if the sum is greater
        // than the existing value
        if (mp.containsKey(temp)) {
            if (arr[i] + mp.get(temp) > ans) {
                pairi = arr[i];
                pairj = mp.get(temp);
                ans = pairi + pairj;
            }
            mp.put(temp, Math.max(arr[i], mp.get(temp)));
        }
        else
        // Change the value in the map
        mp.put(temp, arr[i]);

    }

    System.out.print(pairi+ " " +  pairj
        + " " +  ans +"\n");
}

// Driver Code Starts.
public static void main(String[] args)
{
    int []arr = { 55, 23, 32, 46, 88 };
    int n = arr.length;
    findMax(arr, n);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find sum of digits
def digitSum(n):
    sum = 0
    while (n):
        sum += (n % 10)
        n = n // 10
    return sum

# Function to find maximum sum pair
# having the same sum of digits
def findMax(arr, n):

    # Map to store the sum of digits
    # in a number as the key and
    # the maximum number having
    # that sum of digits as the value
    mp = {}
    ans = -1
    pairi = 0
    pairj = 0
    for i in range(n):

        # Store the current sum of digits
        # of the number in temp
        temp = digitSum(arr[i])

        # If temp is already present
        # in the map then update
        # ans if the sum is greater
        # than the existing value
        if (temp not in mp):
            mp[temp] = 0

        if (mp[temp] != 0) :
            if (arr[i] + mp[temp] > ans):
                pairi = arr[i]
                pairj = mp.get(temp)
                ans = pairi + pairj

        # Change the value in the map
        mp[temp] = max(arr[i], mp[temp])
    print(f"{pairi} {pairj} {ans}")

# Driver Code Starts.
arr = [55, 23, 32, 46, 88]
n = len(arr)
findMax(arr, n)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find sum of digits
static int digitSum(long n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += (int)(n % 10);
        n /= 10;
    }
    return sum;
}

// Function to find maximum sum pair
// having the same sum of digits
static void findMax(int []arr, int n)
{

    // Map to store the sum of digits
    // in a number as the key and
    // the maximum number having
    // that sum of digits as the value
    Dictionary<int,int> mp = new Dictionary<int, int>();
    int ans = -1, pairi = 0, pairj = 0;
    for (int i = 0; i < n; i++) {

        // Store the current sum of digits
        // of the number in temp
        int temp = digitSum(arr[i]);

        // If temp is already present
        // in the map then update
        // ans if the sum is greater
        // than the existing value
        if (mp.ContainsKey(temp)) {
            if (arr[i] + mp[temp] > ans) {
                pairi = arr[i];
                pairj = mp[temp];
                ans = pairi + pairj;
            }
            mp[temp] = Math.Max(arr[i], mp[temp]);
        }
        else
        // Change the value in the map
        mp[temp] = arr[i];

    }

    Console.WriteLine(pairi+ " " +  pairj + " " +  ans );
}

// Driver Code Starts.
public static void Main()
{
    int []arr = { 55, 23, 32, 46, 88 };
    int n = arr.Length;
    findMax(arr, n);
}
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to find sum of digits
       function digitSum(n) {
           let sum = 0;
           while (n) {
               sum += (n % 10);
               n = Math.floor(n / 10);
           }
           return sum;
       }

       // Function to find maximum sum pair
       // having the same sum of digits
       function findMax(arr, n)
       {

           // Map to store the sum of digits
           // in a number as the key and
           // the maximum number having
           // that sum of digits as the value
           let mp = new Map();
           let ans = -1, pairi = 0, pairj = 0;
           for (let i = 0; i < n; i++) {

               // Store the current sum of digits
               // of the number in temp
               let temp = digitSum(arr[i]);

               // If temp is already present
               // in the map then update
               // ans if the sum is greater
               // than the existing value

               if (!mp.has(temp)) {
                   mp.set(temp, 0);
               }
               if (mp.get(temp) != 0) {
                   if (arr[i] + mp.get(temp) > ans) {
                       pairi = arr[i];
                       pairj = mp.get(temp);
                       ans = pairi + pairj;
                   }
               }

               // Change the value in the map
               mp.set(temp, Math.max(arr[i], mp.get(temp)));
           }

           document.write(pairi + " " + pairj
               + " " + ans + '<br>');
       }

       // Driver Code Starts.
       let arr = [55, 23, 32, 46, 88];
       let n = arr.length;
       findMax(arr, n);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
46 55 101
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)