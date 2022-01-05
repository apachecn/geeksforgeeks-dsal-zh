# 将所有等于 K 的值移动到数组的末尾

> 原文:[https://www . geeksforgeeks . org/move-all-values-equal-k-to-the-end-of-the-array/](https://www.geeksforgeeks.org/move-all-values-equal-to-k-to-the-end-of-the-array/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K** ，任务是在数组末尾移动所有等于 **K** 的值后打印数组。

**示例:**

> **输入:**arr =【2，1，2，2，2，3，4，2】，K = 2
> **输出:**【4，1，3，2，2，2，2，2，2】
> **解释:**
> 2 是必须移动到数组 arr[]末尾的数字。因此，进行更改后，数组为[4，1，3，2，2，2，2，2，2]。数字 4、1 和 3 可以有不同的顺序。
> 
> **输入:** arr = [1，1，3，5，6]，K = 1
> **输出:**【6，5，3，1，1】
> **解释:**
> 1 是必须移动到数组 arr[]末尾的数字。因此，进行更改后，数组为[6，5，3，1，1 ]。

**方法:**为了解决上面提到的问题，我们使用 [**双指针技术**](https://www.geeksforgeeks.org/two-pointers-technique/) **。**

1.  初始化两个指针，左边的指针标记数组的开始，右边的指针分别标记数组的结束。
2.  只要右指针**指向 K** 就递减计数，只要左指针**不指向整数 m** 就递增计数。
3.  当两个指针都不移动时，[将它们的值交换到位](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)。
4.  重复这个过程，直到指针互相传递。

下面是上述方法的实现:

## C++

```
// C++ program to move all values
// equal to K to the end of the Array

#include <bits/stdc++.h>
using namespace std;

// Function to move the element to the end
vector<int> moveElementToEnd(
    vector<int> array, int toMove)
{
    // Mark left pointer
    int i = 0;

    // Mark the right pointer
    int j = array.size() - 1;

    // Iterate until left pointer
    // crosses the right pointer
    while (i < j) {

        while (i < j && array[j] == toMove)

            // decrement right pointer
            j--;

        if (array[i] == toMove)

            // swap the two elements
            // in the array
            swap(array[i], array[j]);

        // increment left pointer
        i++;
    }

    // return the result
    return array;
}

// Driver code
int main(int argc, char* argv[])
{

    vector<int> arr = { 1, 1, 3, 5, 6 };
    int K = 1;

    vector<int> ans
        = moveElementToEnd(arr, K);

    for (int i = 0; i < arr.size(); i++)
        cout << ans[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to move all values
// equal to K to the end of the Array
class GFG{

// Function to move the element to the end
static int[] moveElementToEnd(int []array,
                              int toMove)
{
    // Mark left pointer
    int i = 0;

    // Mark the right pointer
    int j = array.length - 1;

    // Iterate until left pointer
    // crosses the right pointer
    while (i < j)
    {
        while (i < j && array[j] == toMove)

            // Decrement right pointer
            j--;

        if (array[i] == toMove)

            // Swap the two elements
            // in the array
            swap(array, i, j);

        // Increment left pointer
        i++;
    }

    // Return the result
    return array;
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 1, 1, 3, 5, 6 };
    int K = 1;
    int []ans = moveElementToEnd(arr, K);

    for(int i = 0; i < arr.length; i++)
       System.out.print(ans[i] + " ");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to move all values
# equal to K to the end of the Array

# Function to move the element to the end
def moveElementToEnd(array, toMove):

    # Mark left pointer
    i = 0

    # Mark the right pointer
    j = len(array) - 1

    # Iterate until left pointer
    # crosses the right pointer
    while (i < j):

        while (i < j and array[j] == toMove):

            # decrement right pointer
            j-=1

        if (array[i] == toMove):

            # swap the two elements
            # in the array
            array[i], array[j] = array[j] , array[i]

        # increment left pointer
        i += 1

    # return the result
    return array

# Driver code
if __name__ =="__main__":

    arr = [ 1, 1, 3, 5, 6 ]
    K = 1
    ans = moveElementToEnd(arr, K)
    for i in range(len(arr)):
        print(ans[i] ,end= " ")

# This code is contributed by chitranayal
```

## C#

```
// C# program to move all values
// equal to K to the end of the Array
using System;
class GFG{

// Function to move the element to the end
static int[] moveElementToEnd(int []array,
                              int toMove)
{
    // Mark left pointer
    int i = 0;

    // Mark the right pointer
    int j = array.Length - 1;

    // Iterate until left pointer
    // crosses the right pointer
    while (i < j)
    {
        while (i < j && array[j] == toMove)

            // Decrement right pointer
            j--;

        if (array[i] == toMove)

            // Swap the two elements
            // in the array
            swap(array, i, j);

        // Increment left pointer
        i++;
    }

    // Return the result
    return array;
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 1, 1, 3, 5, 6 };
    int K = 1;
    int []ans = moveElementToEnd(arr, K);

    for(int i = 0; i < arr.Length; i++)
    Console.Write(ans[i] + " ");
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

    // Javascript program to move all values
    // equal to K to the end of the Array

    // Function to move the element to the end
    function moveElementToEnd(array, toMove)
    {
        // Mark left pointer
        let i = 0;

        // Mark the right pointer
        let j = array.length - 1;

        // Iterate until left pointer
        // crosses the right pointer
        while (i < j)
        {
            while (i < j && array[j] == toMove)

                // Decrement right pointer
                j--;

            if (array[i] == toMove)

                // Swap the two elements
                // in the array
                swap(array, i, j);

            // Increment left pointer
            i++;
        }

        // Return the result
        return array;
    }

    function swap(arr, i, j)
    {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    let arr = [ 1, 1, 3, 5, 6 ];
    let K = 1;
    let ans = moveElementToEnd(arr, K);

    for(let i = 0; i < arr.length; i++)
       document.write(ans[i] + " ");

</script>
```

**Output:** 

```
6 5 3 1 1
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。
***空间复杂度:** O(1)*