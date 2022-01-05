# 检查数组 arr[]是否可以重新排列，使得 arr[2 × i + 1] = 2* arr[2 × i]对于每个第 I 个索引

> 原文:[https://www . geesforgeks . org/check-if-a-arr-arr-can-重排-so-arr 2-x-I-1-2-arr 2-x-I-for-ever-ith-index/](https://www.geeksforgeeks.org/check-if-an-array-arr-can-be-rearranged-such-that-arr2-x-i-1-2-arr2-x-i-for-every-ith-index/)

给定一个由 **2*N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查是否有可能重新排列数组元素，使得 **arr[2 * i + 1] = 2* arr[2 * i]** 每个 i <sup>个</sup>索引。如果可以，则打印**是**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {4，-2，2，-4}，N = 2
> **输出:**是
> **说明:**将数组重新排列为 arr[] = {-2，-4，2，4}。
> 
> **输入:** arr[] = {3，1，3，6}，N = 2
> T3】输出:否

**方法:**解决给定问题的思路是使用[地图](https://www.geeksforgeeks.org/map-interface-java-examples/)和观察，即一个元素需要 **N** 个不同的对，使得一个元素是另一个元素的两倍。按照以下步骤解决问题:

*   初始化一个[映射<整数，整数>](https://www.geeksforgeeks.org/map-interface-java-examples/) ，比如说**计数**，来存储数组元素的计数。
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**并更新地图中各元素的计数**计数**。
*   [迭代地图](https://www.geeksforgeeks.org/iterate-map-java/) **计数**并执行以下操作:
    *   初始化一个变量，说**想要**，与当前元素成对，说 **X** ，如果 **X** 小于 **0** ，则赋值**想要= X/2** 。否则，分配**想要= 2*X.**
    *   检查 **X** 是否小于 **0** 和[T5】X 是奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)还是 **X** 的计数大于**想要的**的计数，然后打印**“否”**，因为不可能与数组的任何其他元素形成剩余的一对 **X** 。
    *   否则，更新地图**中**想要**的计数，将**计数为**计数(想要)–计数(X)。**
*   完成上述步骤后，打印**“是”**，因为存在满足给定属性的任何元素组合。

下面是上述方法的实现:

## C++

```
// cpp program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to rearrange the array elements
// that satisfies the given conditions
string canReorderDoubled(vector<int> A)
{

    // Stores the count of elements
    map<int,int> count;

    // Update the hash table
    for (int a : A)
        count[a]++;

    // Traverse the hash table
    for (auto x : count) {

        // If the count of current
        // element is zero
        if (x.second == 0)
            continue;

        // Stores the element needed
        // to form a pair with the
        // current element
        int xx = x.first;
        int want = xx < 0 ? xx / 2 : xx * 2;

        // If x is less than zero and odd
        if (xx < 0 && xx % 2 != 0)
            return "No";

        // If count of x is greater
        // than count of want
        if (x.second
            > count[want])
            return "No";

        // Update the count of want
        // in the hash table
        count[want] -= x.second;
    }

    // Return true if none of the
    // above cases satisfies
    return "Yes";
}

// Driver Code
int main()
{

    vector<int> arr = { 4, -2, 2, -4 };
    int N = 2;

    string res = canReorderDoubled(arr);

    // Print the result obtained
    cout<<(res);
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to check if it is possible
    // to rearrange the array elements
    // that satisfies the given conditions
    public static String canReorderDoubled(int[] A)
    {
        // Stores the count of elements
        Map<Integer, Integer> count
            = new TreeMap<>();

        // Update the hash table
        for (int a : A)
            count.put(
                a, count.getOrDefault(a, 0) + 1);

        // Traverse the hash table
        for (int x : count.keySet()) {

            // If the count of current
            // element is zero
            if (count.get(x) == 0)
                continue;

            // Stores the element needed
            // to form a pair with the
            // current element
            int want = x < 0 ? x / 2 : x * 2;

            // If x is less than zero and odd
            if (x < 0 && x % 2 != 0)
                return "No";

            // If count of x is greater
            // than count of want
            if (count.get(x)
                > count.getOrDefault(want, 0))
                return "No";

            // Update the count of want
            // in the hash table
            count.put(want,
                      count.get(want)
                          - count.get(x));
        }

        // Return true if none of the
        // above cases satisfies
        return "Yes";
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = { 4, -2, 2, -4 };
        int N = 2;

        String res = canReorderDoubled(arr);

        // Print the result obtained
        System.out.println(res);
    }
}
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to check if it is possible
# to rearrange the array elements
# that satisfies the given conditions

def canReorderDoubled(A):
    # Stores the count of elements
    count = {}

    # Update the hash table
    for a in A:
        if a in count:
            count[a] += 1
        else:
            count[a] = 1

    # Traverse the hash table
    for key,value in count.items():
        # If the count of current
        # element is zero
        if (value == 0):
            continue

        # Stores the element needed
        # to form a pair with the
        # current element
        xx = key
        if xx < 0:
            want = xx / 2
        else:
            want = xx * 2

        # If x is less than zero and odd
        if (xx < 0 and xx % 2 != 0):
            return "No"

        # If count of x is greater
        # than count of want
        if (want in count and value > count[want]):
            return "No"

        # Update the count of want
        # in the hash table
        if want in count:
          count[want] -= value

    # Return true if none of the
    # above cases satisfies
    return "Yes"

# Driver Code
if __name__ == '__main__':
    arr =  [4, -2, 2, -4]
    N = 2

    res = canReorderDoubled(arr)

    # Print the result obtained
    print(res)

    # This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to check if it is possible
// to rearrange the array elements
// that satisfies the given conditions
function canReorderDoubled(A)
{

    // Stores the count of elements
    var count= new Map();

    // Update the hash table
    A.forEach(a => {
        if(count.has(a))
            count.set(a, count.get(a)+1)
        else
            count.set(a, 1)
    });

    // Traverse the hash table
    count.forEach((value, key) => {

        // If the count of current
        // element is zero
        if (value != 0)
        {

            // Stores the element needed
            // to form a pair with the
            // current element
            var xx = key;
                var want = xx < 0 ? xx / 2 : xx * 2;

            // If x is less than zero and odd
            if (xx < 0 && xx % 2 != 0)
                    return "No";

            // If count of x is greater
            // than count of want
            if (value
                > count.get(want))
                return "No";

            // Update the count of want
            // in the hash table
            if(count.has(want))
                    count.set(want, count.get(want)-value)
        }

    });

    // Return true if none of the
    // above cases satisfies
    return "Yes";
}

// Driver Code
var arr = [4, -2, 2, -4];
var N = 2;
var res = canReorderDoubled(arr);
// Print the result obtained
document.write(res);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*