# 求前缀最大长度| Set-2

> 原文:[https://www . geesforgeks . org/find-前缀集的最大长度-2/](https://www.geeksforgeeks.org/find-the-maximum-length-of-the-prefix-set-2/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到[数组](https://www.geeksforgeeks.org/array-data-structure/)的最大前缀长度，这样从前缀中删除一个元素将使剩余前缀元素的频率相同。

**示例:**

> **输入:** arr[] = {1，1，1，2，2，2}
> **输出:** 5
> **说明:**
> 以下前缀满足给定条件:
> 
> 1.  范围[0，0]内的前缀。删除前缀中唯一的元素将变成空的。
> 2.  范围[0，1]内的前缀。从前缀中删除任何一个元素，前缀中每个元素的频率都将相等。
> 3.  范围[0，2]内的前缀。从前缀中移除任何元素，前缀中每个元素的频率都将相等。
> 4.  范围[0，3]内的前缀。从前缀中移除索引 3 处的元素，前缀中每个元素的频率将变得相等。
> 5.  范围[0，4]内的前缀。从前缀中删除[0，2]范围内的任何元素，前缀中每个元素的频率都将相等。
> 
> 因此，满足条件的前缀最大长度为 5。
> 
> **输入:** arr[] = {1，1，1，2，2，2，3，3，3，4，4，5}
> **输出:** 13

本文的[集 1](https://www.geeksforgeeks.org/find-the-maximum-length-of-the-prefix/) 中已经讨论了[散列](https://www.geeksforgeeks.org/hashing-set-1-introduction/)和基于排序的方法。

**方法:**想法是使用两个[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来跟踪元素的频率，并使用以下四个条件来检查有效前缀。

1.  前缀所有元素的频率等于 **1。**
2.  前缀窗口中的所有元素都是相同的。
3.  前缀中的元素只有两个不同的频率，它们之间的差值等于 **1** ，数值较大的频率计数为 **1。**
4.  存在频率为 **1** 的单个元素，除了所有元素的频率相同。

按照以下步骤解决问题:

*   初始化两个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)说 **mp1** 和 **mp2** 分别存储前缀中元素的频率和存储元素的频率。
*   另外，初始化一个变量，比如说**和**为 **0** 来存储前缀的最大长度。
*   使用变量 **i** 遍历范围**【0，N-1】**，并遵循以下步骤:
    *   如果**arr【I】**的计数不等于 **0** ，则从地图 **mp2** 中递减该频率的计数，如果变为 **0** ，则[从地图 **mp2 中清除值**](https://www.geeksforgeeks.org/map-erase-function-in-c-stl/)。
    *   将地图 **mp1** 中**arr【I】**的计数增加 **1** ，然后将地图 **mp2** 中**arr【I】**即**mp1【arr【I】】**的新频率的计数增加 **1。**
    *   如果当前元素的计数等于其前缀长度，即 **(i+1** )或者每个元素在前缀中出现一次，那么将 **ans** 的值更新为 **max(ans，i+1)** 。
    *   现在，如果 **mp2** 的大小等于 **2** ，则执行以下步骤:
        *   将数组元素的频率，即地图的键 **mp2** 分别存储在变量中，如 **freq1** 和 **freq2** 。
        *   将**频率 q1** 和**频率 q2** 的频率计数存储在变量中，如**计数 1** 和**计数 2** 。
        *   检查 **freq2** 和 **freq1** 的差值是否等于 **1** ， **count2** 的值是否等于 **1** ，然后将 **ans** 更新为 **max(ans，i+1)** 。
        *   否则，如果 **freq1** 和 **freq2** 的差值等于 **1** ， **count1** 的值等于 **1** ，则将 **ans** 更新为 **max(ans，i+1)** 。
        *   否则如果 **freq2** 和 **count2** 等于 **1** 或 **freq1** 和 **count1** 等于 **1** ，则将 **ans** 更新为 **max(ans，i+1)** 。
*   最后，完成上述步骤后，打印**和**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// length of the required prefix
int maxPrefixLen(int arr[], int N)
{

    // Stores the frequency of
    // elements
    unordered_map<int, int> a, b;

    // Stores the maximum length
    // of the prefix satisfying
    // the conditions
    int ans = 1;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Stores the count of
        // current element
        int curr = a[arr[i]];

        // If curr is not
        // equal to 0
        if (curr != 0) {

            // Decrement b[curr]
            // by 1
            b[curr]--;

            // If b[curr] is 0
            if (b[curr] == 0) {
                // Remove b[curr]
                // from the b
                b.erase(curr);
            }
        }

        // Update
        a[arr[i]]++;
        b[curr + 1]++;

        // If all elements in the
        // prefix are same or if
        // all elements have frequency
        // 1
        if (a[arr[i]] == i + 1
            or (b.find(1) != b.end() and b[1] == i + 1)) {
            // Update the value of ans
            ans = max(ans, i + 1);
        }

        // Else if the size of b
        // is 2
        else if (b.size() == 2) {

            auto p = b.begin();
            auto q = p;

            // Increment q by 1
            q++;

            int freq1 = p->first;
            int freq2 = q->first;

            int count1 = p->second;
            int count2 = q->second;

            // If difference between
            // freq2 and freq1 is
            // equal to 1 and if
            // count2 is equal to 1
            if (freq2 - freq1 == 1 and count2 == 1) {
                // Update the value
                // of ans
                ans = max(ans, i + 1);
            }

            // If difference between
            // freq1 and freq2 is
            // equal to 1 and if
            // count1 is equal to 1
            else if (freq1 - freq2 == 1 and count1 == 1) {
                // Update the value
                // of ans
                ans = max(ans, i + 1);
            }
            // If freq2 and count2 is 1
            // or freq1 and count1 is 1
            if ((freq2 == 1 and count2 == 1)
                or (freq1 == 1 and count1 == 1)) {
                // Update the value of
                // ans
                ans = max(ans, i + 1);
            }
        }
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{

    int arr[] = { 1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxPrefixLen(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;
class GFG {

    // Function to find the maximum
    // length of the required prefix
    public static int maxPrefixLen(int arr[], int N)
    {

        // Stores the frequency of
        // elements
        HashMap<Integer, Integer> a = new HashMap<Integer, Integer>();
        HashMap<Integer, Integer> b = new HashMap<Integer, Integer>();

        // Stores the maximum length
        // of the prefix satisfying
        // the conditions
        int ans = 1;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Stores the count of
            // current element
            int curr = !a.containsKey(arr[i]) ? 0 : a.get(arr[i]);

            // If curr is not
            // equal to 0
            if (curr != 0) {

                // Decrement b[curr]
                // by 1
                b.put(curr, b.get(curr) - 1);

                // If b[curr] is 0
                if (b.get(curr) == 0)
                {

                    // Remove b[curr]
                    // from the b
                    b.remove(curr);
                }
            }

            // Update
            if (a.containsKey(arr[i])) {
                a.put(arr[i], a.get(arr[i]) + 1);
            } else {
                a.put(arr[i], 1);
            }

            if (b.containsKey(curr + 1)) {
                b.put(curr + 1, b.get(curr + 1) + 1);
            } else {
                b.put(curr + 1, 1);
            }

            // If all elements in the
            // prefix are same or if
            // all elements have frequency
            // 1
            if (a.get(arr[i]) == i + 1 || (b.containsKey(1) && b.get(1) == i + 1))
            {

                // Update the value of ans
                ans = Math.max(ans, i + 1);
            }

            else if (b.size() == 2) {

                int p = b.keySet().toArray()[0].hashCode();
                int q = b.keySet().toArray()[1].hashCode();

                // Increment q by 1

                int freq1 = p;
                int freq2 = q;

                int count1 = b.get(p);
                int count2 = b.get(q);

                // If difference between
                // freq2 and freq1 is
                // equal to 1 and if
                // count2 is equal to 1
                if ((freq2 - freq1) == 1 && count2 == 1)
                {

                    // Update the value
                    // of ans
                    ans = Math.max(ans, i + 1);
                }

                // If difference between
                // freq1 and freq2 is
                // equal to 1 and if
                // count1 is equal to 1
                else if (freq1 - freq2 == 1 && count1 == 1)
                {

                    // Update the value
                    // of ans
                    ans = Math.max(ans, i + 1);
                }
                // If freq2 and count2 is 1
                // or freq1 and count1 is 1
                if ((freq2 == 1 && count2 == 1) || (freq1 == 1 && count1 == 1))
                {

                    // Update the value of
                    // ans
                    ans = Math.max(ans, i + 1);
                }
            }
        }

        // Return ans
        return ans;
    }

    // Driver Code
    public static void main(String args[]) {

        int arr[] = { 1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5 };
        int N = arr.length;

        System.out.println(maxPrefixLen(arr, N));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum
# length of the required prefix
def maxPrefixLen(arr, N):

    # Stores the frequency of
    # elements
    a, b = {}, {}

    # Stores the maximum length
    # of the prefix satisfying
    # the conditions
    ans = 1

    # Traverse the array arr[]
    for i in range(N):

        # Stores the count of
        # current element
        curr = 0 if (arr[i] not in a) else a[arr[i]]

        # If curr is not
        # equal to 0
        if (curr != 0):

            # Decrement b[curr]
            # by 1
            b[curr] -= 1

            # If b[curr] is 0
            if (b[curr] == 0):

                # Remove b[curr]
                # from the b
                del b[curr]

        # Update
        a[arr[i]] = a.get(arr[i], 0) + 1
        b[curr + 1] = b.get(curr + 1, 0) + 1

        # If all elements in the
        # prefix are same or if
        # all elements have frequency
        # 1
        if (a[arr[i]] == i + 1 or
           (1 in b) and b[1] == i + 1):

            # Update the value of ans
            ans = max(ans, i + 1)

        # Else if the size of b
        # is 2
        elif (len(b) == 2):
            p = list(b.keys())[0]
            q = list(b.keys())[1]

            freq1 = p
            freq2 = q

            count1 = b[p]
            count2 = b[q]

            # If difference between
            # freq2 and freq1 is
            # equal to 1 and if
            # count2 is equal to 1
            if (freq2 - freq1 == 1 and count2 == 1):

                # Update the value
                # of ans
                ans = max(ans, i + 1)

            # If difference between
            # freq1 and freq2 is
            # equal to 1 and if
            # count1 is equal to 1
            elif (freq1 - freq2 == 1 and count1 == 1):

                # Update the value
                # of ans
                ans = max(ans, i + 1)

            # If freq2 and count2 is 1
            # or freq1 and count1 is 1
            if ((freq2 == 1 and count2 == 1) or
                (freq1 == 1 and count1 == 1)):

                # Update the value of
                # ans
                ans = max(ans, i + 1)

    # Return ans
    return ans

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 1, 1, 2, 2, 2, 3,
            3, 3, 4, 4, 4, 5 ]
    N = len(arr)

    print(maxPrefixLen(arr, N))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum
// length of the required prefix
function maxPrefixLen(arr, N) {

    // Stores the frequency of
    // elements
    let a = new Map();
    let b = new Map();

    // Stores the maximum length
    // of the prefix satisfying
    // the conditions
    let ans = 1

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

        // Stores the count of
        // current element
        let curr = !(a.has(arr[i])) ? 0 : a.get(arr[i])

        // If curr is not
        // equal to 0
        if (curr != 0) {

            // Decrement b[curr]
            // by 1
            b.set(curr, b.get(curr) - 1)

            // If b[curr] is 0
            if (b.get(curr) == 0) {

                // Remove b[curr]
                // from the b
                b.delete(curr)
            }
        }
        // Update
        if (a.has(arr[i])) {
            a.set(arr[i], a.get(arr[i]) + 1)
        } else {
            a.set(arr[i], 1)
        }
        if (b.has(curr + 1)) {
            b.set(curr + 1, b.get(curr + 1) + 1)
        } else {
            b.set(curr + 1, 1)
        }

        // If all elements in the
        // prefix are same or if
        // all elements have frequency
        // 1
        if (a.get(arr[i]) == i + 1 ||
            (b.has(1)) && b.get(1) == i + 1) {

            // Update the value of ans
            ans = Math.max(ans, i + 1)

            // Else if the size of b
            // is 2
        }
        else if (b.size == 2) {
            let p = [...b.keys()][0]
            let q = [...b.keys()][1]

            let freq1 = p
            let freq2 = q

            let count1 = b.get(p)
            let count2 = b.get(q)

            // If difference between
            // freq2 and freq1 is
            // equal to 1 and if
            // count2 is equal to 1
            if (freq2 - freq1 == 1 && count2 == 1) {

                // Update the value
                // of ans
                ans = Math.max(ans, i + 1)
            }

            // If difference between
            // freq1 and freq2 is
            // equal to 1 and if
            // count1 is equal to 1
            else if (freq1 - freq2 == 1 && count1 == 1) {

                // Update the value
                // of ans
                ans = Math.max(ans, i + 1)
            }

            // If freq2 and count2 is 1
            // or freq1 and count1 is 1
            if ((freq2 == 1 && count2 == 1) ||
                (freq1 == 1 && count1 == 1)) {

                // Update the value of
                // ans
                ans = Math.max(ans, i + 1)
            }
        }
    }

    // Return ans
    return ans

}

// Driver Code

let arr = [1, 1, 1, 2, 2, 2, 3,
    3, 3, 4, 4, 4, 5]
N = arr.length

document.write(maxPrefixLen(arr, N))

// This code is contributed by gfgking
</script>
```

**Output:** 

```
13
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)