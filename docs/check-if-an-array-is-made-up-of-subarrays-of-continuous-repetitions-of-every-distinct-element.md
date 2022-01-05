# 检查一个阵列是否由每个不同元素连续重复的子阵列组成

> 原文:[https://www . geeksforgeeks . org/check-如果数组是由每个不同元素的连续重复子数组组成的/](https://www.geeksforgeeks.org/check-if-an-array-is-made-up-of-subarrays-of-continuous-repetitions-of-every-distinct-element/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是检查整个数组是否仅由子数组组成，使得每个子数组由单个元素的连续重复组成，并且数组中的每个不同元素都是该子数组的一部分。

**示例:**

> **输入:** N = 10，arr[] = {1，1，1，2，2，3，3，3}
> **输出:**是
> **解释:**
> 给定的数组由 3 个不同的元素{1，2，3}和子数组{1，1，1，1}、{2，2}、{3，3，3，3}组成。
> 因此，给定的数组满足条件。
> 
> **输入:** N = 10，arr[] = {1，1，2，2，2，2，1，3，3}
> **输出:**否
> **解释:**
> 给定的数组由 3 个不同的元素{1，2，3}和子数组{1，1，1}、{2，2，2}，{1}、{3，3}组成。
> 由于子阵列{1}不包含任何重复，因此给定阵列不满足条件。

**方法:**
按照以下步骤解决问题:

*   初始化变量 **curr = 0** 以存储遇到的单个重复元素的每个子阵列的大小。
*   如果在**arr[I]≠arr[I–1]**处发现任何此类指数，检查 **curr** 是否大于 **1** 。如果是，将**电流**复位至 **0** 并继续。否则，打印“**否”**，因为单个元素的子阵列不重复存在。
*   否则，增加**电流**。
*   遍历数组后，检查 **curr** 是否大于 **1** 。如果 **curr** 等于 **1** ，这确保最后一个元素不同于第二个最后一个元素。因此，打印“**No”**。
*   否则，打印“**是”**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above problem
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// array is made up of
// subarrays of repetitions
bool ContinuousElements(int a[],
                        int n)
{

    // Base Case
    if (n == 1)
        return false;

    // Stores the size of
    // current subarray
    int curr = 1;
    for (int i = 1; i < n; i++) {

        // If a different element
        // is encountered
        if (a[i] != a[i - 1]) {

            // If the previous subarray
            // was a single element
            if (curr == 1)
                return false;

            // Reset to new subarray
            else
                curr = 0;
        }

        // Increase size of subarray
        curr++;
    }

    // If last element differed from
    // the second last element
    if (curr == 1)
        return false;

    return true;
}

// Driver code
int main()
{
    int a[] = { 1, 1, 2, 2, 1, 3, 3 };
    int n = sizeof(a)
            / sizeof(a[0]);

    if (ContinuousElements(a, n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG{

// Function to check if the
// array is made up of
// subarrays of repetitions
static boolean ContinuousElements(int a[],
                                  int n)
{

    // Base Case
    if (n == 1)
        return false;

    // Stores the size of
    // current subarray
    int curr = 1;
    for (int i = 1; i < n; i++)
    {

        // If a different element
        // is encountered
        if (a[i] != a[i - 1])
        {

            // If the previous subarray
            // was a single element
            if (curr == 1)
                return false;

            // Reset to new subarray
            else
                curr = 0;
        }

        // Increase size of subarray
        curr++;
    }

    // If last element differed from
    // the second last element
    if (curr == 1)
        return false;

    return true;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 1, 2, 2, 1, 3, 3 };
    int n = a.length;

    if (ContinuousElements(a, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to implement
# the above problem

# Function to check if the
# array is made up of
# subarrays of repetitions
def ContinuousElements(a, n):

  # Base Case
  if (n == 1):
    return False

  # Stores the size of
  # current subarray
  curr = 1
  for i in range (1, n):

    # If a different element
    # is encountered
    if (a[i] != a[i - 1]):

      # If the previous subarray
      # was a single element
      if (curr == 1):
        return False

      # Reset to new subarray
      else:
        curr = 0

        # Increase size of subarray
        curr += 1

        # If last element differed from
        # the second last element
        if (curr == 1):
          return False

        return True

# Driver code
if __name__ == "__main__":

    a = [1, 1, 2, 2, 1, 3, 3]
    n = len(a)

    if (ContinuousElements(a, n)):
          print ("Yes")
    else:
          print ("No")

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if the
// array is made up of
// subarrays of repetitions
static Boolean ContinuousElements(int []a,
                                  int n)
{

    // Base Case
    if (n == 1)
        return false;

    // Stores the size of
    // current subarray
    int curr = 1;
    for(int i = 1; i < n; i++)
    {

        // If a different element
        // is encountered
        if (a[i] != a[i - 1])
        {

            // If the previous subarray
            // was a single element
            if (curr == 1)
                return false;

            // Reset to new subarray
            else
                curr = 0;
        }

        // Increase size of subarray
        curr++;
    }

    // If last element differed from
    // the second last element
    if (curr == 1)
        return false;

    return true;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 1, 2, 2, 1, 3, 3 };
    int n = a.Length;

    if (ContinuousElements(a, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above problem

// Function to check if the
// array is made up of
// subarrays of repetitions
function ContinuousElements(a, n)
{

    // Base Case
    if (n == 1)
        return false;

    // Stores the size of
    // current subarray
    let curr = 1;
    for(let i = 1; i < n; i++)
    {

        // If a different element
        // is encountered
        if (a[i] != a[i - 1])
        {

            // If the previous subarray
            // was a single element
            if (curr == 1)
                return false;

            // Reset to new subarray
            else
                curr = 0;
        }

        // Increase size of subarray
        curr++;
    }

    // If last element differed from
    // the second last element
    if (curr == 1)
        return false;

    return true;
}

// Driver code   
let a = [ 1, 1, 2, 2, 1, 3, 3 ];
let n = a.length;

if (ContinuousElements(a, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
No
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)