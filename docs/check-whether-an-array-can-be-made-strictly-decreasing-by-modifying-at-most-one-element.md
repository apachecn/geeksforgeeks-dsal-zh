# 检查一个数组是否可以通过最多修改一个元素来严格递减

> 原文:[https://www . geesforgeks . org/check-一个数组是否可以通过最多修改一个元素来严格递减/](https://www.geeksforgeeks.org/check-whether-an-array-can-be-made-strictly-decreasing-by-modifying-at-most-one-element/)

给定一个正整数数组 **arr[]** ，任务是通过最多修改一个元素来确定是否有可能使这个数组严格递减。
**例:**

> **输入:** arr[] = {12，9，10，5，2}
> **输出:**是
> {12，11，10，5，2}是有效解之一。
> **输入:** arr[] = {1，2，3，4}
> **输出:**否

**方法:**对于每个元素 **arr[i]** ，如果大于**arr[I–1]**和 **arr[i + 1]** 或者小于 arr[I–1]和 arr[i + 1]，那么需要修改 arr[i]。
即**arr[I]=(arr[I–1]+arr[I+1])/2**。如果修改后，**arr[I]= arr[I–1]**或 **arr[i + 1]** 则数组不能严格递减而不影响**最多**一个元素否则计算所有这样的修改，如果最后修改的计数小于或等于 **1** 则打印**是**否则打印**否**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the array
// can be made strictly decreasing
// with at most one change
bool check(vector<int> arr, int n)
{

    // To store the number of modifications
    // required to make the array
    // strictly decreasing
    int modify = 0;

    // Check whether the last element needs
    // to be modify or not
    if (arr[n - 1] >= arr[n - 2]) {
        arr[n - 1] = arr[n - 2] - 1;
        modify++;
    }

    // Check whether the first element needs
    // to be modify or not
    if (arr[0] <= arr[1]) {
        arr[0] = arr[1] + 1;
        modify++;
    }

    // Loop from 2nd element to the 2nd last element
    for (int i = n - 2; i > 0; i--) {

        // Check whether arr[i] needs to be modified
        if ((arr[i - 1] <= arr[i] && arr[i + 1] <= arr[i])
            || (arr[i - 1] >= arr[i] && arr[i + 1] >= arr[i])) {

            // Modifying arr[i]
            arr[i] = (arr[i - 1] + arr[i + 1]) / 2;
            modify++;

            // Check if arr[i] is equal to any of
            // arr[i-1] or arr[i+1]
            if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                return false;
        }
    }

    // If more than 1 modification is required
    if (modify > 1)
        return false;

    return true;
}

// Driver code
int main()
{

    vector<int> arr = { 10, 5, 11, 2 };
    int n = arr.size();

    if (check(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true if the array
    // can be made strictly decreasing
    // with at most one change
    public static boolean check(int[] arr, int n)
    {

        // To store the number of modifications
        // required to make the array
        // strictly decreasing
        int modify = 0;

        // Check whether the last element needs
        // to be modify or not
        if (arr[n - 1] >= arr[n - 2]) {
            arr[n - 1] = arr[n - 2] - 1;
            modify++;
        }

        // Check whether the first element needs
        // to be modify or not
        if (arr[0] <= arr[1]) {
            arr[0] = arr[1] + 1;
            modify++;
        }

        // Loop from 2nd element to the 2nd last element
        for (int i = n - 2; i > 0; i--) {

            // Check whether arr[i] needs to be modified
            if ((arr[i - 1] <= arr[i] && arr[i + 1] <= arr[i])
                || (arr[i - 1] >= arr[i] && arr[i + 1] >= arr[i])) {

                // Modifying arr[i]
                arr[i] = (arr[i - 1] + arr[i + 1]) / 2;
                modify++;

                // Check if arr[i] is equal to any of
                // arr[i-1] or arr[i+1]
                if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                    return false;
            }
        }

        // If more than 1 modification is required
        if (modify > 1)
            return false;

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 10, 5, 11, 3 };
        int n = arr.length;

        if (check(arr, n))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the array
# can be made strictly decreasing
# with at most one change
def check(arr, n):

    modify = 0

    # Check whether the last element needs
    # to be modify or not
    if (arr[n - 1] >= arr[n - 2]):
        arr[n-1] = arr[n-2] - 1
        modify += 1

    # Check whether the first element needs
    # to be modify or not
    if (arr[0] <= arr[1]):
        arr[0] = arr[1] + 1
        modify += 1

    # Loop from 2nd element to the 2nd last element
    for i in range(n-2, 0, -1):

        # Check whether arr[i] needs to be modified
        if (arr[i - 1] <= arr[i] and arr[i + 1] <= arr[i]) or \
        (arr[i - 1] >= arr[i] and arr[i + 1] >= arr[i]):

            # Modifying arr[i]
            arr[i] = (arr[i - 1] + arr[i + 1]) // 2
            modify += 1

            # Check if arr[i] is equal to any of
            # arr[i-1] or arr[i + 1]
            if (arr[i] == arr[i - 1] or arr[i] == arr[i + 1]):
                return False

    # If more than 1 modification is required
    if (modify > 1):
        return False

    return True

# Driver code
if __name__ == "__main__":
    arr = [10, 5, 11, 3]
    n = len(arr)

    if (check(arr, n)):
        print("Yes")
    else:
        print("No")
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if the array
    // can be made strictly decreasing
    // with at most one change
    public static bool check(int[]arr, int n)
    {

        // To store the number of modifications
        // required to make the array
        // strictly decreasing
        int modify = 0;

        // Check whether the last element needs
        // to be modify or not
        if (arr[n - 1] >= arr[n - 2])
        {
            arr[n - 1] = arr[n - 2] - 1;
            modify++;
        }

        // Check whether the first element needs
        // to be modify or not
        if (arr[0] <= arr[1])
        {
            arr[0] = arr[1] + 1;
            modify++;
        }

        // Loop from 2nd element to the 2nd last element
        for (int i = n - 2; i > 0; i--)
        {

            // Check whether arr[i] needs to be modified
            if ((arr[i - 1] <= arr[i] && arr[i + 1] <= arr[i])
                || (arr[i - 1] >= arr[i] && arr[i + 1] >= arr[i]))
            {

                // Modifying arr[i]
                arr[i] = (arr[i - 1] + arr[i + 1]) / 2;
                modify++;

                // Check if arr[i] is equal to any of
                // arr[i-1] or arr[i+1]
                if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                    return false;
            }
        }

        // If more than 1 modification is required
        if (modify > 1)
            return false;

        return true;
    }

    // Driver code
    static public void Main ()
    {
        int[]arr = { 10, 5, 11, 3 };
        int n = arr.Length;

        if (check(arr, n))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that returns true if the array
    // can be made strictly decreasing
    // with at most one change
    function check(arr, n)
    {

        // To store the number of modifications
        // required to make the array
        // strictly decreasing
        let modify = 0;

        // Check whether the last element needs
        // to be modify or not
        if (arr[n - 1] >= arr[n - 2])
        {
            arr[n - 1] = arr[n - 2] - 1;
            modify++;
        }

        // Check whether the first element needs
        // to be modify or not
        if (arr[0] <= arr[1])
        {
            arr[0] = arr[1] + 1;
            modify++;
        }

        // Loop from 2nd element to the 2nd last element
        for (let i = n - 2; i > 0; i--)
        {

            // Check whether arr[i] needs to be modified
            if ((arr[i - 1] <= arr[i] && arr[i + 1] <= arr[i])
                || (arr[i - 1] >= arr[i] && arr[i + 1] >= arr[i]))
            {

                // Modifying arr[i]
                arr[i] = parseInt((arr[i - 1] + arr[i + 1]) / 2, 10);
                modify++;

                // Check if arr[i] is equal to any of
                // arr[i-1] or arr[i+1]
                if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                    return false;
            }
        }

        // If more than 1 modification is required
        if (modify > 1)
            return false;

        return true;
    }

    let arr = [ 10, 5, 11, 3 ];
    let n = arr.length;

    if (check(arr, n))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)