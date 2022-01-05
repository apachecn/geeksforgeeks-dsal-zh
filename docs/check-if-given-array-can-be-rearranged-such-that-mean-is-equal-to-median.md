# 检查给定的数组是否可以重新排列，使得平均值等于中间值

> 原文:[https://www . geeksforgeeks . org/check-if-给定数组-可以重新排列-使得平均值等于中值/](https://www.geeksforgeeks.org/check-if-given-array-can-be-rearranged-such-that-mean-is-equal-to-median/)

给定排序浮动[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。检查 **arr[]** 是否可以重新排列，使其平均值等于其中位数。

**示例**:

> **输入** : arr[] = {1.0，3.0，6.0，9.0，12.0，32.0}
> **输出**:是
> **说明:**给定数组的均值为(1.0+3.0+6.0+9.0+12.0+32.0)/6 = 10.5。
> 将给定数组重新排列为{1.0，3.0，9.0，12.0，6.0，32.0}，这里中值为(9.0 + 12.0) / 2 = 10.5
> 
> **输入** : arr[] = {8.0，13.0，15.0}
> 输出:否

**进场:**给定问题可采用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)和[两点](https://www.geeksforgeeks.org/two-pointers-technique/)进场解决。如果**arr【】**的大小是奇数，这意味着中位数是可以用二分搜索法搜索的单个元素。如果数组大小相等，则可以使用双指针方法，因为中值将由两个元素组成。按照以下步骤解决给定的问题。

*   初始化一个变量，比如说，**表示**来存储**arr【】**的平均值。
*   检查 **arr[]** 的大小是偶数还是奇数。
    *   如果 **arr[]** 的大小是偶数
        *   使用双指针方法搜索平均值= **表示**的两个元素。
        *   将两个指针初始化为 **i=0，j=n-1** 。
        *   执行两个指针方法来搜索**arr【】**中的中间值。
    *   如果 **arr[]** 的大小是奇数
        *   应用二分搜索法查找**是否意味着**存在于**arr【】**中。
*   如果是**表示**被发现返回**是**，否则**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to return true or false if
// size of array is odd
bool binarySearch(float arr[], int size, float key)
{
    int low = 0, high = size - 1, mid;

    while (low <= high) {

        // To prevent overflow
        mid = low + (high - low) / 2;

        // If element is greater than mid, then
        // it can only be present in right subarray
        if (key > arr[mid])
            low = mid + 1;

        // If element is smaller than mid, then
        // it can only be present in left subarray
        else if (key < arr[mid])
            high = mid - 1;

        // Else the element is present at the middle
        // then return 1
        else
            return 1;
    }

    // when element is not present
    // in array then return 0
    return 0;
}

// Function to return true or false
// if size of array is even
bool twoPointers(float arr[], int N, float mean)
{

    int i = 0, j = N - 1;

    while (i < j) {

        // Calculating Candidate Median
        float temp = (arr[i] + arr[j]) / 2;

        // If Candidate Median if greater
        // than Mean then decrement j
        if (temp > mean)
            j--;

        // If Candidate Median if less
        // than Mean then increment i
        else if (temp < mean)
            i++;

        // If Candidate Median if equal
        // to Mean then return 1
        else
            return 1;
    }

    // when No candidate found for mean
    return 0;
}

// Function to return true if Mean
// can be equal to any candidate
// median otherwise return false
bool checkArray(float arr[], int N)
{

    // Calculating Mean
    float sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];

    float mean = sum / N;

    // If N is Odd
    if (N & 1)
        return binarySearch(arr, N, mean);

    // If N is even
    else
        return twoPointers(arr, N, mean);
}

// Driver Code
int main()
{
    float arr[] = { 1.0, 3.0, 6.0, 9.0, 12.0, 32.0 };
    int N = sizeof(arr) / sizeof(arr[0]);

    if (checkArray(arr, N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

public class GFG{

// Function to return true or false if
// size of array is odd
static boolean binarySearch(float []arr, int size, float key)
{
    int low = 0, high = size - 1, mid;

    while (low <= high) {

        // To prevent overflow
        mid = low + (high - low) / 2;

        // If element is greater than mid, then
        // it can only be present in right subarray
        if (key > arr[mid])
            low = mid + 1;

        // If element is smaller than mid, then
        // it can only be present in left subarray
        else if (key < arr[mid])
            high = mid - 1;

        // Else the element is present at the middle
        // then return 1
        else
            return true;
    }

    // when element is not present
    // in array then return 0
    return false;
}

// Function to return true or false
// if size of array is even
static boolean twoPointers(float []arr, int N, float mean)
{

    int i = 0, j = N - 1;

    while (i < j) {

        // Calculating Candidate Median
        float temp = (arr[i] + arr[j]) / 2;

        // If Candidate Median if greater
        // than Mean then decrement j
        if (temp > mean)
            j--;

        // If Candidate Median if less
        // than Mean then increment i
        else if (temp < mean)
            i++;

        // If Candidate Median if equal
        // to Mean then return 1
        else
            return true;
    }

    // when No candidate found for mean
    return false;
}

// Function to return true if Mean
// can be equal to any candidate
// median otherwise return false
static boolean checkArray(float []arr, int N)
{

    // Calculating Mean
    float sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];

    float mean = sum / N;

    // If N is Odd
    if ((N & 1)!=0)
        return binarySearch(arr, N, mean);

    // If N is even
    else
        return twoPointers(arr, N, mean);
}

// Driver Code
public static void main(String []args)
{
    float []arr = { 1.0f, 3.0f, 6.0f, 9.0f, 12.0f, 32.0f };
    int N = arr.length;

    if (checkArray(arr, N))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by AnkThon.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to return true or false if
# size of array is odd
def binarySearch(arr, size, key):

    low = 0
    high = size - 1

    while (low <= high):

                # To prevent overflow
        mid = low + (high - low) // 2

        # If element is greater than mid, then
        # it can only be present in right subarray
        if (key > arr[mid]):
            low = mid + 1

        # If element is smaller than mid, then
        # it can only be present in left subarray
        elif (key < arr[mid]):
            high = mid - 1

            # Else the element is present at the middle
            # then return 1
        else:
            return 1
    # when element is not present
    # in array then return 0
    return 0

# Function to return true or false
# if size of array is even
def twoPointers(arr, N, mean):

    i = 0
    j = N - 1

    while (i < j):

                # Calculating Candidate Median
        temp = (arr[i] + arr[j]) / 2

        # If Candidate Median if greater
        # than Mean then decrement j
        if (temp > mean):
            j = j - 1

            # If Candidate Median if less
            # than Mean then increment i
        elif (temp < mean):
            i = i + 1

            # If Candidate Median if equal
            # to Mean then return 1
        else:
            return 1

        # when No candidate found for mean
    return 0

# Function to return true if Mean
# can be equal to any candidate
# median otherwise return false
def checkArray(arr, N):

        # Calculating Mean
    sum = 0
    for i in range(0, N):
        sum += arr[i]

    mean = sum / N

    # If N is Odd
    if (N & 1):
        return binarySearch(arr, N, mean)

    # If N is even
    else:
        return twoPointers(arr, N, mean)

# Driver Code
if __name__ == "__main__":

    arr = [1.0, 3.0, 6.0, 9.0, 12.0, 32.0]
    N = len(arr)
    if (checkArray(arr, N)):
        print("Yes")
    else:
        print("No")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return true or false if
// size of array is odd
static bool binarySearch(float []arr, int size, float key)
{
    int low = 0, high = size - 1, mid;

    while (low <= high) {

        // To prevent overflow
        mid = low + (high - low) / 2;

        // If element is greater than mid, then
        // it can only be present in right subarray
        if (key > arr[mid])
            low = mid + 1;

        // If element is smaller than mid, then
        // it can only be present in left subarray
        else if (key < arr[mid])
            high = mid - 1;

        // Else the element is present at the middle
        // then return 1
        else
            return true;
    }

    // when element is not present
    // in array then return 0
    return false;
}

// Function to return true or false
// if size of array is even
static bool twoPointers(float []arr, int N, float mean)
{

    int i = 0, j = N - 1;

    while (i < j) {

        // Calculating Candidate Median
        float temp = (arr[i] + arr[j]) / 2;

        // If Candidate Median if greater
        // than Mean then decrement j
        if (temp > mean)
            j--;

        // If Candidate Median if less
        // than Mean then increment i
        else if (temp < mean)
            i++;

        // If Candidate Median if equal
        // to Mean then return 1
        else
            return true;
    }

    // when No candidate found for mean
    return false;
}

// Function to return true if Mean
// can be equal to any candidate
// median otherwise return false
static bool checkArray(float []arr, int N)
{

    // Calculating Mean
    float sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];

    float mean = sum / N;

    // If N is Odd
    if ((N & 1)!=0)
        return binarySearch(arr, N, mean);

    // If N is even
    else
        return twoPointers(arr, N, mean);
}

// Driver Code
public static void Main()
{
    float []arr = { 1.0f, 3.0f, 6.0f, 9.0f, 12.0f, 32.0f };
    int N = arr.Length;

    if (checkArray(arr, N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to return true or false if
    // size of array is odd
    const binarySearch = (arr, size, key) => {
        let low = 0, high = size - 1, mid;

        while (low <= high) {

            // To prevent overflow
            mid = low + parseInt((high - low) / 2);

            // If element is greater than mid, then
            // it can only be present in right subarray
            if (key > arr[mid])
                low = mid + 1;

            // If element is smaller than mid, then
            // it can only be present in left subarray
            else if (key < arr[mid])
                high = mid - 1;

            // Else the element is present at the middle
            // then return 1
            else
                return 1;
        }

        // when element is not present
        // in array then return 0
        return 0;
    }

    // Function to return true or false
    // if size of array is even
    const twoPointers = (arr, N, mean) => {

        let i = 0, j = N - 1;

        while (i < j) {

            // Calculating Candidate Median
            let temp = (arr[i] + arr[j]) / 2;

            // If Candidate Median if greater
            // than Mean then decrement j
            if (temp > mean)
                j--;

            // If Candidate Median if less
            // than Mean then increment i
            else if (temp < mean)
                i++;

            // If Candidate Median if equal
            // to Mean then return 1
            else
                return 1;
        }

        // when No candidate found for mean
        return 0;
    }

    // Function to return true if Mean
    // can be equal to any candidate
    // median otherwise return false
    const checkArray = (arr, N) => {

        // Calculating Mean
        let sum = 0;
        for (let i = 0; i < N; i++)
            sum += arr[i];

        let mean = sum / N;

        // If N is Odd
        if (N & 1)
            return binarySearch(arr, N, mean);

        // If N is even
        else
            return twoPointers(arr, N, mean);
    }

    // Driver Code
    let arr = [1.0, 3.0, 6.0, 9.0, 12.0, 32.0];
    let N = arr.length;

    if (checkArray(arr, N))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by rakeshsahni
</script>
```

**Output**

```
Yes
```

**时间复杂度** : O(N)，当 N 为偶数时。
O(logN)，当 N 为奇数时。
**辅助空间** : O(1)。