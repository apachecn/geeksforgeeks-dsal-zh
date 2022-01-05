# 通过交换位生成元素最大化的数组

> 原文:[https://www . geeksforgeeks . org/generate-a-array-as-with-elements-通过交换位最大化/](https://www.geeksforgeeks.org/generate-an-array-such-with-elements-maximized-through-swapping-bits/)

给定一个数组 **arr[]** ，任务是生成一个修改后的数组，这样它的所有元素都可以通过交换位来最大化。
**例:**

> **输入:** arr[] = {10，15}
> **输出:** 12，15
> **解释:**
> 二进制表示(10)<sub>10</sub>=(1010)<sub>2</sub>。交换第二位和第三位，得到二进制表示为(1100)<sub>2</sub>=(12)<sub>10</sub>。
> 对于 15，它的二进制表示为 1111，不能进一步改变得到更大的值。
> **输入:** arr[] = {8，15，9，10，14}
> **输出:** 8，15，12，12，14

**进场:**
按照以下步骤解决问题:

*   计算每个数组元素中已设置和未设置的位数。
*   将所有设置的位向左(MSB)移动，将所有未设置的位向右(LSB)移动，以最大化数组元素。
*   如果设置位或未设置位的计数等于数组元素的位数，则该元素不能更改(例如(7) <sup>10</sup> = (111) <sup>2</sup>
*   打印数组中最大化的元素

以下是上述方法的实现:

## C++

```
// C++ implementation to
// find maximum sequence by
// swapping bits
#include <bits/stdc++.h>
using namespace std;

// Function to generate the maximized
// array elements
void maximizedArray(
    int arr[], int N)
{
    int num, i = 0;

    // Traverse the array
    while (N--) {
        num = arr[i];
        int one = 0;
        int zero = 0;

        // Iterate to count set and
        // unset bits
        while (num) {

            // Count of unset bits
            if (num % 2 == 0) {
                zero++;
            }
            else {

                // Count of set bits
                one++;
            }

            // Bitwise right shift
            num = num >> 1;
        }

        for (int j = zero; j < (one + zero);
             j++) {

            // Shifting all 1's to MSB
            // and 0's to LSB
            num += (1 << j);
        }
        cout << num;
        i++;

        if (N > 0)
            cout << ", ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 8, 15, 9, 10, 14 };
    int N = sizeof(arr) / sizeof(arr[0]);

    maximizedArray(
        arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// maximum sequence by swapping bits
class GFG{

// Function to generate the maximized
// array elements
public static void maximizedArray(int arr[],
                                  int N)
{
    int num, i = 0;

    // Traverse the array
    for(int l = N; l > 0; l--)
    {
       num = arr[i];
       int one = 0;
       int zero = 0;

       // Iterate to count set and
       // unset bits
       while (num != 0)
       {

           // Count of unset bits
           if (num % 2 == 0)
           {
               zero++;
           }
           else
           {

               // Count of set bits
               one++;
           }

           // Bitwise right shift
           num = num >> 1;
       }

       for(int j = zero; j < (one + zero); j++)
       {

          // Shifting all 1's to MSB
          // and 0's to LSB
          num += (1 << j);
       }
       System.out.print(num);
       i++;

       if (N > 0)
           System.out.print(", ");
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 8, 15, 9, 10, 14 };
    int N = arr.length;

    maximizedArray(arr, N);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 implementation to find
# maximum sequence by swapping bits

# Function to generate the maximized
# array elements
def maximizedArray(arr, N):

    i = 0

    # Traverse the array
    while (N > 0):
        num = arr[i]
        one = 0
        zero = 0

        # Iterate to count set and
        # unset bits
        while (num):

            # Count of unset bits
            if (num % 2 == 0):
                zero += 1

            else:

                # Count of set bits
                one += 1

            # Bitwise right shift
            num = num >> 1

        for j in range(zero, (one + zero)):

            # Shifting all 1's to MSB
            # and 0's to LSB
            num += (1 << j)

        print(num, end = "")
        i += 1

        if (N > 0):
            print(", ", end = "")

        N -= 1

# Driver Code
if __name__ == "__main__":

    arr = [ 8, 15, 9, 10, 14 ]
    N = len(arr)

    maximizedArray(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find
// maximum sequence by swapping bits
using System;
class GFG{

// Function to generate the maximized
// array elements
public static void maximizedArray(int []arr,
                                  int N)
{
    int num, i = 0;

    // Traverse the array
    for(int l = N; l > 0; l--)
    {
        num = arr[i];
        int one = 0;
        int zero = 0;

        // Iterate to count set and
        // unset bits
        while (num != 0)
        {

            // Count of unset bits
            if (num % 2 == 0)
            {
                zero++;
            }
            else
            {

                // Count of set bits
                one++;
            }

            // Bitwise right shift
            num = num >> 1;
        }

        for(int j = zero; j < (one + zero); j++)
        {

            // Shifting all 1's to MSB
            // and 0's to LSB
            num += (1 << j);
        }
        Console.Write(num);
        i++;

        if (N > 0)
            Console.Write(", ");
    }
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 8, 15, 9, 10, 14 };
    int N = arr.Length;

    maximizedArray(arr, N);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript implementation to find
// maximum sequence by swapping bits

// Function to generate the maximized
// array elements
function maximizedArray(arr, N)
{
    let num, i = 0;

    // Traverse the array
    for(let l = N; l > 0; l--)
    {
       num = arr[i];
       let one = 0;
       let zero = 0;

       // Iterate to count set and
       // unset bits
       while (num != 0)
       {

           // Count of unset bits
           if (num % 2 == 0)
           {
               zero++;
           }
           else
           {

               // Count of set bits
               one++;
           }

           // Bitwise right shift
           num = num >> 1;
       }

       for(let j = zero; j < (one + zero); j++)
       {

          // Shifting all 1's to MSB
          // and 0's to LSB
          num += (1 << j);
       }
       document.write(num);
       i++;

       if (N > 0)
           document.write(", ");
    }
}

    // Driver Code

    let arr = [ 8, 15, 9, 10, 14 ];
    let N = arr.length;

    maximizedArray(arr, N);

</script>
```

**Output:** 

```
8, 15, 12, 12, 14
```

***时间复杂度:**O(Nlog<sub>2</sub>N)*
***辅助空间:** O(1)*