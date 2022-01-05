# 反复拆分合并检查一个数组是否可以做成 0

> 原文:[https://www . geeksforgeeks . org/check-一个数组是否可以通过反复拆分合并来制作 0/](https://www.geeksforgeeks.org/check-whether-an-array-can-be-made-0-by-splitting-and-merging-repeatedly/)

给定一个带有 **N** 元素的数组 **arr[]** ，任务是找出给定数组的所有元素是否可以通过给定的运算变成 0。在此阵列上只能执行两种类型的操作:

*   将一个元素 B 拆分为两个元素 C 和 D，使得 **B = C + D** 。
*   将 2 个元素 p 和 q 合并为一个元素 r，使得 **R = P^Q** (即 p 和 q 的异或)。

**示例:**

> **输入:**arr =【9，17】
> **输出:**是
> **解释:**以下是一个可能的操作序列–
> 1)合并，即 9 异或 17 = 24
> 2)将 24 分成两部分，每个部分大小为 12
> 3)合并，即 12 异或 12 = 0
> 因为只有一个元素，即 0。所以是有可能的。
> 
> **输入:**arr =【1】
> **输出:**否
> **说明:**没有可能使其为 0。

**进场:**

1.  如果数组中的任何元素是偶数，那么它可以是 0。将元素分成 arr[I/2]和 arr[I/2]两个相等部分。两个相等数的异或为零。因此，此策略使元素为 0。
2.  如果任何元素是奇数。把它分成两部分:1 和 arr[i]-1。因为 arr[i]-1 是偶数，所以可以通过上述策略使其为 0。因此，奇数元素可以将其大小减少到 1。因此，通过遵循上述策略，两个奇数元素可以被设为 0，并且最终将它们异或(即 1)为 1 异或 1 = 0。因此，如果数组中奇数元素的数量是偶数，那么答案是可能的。否则，值为 1 的元素将被保留，并且不可能满足条件。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds if it is
// possible to make the array
// contain only 1 element i.e. 0
string solve(vector<int>& A)
{
    int i, ctr = 0;
    for (i = 0; i < A.size();
         i++) {

        // Check if element is odd
        if (A[i] % 2) {
            ctr++;
        }
    }

    // According to the logic
    // in above approach
    if (ctr % 2) {
        return "No";
    }
    else {
        return "Yes";
    }
}

// Driver code
int main()
{

    vector<int> arr = { 9, 17 };

    cout << solve(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that finds if it is
// possible to make the array
// contain only 1 element i.e. 0
public static String solve(int[] A)
{
    int i, ctr = 0;

    for(i = 0; i < A.length; i++)
    {

       // Check if element is odd
       if (A[i] % 2 == 1)
       {
           ctr++;
       }
    }

    // According to the logic
    // in above approach
    if (ctr % 2 == 1)
    {
        return "No";
    }
    else
    {
        return "Yes";
    }
}

// Driver code   
public static void main(String[] args)
{
    int[] arr = { 9, 17 };
    System.out.println(solve(arr));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds if it is
# possible to make the array
# contain only 1 element i.e. 0
def solve(A):

    ctr = 0

    for i in range(len(A)):

        # Check if element is odd
        if A[i] % 2 == 1:
            ctr += 1

    # According to the logic
    # in above approach
    if ctr % 2 == 1:
        return 'No'
    else :
        return 'Yes'

# Driver code
if __name__=='__main__':

    arr = [9, 17]

    print(solve(arr))

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that finds if it is
// possible to make the array
// contain only 1 element i.e. 0
public static string solve(int[] A)
{
    int i, ctr = 0;

    for(i = 0; i < A.Length; i++)
    {

       // Check if element is odd
       if (A[i] % 2 == 1)
       {
           ctr++;
       }
    }

    // According to the logic
    // in above approach
    if (ctr % 2 == 1)
    {
        return "No";
    }
    else
    {
        return "Yes";
    }
}

// Driver code
public static void Main()
{
    int[] arr = { 9, 17 };

    Console.Write(solve(arr));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that finds if it is
// possible to make the array
// contain only 1 element i.e. 0
function solve(A)
{
    let i, ctr = 0;
    for (i = 0; i < A.length;
         i++) {

        // Check if element is odd
        if (A[i] % 2) {
            ctr++;
        }
    }

    // According to the logic
    // in above approach
    if (ctr % 2) {
        return "No";
    }
    else {
        return "Yes";
    }
}

// Driver code

    let arr = [ 9, 17 ];

    document.write(solve(arr));

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(1)*