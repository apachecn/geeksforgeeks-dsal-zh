# 通过修改一个元素的氛围来检查一个数组是否可以严格递增

> 原文:[https://www . geesforgeks . org/check-一个数组是否可以通过修改 Atmos-one-element 来严格递增/](https://www.geeksforgeeks.org/check-whether-an-array-can-be-made-strictly-increasing-by-modifying-atmost-one-element/)

给定一个正整数数组 **arr[]** ，任务是通过修改**Atmos**一个元素来确定这个数组是否可以严格递增。
**例:**

> **输入:** arr[] = {2，4，8，6，9，12}
> **输出:**是
> 通过修改 8 到 5，数组将变得严格递增。
> 即{2，4，5，6，9，12}
> **输入:** arr[] = {10，5，2}
> **输出:**否

**方法:**对于每个元素 **arr[i]** ，如果大于**arr[I–1]**和 **arr[i + 1]** 或者小于**arr[I–1]**和 **arr[i + 1]** ，则需要修改 **arr[i]** 。
即**arr[I]=(arr[I–1]+arr[I+1])/2**。如果在修改后，**arr[I]= arr[I–1]**或 **arr[i] = arr[i + 1]** 则不能使数组严格递增而不影响多个元素。否则计算所有此类修改，如果最后修改的次数小于或等于 **1** 则打印**“是”**否则打印**“否”**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if arr[]
// can be made strictly increasing after
// modifying at most one element
bool check(int arr[], int n)
{
    // To store the number of modifications
    // required to make the array
    // strictly increasing
    int modify = 0;

    // Check whether the first element needs
    // to be modify or not
    if (arr[0] > arr[1]) {
        arr[0] = arr[1] / 2;
        modify++;
    }

    // Loop from 2nd element to the 2nd last element
    for (int i = 1; i < n - 1; i++) {

        // Check whether arr[i] needs to be modified
        if ((arr[i - 1] < arr[i] && arr[i + 1] < arr[i])
            || (arr[i - 1] > arr[i] && arr[i + 1] > arr[i])) {

            // Modifying arr[i]
            arr[i] = (arr[i - 1] + arr[i + 1]) / 2;

            // Check if arr[i] is equal to any of
            // arr[i-1] or arr[i+1]
            if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                return false;

            modify++;
        }
    }

    // Check whether the last element needs
    // to be modify or not
    if (arr[n - 1] < arr[n - 2])
        modify++;

    // If more than 1 modification is required
    if (modify > 1)
        return false;

    return true;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 8, 6, 9, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (check(arr, n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true if arr[]
    // can be made strictly increasing after
    // modifying at most one element
    static boolean check(int arr[], int n)
    {
        // To store the number of modifications
        // required to make the array
        // strictly increasing
        int modify = 0;

        // Check whether the first element needs
        // to be modify or not
        if (arr[0] > arr[1]) {
            arr[0] = arr[1] / 2;
            modify++;
        }

        // Loop from 2nd element to the 2nd last element
        for (int i = 1; i < n - 1; i++) {

            // Check whether arr[i] needs to be modified
            if ((arr[i - 1] < arr[i] && arr[i + 1] < arr[i])
                || (arr[i - 1] > arr[i] && arr[i + 1] > arr[i])) {

                // Modifying arr[i]
                arr[i] = (arr[i - 1] + arr[i + 1]) / 2;

                // Check if arr[i] is equal to any of
                // arr[i-1] or arr[i+1]
                if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                    return false;

                modify++;
            }
        }

        // Check whether the last element needs
        // to be modify or not
        if (arr[n - 1] < arr[n - 2])
            modify++;

        // If more than 1 modification is required
        if (modify > 1)
            return false;

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {

        int[] arr = { 2, 4, 8, 6, 9, 12 };
        int n = arr.length;

        if (check(arr, n))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if arr[]
    // can be made strictly increasing after
    // modifying at most one element
    static bool check(int []arr, int n)
    {
        // To store the number of modifications
        // required to make the array
        // strictly increasing
        int modify = 0;

        // Check whether the first element needs
        // to be modify or not
        if (arr[0] > arr[1])
        {
            arr[0] = arr[1] / 2;
            modify++;
        }

        // Loop from 2nd element to the 2nd last element
        for (int i = 1; i < n - 1; i++)
        {

            // Check whether arr[i] needs to be modified
            if ((arr[i - 1] < arr[i] && arr[i + 1] < arr[i])
                || (arr[i - 1] > arr[i] && arr[i + 1] > arr[i]))
            {

                // Modifying arr[i]
                arr[i] = (arr[i - 1] + arr[i + 1]) / 2;

                // Check if arr[i] is equal to any of
                // arr[i-1] or arr[i+1]
                if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                    return false;

                modify++;
            }
        }

        // Check whether the last element needs
        // to be modify or not
        if (arr[n - 1] < arr[n - 2])
            modify++;

        // If more than 1 modification is required
        if (modify > 1)
            return false;

        return true;
    }

    // Driver code
    public static void Main()
    {

        int[] arr = { 2, 4, 8, 6, 9, 12 };
        int n = arr.Length;

        if (check(arr, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function that returns true if arr[]
# can be made strictly increasing after
# modifying at most one element
def check( arr, n):

    # To store the number of modifications
    # required to make the array
    # strictly increasing
    modify = 0

    # Check whether the first element needs
    # to be modify or not
    if (arr[0] > arr[1]) :
        arr[0] = arr[1] // 2
        modify+=1

    # Loop from 2nd element to the 2nd last element
    for i in range ( 1, n - 1):

        # Check whether arr[i] needs to be modified
        if ((arr[i - 1] < arr[i] and arr[i + 1] < arr[i])
            or (arr[i - 1] > arr[i] and arr[i + 1] > arr[i])):

            # Modifying arr[i]
            arr[i] = (arr[i - 1] + arr[i + 1]) // 2

            # Check if arr[i] is equal to any of
            # arr[i-1] or arr[i+1]
            if (arr[i] == arr[i - 1] or arr[i] == arr[i + 1]):
                return False

            modify+=1

    # Check whether the last element needs
    # to be modify or not
    if (arr[n - 1] < arr[n - 2]):
        modify+=1

    # If more than 1 modification is required
    if (modify > 1):
        return False

    return True

# Driver code
if __name__ == "__main__":
    arr = [ 2, 4, 8, 6, 9, 12 ]
    n = len(arr)

    if (check(arr, n)):
        print ( "Yes")
    else:
        print ("No")

# This code is contributed by ChitraNayal   
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if arr[]
// can be made strictly increasing after
// modifying at most one element
function check(arr, n)
{
    // To store the number of modifications
    // required to make the array
    // strictly increasing
    var modify = 0;

    // Check whether the first element needs
    // to be modify or not
    if (arr[0] > arr[1]) {
        arr[0] = arr[1] / 2;
        modify++;
    }

    // Loop from 2nd element to the 2nd last element
    for (var i = 1; i < n - 1; i++) {

        // Check whether arr[i] needs to be modified
        if ((arr[i - 1] < arr[i] && arr[i + 1] < arr[i])
            || (arr[i - 1] > arr[i] && arr[i + 1] > arr[i])) {

            // Modifying arr[i]
            arr[i] = (arr[i - 1] + arr[i + 1]) / 2;

            // Check if arr[i] is equal to any of
            // arr[i-1] or arr[i+1]
            if (arr[i] == arr[i - 1] || arr[i] == arr[i + 1])
                return false;

            modify++;
        }
    }

    // Check whether the last element needs
    // to be modify or not
    if (arr[n - 1] < arr[n - 2])
        modify++;

    // If more than 1 modification is required
    if (modify > 1)
        return false;

    return true;
}

// Driver code
var arr = [ 2, 4, 8, 6, 9, 12 ];
var n = arr.length;
if (check(arr, n))
    document.write( "Yes" );
else
    document.write( "No" );

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```