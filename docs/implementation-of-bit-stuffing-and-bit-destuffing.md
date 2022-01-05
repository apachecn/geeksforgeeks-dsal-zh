# 比特填充和比特去填充的实现

> 原文:[https://www . geesforgeks . org/实现位填充和位去填充/](https://www.geeksforgeeks.org/implementation-of-bit-stuffing-and-bit-destuffing/)

[位填充](https://www.geeksforgeeks.org/bit-stuffing-in-computer-network/)是当帧序列遇到 **5** 连续 **1 的**时，插入一个额外位作为 **0** 的过程。给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，由 **0 的**和 **1 的**组成，任务是在比特填充后返回一个数组。

**示例:**

> **输入:** N = 6，arr[] = {1，1，1，1，1}
> **输出:**11111101
> **解释:**在遍历数组的过程中，在给定数组的第 4 个索引之后会遇到 5 个连续的 1。因此，在第四个索引之后，一个零比特被插入填充数组
> 
> **输入:** N = 6，arr[] = {1，0，1，0，1，0 }
> T3】输出: 101010

**方法:**想法是检查给定的数组是否由 5 个连续的 **1 的**组成。按照以下步骤解决问题:

*   [初始化存储填充数组的数组 **brr[]**](https://www.geeksforgeeks.org/arrays-in-c-cpp/) 。另外，创建一个保持连续 1 的计数的变量计数。
*   [使用范围**【0，N】**中的变量 **i** 在一个间歇循环中遍历](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)，并执行以下任务:
    *   如果**arr【I】**是 **1** ，那么检查下一个 **4** 位是否也是设置位。如果是，则在将所有 5 个设置位插入阵列 **brr[]** 后插入 0 位。
    *   否则，将 **arr[i]** 的值插入到数组 **brr[]** 中。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function for bit stuffing
void bitStuffing(int N, int arr[])
{

    // Stores the stuffed array
    int brr[30];

    // Variables to traverse arrays
    int i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    int count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N)
    {

        // If the current bit is a set bit
        if (arr[i] == 1)
        {

            // Insert into array brr[]
            brr[j] = arr[i];

            // Loop to check for
            // next 5 bits
            for(k = i + 1; arr[k] == 1 && k < N && count < 5;
                k++)
            {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set bits
                // are found insert a 0 bit
                if (count == 5)
                {
                    j++;
                    brr[j] = 0;
                }
                i = k;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr[]
        else
        {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for(i = 0; i < j; i++)
        cout << brr[i];
}

// Driver code
int main()
{
    int N = 6;
    int arr[] = { 1, 1, 1, 1, 1, 1 };

    bitStuffing(N, arr);;
    return 0;
}

// This code is contributed by target_2
```

## C

```
// C program for the above approach
#include <stdio.h>
#include <string.h>

// Function for bit stuffing
void bitStuffing(int N, int arr[])
{
    // Stores the stuffed array
    int brr[30];

    // Variables to traverse arrays
    int i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    int count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N) {

        // If the current bit is a set bit
        if (arr[i] == 1) {

            // Insert into array brr[]
            brr[j] = arr[i];

            // Loop to check for
            // next 5 bits
            for (k = i + 1;
                 arr[k] == 1
                 && k < N
                 && count < 5;
                 k++) {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set bits
                // are found insert a 0 bit
                if (count == 5) {
                    j++;
                    brr[j] = 0;
                }
                i = k;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr[]
        else {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for (i = 0; i < j; i++)
        printf("%d", brr[i]);
}

// Driver Code
int main()
{
    int N = 6;
    int arr[] = { 1, 1, 1, 1, 1, 1 };

    bitStuffing(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function for bit stuffing
static void bitStuffing(int N, int arr[])
{

    // Stores the stuffed array
    int []brr = new int[30];

    // Variables to traverse arrays
    int i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    int count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N) {

        // If the current bit is a set bit
        if (arr[i] == 1) {

            // Insert into array brr[]
            brr[j] = arr[i];

            // Loop to check for
            // next 5 bits
            for (k = i + 1; k < N &&
                 arr[k] == 1

                 && count < 5;
                 k++) {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set bits
                // are found insert a 0 bit
                if (count == 5) {
                    j++;
                    brr[j] = 0;
                }
                i = k;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr[]
        else {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for (i = 0; i < j; i++)
        System.out.printf("%d", brr[i]);
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;
    int arr[] = { 1, 1, 1, 1, 1, 1 };

    bitStuffing(N, arr);

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function for bit stuffing
def bitStuffing(N, arr):

    # Stores the stuffed array
    brr = [0 for _ in range(30)]

    # Variables to traverse arrays
    k = 0
    i = 0
    j = 0

    # Stores the count of consecutive ones
    count = 1

    # Loop to traverse in the range [0, N)
    while (i < N):

        # If the current bit is a set bit
        if (arr[i] == 1):

            # Insert into array brr[]
            brr[j] = arr[i]

            # Loop to check for
            # next 5 bits
            k = i + 1
            while True:
                if not (k < N and arr[k] == 1 and
                        count < 5):
                    break

                j += 1
                brr[j] = arr[k]
                count += 1

                # If 5 consecutive set bits
                # are found insert a 0 bit
                if (count == 5):
                    j += 1
                    brr[j] = 0

                i = k
                k += 1

        # Otherwise insert arr[i] into
        # the array brr[]
        else:
            brr[j] = arr[i]

        i += 1
        j += 1

    # Print Answer
    for i in range(0, j):
        print(brr[i], end = "")

# Driver Code
if __name__ == "__main__":

    N = 6
    arr = [ 1, 1, 1, 1, 1, 1 ]

    bitStuffing(N, arr)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function for bit stuffing
static void bitStuffing(int N, int[] arr)
{

    // Stores the stuffed array
    int[] brr = new int[30];

    // Variables to traverse arrays
    int i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    int count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N)
    {

        // If the current bit is a set bit
        if (arr[i] == 1)
        {

            // Insert into array brr[]
            brr[j] = arr[i];

            // Loop to check for
            // next 5 bits
            k = i + 1;
            while (k < N && arr[k] == 1 && count < 5)
            {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set bits
                // are found insert a 0 bit
                if (count == 5)
                {
                    j++;
                    brr[j] = 0;
                }
                i = k;
                k++;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr[]
        else
        {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for(i = 0; i < j; i++)
        Console.Write(brr[i]);
}

// Driver Code
public static void Main()
{
    int N = 6;
    int[] arr = { 1, 1, 1, 1, 1, 1 };

    bitStuffing(N, arr);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach

      // Function for bit stuffing
      function bitStuffing(N, arr)
      {

          // Stores the stuffed array
          let brr = new Array(30);

          // Variables to traverse arrays
          let i, j, k;
          i = 0;
          j = 0;

          // Stores the count of consecutive ones
          let count = 1;

          // Loop to traverse in the range [0, N)
          while (i < N) {

              // If the current bit is a set bit
              if (arr[i] == 1) {

                  // Insert into array brr[]
                  brr[j] = arr[i];

                  // Loop to check for
                  // next 5 bits
                  for (k = i + 1;
                      arr[k] == 1
                      && k < N
                      && count < 5;
                      k++) {
                      j++;
                      brr[j] = arr[k];
                      count++;

                      // If 5 consecutive set bits
                      // are found insert a 0 bit
                      if (count == 5) {
                          j++;
                          brr[j] = 0;
                      }
                      i = k;
                  }
              }

              // Otherwise insert arr[i] into
              // the array brr[]
              else {
                  brr[j] = arr[i];
              }
              i++;
              j++;
          }

          // Print Answer
          for (i = 0; i < j; i++)
              document.write(brr[i] + " ");
      }

      // Driver Code
      let N = 6;
      let arr = [1, 1, 1, 1, 1, 1];

      bitStuffing(N, arr);

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
1111101
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**钻头去毛刺**或**钻头去毛刺**是在[钻头填充](https://www.geeksforgeeks.org/bit-stuffing-in-computer-network/)过程中撤销阵列变化的过程，即在连续遇到 **5** 个 **1 个**后移除多余的 **0** 钻头。

**示例:**

> **输入:** N = 7，arr[] = {1，1，1，1，0，1}
> **输出:**1111111
> **解释:**在遍历数组的过程中，在给定数组的第 4 个索引后会遇到 5 个连续的 1。因此，下一个 0 位必须被移除以解填充数组。
> 
> **输入:** N = 6，arr[] = {1，0，1，0，1，0 }
> T3】输出: 101010

**处理方法:**这个问题可以类似于[比特填充](https://www.geeksforgeeks.org/bit-stuffing-in-computer-network/)问题来解决。上述方法中唯一需要的改变是每当遇到 **5** 连续的**1**时，跳过[数组中的下一位](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，而不是在数组 **brr[]** 中插入一个 **0** 位。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>
#include <string.h>

// Function for bit de-stuffing
void bitDestuffing(int N, int arr[])
{
    // Stores the de-stuffed array
    int brr[30];

    // Variables to traverse the arrays
    int i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    int count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N) {

        // If the current bit is a set bit
        if (arr[i] == 1) {

            // Insert into array brr[]
            brr[j] = arr[i];

            // Loop to check for
            // the next 5 bits
            for (k = i + 1;
                 arr[k] == 1
                 && k < N
                 && count < 5;
                 k++) {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set
                // bits are found skip the
                // next bit in arr[]
                if (count == 5) {
                    k++;
                }
                i = k;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr
        else {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for (i = 0; i < j; i++)
        printf("%d", brr[i]);
}

// Driver Code
int main()
{
    int N = 7;
    int arr[] = { 1, 1, 1, 1, 1, 0, 1 };

    bitDestuffing(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function for bit de-stuffing
static void bitDestuffing(int N, int arr[])
{

    // Stores the de-stuffed array
    int []brr = new int[30];

    // Variables to traverse the arrays
    int i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    int count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N) {

        // If the current bit is a set bit
        if (arr[i] == 1) {

            // Insert into array brr[]
            brr[j] = arr[i];

            // Loop to check for
            // the next 5 bits
            for (k = i + 1; k<N &&
                 arr[k] == 1

                 && count < 5;
                 k++) {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set
                // bits are found skip the
                // next bit in arr[]
                if (count == 5) {
                    k++;
                }
                i = k;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr
        else {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for (i = 0; i < j; i++)
        System.out.printf("%d", brr[i]);
}

// Driver Code
public static void main(String[] args)
{
    int N = 7;
    int arr[] = { 1, 1, 1, 1, 1, 0, 1 };

    bitDestuffing(N, arr);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function for bit de-stuffing
def bitDestuffing(N, arr):

    # Stores the de-stuffed array
    brr = [0 for i in range(30)];

    # Variables to traverse the arrays
    k = 0;
    i = 0;
    j = 0;

    # Stores the count of consecutive ones
    count = 1;

    # Loop to traverse in the range [0, N)
    while (i < N):

        # If the current bit is a set bit
        if (arr[i] == 1):

            # Insert into array brr
            brr[j] = arr[i];

            # Loop to check for
            # the next 5 bits
            for k in range(i + 1, k < N and arr[k] == 1 and count < 5,1):
                j += 1;
                brr[j] = arr[k];
                count += 1;

                # If 5 consecutive set
                # bits are found skip the
                # next bit in arr
                if (count == 5):
                    k += 1;

                i = k;

        # Otherwise insert arr[i] into
        # the array brr
        else:
            brr[j] = arr[i];

        i += 1;
        j += 1;

    # PrAnswer
    for i in range(0, j):
        print(brr[i],end="");

# Driver Code
if __name__ == '__main__':
    N = 7;
    arr = [1, 1, 1, 1, 1, 0, 1];

    bitDestuffing(N, arr);

# This code contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function for bit de-stuffing
static void bitDestuffing(int N, int[] arr)
{

    // Stores the de-stuffed array
    int []brr = new int[30];

    // Variables to traverse the arrays
    int i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    int count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N) {

        // If the current bit is a set bit
        if (arr[i] == 1) {

            // Insert into array brr[]
            brr[j] = arr[i];

            // Loop to check for
            // the next 5 bits
            for (k = i + 1; k<N &&
                 arr[k] == 1

                 && count < 5;
                 k++) {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set
                // bits are found skip the
                // next bit in arr[]
                if (count == 5) {
                    k++;
                }
                i = k;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr
        else {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for (i = 0; i < j; i++)
        Console.Write(brr[i]);
}

// Driver Code
public static void Main()
{
    int N = 7;
    int[] arr = { 1, 1, 1, 1, 1, 0, 1 };

    bitDestuffing(N, arr);
}
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
// javascript program for the above approach// Function for bit de-stuffing
function bitDestuffing(N , arr)
{

    // Stores the de-stuffed array
    var brr = Array.from({length: 30}, (_, i) => 0);

    // Variables to traverse the arrays
    var i, j, k;
    i = 0;
    j = 0;

    // Stores the count of consecutive ones
    var count = 1;

    // Loop to traverse in the range [0, N)
    while (i < N) {

        // If the current bit is a set bit
        if (arr[i] == 1) {

            // Insert into array brr
            brr[j] = arr[i];

            // Loop to check for
            // the next 5 bits
            for (k = i + 1; k<N &&
                 arr[k] == 1

                 && count < 5;
                 k++) {
                j++;
                brr[j] = arr[k];
                count++;

                // If 5 consecutive set
                // bits are found skip the
                // next bit in arr
                if (count == 5) {
                    k++;
                }
                i = k;
            }
        }

        // Otherwise insert arr[i] into
        // the array brr
        else {
            brr[j] = arr[i];
        }
        i++;
        j++;
    }

    // Print Answer
    for (i = 0; i < j; i++)
        document.write(brr[i]);
}

// Driver Code
var N = 7;
var arr = [ 1, 1, 1, 1, 1, 0, 1 ];

bitDestuffing(N, arr);

// This code is contributed by 29AjayKumar
</script>
```

**Output**

```
1111101
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)