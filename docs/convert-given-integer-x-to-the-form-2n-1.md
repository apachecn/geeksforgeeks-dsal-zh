# 将给定整数 x 转换为 2^n-1 形式

> 原文:[https://www . geesforgeks . org/convert-给定整数-x-to-form-2n-1/](https://www.geeksforgeeks.org/convert-given-integer-x-to-the-form-2n-1/)

给定一个整数 **x** 。任务是通过在 **x** 上按指定顺序执行以下操作，将 **x** 转换为形式**2<sup>n</sup>–1**

1.  您可以选择任意非负整数 **n** 并更新**x = x xor(2<sup>n</sup>–1)**
2.  将 **x** 替换为 **x + 1** 。

第一个应用的操作必须是第一种类型，第二个是第二种类型，第三个也是第一种类型，依此类推。从形式上来说，如果我们按照操作执行的顺序对操作进行编号，那么奇数操作必须是第一种类型，偶数操作必须是第二种类型。任务是找到将 **x** 转换成**2<sup>n</sup>–1**形式所需的操作数。
**举例:**

> **输入:** x = 39
> **输出:** 4
> 运算 1: Pick n = 5，x 变换为(39 xor 31) = 56。
> 运算 2: x = 56 + 1 = 57
> 运算 3: Pick n = 3，x 转化为(57 异或 7) = 62。
> 操作 4: x = 62 + 1 = 63 即(2<sup>6</sup>–1)。
> 所以，操作总数为 4。
> **输入:** x = 7
> **输出:** 0
> As 2 <sup>3</sup> -1 = 7。
> 所以，不需要手术。

**方式:**取大于 **x** 的最小数，形式为**2<sup>n</sup>–1**表示**数**，然后更新 **x = x xor 数**，然后 **x = x + 1** 进行两次运算。重复该步骤，直到 **x** 形成**2<sup>n</sup>–1**。打印最后执行的操作数。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 24;

// Function to return the count
// of operations required
int countOp(int x)
{

    // To store the powers of 2
    int arr[MAX];
    arr[0] = 1;
    for (int i = 1; i < MAX; i++)
        arr[i] = arr[i - 1] * 2;

    // Temporary variable to store x
    int temp = x;

    bool flag = true;

    // To store the index of
    // smaller number larger than x
    int ans;

    // To store the count of operations
    int operations = 0;

    bool flag2 = false;

    for (int i = 0; i < MAX; i++) {

        if (arr[i] - 1 == x)
            flag2 = true;

        // Stores the index of number
        // in the form of 2^n - 1
        if (arr[i] > x) {
            ans = i;
            break;
        }
    }

    // If x is already in the form
    // 2^n - 1 then no operation is required
    if (flag2)
        return 0;

    while (flag) {

        // If number is less than x increase the index
        if (arr[ans] < x)
            ans++;

        operations++;

        // Calculate all the values (x xor 2^n-1)
        // for all possible n
        for (int i = 0; i < MAX; i++) {
            int take = x ^ (arr[i] - 1);
            if (take <= arr[ans] - 1) {

                // Only take value which is
                // closer to the number
                if (take > temp)
                    temp = take;
            }
        }

        // If number is in the form of 2^n - 1 then break
        if (temp == arr[ans] - 1) {
            flag = false;
            break;
        }

        temp++;
        operations++;
        x = temp;

        if (x == arr[ans] - 1)
            flag = false;
    }

    // Return the count of operations
    // required to obtain the number
    return operations;
}

// Driver code
int main()
{
    int x = 39;

    cout << countOp(x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int MAX = 24;

// Function to return the count
// of operations required
static int countOp(int x)
{

    // To store the powers of 2
    int arr[] = new int[MAX];
    arr[0] = 1;
    for (int i = 1; i < MAX; i++)
        arr[i] = arr[i - 1] * 2;

    // Temporary variable to store x
    int temp = x;

    boolean flag = true;

    // To store the index of
    // smaller number larger than x
    int ans =0;

    // To store the count of operations
    int operations = 0;

    boolean flag2 = false;

    for (int i = 0; i < MAX; i++)
    {

        if (arr[i] - 1 == x)
            flag2 = true;

        // Stores the index of number
        // in the form of 2^n - 1
        if (arr[i] > x)
        {
            ans = i;
            break;
        }
    }

    // If x is already in the form
    // 2^n - 1 then no operation is required
    if (flag2)
        return 0;

    while (flag)
    {

        // If number is less than x increase the index
        if (arr[ans] < x)
            ans++;

        operations++;

        // Calculate all the values (x xor 2^n-1)
        // for all possible n
        for (int i = 0; i < MAX; i++)
        {
            int take = x ^ (arr[i] - 1);
            if (take <= arr[ans] - 1)
            {

                // Only take value which is
                // closer to the number
                if (take > temp)
                    temp = take;
            }
        }

        // If number is in the form of 2^n - 1 then break
        if (temp == arr[ans] - 1)
        {
            flag = false;
            break;
        }

        temp++;
        operations++;
        x = temp;

        if (x == arr[ans] - 1)
            flag = false;
    }

    // Return the count of operations
    // required to obtain the number
    return operations;
}

    // Driver code
    public static void main (String[] args)
    {
        int x = 39;
        System.out.println(countOp(x));
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 24;

# Function to return the count
# of operations required
def countOp(x) :

    # To store the powers of 2
    arr = [0]*MAX ;
    arr[0] = 1;
    for i in range(1, MAX) :
        arr[i] = arr[i - 1] * 2;

    # Temporary variable to store x
    temp = x;

    flag = True;

    # To store the index of
    # smaller number larger than x
    ans = 0;

    # To store the count of operations
    operations = 0;

    flag2 = False;

    for i in range(MAX) :

        if (arr[i] - 1 == x) :
            flag2 = True;

        # Stores the index of number
        # in the form of 2^n - 1
        if (arr[i] > x) :
            ans = i;
            break;

    # If x is already in the form
    # 2^n - 1 then no operation is required
    if (flag2) :
        return 0;

    while (flag) :

        # If number is less than x increase the index
        if (arr[ans] < x) :
            ans += 1;

        operations += 1;

        # Calculate all the values (x xor 2^n-1)
        # for all possible n
        for i in range(MAX) :
            take = x ^ (arr[i] - 1);

            if (take <= arr[ans] - 1) :

                # Only take value which is
                # closer to the number
                if (take > temp) :
                    temp = take;

        # If number is in the form of 2^n - 1 then break
        if (temp == arr[ans] - 1) :
            flag = False;
            break;

        temp += 1;
        operations += 1;
        x = temp;

        if (x == arr[ans] - 1) :
            flag = False;

    # Return the count of operations
    # required to obtain the number
    return operations;

# Driver code
if __name__ == "__main__" :

    x = 39;

    print(countOp(x));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 24;

// Function to return the count
// of operations required
static int countOp(int x)
{

    // To store the powers of 2
    int []arr = new int[MAX];
    arr[0] = 1;
    for (int i = 1; i < MAX; i++)
        arr[i] = arr[i - 1] * 2;

    // Temporary variable to store x
    int temp = x;

    bool flag = true;

    // To store the index of
    // smaller number larger than x
    int ans = 0;

    // To store the count of operations
    int operations = 0;

    bool flag2 = false;

    for (int i = 0; i < MAX; i++)
    {

        if (arr[i] - 1 == x)
            flag2 = true;

        // Stores the index of number
        // in the form of 2^n - 1
        if (arr[i] > x)
        {
            ans = i;
            break;
        }
    }

    // If x is already in the form
    // 2^n - 1 then no operation is required
    if (flag2)
        return 0;

    while (flag)
    {

        // If number is less than x increase the index
        if (arr[ans] < x)
            ans++;

        operations++;

        // Calculate all the values (x xor 2^n-1)
        // for all possible n
        for (int i = 0; i < MAX; i++)
        {
            int take = x ^ (arr[i] - 1);
            if (take <= arr[ans] - 1)
            {

                // Only take value which is
                // closer to the number
                if (take > temp)
                    temp = take;
            }
        }

        // If number is in the form of 2^n - 1 then break
        if (temp == arr[ans] - 1)
        {
            flag = false;
            break;
        }

        temp++;
        operations++;
        x = temp;

        if (x == arr[ans] - 1)
            flag = false;
    }

    // Return the count of operations
    // required to obtain the number
    return operations;
}

// Driver code
static public void Main ()
{

    int x = 39;
    Console.WriteLine(countOp(x));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation
// of the approach

const MAX = 24;

// Function to return the count
// of operations required
function countOp(x)
{

    // To store the powers of 2
    let arr = new Array(MAX);
    arr[0] = 1;
    for (let i = 1; i < MAX; i++)
        arr[i] = arr[i - 1] * 2;

    // Temporary variable to store x
    let temp = x;

    let flag = true;

    // To store the index of
    // smaller number larger than x
    let ans;

    // To store the count of operations
    let operations = 0;

    let flag2 = false;

    for (let i = 0; i < MAX; i++) {

        if (arr[i] - 1 == x)
            flag2 = true;

        // Stores the index of number
        // in the form of 2^n - 1
        if (arr[i] > x) {
            ans = i;
            break;
        }
    }

    // If x is already in the form
    // 2^n - 1 then no operation is
    // required
    if (flag2)
        return 0;

    while (flag) {

        // If number is less than x
        // increase the index
        if (arr[ans] < x)
            ans++;

        operations++;

        // Calculate all the values
        // (x xor 2^n-1)
        // for all possible n
        for (let i = 0; i < MAX; i++) {
            let take = x ^ (arr[i] - 1);
            if (take <= arr[ans] - 1) {

                // Only take value which is
                // closer to the number
                if (take > temp)
                    temp = take;
            }
        }

        // If number is in the form of
        // 2^n - 1 then break
        if (temp == arr[ans] - 1) {
            flag = false;
            break;
        }

        temp++;
        operations++;
        x = temp;

        if (x == arr[ans] - 1)
            flag = false;
    }

    // Return the count of operations
    // required to obtain the number
    return operations;
}

// Driver code
    let x = 39;

    document.write(countOp(x));

</script>
```

**Output:** 

```
4
```