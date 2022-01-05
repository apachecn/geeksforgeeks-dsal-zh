# C/C++程序，使用结构

添加英寸英尺系统中给定的 N 个距离

> 原文:[https://www . geesforgeks . org/c-CPP-program-to-add-n-distance-给定英寸-英尺-系统使用结构/](https://www.geeksforgeeks.org/c-cpp-program-to-add-n-distances-given-in-inch-feet-system-using-structures/)

给定一个包含英寸-英尺系统的 **N** 距离的数组 **arr[]** ，使得数组的每个元素以**{英寸，英尺}** 的形式表示一个距离。任务是使用[结构](https://www.geeksforgeeks.org/structures-c/)添加所有 **N 英寸英尺**距离。

**示例:**

> **输入:** arr[] = { { 10，3.7 }，{ 10，5.5 }，{ 6，8.0 } }；
> T3】输出:T5】尺和:27
> 寸和:5.20
> 
> **输入:** arr[] = { { 1，1.7 }，{ 1，1.5 }，{ 6，8 } }；
> T3】输出:T5】尺和:8
> 寸和:11.20

**进场:**

1.  遍历结构数组 **arr** ，求给定的一组 **N** 距离的所有英寸的总和，如下所示:

    ```
    feet_sum = feet_sum + arr[i].feet;
    inch_sum = inch_sum + arr[i].inch;

    ```

2.  If the sum of all the inches (say **inch_sum**) is greater than 12, then convert the inch_sum into feet because

    ```
    1 feet = 12 inches

    ```

    因此将**英寸 _ 总和**更新为**英寸 _ 总和% 12** 。然后求 **N** 距离的所有英尺(比如**英尺 _ 总和**)的总和，并将**英寸 _ 总和/12** 加到这个总和上。

3.  分别打印**英尺 _ 总和**和**英寸 _ 总和**。

下面是上述方法的实现:

## C

```
// C program for the above approach

#include "stdio.h"

// Struct defined for the inch-feet system
struct InchFeet {

    // Variable to store the inch-feet
    int feet;
    float inch;
};

// Function to find the sum of all N
// set of Inch Feet distances
void findSum(struct InchFeet arr[], int N)
{

    // Variable to store sum
    int feet_sum = 0;
    float inch_sum = 0.0;

    int x;

    // Traverse the InchFeet array
    for (int i = 0; i < N; i++) {

        // Find the total sum of
        // feet and inch
        feet_sum += arr[i].feet;
        inch_sum += arr[i].inch;
    }

    // If inch sum is greater than 11
    // convert it into feet
    // as 1 feet = 12 inch
    if (inch_sum >= 12) {

        // Find integral part of inch_sum
        x = (int)inch_sum;

        // Delete the integral part x
        inch_sum -= x;

        // Add x%12 to inch_sum
        inch_sum += x % 12;

        // Add x/12 to feet_sum
        feet_sum += x / 12;
    }

    // Print the corresponding sum of
    // feet_sum and inch_sum
    printf("Feet Sum: %d\n", feet_sum);
    printf("Inch Sum: %.2f", inch_sum);
}

// Driver Code
int main()
{

    // Given set of inch-feet
    struct InchFeet arr[]
        = { { 10, 3.7 },
            { 10, 5.5 },
            { 6, 8.0 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findSum(arr, N);

    return 0;
}
```

## C++

```
// C++ program for the above approach
#include "iostream"
using namespace std;

// Struct defined for the inch-feet system
struct InchFeet {

    // Variable to store the inch-feet
    int feet;
    float inch;
};

// Function to find the sum of all N
// set of Inch Feet distances
void findSum(InchFeet arr[], int N)
{

    // Variable to store sum
    int feet_sum = 0;
    float inch_sum = 0.0;

    int x;

    // Traverse the InchFeet array
    for (int i = 0; i < N; i++) {

        // Find the total sum of
        // feet and inch
        feet_sum += arr[i].feet;
        inch_sum += arr[i].inch;
    }

    // If inch sum is greater than 11
    if (inch_sum >= 12) {

        // Find integral part of inch_sum
        int x = (int)inch_sum;

        // Delete the integral part x
        inch_sum -= x;

        // Add x%12 to inch_sum
        inch_sum += x % 12;

        // Add x/12 to feet_sum
        feet_sum += x / 12;
    }

    // Print the corresponding sum of
    // feet_sum and inch_sum
    cout << "Feet Sum: "
         << feet_sum << '\n'
         << "Inch Sum: "
         << inch_sum << endl;
}

// Driver Code
int main()
{

    // Given a set of inch-feet
    InchFeet arr[]
        = { { 10, 3.7 },
            { 10, 5.5 },
            { 6, 8.0 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findSum(arr, N);

    return 0;
}
```

**Output:**

```
Feet Sum: 27
Inch Sum: 5.20

```

**时间复杂度:** *O(N)* ，其中 N 为英寸-英尺距离数。