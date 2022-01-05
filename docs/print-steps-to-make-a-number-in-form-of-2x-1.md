# 以 2^x-1

的形式打印制作数字的步骤

> 原文:[https://www . geesforgeks . org/print-steps-to-make-a-number-in-form-2x-1/](https://www.geeksforgeeks.org/print-steps-to-make-a-number-in-form-of-2x-1/)

给定一个数字 **N** ，需要执行两个步骤。

1.  奇数步，将数字与任意 **2^M-1** 异或，其中 **M** 由你选择。
2.  偶数步，增加 **1** 号。

继续执行这些步骤，直到 n 变成 **2^X-1** (其中 x 可以是任意整数)。任务是打印所有步骤。
**例:**

> **输入:** 39
> **输出:**
> 第 1 步:与 31
> 异或第 2 步:增加 1
> 第 3 步:与 7
> 异或第 4 步:增加 1
> Pick M = 5，n 转化为 39 ^ 31 = 56。
> 增加 N 1，将其值改为 N = 57。
> Pick M = 3，x 转化为 57 ^ 7 = 62。
> 将 x 增加 1，将其值更改为 63 = 2^6–1。
> **输入:** 7
> **输出:**不需要步骤。

**接近**:可以按照以下步骤解决上述问题:

*   在每一个奇数步，找到数字中最左边的未设置位(比如 1 索引中的位置 x)，并与 2^x-1.进行异或运算
*   在每一个偶数步，将数字增加 1。
*   如果在任何一步，该数字没有未设置的位，则返回。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the leftmost
// unset bit in a number.
int find_leftmost_unsetbit(int n)
{
    int ind = -1;
    int i = 1;
    while (n) {
        if (!(n & 1))
            ind = i;

        i++;
        n >>= 1;
    }
    return ind;
}

// Function that perform
// the step
void perform_steps(int n)
{

    // Find the leftmost unset bit
    int left = find_leftmost_unsetbit(n);

    // If the number has no bit
    // unset, it means it is in form 2^x -1
    if (left == -1) {
        cout << "No steps required";
        return;
    }

    // Count the steps
    int step = 1;

    // Iterate till number is of form 2^x - 1
    while (find_leftmost_unsetbit(n) != -1) {

        // At even step increase by 1
        if (step % 2 == 0) {
            n += 1;
            cout << "Step" << step << ": Increase by 1\n";
        }

        // Odd step xor with any 2^m-1
        else {

            // Find the leftmost unset bit
            int m = find_leftmost_unsetbit(n);

            // 2^m-1
            int num = pow(2, m) - 1;

            // Perform the step
            n = n ^ num;

            cout << "Step" << step
                 << ": Xor with " << num << endl;
        }

        // Increase the steps
        step += 1;
    }
}

// Driver code
int main()
{
    int n = 39;
    perform_steps(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

class GFG
{

    // Function to find the leftmost
    // unset bit in a number.
    static int find_leftmost_unsetbit(int n)
    {
        int ind = -1;
        int i = 1;
        while (n > 0)
        {
            if ((n % 2) != 1)
            {
                ind = i;
            }

            i++;
            n >>= 1;
        }
        return ind;
    }

    // Function that perform
    // the step
    static void perform_steps(int n)
    {

        // Find the leftmost unset bit
        int left = find_leftmost_unsetbit(n);

        // If the number has no bit
        // unset, it means it is in form 2^x -1
        if (left == -1)
        {
            System.out.print("No steps required");
            return;
        }

        // Count the steps
        int step = 1;

        // Iterate till number is of form 2^x - 1
        while (find_leftmost_unsetbit(n) != -1)
        {

            // At even step increase by 1
            if (step % 2 == 0)
            {
                n += 1;
                System.out.println("Step" + step + ": Increase by 1");
            }

            // Odd step xor with any 2^m-1
            else
            {

                // Find the leftmost unset bit
                int m = find_leftmost_unsetbit(n);

                // 2^m-1
                int num = (int) (Math.pow(2, m) - 1);

                // Perform the step
                n = n ^ num;

                System.out.println("Step" + step
                        + ": Xor with " + num);
            }

            // Increase the steps
            step += 1;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 39;
        perform_steps(n);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the leftmost
# unset bit in a number.
def find_leftmost_unsetbit(n):
    ind = -1;
    i = 1;
    while (n):
        if ((n % 2) != 1):
            ind = i;

        i += 1;
        n >>= 1;
    return ind;

# Function that perform
# the step
def perform_steps(n):

    # Find the leftmost unset bit
    left = find_leftmost_unsetbit(n);

    # If the number has no bit
    # unset, it means it is in form 2^x -1
    if (left == -1):
        print("No steps required");
        return;

    # Count the steps
    step = 1;

    # Iterate till number is of form 2^x - 1
    while (find_leftmost_unsetbit(n) != -1):

        # At even step increase by 1
        if (step % 2 == 0):
            n += 1;
            print("Step" , step ,
                  ": Increase by 1\n");

        # Odd step xor with any 2^m-1
        else:

            # Find the leftmost unset bit
            m = find_leftmost_unsetbit(n);

            # 2^m-1
            num = (2**m) - 1;

            # Perform the step
            n = n ^ num;

            print("Step" , step,
                  ": Xor with" , num );

        # Increase the steps
        step += 1;

# Driver code
n = 39;
perform_steps(n);

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

    // Function to find the leftmost
    // unset bit in a number.
    static int find_leftmost_unsetbit(int n)
    {
        int ind = -1;
        int i = 1;
        while (n > 0)
        {
            if ((n % 2) != 1)
            {
                ind = i;
            }

            i++;
            n >>= 1;
        }
        return ind;
    }

    // Function that perform
    // the step
    static void perform_steps(int n)
    {

        // Find the leftmost unset bit
        int left = find_leftmost_unsetbit(n);

        // If the number has no bit
        // unset, it means it is in form 2^x -1
        if (left == -1)
        {
            Console.Write("No steps required");
            return;
        }

        // Count the steps
        int step = 1;

        // Iterate till number is of form 2^x - 1
        while (find_leftmost_unsetbit(n) != -1)
        {

            // At even step increase by 1
            if (step % 2 == 0)
            {
                n += 1;
                Console.WriteLine("Step" + step + ": Increase by 1");
            }

            // Odd step xor with any 2^m-1
            else
            {

                // Find the leftmost unset bit
                int m = find_leftmost_unsetbit(n);

                // 2^m-1
                int num = (int) (Math.Pow(2, m) - 1);

                // Perform the step
                n = n ^ num;

                Console.WriteLine("Step" + step
                        + ": Xor with " + num);
            }

            // Increase the steps
            step += 1;
        }
    }

    // Driver code
    static public void Main ()
    {
        int n = 39;
        perform_steps(n);
    }
}

// This code contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to implement
// the above approach

// Function to find the leftmost
// unset bit in a number.
function find_leftmost_unsetbit($n)
{
    $ind = -1;
    $i = 1;
    while ($n)
    {
        if (!($n & 1))
            $ind = $i;

        $i++;
        $n >>= 1;
    }
    return $ind;
}

// Function that perform
// the step
function perform_steps($n)
{

    // Find the leftmost unset bit
    $left = find_leftmost_unsetbit($n);

    // If the number has no bit
    // unset, it means it is in form 2^x -1
    if ($left == -1)
    {
        echo "No steps required";
        return;
    }

    // Count the steps
    $step = 1;

    // Iterate till number is of form 2^x - 1
    while (find_leftmost_unsetbit($n) != -1)
    {

        // At even step increase by 1
        if ($step % 2 == 0)
        {
            $n += 1;
            echo "Step",$step, ": Increase by 1\n";
        }

        // Odd step xor with any 2^m-1
        else
        {

            // Find the leftmost unset bit
            $m = find_leftmost_unsetbit($n);

            // 2^m-1
            $num = pow(2, $m) - 1;

            // Perform the step
            $n = $n ^ $num;

            echo "Step",$step ,": Xor with ", $num ,"\n";
        }

        // Increase the steps
        $step += 1;
    }
}

    // Driver code
    $n = 39;
    perform_steps($n);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the leftmost
// unset bit in a number.
function find_leftmost_unsetbit(n)
{
    let ind = -1;
    let i = 1;
    while (n) {
        if (!(n & 1))
            ind = i;

        i++;
        n >>= 1;
    }
    return ind;
}

// Function that perform
// the step
function perform_steps(n)
{

    // Find the leftmost unset bit
    let left = find_leftmost_unsetbit(n);

    // If the number has no bit
    // unset, it means it is in form 2^x -1
    if (left == -1) {
        document.write("No steps required");
        return;
    }

    // Count the steps
    let step = 1;

    // Iterate till number is of form 2^x - 1
    while (find_leftmost_unsetbit(n) != -1) {

        // At even step increase by 1
        if (step % 2 == 0) {
            n += 1;
            document.write(
            "Step" + step + ": Increase by 1<br>"
            );
        }

        // Odd step xor with any 2^m-1
        else {

            // Find the leftmost unset bit
            let m = find_leftmost_unsetbit(n);

            // 2^m-1
            let num = Math.pow(2, m) - 1;

            // Perform the step
            n = n ^ num;

            document.write("Step" + step
                 + ": Xor with " + num + "<br>");
        }

        // Increase the steps
        step += 1;
    }
}

// Driver code
    let n = 39;
    perform_steps(n);

</script>
```

**Output:** 

```
Step1: Xor with 31
Step2: Increase by 1
Step3: Xor with 7
Step4: Increase by 1
```