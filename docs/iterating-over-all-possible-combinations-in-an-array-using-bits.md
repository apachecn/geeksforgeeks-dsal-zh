# 使用位迭代数组中所有可能的组合

> 原文:[https://www . geeksforgeeks . org/iterating-over-all-over-over-over-over-over-over-over-over-over-over-over-over-over-over-over-over-over-over-over-over-over-](https://www.geeksforgeeks.org/iterating-over-all-possible-combinations-in-an-array-using-bits/)

在解决一个问题时会出现几种情况，我们需要迭代一个数组的所有可能组合。在本文中，我们将讨论使用位来实现这一点的方法。
为了解释，考虑以下问题:

> 给定数组 b[] = {2，1，4}。任务是检查这个数组中是否存在元素总和等于 k = 6 的元素组合。

**使用位操作的解决方案** :
由于这个数组中有 3 个元素，因此我们需要 3 位来表示每个数字。对应于该元素的位设置为 1 意味着在计算总和时包含该元素，如果该元素为 0，则不包含该元素。
可能的组合有:

```
000 : No element is selected.
001 : 4 is selected.
010 : 1 is selected.
011 : 1 and 4 are selected.
100 : 2 is selected.
101 : 2 and 4 are selected.
110 : 2 and 1 are selected.
111 : All elements are selected.
```

因此，访问所有这些位所需的范围是 0–7。我们迭代每个可能组合的每个位，并检查每个组合所选元素的总和是否等于所需的总和。

**示例:**

```
Input : A = {3, 4, 1, 2} and k = 6 
Output : YES
Here, the combination of using 3, 1 and 2 yields 
the required sum.

Input : A = {3, 4, 1, 2} and k = 11
Output : NO
```

下面是上述方法的实现:

## C++

```
// C++ program to iterate over all possible
// combinations of array elements

#include <bits/stdc++.h>
using namespace std;

// Function to check if any combination of
// elements of the array sums to k
bool checkSum(int a[], int n, int k)
{
    // Flag variable to check if
    // sum exists
    int flag = 0;

    // Calculate number of bits
    int range = (1 << n) - 1;

    // Generate combinations using bits
    for (int i = 0; i <= range; i++) {

        int x = 0, y = i, sum = 0;

        while (y > 0) {

            if (y & 1 == 1) {

                // Calculate sum
                sum = sum + a[x];
            }
            x++;
            y = y >> 1;
        }

        // If sum is found, set flag to 1
        // and terminate the loop
        if (sum == k)
           return true;
    }

    return false;
}

// Driver Code
int main()
{
    int k = 6;
    int a[] = { 3, 4, 1, 2 };
    int n = sizeof(a)/sizeof(a[0]);
    if (checkSum(a, n, k))
       cout << "Yes";
    else
       cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to iterate over all possible
// combinations of array elements
class GFG
{

// Function to check if any combination
// of elements of the array sums to k
static boolean checkSum(int a[], int n, int k)
{
    // Flag variable to check if
    // sum exists
    int flag = 0;

    // Calculate number of bits
    int range = (1 << n) - 1;

    // Generate combinations using bits
    for (int i = 0; i <= range; i++)
    {
        int x = 0, y = i, sum = 0;

        while (y > 0)
        {
            if ((y & 1) == 1)
            {

                // Calculate sum
                sum = sum + a[x];
            }
            x++;
            y = y >> 1;
        }

        // If sum is found, set flag to 1
        // and terminate the loop
        if (sum == k)
        return true;
    }

    return false;
}

// Driver Code
public static void main(String[] args)
{
    int k = 6;
    int a[] = { 3, 4, 1, 2 };
    int n = a.length;
    if (checkSum(a, n, k))
    System.out.println("Yes");
    else
    System.out.println("No");

}
}

// This code is contributed
// by Code_Mech
```

## 蟒蛇 3

```
# Python 3 program to iterate over all
# possible combinations of array elements

# Function to check if any combination of
# elements of the array sums to k
def checkSum(a, n, k):

    # Flag variable to check if
    # sum exists
    flag = 0

    # Calculate number of bits
    range__ = (1 << n) - 1

    # Generate combinations using bits
    for i in range(range__ + 1):
        x = 0
        y = i
        sum = 0

        while (y > 0):
            if (y & 1 == 1):

                # Calculate sum
                sum = sum + a[x]

            x += 1
            y = y >> 1

        # If sum is found, set flag to 1
        # and terminate the loop
        if (sum == k):
            return True

    return False

# Driver Code
if __name__ == '__main__':
    k = 6
    a = [3, 4, 1, 2]
    n = len(a)
    if (checkSum(a, n, k)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to iterate over all possible
// combinations of array elements
using System;
class GFG
{
// Function to check if any combination
// of elements of the array sums to k
static bool checkSum(int[] a, int n, int k)
{
    // Flag variable to check if
    // sum exists
    int // C# program to iterate over all possible
// combinations of array elements
using System;

class GFG
{

// Function to check if any combination
// of elements of the array sums to k
static bool checkSum(int[] a, int n, int k)
{
    // Flag variable to check if
    // sum exists
    int flag = 0;

    // Calculate number of bits
    int range = (1 << n) - 1;

    // Generate combinations using bits
    for (int i = 0; i <= range; i++)
    {
        int x = 0, y = i, sum = 0;

        while (y > 0)
        {
            if ((y & 1) == 1)
            {

                // Calculate sum
                sum = sum + a[x];
            }
            x++;
            y = y >> 1;
        }

        // If sum is found, set flag to 1
        // and terminate the loop
        if (sum == k)
        return true;
    }

    return false;
}

// Driver Code
public static void Main()
{
    int k = 6;
    int[] a = { 3, 4, 1, 2 };
    int n = a.Length;
    if (checkSum(a, n, k))
    Console.WriteLine("Yes");
    else
    Console.WriteLine("No");
}
}

// This code is contributed
// by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to iterate over all possible
// combinations of array elements

// Function to check if any combination of
// elements of the array sums to k
function checkSum($a, $n, $k)
{
    // Flag variable to check if
    // sum exists
    $flag = 0;

    // Calculate number of bits
    $range = (1 << $n) - 1;

    // Generate combinations using bits
    for ($i = 0; $i <= $range; $i++)
    {

        $x = 0;
        $y = $i;
        $sum = 0;

        while ($y > 0)
        {

            if ($y & 1 == 1)
            {

                // Calculate sum
                $sum = $sum + $a[$x];
            }
            $x++;
            $y = $y >> 1;
        }

        // If sum is found, set flag to 1
        // and terminate the loop
        if ($sum == $k)
        return true;
    }

    return false;
}

    // Driver Code
    $k = 6;
    $a = array( 3, 4, 1, 2 );
    $n = sizeof($a);
    if (checkSum($a, $n, $k))
        echo "Yes";
    else
        echo "No";

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript program to iterate over all possible
    // combinations of array elements

    // Function to check if any combination
    // of elements of the array sums to k
    function checkSum(a, n, k)
    {
        // Flag variable to check if
        // sum exists
        let flag = 0;

        // Calculate number of bits
        let range = (1 << n) - 1;

        // Generate combinations using bits
        for (let i = 0; i <= range; i++)
        {
            let x = 0, y = i, sum = 0;

            while (y > 0)
            {
                if ((y & 1) == 1)
                {

                    // Calculate sum
                    sum = sum + a[x];
                }
                x++;
                y = y >> 1;
            }

            // If sum is found, set flag to 1
            // and terminate the loop
            if (sum == k)
            return true;
        }

        return false;
    }

    let k = 6;
    let a = [ 3, 4, 1, 2 ];
    let n = a.length;
    if (checkSum(a, n, k))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度** : 2 <sup>(位数)</sup>T4】