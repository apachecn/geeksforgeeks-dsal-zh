# 从数组 A 加上某个值 X 形成的数组 B 中找出缺失的值

> 原文:[https://www . geeksforgeeks . org/find-数组中缺少的值-b-通过向数组 a 中添加一些值-x 形成/](https://www.geeksforgeeks.org/find-the-missing-value-from-array-b-formed-by-adding-some-value-x-to-array-a/)

给定两个阵列 **arr1[]** 和 **arr2[]** ，大小分别为 **N** 和**N–1**。**arr 2【】**中的每一个值都是通过在 **N-1** 次的任意 **arr1[i]** 上加上一个隐藏值如 **X** 得到的，这意味着对于任意 **i** ， **arr1[i]+X** 不包含在**arr 2【】**中，也就是**arr 2【】**中的缺失值。任务是找到隐藏值 **X** 和未从**arr 1【】**中选取的缺失值。

**示例:**

> **输入:** arr1[] = {3，6，5，10}，arr2[] = {17，10，13}
> **输出:** Hidden = 7，Missing = 5
> **说明:**第二个数组的元素是这样得到的:
> 第一个元素:(10 + 7) = 17，10 是 arr 1[
> 第二个元素(3 + 7) = 10 的索引 4 处的元素， 3 是 arr1[]
> 索引 0 处的元素第三个元素:(6 + 7) = 13，6 是 arr1[]
> 索引 1 处的元素所以，7 是隐藏值，5 是缺失值。
> 
> **输入:** arr1[] = {4，1，7}，arr2[] = {4，10}
> **输出:**隐藏= 3，缺失= 4

**做法:这个问题可以用**解决

*   [按非递减顺序对两个给定数组进行排序](https://www.geeksforgeeks.org/sort-c-stl/)。
*   创建一个[无序地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)来存储差异。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) s 直到**N–1**，通过存储两个数组元素的**差**来检查值。
    *   让**a = arr 2[I]–arr 1[I]**和**b = arr 2[I]–arr 1[I+1]**。
    *   如果**一个！=b** 然后检查是否
        *   **a > 0** ，然后存储在地图中。
        *   **b > 0** ，然后存入地图。
    *   否则检查 a 是否> 0，然后将其存储在地图中。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)找到**隐藏的**值并打印出来。
*   通过添加隐藏值遍历 **arr1[]** ，检查是否存在于 **arr2[]** 中，否则打印**缺失的**值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the hidden
// and missing values
void findHiddenMissing(int arr1[], int arr2[], int N)
{
    // Sorting both the arrays
    sort(arr1, arr1 + N);
    sort(arr2, arr2 + N - 1);

    // Create a map
    unordered_map<int, int> mp;

    // Traversing the arrays and
    // checking for the values
    for (int i = 0; i < N - 1; i++) {
        // Variable to store the difference
        // between the elements of arr2
        // and arr1 in same indices
        int a = arr2[i] - arr1[i];

        // Variable to store the difference
        // between the elements of arr2
        // and arr1 next index
        int b = arr2[i] - arr1[i + 1];

        // If a is not equals to b
        if (a != b) {
            // If a is greater than 0
            if (a > 0)
                mp[a] += 1;

            // If b is greater than 0
            if (b > 0)
                mp[b] += 1;
        }

        // If a is equal to b
        else {
            // If a is greater than 0
            if (a > 0)
                mp[a] += 1;
        }
    }

    // To store the hidden value
    int hidden;

    // Iterate over the map and searching
    // for the hidden value
    for (auto it : mp) {
        if (it.second == N - 1) {
            hidden = it.first;
            cout << "Hidden: " << it.first;
            break;
        }
    }
    cout << endl;

    // Find the missing value
    for (int i = 0; i < N; i++) {
        if (arr1[i] + hidden != arr2[i]) {
            cout << "Missing: " << arr1[i];
            break;
        }
    }
}

// Driver Code
int main()
{
    int arr1[] = { 3, 6, 5, 10 };
    int arr2[] = { 17, 10, 13 };

    int N = sizeof(arr1) / sizeof(arr1[0]);

    findHiddenMissing(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
import java.util.HashMap;

class GFG {

    // Function to find the hidden
    // and missing values
    public static void findHiddenMissing(int arr1[], int arr2[], int N)
    {

        // Sorting both the arrays
        Arrays.sort(arr1);
        Arrays.sort(arr2);

        // Create a map
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Traversing the arrays and
        // checking for the values
        for (int i = 0; i < N - 1; i++)
        {

            // Variable to store the difference
            // between the elements of arr2
            // and arr1 in same indices
            int a = arr2[i] - arr1[i];

            // Variable to store the difference
            // between the elements of arr2
            // and arr1 next index
            int b = arr2[i] - arr1[i + 1];

            // If a is not equals to b
            if (a != b) {
                // If a is greater than 0
                if (a > 0) {
                    if (mp.containsKey(a))
                        mp.put(a, mp.get(a) + 1);
                    else
                        mp.put(a, 1);
                }

                // If b is greater than 0
                if (b > 0)
                    if (mp.containsKey(b))
                        mp.put(b, mp.get(b) + 1);
                    else
                        mp.put(b, 1);
            }

            // If a is equal to b
            else {
                // If a is greater than 0
                if (a > 0)
                    if (mp.containsKey(a))
                        mp.put(a, mp.get(a) + 1);
                    else
                        mp.put(a, 1);

            }
        }

        // To store the hidden value
        int hidden = 0;

        // Iterate over the map and searching
        // for the hidden value
        for (int it : mp.keySet()) {
            if (mp.get(it) == N - 1) {
                hidden = it;
                System.out.println("Hidden: " + it);
                break;
            }
        }

        // Find the missing value
        for (int i = 0; i < N; i++) {
            if (arr1[i] + hidden != arr2[i]) {
                System.out.println("Missing: " + arr1[i]);
                break;
            }
        }
    }

    // Driver Code
    public static void main(String args[]) {
        int arr1[] = { 3, 6, 5, 10 };
        int arr2[] = { 17, 10, 13 };

        int N = arr1.length;

        findHiddenMissing(arr1, arr2, N);

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the hidden
# and missing values
def findHiddenMissing(arr1, arr2, N):

        # Sorting both the arrays
    arr1.sort()
    arr2.sort()

    # Create a map
    mp = {}

    # Traversing the arrays and
    # checking for the values
    for i in range(0, N - 1):

                # Variable to store the difference
                # between the elements of arr2
                # and arr1 in same indices
        a = arr2[i] - arr1[i]

        # Variable to store the difference
        # between the elements of arr2
        # and arr1 next index
        b = arr2[i] - arr1[i + 1]

        # If a is not equals to b
        if (a != b):
                        # If a is greater than 0
            if (a > 0):
                if not a in mp:
                    mp[a] = 1
                else:
                    mp[a] += 1

                    # If b is greater than 0
            if (b > 0):
                if not b in mp:
                    mp[b] = 1
                else:
                    mp[b] += 1

                # If a is equal to b
        else:
                        # If a is greater than 0
            if (a > 0):
                if not a in mp:
                    mp[a] = 1
                else:
                    mp[a] += 1

        # To store the hidden value
    hidden = 0

    # Iterate over the map and searching
    # for the hidden value
    for it in mp:
        if (mp[it] == N - 1):
            hidden = it
            print("Hidden:", end=" ")
            print(it)
            break

        # Find the missing value
    for i in range(0, N):
        if (arr1[i] + hidden != arr2[i]):
            print("Missing:", end=" ")
            print(arr1[i])
            break

# Driver Code
if __name__ == "__main__":

    arr1 = [3, 6, 5, 10]
    arr2 = [17, 10, 13]

    N = len(arr1)

    findHiddenMissing(arr1, arr2, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG {

    // Function to find the hidden
    // and missing values
    public static void findHiddenMissing(int []arr1, int []arr2, int N)
    {

        // Sorting both the arrays
        Array.Sort(arr1);
        Array.Sort(arr2);

        // Create a map
        Dictionary<int, int> mp = new Dictionary<int, int>();

        // Traversing the arrays and
        // checking for the values
        for (int i = 0; i < N - 1; i++)
        {

            // Variable to store the difference
            // between the elements of arr2
            // and arr1 in same indices
            int a = arr2[i] - arr1[i];

            // Variable to store the difference
            // between the elements of arr2
            // and arr1 next index
            int b = arr2[i] - arr1[i + 1];

            // If a is not equals to b
            if (a != b) {
                // If a is greater than 0
                if (a > 0) {
                    if (mp.ContainsKey(a))
                        mp[a] = mp[a] + 1;
                    else
                        mp.Add(a, 1);
                }

                // If b is greater than 0
                if (b > 0)
                    if (mp.ContainsKey(b))
                        mp[b] = mp[b] + 1;
                    else
                        mp.Add(b, 1);
            }

            // If a is equal to b
            else {
                // If a is greater than 0
                if (a > 0)
                    if (mp.ContainsKey(a))
                        mp[a] = mp[a] + 1;
                    else
                        mp.Add(a, 1);

            }
        }

        // To store the hidden value
        int hidden = 0;

        // Iterate over the map and searching
        // for the hidden value
        foreach(int it in mp.Keys) {
            if (mp[it] == N - 1) {
                hidden = it;
                Console.WriteLine("Hidden: " + it);
                break;
            }
        }

        // Find the missing value
        for (int i = 0; i < N; i++) {
            if (arr1[i] + hidden != arr2[i]) {
                Console.WriteLine("Missing: " + arr1[i]);
                break;
            }
        }
    }

    // Driver Code
    public static void Main(string []args) {
        int []arr1 = { 3, 6, 5, 10 };
        int []arr2 = { 17, 10, 13 };

        int N = arr1.Length;

        findHiddenMissing(arr1, arr2, N);

    }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the hidden
// and missing values
function findHiddenMissing(arr1, arr2, N)
{

  // Sorting both the arrays
  arr1.sort((a, b) => a - b);
  arr2.sort((a, b) => a - b);

  // Create a map
  let mp = new Map();

  // Traversing the arrays and
  // checking for the values
  for (let i = 0; i < N - 1; i++)
  {

    // Variable to store the difference
    // between the elements of arr2
    // and arr1 in same indices
    let a = arr2[i] - arr1[i];

    // Variable to store the difference
    // between the elements of arr2
    // and arr1 next index
    let b = arr2[i] - arr1[i + 1];

    // If a is not equals to b
    if (a != b) {
      // If a is greater than 0
      if (a > 0) {
        if (mp.has(a)) {
          mp.set(a, mp.get(a) + 1);
        } else {
          mp.set(a, 1);
        }
      }

      // If b is greater than 0
      if (b > 0)
        if (mp.has(b)) {
          mp.set(b, mp.get(b) + 1);
        } else {
          mp.set(b, 1);
        }
    }

    // If a is equal to b
    else {
      // If a is greater than 0
      if (a > 0) {
        if (mp.has(a)) {
          mp.set(a, mp.get(a) + 1);
        } else {
          mp.set(a, 1);
        }
      }
    }
  }

  // To store the hidden value
  let hidden;

  // Iterate over the map and searching
  // for the hidden value
  for (let it of mp) {
    if (it[1] == N - 1) {
      hidden = it[0];
      document.write("Hidden: " + it[0]);
      break;
    }
  }
  document.write("<br>");

  // Find the missing value
  for (let i = 0; i < N; i++) {
    if (arr1[i] + hidden != arr2[i]) {
      document.write("Missing: " + arr1[i]);
      break;
    }
  }
}

// Driver Code
let arr1 = [3, 6, 5, 10];
let arr2 = [17, 10, 13];

let N = arr1.length;

findHiddenMissing(arr1, arr2, N);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
Hidden: 7
Missing: 5
```

**时间复杂度:** O(N)

**辅助空间:** O(N)