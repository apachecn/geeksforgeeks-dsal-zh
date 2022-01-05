# 检查所有数组元素是否可以通过给定的操作

移除

> 原文:[https://www . geesforgeks . org/check-if-all-array-elements-可以通过给定的操作移除/](https://www.geeksforgeeks.org/check-if-all-array-elements-can-be-removed-by-the-given-operations/)

给定包含不同元素的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过选择任意两个相邻的索引来检查是否可以移除所有数组元素，使得 **arr[i] < arr[i+1]** 并在每个步骤移除两个元素中的一个或两个。如果可能，则打印**“是”**。否则，打印**“否”**。
**举例:**

> **输入:** arr[] = {2，8，6，1，3，5}
> **输出:**是
> **解释:**
> 选择 arr[4]和 arr[5]。从 3 < 5 开始，删除 3，从而修改数组 arr[] = {2，8，6，1，5}
> 选择 arr[0]和 arr[1]。从 2 < 8 开始，删除 8，从而修改数组 arr[] = {2，6，1，5}
> 选择 arr[0]和 arr[1]。从 2 < 6 开始，删除 2 和 6，从而修改数组 arr[] = {1，5}
> 选择 arr[0]和 arr[1]。从 1 < 5 开始，删除 1 和 5，从而修改数组 arr[] = {}
> **输入:** arr[] = {6，5，1}
> **输出:**否

**天真方法:**
想法是考虑给定数组中的所有相邻对，如果它满足给定条件，则移除其中一个数字，并重复该过程，直到所有元素都被移除。如果可能，则打印**“是”**。否则打印**“否”**。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效途径:**
由于数组的元素是不同的，可以观察到，如果数组的第一个元素小于数组的最后一个元素，那么数组的所有元素都可以被移除。否则，无法移除给定数组的所有元素。
按照以下步骤解决问题:

*   检查**是否 arr[0]<arr[n–1]**，打印**是**。
*   否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to remove all array elements
void removeAll(int arr[], int n)
{

    // Condition if we can remove
    // all elements from the array
    if (arr[0] < arr[n - 1])
        cout << "YES";
    else
        cout << "NO";
}

// Driver Code
int main()
{

    int Arr[] = { 10, 4, 7, 1, 3, 6 };

    int size = sizeof(Arr) / sizeof(Arr[0]);

    removeAll(Arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to check if it is possible
// to remove all array elements
static void removeAll(int arr[], int n)
{

    // Condition if we can remove
    // all elements from the array
    if (arr[0] < arr[n - 1])
        System.out.print("YES");
    else
        System.out.print("NO");
}

// Driver Code
public static void main(String[] args)
{
    int Arr[] = { 10, 4, 7, 1, 3, 6 };

    int size = Arr.length;

    removeAll(Arr, size);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach

# Function to check if it is possible
# to remove all array elements
def removeAll(arr, n):

  # Condition if we can remove
  # all elements from the array
  if arr[0] < arr[n - 1]:
    print("YES")
  else:
    print("NO")

# Driver code
arr = [ 10, 4, 7, 1, 3, 6 ]

removeAll(arr, len(arr))

# This code is contributed by dipesh99kumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if it is possible
// to remove all array elements
static void removeAll(int []arr, int n)
{

    // Condition if we can remove
    // all elements from the array
    if (arr[0] < arr[n - 1])
        Console.Write("YES");
    else
        Console.Write("NO");
}

// Driver Code
public static void Main(String[] args)
{
    int []Arr = { 10, 4, 7, 1, 3, 6 };

    int size = Arr.Length;

    removeAll(Arr, size);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to check if it is possible
// to remove all array elements
function removeAll(arr,n)
{

    // Condition if we can remove
    // all elements from the array
    if (arr[0] < arr[n - 1])
        document.write("YES");
    else
        document.write("NO");
}

    let Arr = [ 10, 4, 7, 1, 3, 6 ];
    let size = Arr.length;
    removeAll(Arr, size);

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
NO
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*