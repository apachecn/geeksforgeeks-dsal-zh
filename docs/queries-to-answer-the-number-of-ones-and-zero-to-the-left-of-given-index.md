# 查询给定索引左边的 1 和 0 的个数

> 原文:[https://www . geesforgeks . org/query-to-answer-number-of-one-and-to-zero-the-left-of-给定索引/](https://www.geeksforgeeks.org/queries-to-answer-the-number-of-ones-and-zero-to-the-left-of-given-index/)

给定一个**二进制**数组和 **Q** 查询。每个查询都由一个数字 **K** 组成，任务是打印索引 **K** 左边的 1 和 0 的数字。
**举例:**

> **输入:** arr[] = {1，1，1，0，0，1，0，1，1}，Q[] = {0，1，2，4}
> **输出:**
> 0 1 0 0 0
> 1 1 0 0
> 2 1 0 0
> 3 1 0
> **输入:** arr[] = {1，0，1，0，1，1}，Q[] = {2，3}

****方法:**可以按照以下步骤解决上述问题:** 

*   **声明一个对的数组(比如**left【】**)，它将用于预先计算左边的 1 和 0 的数量。**
*   **迭代数组，每一步用左边的 1 和 0 初始化左边的**【I】**。**
*   **每个查询的 1 的数量将是**左[k]。首先**和零的数量将是**左边的【k】。第二****

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to pre-calculate the left[] array
void preCalculate(int binary[], int n, pair<int, int> left[])
{
    int count1 = 0, count0 = 0;

    // Iterate in the binary array
    for (int i = 0; i < n; i++) {

        // Initialize the number
        // of 1 and 0
        left[i].first = count1;
        left[i].second = count0;

        // Increase the count
        if (binary[i])
            count1++;
        else
            count0++;
    }
}

// Driver code
int main()
{

    int binary[] = { 1, 1, 1, 0, 0, 1, 0, 1, 1 };
    int n = sizeof(binary) / sizeof(binary[0]);
    pair<int, int> left[n];
    preCalculate(binary, n, left);

    // Queries
    int queries[] = { 0, 1, 2, 4 };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Solve queries
    for (int i = 0; i < q; i++)
        cout << left[queries[i]].first << " ones "
             << left[queries[i]].second << " zeros\n";

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG {

    // pair class
    static class pair {
        int first, second;
        pair(int a, int b)
        {
            first = a;
            second = b;
        }
    }

    // Function to pre-calculate the left[] array
    static void preCalculate(int binary[], int n,
                             pair left[])
    {
        int count1 = 0, count0 = 0;

        // Iterate in the binary array
        for (int i = 0; i < n; i++) {

            // Initialize the number
            // of 1 and 0
            left[i].first = count1;
            left[i].second = count0;

            // Increase the count
            if (binary[i] != 0)
                count1++;
            else
                count0++;
        }
    }

    // Driver code
    public static void main(String args[])
    {

        int binary[] = { 1, 1, 1, 0, 0, 1, 0, 1, 1 };
        int n = binary.length;
        pair left[] = new pair[n];

        for (int i = 0; i < n; i++)
            left[i] = new pair(0, 0);

        preCalculate(binary, n, left);

        // Queries
        int queries[] = { 0, 1, 2, 4 };
        int q = queries.length;

        // Solve queries
        for (int i = 0; i < q; i++)
            System.out.println(left[queries[i]].first + " ones "
                               + left[queries[i]].second + " zeros\n");
    }
}

// This code is contributed by Arnab Kundu
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function to pre-calculate the left[] array
def preCalculate(binary, n, left):

    count1, count0 = 0, 0

    # Iterate in the binary array
    for i in range(n):

        # Initialize the number
        # of 1 and 0
        left[i][0] = count1
        left[i][1] = count0

        # Increase the count
        if (binary[i]):
            count1 += 1
        else:
            count0 += 1

# Driver code
binary = [1, 1, 1, 0, 0, 1, 0, 1, 1]

n = len(binary)

left = [[ 0 for i in range(2)]
            for i in range(n)]

preCalculate(binary, n, left)

queries = [0, 1, 2, 4 ]

q = len(queries)

# Solve queries
for i in range(q):
    print(left[queries[i]][0], "ones",
          left[queries[i]][1], "zeros")

# This code is contributed
# by mohit kumar
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG {

    // pair class
    public class pair {
        public int first, second;
        public pair(int a, int b)
        {
            first = a;
            second = b;
        }
    }

    // Function to pre-calculate the left[] array
    static void preCalculate(int[] binary, int n,
                             pair[] left)
    {
        int count1 = 0, count0 = 0;

        // Iterate in the binary array
        for (int i = 0; i < n; i++) {

            // Initialize the number
            // of 1 and 0
            left[i].first = count1;
            left[i].second = count0;

            // Increase the count
            if (binary[i] != 0)
                count1++;
            else
                count0++;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {

        int[] binary = { 1, 1, 1, 0, 0, 1, 0, 1, 1 };
        int n = binary.Length;
        pair[] left = new pair[n];

        for (int i = 0; i < n; i++)
            left[i] = new pair(0, 0);

        preCalculate(binary, n, left);

        // Queries
        int[] queries = { 0, 1, 2, 4 };
        int q = queries.Length;

        // Solve queries
        for (int i = 0; i < q; i++)
            Console.WriteLine(left[queries[i]].first + " ones "
                              + left[queries[i]].second + " zeros\n");
    }
}

// This code contributed by Rajput-Ji
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Function to pre-calculate the left[] array
function preCalculate($binary, $n)
{
    $left = array();
    $count1 = 0; $count0 = 0;

    // Iterate in the binary array
    for ($i = 0; $i < $n; $i++)
    {

        // Initialize the number
        // of 1 and 0
        $left[$i] = array($count1,
                          $count0);

        // Increase the count
        if ($binary[$i])
            $count1++;
        else
            $count0++;
    }
    return $left;
}

// Driver code
$binary = array( 1, 1, 1, 0, 0, 1, 0, 1, 1 );
$n = count($binary);

$left = preCalculate($binary, $n);

// Queries
$queries = array( 0, 1, 2, 4 );
$q = count($queries);

// Solve queries
for ($i = 0; $i < $q; $i++)
    echo $left[$queries[$i]][0], " ones ",
         $left[$queries[$i]][1], " zeros\n";

// This code is contributed by Ryuga
?>
```

## **java 描述语言**

```
<script>
// Javascript implementation of the approach

// Function to pre-calculate the left[] array   
function preCalculate(binary,n,left)
{
    let count1 = 0, count0 = 0;

        // Iterate in the binary array
        for (let i = 0; i < n; i++) {

            // Initialize the number
            // of 1 and 0
            left[i][0] = count1;
            left[i][1] = count0;

            // Increase the count
            if (binary[i] != 0)
                count1++;
            else
                count0++;
        }
}

// Driver code
let binary=[1, 1, 1, 0, 0, 1, 0, 1, 1];
let n = binary.length;

let left=new Array(n);

    for (let i = 0; i < n; i++)
            left[i] = [0, 0];

        preCalculate(binary, n, left);

        // Queries
        let queries = [ 0, 1, 2, 4 ];
        let q = queries.length;

        // Solve queries
        for (let i = 0; i < q; i++)
            document.write(left[queries[i]][0] + " ones "
                               + left[queries[i]][1] + " zeros<br>");

// This code is contributed by unknown2108
</script>
```

****Output:** 

```
0 ones 0 zeros
1 ones 0 zeros
2 ones 0 zeros
3 ones 1 zeros
```** 

****时间复杂度:** O(N)用于预计算，O(1)用于每个查询。**