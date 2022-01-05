# 将一个数组划分为两个具有相同数量唯一元素的子集

> 原文:[https://www . geeksforgeeks . org/将一个数组划分为两个具有相同数量唯一元素的子集/](https://www.geeksforgeeks.org/partition-an-array-into-two-subsets-with-equal-count-of-unique-elements/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是将数组划分为两个[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，使得两个子集中唯一元素的[计数相同，对于每个元素，如果该元素属于第一个子集，则打印 **1** 。否则，打印 **2** 。如果做不到这样的分区，那么打印**-1”**。](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)

**示例:**

> **输入:** arr[] = {1，1，2，3，4，4}
> **输出:**1 1 2 1 1
> **解释:**将数组分区的第一个和第二个子集视为{1，1，2，4 4}和{3}。现在，上述子集划分具有相同数量的不同元素..
> 
> **输入:** arr[] = {1，1，2，2，3}
> **输出:** -1

**天真方法:**给定的问题可以通过[将数组元素的所有可能的分区生成为两个子集](https://www.geeksforgeeks.org/count-number-of-ways-to-partition-a-set-into-k-subsets/)来解决，如果存在任何这样的分区，其不同元素的[计数](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)相同，则根据数组元素所属的相应集合打印 **1** 和 **2** 。否则，打印**-1”**，因为不存在任何这种可能的阵列分区。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过[找到唯一数组元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)进行优化，如果频率是奇数，那么就没有这种可能的划分。否则，相应地打印子集的分区。按照以下步骤解决问题:

*   初始化一张[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，说**M**T4【存储所有阵元的频率】。
*   初始化数组，比如**ans【】**存储每个数组元素所属的子集号。
*   通过在地图 **M** 中计数具有频率 **1** 的元素，找到数组中唯一元素的计数。让这个数成为 **C** 。
*   [如果 **C** 的值为偶数](https://www.geeksforgeeks.org/check-if-a-number-is-odd-or-even-using-bitwise-operators/)，则通过将这些元素标记为 **1** 将这些元素的一半移动到第一个子集中，并将数组中的所有元素标记为**2****ans[]**。
*   否则，检查是否存在任何频率大于 **2** 的元素，然后将该元素的一个实例转移到第二个子集。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to partition the array into
// two subsets such that count of unique
// elements in both subsets is the same
void arrayPartition(int a[], int n)
{
    // Stores the subset number for
    // each array elements
    int ans[n];

    // Stores the count of unique
    // array elements
    int cnt = 0;
    int ind, flag = 0;

    // Stores the frequency of elements
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < n; i++) {
        mp[a[i]]++;
    }

    // Count of elements having a
    // frequency of 1
    for (int i = 0; i < n; i++) {

        if (mp[a[i]] == 1)
            cnt++;

        // Check if there exists any
        // element with frequency > 2
        if (mp[a[i]] > 2 && flag == 0) {
            flag = 1;
            ind = i;
        }
    }

    // Count of elements needed to
    // have frequency exactly 1 in
    // each subset
    int p = (cnt + 1) / 2;
    int ans1 = 0;

    // Initialize all values in the
    /// array ans[] as 1
    for (int i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array ans[]
    for (int i = 0; i < n; i++) {

        // This array element is a
        // part of first subset
        if (mp[a[i]] == 1 && ans1 < p) {
            ans[i] = 1;
            ans1++;
        }

        // Half array elements with
        // frequency 1 are part of
        // the second subset
        else if (mp[a[i]] == 1) {
            ans[i] = 2;
        }
    }

    // If count of elements is exactly
    // 1 are odd and has no element
    // with frequency > 2
    if (cnt % 2 == 1 && flag == 0) {
        cout << -1 << endl;
        return;
    }

    // If count of elements that occurs
    // exactly once are even
    if (cnt % 2 == 0) {

        // Print the result
        for (int i = 0; i < n; i++) {
            cout << ans[i] << " ";
        }
    }

    // If the count of elements has
    // exactly 1 frequency are odd
    // and there is an element with
    // frequency greater than 2
    else {

        // Print the result
        for (int i = 0; i < n; i++) {
            if (ind == i)
                cout << 2 << " ";
            else
                cout << ans[i] << " ";
        }
    }
}

// Driver Codea
int main()
{
    int arr[] = { 1, 1, 2, 3, 4, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    arrayPartition(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.HashMap;

class GFG{

// Function to partition the array into
// two subsets such that count of unique
// elements in both subsets is the same
public static void arrayPartition(int a[], int n)
{
    // Stores the subset number for
    // each array elements
    int[] ans = new int[n];

    // Stores the count of unique
    // array elements
    int cnt = 0;
    int ind = 0, flag = 0;

    // Stores the frequency of elements
    HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

    // Traverse the array
    for (int i = 0; i < n; i++) {
        if(mp.containsKey(a[i])){
            mp.put(a[i], mp.get(a[i]) + 1);
        }else{
            mp.put(a[i], 1);
        }
    }

    // Count of elements having a
    // frequency of 1
    for (int i = 0; i < n; i++) {

        if (mp.get(a[i]) == 1)
            cnt++;

        // Check if there exists any
        // element with frequency > 2
        if (mp.get(a[i]) > 2 && flag == 0) {
            flag = 1;
            ind = i;
        }
    }

    // Count of elements needed to
    // have frequency exactly 1 in
    // each subset
    int p = (cnt + 1) / 2;
    int ans1 = 0;

    // Initialize all values in the
    /// array ans[] as 1
    for (int i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array ans[]
    for (int i = 0; i < n; i++) {

        // This array element is a
        // part of first subset
        if (mp.get(a[i]) == 1 && ans1 < p) {
            ans[i] = 1;
            ans1++;
        }

        // Half array elements with
        // frequency 1 are part of
        // the second subset
        else if (mp.get(a[i]) == 1) {
            ans[i] = 2;
        }
    }

    // If count of elements is exactly
    // 1 are odd and has no element
    // with frequency > 2
    if (cnt % 2 == 1 && flag == 0) {
        System.out.println(-1 + "\n");
        return;
    }

    // If count of elements that occurs
    // exactly once are even
    if (cnt % 2 == 0) {

        // Print the result
        for (int i = 0; i < n; i++) {
            System.out.print(ans[i] + " ");
        }
    }

    // If the count of elements has
    // exactly 1 frequency are odd
    // and there is an element with
    // frequency greater than 2
    else {

        // Print the result
        for (int i = 0; i < n; i++) {
            if (ind == i)
            System.out.print(2 + " ");
            else
            System.out.print(ans[i] + " ");
        }
    }
}

// Driver Codea
public static void main(String args[])
{
    int arr[] = { 1, 1, 2, 3, 4, 4 };
    int N = arr.length;
    arrayPartition(arr, N);

}
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to partition the array into
# two subsets such that count of unique
# elements in both subsets is the same
def arrayPartition(a, n):

    # Stores the subset number for
    # each array elements
    ans = [0] * n

    # Stores the count of unique
    # array elements
    cnt = 0
    ind, flag = 0, 0

    # Stores the frequency of elements
    mp = {}

    # Traverse the array
    for i in a:
        mp[i] = mp.get(i, 0) + 1

    # Count of elements having a
    # frequency of 1
    for i in range(n):
        if ((a[i] in mp) and mp[a[i]] == 1):
            cnt += 1

        # Check if there exists any
        # element with frequency > 2
        if (mp[a[i]] > 2 and flag == 0):
            flag = 1
            ind = i

    # Count of elements needed to
    # have frequency exactly 1 in
    # each subset
    p = (cnt + 1) // 2
    ans1 = 0

    # Initialize all values in the
    # array ans[] as 1
    for i in range(n):
        ans[i] = 1

    # Traverse the array ans[]
    for i in range(n):

        # This array element is a
        # part of first subset
        if ((a[i] in mp) and mp[a[i]] == 1 and
            ans1 < p):
            ans[i] = 1
            ans1 += 1

        # Half array elements with
        # frequency 1 are part of
        # the second subset
        elif ((a[i] in mp) and mp[a[i]] == 1):
            ans[i] = 2

    # If count of elements is exactly
    # 1 are odd and has no element
    # with frequency > 2
    if (cnt % 2 == 1 and flag == 0):
        print (-1)
        return

    # If count of elements that occurs
    # exactly once are even
    if (cnt % 2 == 0):

        # Print the result
        print(*ans)

    # If the count of elements has
    # exactly 1 frequency are odd
    # and there is an element with
    # frequency greater than 2
    else:

        # Print the result
        for i in range(n):
            if (ind == i):
                print(2, end = " ")
            else:
                print(ans[i], end = " ")

# Driver Codea
if __name__ == '__main__':

    arr = [ 1, 1, 2, 3, 4, 4 ]
    N = len(arr)

    arrayPartition(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to partition the array into
// two subsets such that count of unique
// elements in both subsets is the same
static void arrayPartition(int []a, int n)
{
    // Stores the subset number for
    // each array elements
    int []ans = new int[n];

    // Stores the count of unique
    // array elements
    int cnt = 0;
    int ind=0, flag = 0;

    // Stores the frequency of elements
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Traverse the array
    for (int i = 0; i < n; i++) {
        if(mp.ContainsKey(a[i]))
         mp[a[i]]++;
        else
          mp.Add(a[i],1);
    }

    // Count of elements having a
    // frequency of 1
    for (int i = 0; i < n; i++) {

        if (mp.ContainsKey(a[i]) && mp[a[i]] == 1)
            cnt++;

        // Check if there exists any
        // element with frequency > 2
        if (mp.ContainsKey(a[i]) && mp[a[i]] > 2 && flag == 0) {
            flag = 1;
            ind = i;
        }
    }

    // Count of elements needed to
    // have frequency exactly 1 in
    // each subset
    int p = (cnt + 1) / 2;
    int ans1 = 0;

    // Initialize all values in the
    /// array ans[] as 1
    for (int i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array ans[]
    for (int i = 0; i < n; i++) {

        // This array element is a
        // part of first subset
        if (mp.ContainsKey(a[i]) && mp[a[i]] == 1 && ans1 < p) {
            ans[i] = 1;
            ans1++;
        }

        // Half array elements with
        // frequency 1 are part of
        // the second subset
        else if (mp.ContainsKey(a[i]) && mp[a[i]] == 1) {
            ans[i] = 2;
        }
    }

    // If count of elements is exactly
    // 1 are odd and has no element
    // with frequency > 2
    if (cnt % 2 == 1 && flag == 0) {
        Console.Write(-1);
        return;
    }

    // If count of elements that occurs
    // exactly once are even
    if (cnt % 2 == 0) {

        // Print the result
        for (int i = 0; i < n; i++) {
            Console.Write(ans[i] + " ");
        }
    }

    // If the count of elements has
    // exactly 1 frequency are odd
    // and there is an element with
    // frequency greater than 2
    else {

        // Print the result
        for (int i = 0; i < n; i++) {
            if (ind == i)
                Console.Write(2 + " ");
            else
                Console.Write(ans[i] + " ");
        }
    }
}

// Driver Codea
public static void Main()
{
    int []arr = { 1, 1, 2, 3, 4, 4 };
    int N = arr.Length;
    arrayPartition(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to partition the array into
// two subsets such that count of unique
// elements in both subsets is the same
function arrayPartition(a, n) {
    // Stores the subset number for
    // each array elements
    let ans = new Array(n);

    // Stores the count of unique
    // array elements
    let cnt = 0;
    let ind, flag = 0;

    // Stores the frequency of elements
    let mp = new Map();

    // Traverse the array
    for (let i = 0; i < n; i++) {
        if (mp.has(a[i])) {
            mp.set(a[i], mp.get(a[i]) + 1)
        } else {
            mp.set(a[i], 1)
        }
    }

    // Count of elements having a
    // frequency of 1
    for (let i = 0; i < n; i++) {

        if (mp.get(a[i]) == 1)
            cnt++;

        // Check if there exists any
        // element with frequency > 2
        if (mp.get(a[i]) > 2 && flag == 0) {
            flag = 1;
            ind = i;
        }
    }

    // Count of elements needed to
    // have frequency exactly 1 in
    // each subset
    let p = Math.floor((cnt + 1) / 2);
    let ans1 = 0;

    // Initialize all values in the
    /// array ans[] as 1
    for (let i = 0; i < n; i++)
        ans[i] = 1;

    // Traverse the array ans[]
    for (let i = 0; i < n; i++) {

        // This array element is a
        // part of first subset
        if (mp.get(a[i]) == 1 && ans1 < p) {
            ans[i] = 1;
            ans1++;
        }

        // Half array elements with
        // frequency 1 are part of
        // the second subset
        else if (mp.get(a[i]) == 1) {
            ans[i] = 2;
        }
    }

    // If count of elements is exactly
    // 1 are odd and has no element
    // with frequency > 2
    if (cnt % 2 == 1 && flag == 0) {
        document.write(-1 + "<br>");
        return;
    }

    // If count of elements that occurs
    // exactly once are even
    if (cnt % 2 == 0) {

        // Print the result
        for (let i = 0; i < n; i++) {
            document.write(ans[i] + " ");
        }
    }

    // If the count of elements has
    // exactly 1 frequency are odd
    // and there is an element with
    // frequency greater than 2
    else {

        // Print the result
        for (let i = 0; i < n; i++) {
            if (ind == i)
                document.write(2 + " ");
            else
                document.write(ans[i] << " ");
        }
    }
}

// Driver Codea

let arr = [1, 1, 2, 3, 4, 4];
let N = arr.length
arrayPartition(arr, N);

</script>
```

**Output:** 

```
1 1 1 2 1 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)