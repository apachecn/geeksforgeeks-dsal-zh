# 使每个数组元素的频率等于其值所需的最小移除量

> 原文:[https://www . geeksforgeeks . org/最小移除量-要求使每个数组元素的频率等于其值/](https://www.geeksforgeeks.org/minimum-removals-required-to-make-frequency-of-each-array-element-equal-to-its-value/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到需要移除的数组元素的最小数量，使得每个数组元素的频率等于其值

**示例:**

> **输入:** arr[] = { 2，4，1，4，2 }
> **输出:** 2
> **解释:**
> 从数组中移除 arr[1]会将 arr[]修改为{ 2，1，4，2 }
> 从数组中移除 arr[2]会将 arr[]修改为{ 2，1，2 }
> 数组中不同的元素分别为:{ 1，2 }，频率为 1 和 2。
> 因此，要求的输出为 2。
> 
> **输入:** arr[] = { 2，7，1，8，2，8，1，8 }
> **输出:** 5

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)比如说， **mp** 来存储数组中每个不同元素的频率。
*   [遍历数组](https://www.geeksforgeeks.org/greedy-algorithms/)和[存储数组](https://www.geeksforgeeks.org/greedy-algorithms/)中每个不同元素的频率。
*   初始化一个变量，比如 **cntMinRem** 来存储需要移除的数组元素的最小数量，使得**arr【I】**的频率等于**arr【I】**。
*   [使用地图的键值作为 **i** 遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，检查以下条件:
    *   如果 **mp[i] < i** ，则更新 **cntMinRem += mp[i]** 的值。
    *   如果 **mp[i] > i** ，则更新**cntMinRem+=(MP[I]–I)**的值。

*   最后，打印 **cntMinRem** 的值。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of
// elements required to be removed such
// that frequency of arr[i] equal to arr[i]
int min_elements(int arr[], int N)
{
    // Stores frequency of each
    // element of the array
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency
        // of arr[i]
        mp[arr[i]]++;
    }

    // Stores minimum count of removals
    int cntMinRem = 0;

    // Traverse the map
    for (auto it : mp) {

        // Stores key value
        // of the map
        int i = it.first;

        // If frequency of i is
        // less than i
        if (mp[i] < i) {

            // Update cntMinRem
            cntMinRem += mp[i];
        }

        // If frequency of i is
        // greater than i
        else if (mp[i] > i) {

            // Update cntMinRem
            cntMinRem += (mp[i] - i);
        }
    }

    return cntMinRem;
}

// Driver Code
int main()
{

    int arr[] = { 2, 4, 1, 4, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << min_elements(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the minimum count of
// elements required to be removed such
// that frequency of arr[i] equal to arr[i]
public static int min_elements(int arr[], int N)
{

    // Stores frequency of each
    // element of the array
    Map<Integer,
        Integer> mp = new HashMap<Integer,
                                  Integer>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        mp.put(arr[i],
               mp.getOrDefault(arr[i], 0) + 1);
    }

    // Stores minimum count of removals
    int cntMinRem = 0;

    // Traverse the map
    for(int key : mp.keySet())
    {

        // Stores key value
        // of the map
        int i = key;
        int val = mp.get(i);

        // If frequency of i is
        // less than i
        if (val < i)
        {

            // Update cntMinRem
            cntMinRem += val;
        }

        // If frequency of i is
        // greater than i
        else if (val > i)
        {

            // Update cntMinRem
            cntMinRem += (val - i);
        }
    }
    return cntMinRem;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 1, 4, 2 };

    System.out.println(min_elements(
        arr, arr.length));
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum count of
# elements required to be removed such
# that frequency of arr[i] equal to arr[i]
def min_elements(arr, N) :

    # Stores frequency of each
    # element of the array
    mp = {};

    # Traverse the array
    for i in range(N) :

        # Update frequency
        # of arr[i]
        if arr[i] in mp :
            mp[arr[i]] += 1;
        else :
            mp[arr[i]] = 1;

    # Stores minimum count of removals
    cntMinRem = 0;

    # Traverse the map
    for it in mp :

        # Stores key value
        # of the map
        i = it;

        # If frequency of i is
        # less than i
        if (mp[i] < i) :

            # Update cntMinRem
            cntMinRem += mp[i];

        # If frequency of i is
        # greater than i
        elif (mp[i] > i) :

            # Update cntMinRem
            cntMinRem += (mp[i] - i);

    return cntMinRem;

# Driver Code
if __name__ == "__main__" :

    arr = [ 2, 4, 1, 4, 2 ];
    N = len(arr);
    print(min_elements(arr, N));

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the minimum count of
    // elements required to be removed such
    // that frequency of arr[i] equal to arr[i]
    static int min_elements(int[] arr, int N)
    {

        // Stores frequency of each
        // element of the array
        Dictionary<int, int> mp = new Dictionary<int, int>(); 

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Update frequency
            // of arr[i]
            if(mp.ContainsKey(arr[i]))
            {
                mp[arr[i]]++;
            }
            else
            {
                mp[arr[i]] = 1;
            }
        }

        // Stores minimum count of removals
        int cntMinRem = 0;

        // Traverse the map
        foreach (KeyValuePair<int, int> it in mp)
        {

            // Stores key value
            // of the map
            int i = it.Key;

            // If frequency of i is
            // less than i
            if (mp[i] < i)
            {

                // Update cntMinRem
                cntMinRem += mp[i];
            }

            // If frequency of i is
            // greater than i
            else if (mp[i] > i)
            {

                // Update cntMinRem
                cntMinRem += (mp[i] - i);
            }
        }    
        return cntMinRem;
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 2, 4, 1, 4, 2 };
    int N = arr.Length;
    Console.Write(min_elements(arr, N));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the minimum count of
// elements required to be removed such
// that frequency of arr[i] equal to arr[i]
function min_elements(arr, N)
{
    // Stores frequency of each
    // element of the array
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Update frequency
        // of arr[i]
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i])+1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // Stores minimum count of removals
    var cntMinRem = 0;

    // Traverse the map
    mp.forEach((value, key) => {

        // Stores key value
        // of the map
        var i = key;

        // If frequency of i is
        // less than i
        if (mp.get(i) < i) {

            // Update cntMinRem
            cntMinRem += mp.get(i);
        }

        // If frequency of i is
        // greater than i
        else if (mp.get(i) > i) {

            // Update cntMinRem
            cntMinRem += (mp.get(i) - i);
        }
    });

    return cntMinRem;
}

// Driver Code
var arr = [2, 4, 1, 4, 2];
var N = arr.length;
document.write( min_elements(arr, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)