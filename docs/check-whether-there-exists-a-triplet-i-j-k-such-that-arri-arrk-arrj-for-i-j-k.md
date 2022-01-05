# 检查是否存在三元组(I，j，k ),使得对于 I<j<k

, arr【I】<arr【k】<arr【j】

> 原文:[https://www . geeksforgeeks . org/check-是否存在-a-triple-I-j-k-so-arri-arrk-arrj-for-I-j-k/](https://www.geeksforgeeks.org/check-whether-there-exists-a-triplet-i-j-k-such-that-arri-arrk-arrj-for-i-j-k/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查是否存在三元组 **(i，j，k)** ，使得**arr【I】<arr【k】<arr【j】和 i < j < k** 然后打印**是**否则打印**否**。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:**否
> **解释:**
> 不存在 arr[i] < arr[k] < arr[j]这样的子序列
> 
> **输入:** arr[] = {3，1，5，0，4}
> **输出:**是
> **解释:**
> 存在一个三元组(3，5，4)，即 arr[i] < arr[k] < arr[j]

**天真方法:**想法是生成所有可能的三胞胎，如果有任何三胞胎满足给定条件，打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to check if there exist
// triplet in the array such that
// i < j < k and arr[i] < arr[k] < arr[j]
bool findTriplet(vector<int> nums)
{
    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            for (int k = j + 1; k < nums.size(); k++) {
                // Triplet found, hence return false
                if (nums[i] < nums[k] && nums[k] < nums[j])
                    return true;
            }
        }
    }
    // No triplet found, hence return false
    return false;
}

// Driver Code
int main()
{
    // Given array
    vector<int> arr = { 4, 7, 5, 6 };

    // Function Call
    if (findTriplet(arr)) {
        cout << " Yes" << '\n';
    }
    else {
        cout << " No" << '\n';
    }
    return 0;
}
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*
**高效方法:**优化上述方法的思路是使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)来跟踪数组中每个元素右侧的较小元素**arr【】**。以下是步骤:

*   从末尾开始遍历数组，并保持一个堆栈，该堆栈以降序存储元素。
*   要保持堆栈按降序排列，请弹出比当前元素小的元素。然后将弹出的元素标记为三元组的第三个元素。
*   如果任何元素小于最后弹出的元素(标记为三元组的第三个元素)，则反向遍历数组。那么它们存在一个满足给定条件的三元组，并打印**是**。
*   否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there exist
// triplet in the array such that
// i < j < k and arr[i] < arr[k] < arr[j]
bool findTriplet(vector<int>& arr)
{
    int n = arr.size();
    stack<int> st;

    // Initialize the heights of h1 and h2
    // to INT_MAX and INT_MIN respectively
    int h3 = INT_MIN, h1 = INT_MAX;
    for (int i = n - 1; i >= 0; i--) {

        // Store the current element as h1
        h1 = arr[i];

        // If the element at top of stack
        // is less than the current element
        // then pop the stack top
        // and keep updating the value of h3
        while (!st.empty()
            && st.top() < arr[i]) {

            h3 = st.top();
            st.pop();
        }

        // Push the current element
        // on the stack
        st.push(arr[i]);

        // If current element is less
        // than h3, then we found such
        // triplet and return true
        if (h1 < h3) {
            return true;
        }
    }

    // No triplet found, hence return false
    return false;
}

// Driver Code
int main()
{
    // Given array
    vector<int> arr = { 4, 7, 5, 6 };

    // Function Call
    if (findTriplet(arr)) {
        cout << " Yes" << '\n';
    }
    else {
        cout << " No" << '\n';
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if there exist
// triplet in the array such that
// i < j < k and arr[i] < arr[k] < arr[j]
public static boolean findTriplet(int[] arr)
{
    int n = arr.length;
    Stack<Integer> st = new Stack<>();

    // Initialize the heights of h1 and h2
    // to INT_MAX and INT_MIN respectively
    int h3 = Integer.MIN_VALUE;
    int h1 = Integer.MAX_VALUE;

    for(int i = n - 1; i >= 0; i--)
    {

        // Store the current element as h1
        h1 = arr[i];

        // If the element at top of stack
        // is less than the current element
        // then pop the stack top
        // and keep updating the value of h3
        while (!st.empty() && st.peek() < arr[i])
        {
            h3 = st.peek();
            st.pop();
        }

        // Push the current element
        // on the stack
        st.push(arr[i]);

        // If current element is less
        // than h3, then we found such
        // triplet and return true
        if (h1 < h3)
        {
            return true;
        }
    }

    // No triplet found, hence return false
    return false;
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 4, 7, 5, 6 };

    // Function call
    if (findTriplet(arr))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to check if there exist
# triplet in the array such that
# i < j < k and arr[i] < arr[k] < arr[j]
def findTriplet(arr):
    n = len(arr)
    st = []

    # Initialize the heights of h1 and h3
    # to INT_MAX and INT_MIN respectively
    h3 = -sys.maxsize - 1
    h1 = sys.maxsize

    for i in range(n - 1, -1, -1):

        # Store the current element as h1
        h1 = arr[i]

        # If the element at top of stack
        # is less than the current element
        # then pop the stack top
        # and keep updating the value of h3
        while (len(st) > 0 and st[-1] < arr[i]):
            h3 = st[-1]
            del st[-1]

        # Push the current element
        # on the stack
        st.append(arr[i])

        # If current element is less
        # than h3, then we found such
        # triplet and return true
        if (h1 < h3):
            return True

    # No triplet found, hence
    # return false
    return False

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 4, 7, 5, 6 ]

    # Function Call
    if (findTriplet(arr)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if there exist
// triplet in the array such that
// i < j < k and arr[i] < arr[k] < arr[j]
public static bool findTriplet(int[] arr)
{
    int n = arr.Length;
    Stack<int> st = new Stack<int>();

    // Initialize the heights of h1 and h2
    // to INT_MAX and INT_MIN respectively
    int h3 = int.MinValue;
    int h1 = int.MaxValue;

    for(int i = n - 1; i >= 0; i--)
    {

        // Store the current element as h1
        h1 = arr[i];

        // If the element at top of stack
        // is less than the current element
        // then pop the stack top
        // and keep updating the value of h3
        while (st.Count != 0 && st.Peek() < arr[i])
        {
            h3 = st.Peek();
            st.Pop();
        }

        // Push the current element
        // on the stack
        st.Push(arr[i]);

        // If current element is less
        // than h3, then we found such
        // triplet and return true
        if (h1 < h3)
        {
            return true;
        }
    }

    // No triplet found, hence return false
    return false;
}

// Driver code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 4, 7, 5, 6 };

    // Function call
    if (findTriplet(arr))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if there exist
// triplet in the array such that
// i < j < k and arr[i] < arr[k] < arr[j]
function findTriplet(arr)
{
    var n = arr.length;
    var st = [];

    // Initialize the heights of h1 and h2
    // to INT_MAX and INT_MIN respectively
    var h3 = -1000000000, h1 = 1000000000;
    for (var i = n - 1; i >= 0; i--) {

        // Store the current element as h1
        h1 = arr[i];

        // If the element at top of stack
        // is less than the current element
        // then pop the stack top
        // and keep updating the value of h3
        while (st.length!=0
            && st[st.length-1] < arr[i]) {

            h3 = st[st.length-1];
            st.pop();
        }

        // Push the current element
        // on the stack
        st.push(arr[i]);

        // If current element is less
        // than h3, then we found such
        // triplet and return true
        if (h1 < h3) {
            return true;
        }
    }

    // No triplet found, hence return false
    return false;
}

// Driver Code
// Given array
var arr = [4, 7, 5, 6 ];
// Function Call
if (findTriplet(arr)) {
    document.write( " Yes");
}
else {
    document.write( " No" );
}

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*