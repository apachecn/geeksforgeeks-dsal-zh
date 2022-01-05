# 检查数组中每一对 1 是否至少相距 K 个长度

> 原文:[https://www . geeksforgeeks . org/check-如果阵列中的每一对 1 至少相距 k 个长度/](https://www.geeksforgeeks.org/check-if-every-pair-of-1-in-the-array-is-at-least-k-length-apart-from-each-other/)

给定一个**二进制数组**和一个**整数 K** ，检查数组中的每一对 1 是否彼此相距至少 K 个长度**。如果条件成立，则返回 true，否则返回 false。
**举例:**** 

> **输入:** arr = [1，0，0，0，1，0，0，1，0，0]，K = 2。
> **输出:**真
> **说明:**
> 阵中每 1 个至少相隔 K 距离。
> **输入:**【1，0，1，0，1，1】，K = 1
> **输出:**假
> **说明:**
> 第五个 1 和第六个 1 互不相隔。因此，输出为假。

**进场:**
要解决上面提到的问题我们必须**检查每对相邻 1** 之间的距离。找到 1 的第一个位置，然后遍历数组的其余部分，如果距离为 0，则增加距离，否则，如果距离小于 k，则执行检查操作，并将计数再次重置为 0。
以下是上述方法的实施:

## C++

```
// C++ implementation to Check if every pair of 1 in
// the array is at least K length from each other

#include <bits/stdc++.h>
using namespace std;

// Function to check distance
bool kLengthApart(vector<int>& nums, int k)
{
    // Find first position of 1
    int pos = 0, count = 0;

    while (pos < nums.size() && nums[pos] == 0)
        pos++;

    // Iterate through the rest of array
    for (int i = pos + 1; i < nums.size(); i++) {
        // Increment distance if its 0
        if (nums[i] == 0)
            count++;

        // Check if the distance is less than k
        else {
            if (count < k)
                return false;

            // Reset count to 0
            count = 0;
        }
    }

    // Return the result
    return true;
}

// Driver code
int main()
{
    vector<int> nums = { 1, 0, 0, 0, 1, 0, 0, 1, 0, 0 };
    int k = 2;

    bool ans = kLengthApart(nums, k);
    if (ans == 1)
        cout << "True" << endl;

    else
        cout << "False" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// every pair of 1 in the array is
// at least K length from each other
class Main{

// Function to check distance
public static boolean kLengthApart(int[] nums,
                                   int k)
{

    // Find first position of 1
    int pos = 0, count = 0;

    while (pos < nums.length && nums[pos] == 0)
        pos++;

    // Iterate through the rest of array
    for(int i = pos + 1; i < nums.length; i++)
    {

       // Increment distance if its 0
       if (nums[i] == 0)
           count++;

       // Check if the distance is less than k
       else
       {
           if (count < k)
               return false;

           // Reset count to 0
           count = 0;
       }
    }

    // Return the result
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int[] nums = { 1, 0, 0, 0, 1,
                   0, 0, 1, 0, 0 };
    int k = 2;
    boolean ans = kLengthApart(nums, k);

    if (ans)
        System.out.println("True");

    else
        System.out.println("False");
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to check if
# every pair of 1 in the array is
# at least K length from each other

# Function to check distance
def kLengthApart(nums, k):

    # Find first position of 1
    pos = 0
    count = 0

    while (pos < len(nums) and nums[pos] == 0):
        pos += 1

    # Iterate through the rest of list
    for i in range(pos + 1, len(nums)):

        # Increment distance if its 0
        if nums[i] == 0:
            count += 1

        # Check if the distance is less than k
        else :
            if count < k:
                return False

            # Reset count to 0
            count = 0

        # Return the result
    return True

# Driver Code
if __name__ == "__main__":

    nums = [ 1, 0, 0, 0, 1, 0, 0, 1, 0, 0 ]
    k = 2

    print(kLengthApart(nums, k))

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to check if
// every pair of 1 in the array is
// at least K length from each other
using System;

class GFG{

// Function to check distance
public static bool kLengthApart(int[] nums,
                                int k)
{

    // Find first position of 1
    int pos = 0, count = 0;

    while (pos < nums.Length && nums[pos] == 0)
        pos++;

    // Iterate through the rest of array
    for(int i = pos + 1; i < nums.Length; i++)
    {

       // Increment distance if its 0
       if (nums[i] == 0)
           count++;

       // Check if the distance is
       // less than k
       else
       {
           if (count < k)
               return false;

           // Reset count to 0
           count = 0;
       }
    }

    // Return the result
    return true;
}

// Driver Code
public static void Main()
{
    int[] nums = { 1, 0, 0, 0, 1,
                   0, 0, 1, 0, 0 };
    int k = 2;
    bool ans = kLengthApart(nums, k);

    if (ans)
        Console.Write("True");
    else
        Console.Write("False");
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript implementation to
// Check if every pair of 1 in
// the array is at least K length
// from each other

// Function to check distance
function kLengthApart(nums, k)
{
    // Find first position of 1
    var pos = 0, count = 0;
    var i;
    while (pos < nums.length && nums[pos] == 0)
        pos++;

    // Iterate through the rest of array
    for (i = pos + 1; i < nums.length; i++) {
        // Increment distance if its 0
        if (nums[i] == 0)
            count++;

        // Check if the distance is less than k
        else {
            if (count < k)
                return false;

            // Reset count to 0
            count = 0;
        }
    }

    // Return the result
    return true;
}

// Driver code
    var nums = [1, 0, 0, 0, 1, 0, 0, 1, 0, 0];
    var k = 2;

    var ans = kLengthApart(nums, k);
    if (ans == 1)
        document.write("True");

    else
        document.write("False");

</script>
```

**Output:** 

```
True
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)