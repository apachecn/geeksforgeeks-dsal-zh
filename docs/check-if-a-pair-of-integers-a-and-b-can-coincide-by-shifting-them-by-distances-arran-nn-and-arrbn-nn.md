# 通过将一对整数 A 和 B 移动距离 arr[(A%N +N)%N]和 arr[(B % N+N)% N]]来检查它们是否可以重合

> 原文:[https://www . geeksforgeeks . org/check-如果一对整数 a 和 b 可以通过按距离移动它们来重合-arran-nn 和-arrbn-nn/](https://www.geeksforgeeks.org/check-if-a-pair-of-integers-a-and-b-can-coincide-by-shifting-them-by-distances-arran-nn-and-arrbn-nn/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在将两个整数 **A** 和 **B** 移动一个距离 **arr[(A%N +N)%N]** 和 **arr[(B%N +N)%N]** 后，检查它们是否在数字线上的一个点重合。如果不可能，则打印**“否”**。否则，打印**“是”**。

**示例:**

> **输入:** arr[] = {5，4，3}
> **输出:**是
> **解释:**
> 让 A = -4 和 B = -6 的值在数字线上的点-1 重合。
> 换挡后，
> A =-4+arr[(-4% 3+3)% 3]=-4+arr[2]=-4+3 =-1。
> B =-6+arr[(-6% 3+3)% 3]=-6+5 =-1。
> 
> **输入:** arr[]= {-4，4，4，4}
> 输出:否

**方法:**按照以下步骤解决问题:

*   初始化一个 [Hashmap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) ，比如 **mp，**来存储整数的最终位置。
*   初始化一个字符串，说 **ans，**为“**No”**存储需要的答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   将 **i** 的最终位置存储在一个变量中，比如说**temp =****((I+arr[I])% N+N)% N**。
    *   如果 [**温度**的值存在于 **mp**](https://www.geeksforgeeks.org/map-find-function-in-c-stl/) 中，则将 **ans** 设置为**“是”**[并断开回路](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   通过将 **mp【温度】**增加 **1** ，将**温度**标记为已访问。
*   完成上述步骤后，打印**和**的值作为所需答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if two
// integers coincide at a point
void checkSamePosition(int arr[], int n)
{
    // Store the final position
    // of integers A and B
    unordered_map<int, int> mp;

    // Iterate over the range[0, n]
    for (int i = 0; i < n; i++) {

        // Store the final position
        // of the integer i
        int temp = ((i + arr[i]) % n + n) % n;

        // If temp is present in the Map
        if (mp.find(temp) != mp.end()) {

            // Print Yes and return
            cout << "Yes";
            return;
        }

        // Mark its final
        // position as visited
        mp[temp]++;
    }

    // If every integer stored
    // in the Map is unique
    cout << "No";
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    checkSamePosition(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

  // Function to check if two
  // integers coincide at a point
  static void checkSamePosition(int[] arr, int n)
  {

    // Store the final position
    // of integers A and B
    Map<Integer,
    Integer> mp = new HashMap<Integer,
    Integer>();

    // Iterate over the range[0, n]
    for (int i = 0; i < n; i++) {

      // Store the final position
      // of the integer i
      int temp = ((i + arr[i]) % n + n) % n;

      // If temp is present in the Map
      if (mp.get(temp) == null) {

        // Print Yes and return
        System.out.println("Yes");
        return;
      }

      // Mark its final
      // position as visited

      mp.get(temp + 1);
    }

    // If every integer stored
    // in the Map is unique
    System.out.println("No");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 5, 4, 3 };
    int N = arr.length;

    checkSamePosition(arr, N);
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if two
# integers coincide at a point
def checkSamePosition(arr, n):
    # Store the final position
    # of integers A and B
    mp = {}

    # Iterate over the range[0, n]
    for i in range(n):
        # Store the final position
        # of the integer i
        temp = ((i + arr[i]) % n + n) % n

        # If temp is present in the Map
        if temp in mp:
            # Print Yes and return
            print("Yes")
            return

        # Mark its final
        # position as visited
        if(temp in mp):
            mp[temp] += 1
        else:
            mp[temp] = mp.get(temp,0)+1

    # If every integer stored
    # in the Map is unique
    print("No")

# Driver Code
if __name__ == '__main__':
    arr =  [5, 4, 3]
    N = len(arr)
    checkSamePosition(arr, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to check if two
    // integers coincide at a point
    static void checkSamePosition(int[] arr, int n)
    {

        // Store the final position
        // of integers A and B
        Dictionary<int, int> mp = new Dictionary<int, int>();

        // Iterate over the range[0, n]
        for (int i = 0; i < n; i++) {

            // Store the final position
            // of the integer i
            int temp = ((i + arr[i]) % n + n) % n;

            // If temp is present in the Map
            if (mp.ContainsKey(temp)) {

                // Print Yes and return
                Console.Write("Yes");
                return;
            }

            // Mark its final
            // position as visited
            mp[temp] = 1;
        }

        // If every integer stored
        // in the Map is unique
        Console.Write("No");
    }

  // Driver code
  static void Main() {
    int[] arr = { 5, 4, 3 };
    int N = arr.Length;

    checkSamePosition(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if two
// integers coincide at a point
function checkSamePosition(arr, n)
{
    // Store the final position
    // of integers A and B
    var mp = new Map();

    // Iterate over the range[0, n]
    for (var i = 0; i < n; i++) {

        // Store the final position
        // of the integer i
        var temp = ((i + arr[i]) % n + n) % n;

        // If temp is present in the Map
        if (mp.has(temp)) {

            // Print Yes and return
            document.write( "Yes");
            return;
        }

        // Mark its final
        // position as visited
        if(mp.has(temp))
        {
            mp.set(temp, mp.get(temp)+1)
        }
        else  
            mp.set(temp, 1)
    }

    // If every integer stored
    // in the Map is unique
    document.write( "No");
}

// Driver Code

var arr = [5, 4, 3 ];
var N = arr.length;

checkSamePosition(arr, N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)