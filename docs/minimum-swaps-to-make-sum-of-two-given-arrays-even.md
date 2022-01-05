# 使两个给定数组的和为偶数所需的相同索引元素的最小交换量

> 原文:[https://www . geesforgeks . org/minimum-swaps-to-make-sum-of-of-of-给定数组-even/](https://www.geeksforgeeks.org/minimum-swaps-to-make-sum-of-two-given-arrays-even/)

给定两个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr 1【】**和**arr 2【】**，任务是计算两个数组**arr 1【】**和**arr 2【】**中相同索引元素的最小交换次数，以使两个数组的所有元素之和[相等。如果不可能，则打印**-1”**。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> ***输入:** arr1[] = {1，4，2，3}，arr2[] = {2，3，4，1}*
> ***输出:** 0*
> ***说明:**arr 1[]和 arr2[]的所有元素之和分别为 10 和 10，已经是偶数了。因此，所需的操作计数为 0。*
> 
> ***输入:** arr1[] = {11，14，20，2}，arr2[] = {5，9，6，3}*
> ***输出:** 1*
> ***说明:**arr 1[]和 arr2[]的所有元素之和分别为 37 和 23。交换 arr1[1]( = 14)和 arr2[1]( = 9)分别得到 arr1[]和 arr2[]、32 和 28 的和。因此，所需的操作数为 1。*

**方法:**该思想基于以下观察，假设数组**arr 1【】**的和为**sumar 1**而**arr 2【】**的和为**sumar 2**。

*   **如果 sumArr1 为偶数，sumArr2 为偶数:**不需要交换。
*   **如果 sumArr1 为奇数，sumArr2 为奇数:**找到一对和为奇数的同索引元素，并交换它们。这样的一对包含一个偶数和一个奇数。交换它们会使一个阵列的总和增加 **1** 并使另一个阵列的总和减少 **1** 。因此，两个数组的和是偶数。
*   **如果 sumArr1 为偶数，sumArr2 为奇数:**不可能使两个数组的和为偶数。
*   **如果 sumArr1 为奇数，sumArr2 为偶数:**不可能使两个数组的和为偶数。

按照以下步骤解决问题:

*   初始化 **sumArr1 = 0** 和 **sumArr2 = 0** 到[分别存储**arr 1【】**和**arr 2【】**T9】的和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   如果**sumar 1**和**sumar 2**均为偶数，则打印 **0** 。
*   如果发现**sumar 1**和**sumar 2**都是奇数，则[在范围**【0，N-1】**上循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，并检查是否存在其和为奇数的对应对。如果找到这样的一对，则打印 **1** 。
*   否则，对于所有其他情况，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum swaps
// of same-indexed elements from arrays
// arr1[] and arr2[] required to make
// the sum of both the arrays even
void minimumSwaps(int arr1[], int arr2[],
                  int n)
{
    // Store the sum of elements of
    // the array arr1 and arr2 respectively
    int sumArr1 = 0, sumArr2 = 0;

    // Store the array sum of both the arrays
    for (int i = 0; i < n; ++i) {
        sumArr1 += arr1[i];
        sumArr2 += arr2[i];
    }

    // If both sumArr1 and sumArr2
    // are even, print 0 and return
    if (sumArr1 % 2 == 0
        && sumArr2 % 2 == 0) {
        cout << 0;
        return;
    }

    // If both sumArr1 and sumArr2
    // are odd and check for a pair
    // with sum odd sum
    if (sumArr1 % 2 != 0
        && sumArr2 % 2 != 0) {

        // Stores if a pair with
        // odd sum exists or not
        int flag = -1;

        // Traverse the array
        for (int i = 0; i < n; ++i) {

            // If a pair exists with odd
            // sum, set flag = 1
            if ((arr1[i] + arr2[i]) % 2 == 1){
                flag = 1;
                break;
            }
        }

        // Print the answer and return
        cout << flag;

        return;
    }

    // For all other cases, print -1
    cout << -1;
}

// Driver Code
int main()
{
    int arr1[] = { 11, 14, 20, 2 };
    int arr2[] = { 5, 9, 6, 3 };
    int N = sizeof(arr1) / sizeof(arr1[0]);

    // Function Call
    minimumSwaps(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the minimum swaps
// of same-indexed elements from arrays
// arr1[] and arr2[] required to make
// the sum of both the arrays even
static void minimumSwaps(int arr1[], int arr2[],
                         int n)
{

    // Store the sum of elements of
    // the array arr1 and arr2 respectively
    int sumArr1 = 0, sumArr2 = 0;

    // Store the array sum of both the arrays
    for(int i = 0; i < n; ++i)
    {
        sumArr1 += arr1[i];
        sumArr2 += arr2[i];
    }

    // If both sumArr1 and sumArr2
    // are even, print 0 and return
    if (sumArr1 % 2 == 0 && sumArr2 % 2 == 0)
    {
        System.out.print(0);
        return;
    }

    // If both sumArr1 and sumArr2
    // are odd and check for a pair
    // with sum odd sum
    if (sumArr1 % 2 != 0 && sumArr2 % 2 != 0)
    {

        // Stores if a pair with
        // odd sum exists or not
        int flag = -1;

        // Traverse the array
        for(int i = 0; i < n; ++i)
        {

            // If a pair exists with odd
            // sum, set flag = 1
            if ((arr1[i] + arr2[i]) % 2 == 1)
            {
                flag = 1;
                break;
            }
        }

        // Print the answer and return
        System.out.print(flag);
        return;
    }

    // For all other cases, print -1
    System.out.print(-1);
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 11, 14, 20, 2 };
    int arr2[] = { 5, 9, 6, 3 };
    int N = arr1.length;

    // Function Call
    minimumSwaps(arr1, arr2, N);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the minimum swaps
# of same-indexed elements from arrays
# arr1 and arr2 required to make
# the sum of both the arrays even
def minimumSwaps(arr1, arr2, n):

    # Store the sum of elements of
    # the array arr1 and arr2 respectively
    sumArr1 = 0; sumArr2 = 0;

    # Store the array sum of both the arrays
    for i in range(n):
        sumArr1 += arr1[i];
        sumArr2 += arr2[i];

    # If both sumArr1 and sumArr2
    # are even, pr0 and return
    if (sumArr1 % 2 == 0 and sumArr2 % 2 == 0):
        print(0);
        return;

    # If both sumArr1 and sumArr2
    # are odd and check for a pair
    # with sum odd sum
    if (sumArr1 % 2 != 0 and sumArr2 % 2 != 0):

        # Stores if a pair with
        # odd sum exists or not
        flag = -1;

        # Traverse the array
        for i in range(n):

            # If a pair exists with odd
            # sum, set flag = 1
            if ((arr1[i] + arr2[i]) % 2 == 1):
                flag = 1;
                break;

        # Print the answer and return
        print(flag);
        return;

    # For all other cases, pr-1
    print(-1);

# Driver code
if __name__ == '__main__':
    arr1 = [11, 14, 20, 2];
    arr2 = [5, 9, 6, 3];
    N = len(arr1);

    # Function Call
    minimumSwaps(arr1, arr2, N);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG{

// Function to count the minimum swaps
// of same-indexed elements from arrays
// arr1[] and arr2[] required to make
// the sum of both the arrays even
static void minimumSwaps(int[] arr1, int[] arr2,
                         int n)
{

    // Store the sum of elements of
    // the array arr1 and arr2 respectively
    int sumArr1 = 0, sumArr2 = 0;

    // Store the array sum of both the arrays
    for(int i = 0; i < n; ++i)
    {
        sumArr1 += arr1[i];
        sumArr2 += arr2[i];
    }

    // If both sumArr1 and sumArr2
    // are even, print 0 and return
    if (sumArr1 % 2 == 0 && sumArr2 % 2 == 0)
    {
        Console.Write(0);
        return;
    }

    // If both sumArr1 and sumArr2
    // are odd and check for a pair
    // with sum odd sum
    if (sumArr1 % 2 != 0 && sumArr2 % 2 != 0)
    {

        // Stores if a pair with
        // odd sum exists or not
        int flag = -1;

        // Traverse the array
        for(int i = 0; i < n; ++i)
        {

            // If a pair exists with odd
            // sum, set flag = 1
            if ((arr1[i] + arr2[i]) % 2 == 1)
            {
                flag = 1;
                break;
            }
        }

        // Print the answer and return
        Console.Write(flag);
        return;
    }

    // For all other cases, print -1
    Console.Write(-1);
}

// Driver code
public static void Main()
{
    int[] arr1 = { 11, 14, 20, 2 };
    int[] arr2 = { 5, 9, 6, 3 };
    int N = arr1.Length;

    // Function Call
    minimumSwaps(arr1, arr2, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the minimum swaps
// of same-indexed elements from arrays
// arr1[] and arr2[] required to make
// the sum of both the arrays even
function minimumSwaps(arr1, arr2, n)
{

    // Store the sum of elements of
    // the array arr1 and arr2 respectively
    let sumArr1 = 0, sumArr2 = 0;

    // Store the array sum of both the arrays
    for(let i = 0; i < n; ++i)
    {
        sumArr1 += arr1[i];
        sumArr2 += arr2[i];
    }

    // If both sumArr1 and sumArr2
    // are even, print 0 and return
    if (sumArr1 % 2 == 0 && sumArr2 % 2 == 0)
    {
        document.write(0);
        return;
    }

    // If both sumArr1 and sumArr2
    // are odd and check for a pair
    // with sum odd sum
    if (sumArr1 % 2 != 0 && sumArr2 % 2 != 0)
    {

        // Stores if a pair with
        // odd sum exists or not
        let flag = -1;

        // Traverse the array
        for(let i = 0; i < n; ++i)
        {

            // If a pair exists with odd
            // sum, set flag = 1
            if ((arr1[i] + arr2[i]) % 2 == 1)
            {
                flag = 1;
                break;
            }
        }

        // Print the answer and return
        document.write(flag);
        return;
    }

    // For all other cases, print -1
    document.write(-1);
}

// Driver Code
let arr1 = [ 11, 14, 20, 2 ];
let arr2 = [ 5, 9, 6, 3 ];
let N = arr1.length;

// Function Call
minimumSwaps(arr1, arr2, N);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)