# 通过移除最大值及其右侧来清空数组的步骤

> 原文:[https://www . geesforgeks . org/steps-make-array-empty-remove-maximum-right-side/](https://www.geeksforgeeks.org/steps-make-array-empty-removing-maximum-right-side/)

给我们一个整数数组。我们必须对阵列执行以下操作，直到它完全耗尽。

*   选择数组中的最大数字，并删除该数字，包括数组中其右侧的所有数字。
*   对数组的左边元素重复步骤 1，即选择左边元素中的最大元素，并删除它，包括它右边的所有数字。

我们的任务是模拟上述过程，并返回将采取的步骤数，直到数组的第一个元素(索引 0)也被删除，并且数组被认为已用尽。
示例:

```
Input : Array = [2, 3, 5, 4, 1]
Output : Steps Taken: 3
Explanation: Step 1: Remove 5 and elements to its right
             so, Array becomes [2, 3]
             Step 2: Remove 3 as it is the maximum and 
             right most already so, Array becomes [2]
             Step 3: Remove 2 and the array becomes EMPTY
             Hence, at the end of step 3 the array stands 
             exhausted.

Input : Array = [2, 5, 8, 24, 4, 11, 6, 1, 15, 10]
Output : Steps Taken: 4
Explanation: Step 1: Remove 24 and elements to its right
             so, Array becomes [2, 5, 8]
             Step 2: Remove 8 and elements to its right
             so, Array becomes [2, 5]
             Step 3: Remove 5 and elements to its right
             so, Array becomes [2]
             Step 4: Remove 2 and the array becomes EMPTY
             Hence, at the end of step 4 the array stands 
             exhausted.
```

**天真方法:**
解决这个问题的一个简单方法是找到数组中的最大值并存储其索引，然后再次找到数组中范围 0 和之前存储的索引之间的最大值。重复此过程，直到删除第 0 个索引元素。

## C++

```
// C++ program to simulate max deletion
// and calculate number of steps.
#include <bits/stdc++.h>
using namespace std;

// Function to find index of the maximum number
// in the array of size n
int findMax(int arr[], int n)
{
    int max = 0, index = 0;
    for (int i = 0; i < n; i++)

        // Condition to get the maximum
        if (arr[i] > max) {
            max = arr[i];
            index = i;
        }

    // return the index of the maximum element
    return index;
}

int countSteps(int arr[], int n)
{
    // Find the index of largest number in the array
    int index = findMax(arr, n);

    //'steps' variable calculates the number of
    // steps being taken.
    int steps = 1;

    // Check until the first element of array is removed,
    // hence until index!=0
    while (index != 0) {

        // Update index with the index value of highest
        // element in the remaining array.
        index = findMax(arr, index);
        steps++;
    }

    return steps;
}

// Driver Code
int main()
{
    int arr[] = { 2, 5, 8, 24, 4, 11, 6, 1, 15, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Steps Taken: ";
    cout << countSteps(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to simulate max deletion
// and calculate number of steps.
import java.util.*;

class GFG {

    // Function to find index of the maximum
    // number in the array of size n
    static int findMax(int arr[], int n)
    {
        int max = 0, index = 0;
        for (int i = 0; i < n; i++)

            // Condition to get the maximum
            if (arr[i] > max) {
                max = arr[i];
                index = i;
            }

        // return the index of the maximum
        // element
        return index;
    }

    static int countSteps(int arr[], int n)
    {
        // Find the index of largest number
        // in the array
        int index = findMax(arr, n);

        //'steps' variable calculates the
        // number of steps being taken.
        int steps = 1;

        // Check until the first element
        // of array is removed, hence
        // until index!=0
        while (index != 0) {

            // Update index with the index
            // value of highest element in
            // the remaining array.
            index = findMax(arr, index);
            steps++;
        }

        return steps;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 2, 5, 8, 24, 4, 11,
                      6, 1, 15, 10 };
        int n = arr.length;

        System.out.print("Steps Taken: ");
        System.out.println(countSteps(arr, n));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python program to simulate max deletion
# and calculate number of steps.

# Function to find index of the maximum number
# in the array of size n
def findMax(arr, n):
    large, index = 0, 0

    for i in range(n):

        # Condition to get the maximum
        if arr[i] > large:
            large = arr[i]
            index = i

    # return the index of the maximum element
    return index

def countSteps(arr, n):

    # Find the index of largest number in the array
    index = findMax(arr, n)

    #'steps' variable calculates the number of
    # steps being taken.
    steps = 1

    # Check until the first element of array is removed,
    # hence until index != 0
    while index != 0:

        # Update index with the index value of highest
        # element in the remaining array.
        index = findMax(arr, index)
        steps += 1

    return steps

# Driver Code
if __name__ == "__main__":
    arr = [2, 5, 8, 24, 4, 11, 6, 1, 15, 10]
    n = len(arr)
    print("Steps Taken:", countSteps(arr, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to simulate max
// deletion and calculate
// number of steps.
using System;

class GFG {

    // Function to find index
    // of the maximum number
    // in the array of size n
    static int findMax(int[] arr, int n)
    {
        int max = 0, index = 0;
        for (int i = 0; i < n; i++)

            // Condition to get
            // the maximum
            if (arr[i] > max)
            {
                max = arr[i];
                index = i;
            }

        // return the index of the
        // maximum element
        return index;
    }

    static int countSteps(int[] arr,
                                int n)
    {
        // Find the index of largest
        // number in the array
        int index = findMax(arr, n);

        //'steps' variable calculates
        // the number of steps being
        // taken.
        int steps = 1;

        // Check until the first
        // element of array is
        // removed, hence until
        // index!=0
        while (index != 0) {

            // Update index with
            // the index value of
            // highest element in
            // the remaining array.
            index = findMax(arr, index);
            steps++;
        }

        return steps;
    }

    /* Driver program to test
    above function */
    public static void Main()
    {
        int[] arr = { 2, 5, 8, 24, 4,
                  11, 6, 1, 15, 10 };
        int n = arr.Length;

        Console.Write("Steps Taken: ");

        Console.WriteLine(
                  countSteps(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to simulate max deletion
// and calculate number of steps.

// Function to find index of the maximum
// number in the array of size n
function findMax($arr, $n)
{
    $max = 0; $index = 0;
    for ( $i = 0; $i < $n; $i++)

        // Condition to get the maximum
        if ($arr[$i] > $max)
        {
            $max = $arr[$i];
            $index = $i;
        }

    // return the index of
    // the maximum element
    return $index;
}

function countSteps($arr, $n)
{
    // Find the index of largest
    // number in the array
    $index = findMax($arr, $n);

    //'steps' variable calculates
    // the number of steps being taken.
    $steps = 1;

    // Check until the first
    // element of array is removed,
    // hence until index!=0
    while ($index != 0)
    {

        // Update index with the
        // index value of highest
        // element in the remaining array.
        $index = findMax($arr, $index);
        $steps++;
    }

    return $steps;
}

    // Driver Code
    $arr = array(2, 5, 8, 24, 4,
              11, 6, 1, 15, 10);
    $n = sizeof($arr);
    echo "Steps Taken: ";
    echo countSteps($arr, $n) ,"\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to simulate max
    // deletion and calculate
    // number of steps.

    // Function to find index
    // of the maximum number
    // in the array of size n
    function findMax(arr, n)
    {
        let max = 0, index = 0;
        for (let i = 0; i < n; i++)

            // Condition to get
            // the maximum
            if (arr[i] > max)
            {
                max = arr[i];
                index = i;
            }

        // return the index of the
        // maximum element
        return index;
    }

    function countSteps(arr, n)
    {
        // Find the index of largest
        // number in the array
        let index = findMax(arr, n);

        //'steps' variable calculates
        // the number of steps being
        // taken.
        let steps = 1;

        // Check until the first
        // element of array is
        // removed, hence until
        // index!=0
        while (index != 0) {

            // Update index with
            // the index value of
            // highest element in
            // the remaining array.
            index = findMax(arr, index);
            steps++;
        }

        return steps;
    }

    let arr = [ 2, 5, 8, 24, 4, 11, 6, 1, 15, 10 ];
    let n = arr.length;

    document.write("Steps Taken: ");

    document.write(countSteps(arr, n));

</script>
```

**输出:**

```
Steps Taken: 4
```

这种方法的时间复杂度是 **O(n^2)** 。
**有效方法:**
有效方法是将 max 初始化为-1，并在计算数组中的 max 时计算交换条件执行的次数，即该条件:

## 卡片打印处理机（Card Print Processor 的缩写）

```
if (max < arr[i]) {

    // keep a count of number of times this
    // condition executes.
    max = arr[i];
}
```

每次交换发生时，保证数组中先前的数字小于当前元素。这给了我们给定整数集将发生的确切步数。

## C++

```
// C++ program to simulate max deletion
// and calculate number of steps.
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number in the
// array upto index n and return its index.
int countSteps(int arr[], int n)
{
    int max = -1, steps = 0;
    for (int i = 0; i < n; i++) {

        // condition to find max
        if (arr[i] > max) {

            max = arr[i];

            // Count the number of times this
            // condition executes that will the
            // number of turns being played.
            steps++;
        }
    }

    // return the number of turns played
    return steps;
}

// Driver Code
int main()
{
    int arr[] = { 2, 5, 8, 24, 4, 11, 6, 1, 15, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    //'steps' variable calculates the number of
    // steps being taken.
    cout << "Steps Taken: ";
    cout << countSteps(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to simulate max deletion
// and calculate number of steps.
import java.util.*;

class GFG {

    // Function to find the maximum number in the
    // array upto index n and return its index.
    static int countSteps(int arr[], int n)
    {
        int max = -1, steps = 0;
        for (int i = 0; i < n; i++) {

            // condition to find max
            if (arr[i] > max) {

                max = arr[i];

                // Count the number of times this
                // condition executes that will the
                // number of turns being played.
                steps++;
            }
        }

        // return the number of turns played
        return steps;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 2, 5, 8, 24, 4, 11, 6,
                      1, 15, 10 };
        int n = arr.length;

        System.out.print("Steps Taken: ");
        System.out.println(countSteps(arr, n));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python program to simulate max deletion
# and calculate number of steps.

# Function to find the maximum number in the
# array upto index n and return its index.
def countSteps(arr, n):
    large, steps = -1, 0

    for i in range(n):

        # condition to find max
        if arr[i] > large:
            large = arr[i]

            # Count the number of times this
            # condition executes that will the
            # number of turns being played.
            steps += 1

    # return the number of turns played
    return steps

# Driver Code
if __name__ == "__main__":
    arr = [2, 5, 8, 24, 4, 11, 6, 1, 15, 10]
    n = len(arr)

    #'steps' variable calculates the number of
    # steps being taken.
    print("Steps Taken:", countSteps(arr, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# code to simulate max
// deletion and calculate
// number of steps.
using System;

class GFG {

    // Function to find the maximum
    // number in the array upto index
    // n and return its index.
    static int countSteps(int[] arr, int n)
    {
        int max = -1, steps = 0;
        for (int i = 0; i < n; i++)
        {

            // condition to find max
            if (arr[i] > max) {

                max = arr[i];

                // Count the number of times
                // this condition executes
                // that will the number of
                // turns being played.
                steps++;
            }
        }

        // return the number of turns played
        return steps;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 2, 5, 8, 24, 4, 11, 6,
                                 1, 15, 10 };
        int n = arr.Length;

        Console.Write("Steps Taken: ");

        Console.WriteLine(countSteps(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to simulate max deletion
// and calculate number of steps.

// Function to find the
// maximum number in the
// array upto index n and
// return its index.
function countSteps($arr, $n)
{
    $max = -1;
    $steps = 0;
    for ( $i = 0; $i < $n; $i++)
    {

        // condition to find max
        if ($arr[$i] > $max)
        {

            $max = $arr[$i];

            // Count the number
            // of times this
            // condition executes
            // that will the number
            // of turns being played.
            $steps++;
        }
    }

    // return the number
    // of turns played
    return $steps;
}

    // Driver Code
    $arr = array(2, 5, 8, 24, 4,
                11, 6, 1, 15, 10);
    $n = count($arr);

    //'steps' variable calculates
    // the number of steps being
    // taken.
    echo "Steps Taken: ";
    echo countSteps($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to simulate max deletion
    // and calculate number of steps.

    // Function to find the maximum number in the
    // array upto index n and return its index.
    function countSteps(arr, n)
    {
        let max = -1, steps = 0;
        for (let i = 0; i < n; i++) {

            // condition to find max
            if (arr[i] > max) {

                max = arr[i];

                // Count the number of times this
                // condition executes that will the
                // number of turns being played.
                steps++;
            }
        }

        // return the number of turns played
        return steps;
    }

    let arr = [ 2, 5, 8, 24, 4, 11, 6, 1, 15, 10 ];
    let n = arr.length;

    //'steps' variable calculates the number of
    // steps being taken.
    document.write("Steps Taken: ");
    document.write(countSteps(arr, n));

</script>
```

**输出:**

```
Steps Taken: 4
```

这种方法的时间复杂度为 **O(n)** 。
本文由 [**丹麦语**](http://www.linkedin.com/in/mohdanishh) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。