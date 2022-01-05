# 使数组乘积等于 1 的最小步数

> 原文:[https://www . geeksforgeeks . org/使阵列产品等于 1 的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-to-make-the-product-of-the-array-equal-to-1/)

给定一个包含整数 **N** 的数组 **arr[]** 。在一个步骤中，数组的任何元素都可以增加或减少一。任务是找到所需的最小步骤，使阵列元素的乘积成为 **1** 。

**示例:**

> **输入:** arr[] = { -2，4，0 }
> **输出:** 5
> 我们可以把-2 改成-1，0 改成-1，4 改成 1。
> 因此，总共需要 5 个步骤来更新元素
> ，使得最终数组的乘积为 1。
> 
> **输入:** arr[] = { -1，1，-1 }
> T3】输出: 0

**方法:**按照以下步骤解决问题:

1.  当数组中只有 1 和-1，并且-1 的计数为偶数时，数组元素的乘积只能等于 **1** 。
2.  现在，所有正数都可以简化为 **1** ，因为它们离 **1** 比离**1**更近。
3.  同样，所有负数都可以更新为 **-1** 。
4.  如果阵列中存在 **0** s，则可以根据情况将其减少为 **1** 或**-1**(1 的计数必须为偶数)。
5.  如果 **-ve 数**的计数是偶数，那么它们总是会产生 **-1** 。
6.  但是如果有奇数个 **-ve 数**，那么它们将产生奇数个 **-1s** 。要解决这个问题，有两种可能:
    *   先试着找到数组中的计数 **0s** ，因为需要 **1** 运算才能成为 **-1** 。
    *   如果数组中没有零，则只需在答案中添加 **2** ，因为它需要两步才能使 **-1** 变为 **1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// steps required
int MinStep(int a[], int n)
{

    // To store the count of 0s, positive
    // and negative numbers
    int positive = 0,
        negative = 0,
        zero = 0;

    // To store the ans
    int step = 0;

    for (int i = 0; i < n; i++) {

        // If array element is
        // equal to 0
        if (a[i] == 0) {
            zero++;
        }

        // If array element is
        // a negative number
        else if (a[i] < 0) {
            negative++;

            // Extra cost needed
            // to make it -1
            step = step + (-1 - a[i]);
        }

        // If array element is
        // a positive number
        else {
            positive++;

            // Extra cost needed
            // to make it 1
            step = step + (a[i] - 1);
        }
    }

    // Now the array will
    // have -1, 0 and 1 only
    if (negative % 2 == 0) {

        // As count of negative is even
        // so we will change all 0 to 1
        // total cost here will be
        // count of 0s
        step = step + zero;
    }
    else {

        // If there are zeroes present
        // in the array
        if (zero > 0) {

            // Change one zero to -1
            // and rest of them to 1
            // Total cost here will
            // be count of '0'
            step = step + zero;
        }

        // If there are no zeros in the array
        else {

            // As no 0s are available so we
            // have to change one -1 to 1
            // which will cost 2 to
            // change -1 to 1
            step = step + 2;
        }
    }

    return step;
}

// Driver code
int main()
{
    int a[] = { 0, -2, -1, -3, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MinStep(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum
    // steps required
    static int MinStep(int a[], int n)
    {

        // To store the count of 0s, positive
        // and negative numbers
        int positive = 0,
            negative = 0,
            zero = 0;

        // To store the ans
        int step = 0;

        for (int i = 0; i < n; i++) {

            // If array element is
            // equal to 0
            if (a[i] == 0) {
                zero++;
            }

            // If array element is
            // a negative number
            else if (a[i] < 0) {
                negative++;

                // Extra cost needed
                // to make it -1
                step = step + (-1 - a[i]);
            }

            // If array element is
            // a positive number
            else {
                positive++;

                // Extra cost needed
                // to make it 1
                step = step + (a[i] - 1);
            }
        }

        // Now the array will
        // have -1, 0 and 1 only
        if (negative % 2 == 0) {

            // As count of negative is even
            // so we will change all 0 to 1
            // total cost here will be
            // count of 0s
            step = step + zero;
        }
        else {

            // If there are zeroes present
            // in the array
            if (zero > 0) {

                // Change one zero to -1
                // and rest of them to 1
                // Total cost here will
                // be count of '0'
                step = step + zero;
            }

            // If there are no zeros in the array
            else {

                // As no 0s are available so we
                // have to change one -1 to 1
                // which will cost 2 to
                // change -1 to 1
                step = step + 2;
            }
        }

        return step;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 0, -2, -1, -3, 4 };
        int n = a.length;

        System.out.println(MinStep(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# steps required
def MinStep(a, n):

    # To store the count of 0s, positive
    # and negative numbers
    positive = 0;
    negative = 0;
    zero = 0;

    # To store the ans
    step = 0;

    for i in range(n):

        # If array element is
        # equal to 0
        if (a[i] == 0):
            zero += 1;

        # If array element is
        # a negative number
        elif (a[i] < 0):

            negative += 1;

            # Extra cost needed
            # to make it -1
            step = step + (-1 - a[i]);

        # If array element is
        # a positive number
        else:
            positive += 1;

            # Extra cost needed
            # to make it 1
            step = step + (a[i] - 1);

    # Now the array will
    # have -1, 0 and 1 only
    if (negative % 2 == 0):

        # As count of negative is even
        # so we will change all 0 to 1
        # total cost here will be
        # count of 0s
        step = step + zero;

    else:

        # If there are zeroes present
        # in the array
        if (zero > 0):

            # Change one zero to -1
            # and rest of them to 1
            # Total cost here will
            # be count of '0'
            step = step + zero;

        # If there are no zeros in the array
        else:

            # As no 0s are available so we
            # have to change one -1 to 1
            # which will cost 2 to
            # change -1 to 1
            step = step + 2;
    return step;

# Driver code
if __name__ == '__main__':
    a = [0, -2, -1, -3, 4];
    n = len(a);

    print(MinStep(a, n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the minimum
    // steps required
    static int MinStep(int[] a, int n)
    {

        // To store the count of 0s,
        // positive and negative numbers
        int positive = 0,
            negative = 0,
            zero = 0;

        // To store the ans
        int step = 0;

        for (int i = 0; i < n; i++) {

            // If array element is
            // equal to 0
            if (a[i] == 0) {
                zero++;
            }

            // If array element is
            // a negative number
            else if (a[i] < 0) {
                negative++;

                // Extra cost needed
                // to make it -1
                step = step + (-1 - a[i]);
            }

            // If array element is
            // a positive number
            else {
                positive++;

                // Extra cost needed
                // to make it 1
                step = step + (a[i] - 1);
            }
        }

        // Now the array will
        // have -1, 0 and 1 only
        if (negative % 2 == 0) {

            // As count of negative is even
            // so we will change all 0 to 1
            // total cost here will be
            // count of 0s
            step = step + zero;
        }
        else {

            // If there are zeroes present
            // in the array
            if (zero > 0) {

                // Change one zero to -1
                // and rest of them to 1
                // Total cost here will
                // be count of '0'
                step = step + zero;
            }

            // If there are no zeros in the array
            else {

                // As no 0s are available so we
                // have to change one -1 to 1
                // which will cost 2 to
                // change -1 to 1
                step = step + 2;
            }
        }

        return step;
    }

    // Driver code
    static public void Main()
    {
        int[] a = { 0, -2, -1, -3, 4 };
        int n = a.Length;

        Console.Write(MinStep(a, n));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum
// steps required
function MinStep(a, n)
{

    // To store the count of 0s, positive
    // and negative numbers
    let positive = 0,
        negative = 0,
        zero = 0;

    // To store the ans
    let step = 0;

    for (let i = 0; i < n; i++) {

        // If array element is
        // equal to 0
        if (a[i] == 0) {
            zero++;
        }

        // If array element is
        // a negative number
        else if (a[i] < 0) {
            negative++;

            // Extra cost needed
            // to make it -1
            step = step + (-1 - a[i]);
        }

        // If array element is
        // a positive number
        else {
            positive++;

            // Extra cost needed
            // to make it 1
            step = step + (a[i] - 1);
        }
    }

    // Now the array will
    // have -1, 0 and 1 only
    if (negative % 2 == 0) {

        // As count of negative is even
        // so we will change all 0 to 1
        // total cost here will be
        // count of 0s
        step = step + zero;
    }
    else {

        // If there are zeroes present
        // in the array
        if (zero > 0) {

            // Change one zero to -1
            // and rest of them to 1
            // Total cost here will
            // be count of '0'
            step = step + zero;
        }

        // If there are no zeros in the array
        else {

            // As no 0s are available so we
            // have to change one -1 to 1
            // which will cost 2 to
            // change -1 to 1
            step = step + 2;
        }
    }

    return step;
}

// Driver code
    let a = [ 0, -2, -1, -3, 4 ];
    let n = a.length;

    document.write(MinStep(a, n));

</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N)

？列表= PLM 68 oyaq FM 7q-SV 3ga 5 xbzgvkoq 0 xdrw