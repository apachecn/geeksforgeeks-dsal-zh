# 生成最小和的数组，可以通过 P 步

删除

> 原文:[https://www . geesforgeks . org/generate-array-with-minimum-sum-哪些可以在 p-steps 中删除/](https://www.geeksforgeeks.org/generate-array-with-minimum-sum-which-can-be-deleted-in-p-steps/)

给定两个数字 **N** 和 **P** 。任务是生成一个包含所有正元素的数组，在一个操作中，您可以选择数组中的一个最小数量，并从所有数组元素中减去它。如果数组元素变为 0，那么您将移除它。
你必须打印该数组和一个可能数组的最小可能和，这样在精确应用 P 步后，该数组将消失。

**示例:**

> **输入:** N = 4，P = 2
> **输出:**
> 最小可能和为:5
> 数组元素为:1 2 1 1
> **说明:**
> 数组可以是【1，2，1，1】第一步后变成【0，1，0，0】变成【1】，第二步后消失。因此总和是 5，它是最小可能值。
> **输入** : N = 3，P = 1
> **输出** :
> 最小可能和为:3
> 数组元素为:1 1 1

**方法:**遵循贪婪的方法可以解决问题。首先，我们将首先放置 P 个自然数，对于其余(N–P)个位置，我们将用 1 填充它，因为我们必须最小化总和。
所以总和将是**P *(P+1)/2+(N–P)**。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required array
void findArray(int N, int P)
{
    // calculating minimum possible sum
    int ans = (P * (P + 1)) / 2 + (N - P);

    // Array
    int arr[N + 1];

    // place first P natural elements
    for (int i = 1; i <= P; i++)
        arr[i] = i;

    // Fill rest of the elements with 1
    for (int i = P + 1; i <= N; i++)
        arr[i] = 1;

    cout << "The Minimum Possible Sum is: " << ans << "\n";
    cout << "The Array Elements are: \n";

    for (int i = 1; i <= N; i++)
        cout << arr[i] << ' ';
}

// Driver Code
int main()
{
    int N = 5, P = 3;

    findArray(N, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find the required array
    static void findArray(int N, int P)
    {
        // calculating minimum possible sum
        int ans = (P * (P + 1)) / 2 + (N - P);

        // Array
        int arr[] = new int[N + 1];

        // place first P natural elements
        for (int i = 1; i <= P; i++)
        {
            arr[i] = i;
        }

        // Fill rest of the elements with 1
        for (int i = P + 1; i <= N; i++)
        {
            arr[i] = 1;
        }

        System.out.print("The Minimum Possible Sum is: " +
                                                ans + "\n");
        System.out.print("The Array Elements are: \n");

        for (int i = 1; i <= N; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5, P = 3;

        findArray(N, P);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find the required array
def findArray(N, P):

    # calculating minimum possible sum
    ans = (P * (P + 1)) // 2 + (N - P);

    # Array
    arr = [0] * (N + 1);

    # place first P natural elements
    for i in range(1, P + 1):
        arr[i] = i;

    # Fill rest of the elements with 1
    for i in range(P + 1, N + 1):
        arr[i] = 1;

    print("The Minimum Possible Sum is: ", ans);
    print("The Array Elements are: ");

    for i in range(1, N + 1):
        print(arr[i], end = " ");

# Driver Code
N = 5;
P = 3;
findArray(N, P);

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the required array
    static void findArray(int N, int P)
    {
        // calculating minimum possible sum
        int ans = (P * (P + 1)) / 2 + (N - P);

        // Array
        int []arr = new int[N + 1];

        // place first P natural elements
        for (int i = 1; i <= P; i++)
        {
            arr[i] = i;
        }

        // Fill rest of the elements with 1
        for (int i = P + 1; i <= N; i++)
        {
            arr[i] = 1;
        }

        Console.Write("The Minimum Possible Sum is: " +
                                                ans + "\n");
        Console.Write("The Array Elements are: \n");

        for (int i = 1; i <= N; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int N = 5, P = 3;

        findArray(N, P);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the required array
function findArray($N, $P)
{
    // calculating minimum possible sum
    $ans = ($P * ($P + 1)) / 2 + ($N - $P);

    // Array
    $arr[$N + 1] = array();

    // place first P natural elements
    for ($i = 1; $i <= $P; $i++)
        $arr[$i] = $i;

    // Fill rest of the elements with 1
    for ($i = $P + 1; $i <= $N; $i++)
        $arr[$i] = 1;

    echo "The Minimum Possible Sum is: ",
                              $ans, "\n";
    echo "The Array Elements are: \n";

    for ($i = 1; $i <= $N; $i++)
    echo $arr[$i], ' ';
}

// Driver Code
$N = 5;
$P = 3;
findArray($N, $P);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to find the required array
    function findArray(N, P)
    {
        // calculating minimum possible sum
        let ans = parseInt((P * (P + 1)) / 2, 10) + (N - P);

        // Array
        let arr = new Array(N + 1);

        // place first P natural elements
        for (let i = 1; i <= P; i++)
        {
            arr[i] = i;
        }

        // Fill rest of the elements with 1
        for (let i = P + 1; i <= N; i++)
        {
            arr[i] = 1;
        }

        document.write("The Minimum Possible Sum is: " +
                                                ans + "</br>");
        document.write("The Array Elements are: " + "</br>");

        for (let i = 1; i <= N; i++)
        {
            document.write(arr[i] + " ");
        }
    }

    let N = 5, P = 3;

      findArray(N, P);

</script>
```

**Output:** 

```
The Minimum Possible Sum is: 8
The Array Elements are: 
1 2 3 1 1
```

**时间复杂度:** O(N)