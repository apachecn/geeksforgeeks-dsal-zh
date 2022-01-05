# 生成一个整数的所有唯一分区

> 原文:[https://www . geeksforgeeks . org/generate-unique-partitions-of-a-integer/](https://www.geeksforgeeks.org/generate-unique-partitions-of-an-integer/)

给定一个正整数 n，生成所有可能的唯一方法，将 n 表示为正整数的和。

**示例:**

```
  Input: n = 2
  Output: 
  2
  1 1

  Input: n = 3
  Output: 
  3
  2 1
  1 1 1
  Note: 2+1 and 1+2 are considered as duplicates.

  Input: n = 4
  Output: 
  4
  3 1
  2 2
  2 1 1
  1 1 1 1 
```

**解决方案:**我们按排序顺序打印所有分区，一个分区内的数字也按排序顺序打印(如上例所示)。想法是使用当前分区中的值获取下一个分区。我们将每个分区存储在一个数组 p[]中。我们将 p[]初始化为 n，其中 n 是输入数。在每次迭代中。我们首先打印 p[]，然后更新 p[]，以存储下一个分区。所以主要问题是从给定的分区中获取下一个分区。

**从当前分区获取下一个分区的步骤:**
我们在 p[]中给出了当前分区及其大小。我们需要更新 p[]来存储下一个分区。p[]中的值必须按非递增顺序排序。

1.  在 p[]中找到最右边的非 1 值，并将在非 1 值之前遇到的 1 的计数存储在变量 rem_val 中(它指示右侧要更新的值的总和)。设非一值的指数为 k。
2.  将 p[k]的值减少 1，将 rem_val 增加 1。现在可能有两种情况:
    *   **a)如果** p[k]大于或等于 rem_val。这是一个简单的例子(我们在新的分区中有排序顺序)。把 rem_val 放在 p[k+1]处，p[0…k+1]就是我们的新分区。
    *   **b) Else** (这是一个有趣的情况，取初始 p[]为{3，1，1，1}，p[k]从 3 减少到 2，rem_val 从 3 增加到 4，下一个分区应该是{2，2，2})。
3.  当 p[k]小于 rem_val 时，将 p[k]复制到下一个位置，增加 k 并减少 p[k]计数。最后，把 rem_val 放在 p[k+1]处，p[0…k+1]就是我们的新分区。这一步就像用 p[k]来划分 rem _ val 除以 2)。

以下是上述算法的实现:

## C++

```
// CPP program to generate all unique
// partitions of an integer
#include<iostream>
using namespace std;

// A utility function to print an array p[] of size 'n'
void printArray(int p[], int n)
{
    for (int i = 0; i < n; i++)
    cout << p[i] << " ";
    cout << endl;
}

void printAllUniqueParts(int n)
{
    int p[n]; // An array to store a partition
    int k = 0; // Index of last element in a partition
    p[k] = n; // Initialize first partition as number itself

    // This loop first prints current partition then generates next
    // partition. The loop stops when the current partition has all 1s
    while (true)
    {
        // print current partition
        printArray(p, k+1);

        // Generate next partition

        // Find the rightmost non-one value in p[]. Also, update the
        // rem_val so that we know how much value can be accommodated
        int rem_val = 0;
        while (k >= 0 && p[k] == 1)
        {
            rem_val += p[k];
            k--;
        }

        // if k < 0, all the values are 1 so there are no more partitions
        if (k < 0) return;

        // Decrease the p[k] found above and adjust the rem_val
        p[k]--;
        rem_val++;

        // If rem_val is more, then the sorted order is violated. Divide
        // rem_val in different values of size p[k] and copy these values at
        // different positions after p[k]
        while (rem_val > p[k])
        {
            p[k+1] = p[k];
            rem_val = rem_val - p[k];
            k++;
        }

        // Copy rem_val to next position and increment position
        p[k+1] = rem_val;
        k++;
    }
}

// Driver program to test above functions
int main()
{
    cout << "All Unique Partitions of 2 \n";
    printAllUniqueParts(2);

    cout << "\nAll Unique Partitions of 3 \n";
    printAllUniqueParts(3);

    cout << "\nAll Unique Partitions of 4 \n";
    printAllUniqueParts(4);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate all unique
// partitions of an integer
import java.io.*;

class GFG
{
    // Function to print an array p[] of size n
    static void printArray(int p[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(p[i]+" ");
        System.out.println();
    }

    // Function to generate all unique partitions of an integer
    static void printAllUniqueParts(int n)
    {
        int[] p = new int[n]; // An array to store a partition
        int k = 0;  // Index of last element in a partition
        p[k] = n;  // Initialize first partition as number itself

        // This loop first prints current partition then generates next
        // partition. The loop stops when the current partition has all 1s
        while (true)
        {
            // print current partition
            printArray(p, k+1);

            // Generate next partition

            // Find the rightmost non-one value in p[]. Also, update the
            // rem_val so that we know how much value can be accommodated
            int rem_val = 0;
            while (k >= 0 && p[k] == 1)
            {
                rem_val += p[k];
                k--;
            }

            // if k < 0, all the values are 1 so there are no more partitions
            if (k < 0)  return;

            // Decrease the p[k] found above and adjust the rem_val
            p[k]--;
            rem_val++;

            // If rem_val is more, then the sorted order is violated.  Divide
            // rem_val in different values of size p[k] and copy these values at
            // different positions after p[k]
            while (rem_val > p[k])
            {
                p[k+1] = p[k];
                rem_val = rem_val - p[k];
                k++;
            }

            // Copy rem_val to next position and increment position
            p[k+1] = rem_val;
            k++;
        }
    }

    // Driver program
    public static void main (String[] args)
    {
        System.out.println("All Unique Partitions of 2");
        printAllUniqueParts(2);

        System.out.println("All Unique Partitions of 3");
        printAllUniqueParts(3);

        System.out.println("All Unique Partitions of 4");
        printAllUniqueParts(4);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# A utility function to print an
# array p[] of size 'n'
def printArray(p, n):
    for i in range(0, n):
        print(p[i], end = " ")
    print()

def printAllUniqueParts(n):
    p = [0] * n     # An array to store a partition
    k = 0         # Index of last element in a partition
    p[k] = n     # Initialize first partition
                 # as number itself

    # This loop first prints current partition,
    # then generates next partition.The loop
    # stops when the current partition has all 1s
    while True:

            # print current partition
            printArray(p, k + 1)

            # Generate next partition

            # Find the rightmost non-one value in p[].
            # Also, update the rem_val so that we know
            # how much value can be accommodated
            rem_val = 0
            while k >= 0 and p[k] == 1:
                rem_val += p[k]
                k -= 1

            # if k < 0, all the values are 1 so
            # there are no more partitions
            if k < 0:
                print()
                return

            # Decrease the p[k] found above
            # and adjust the rem_val
            p[k] -= 1
            rem_val += 1

            # If rem_val is more, then the sorted
            # order is violated. Divide rem_val in
            # different values of size p[k] and copy
            # these values at different positions after p[k]
            while rem_val > p[k]:
                p[k + 1] = p[k]
                rem_val = rem_val - p[k]
                k += 1

            # Copy rem_val to next position
            # and increment position
            p[k + 1] = rem_val
            k += 1

# Driver Code
print('All Unique Partitions of 2')
printAllUniqueParts(2)

print('All Unique Partitions of 3')
printAllUniqueParts(3)

print('All Unique Partitions of 4')
printAllUniqueParts(4)

# This code is contributed
# by JoshuaWorthington
```

## C#

```
// C# program to generate all unique
// partitions of an integer
using System;

class GFG {

    // Function to print an array p[]
    // of size n
    static void printArray(int []p, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(p[i]+" ");

        Console.WriteLine();
    }

    // Function to generate all unique
    // partitions of an integer
    static void printAllUniqueParts(int n)
    {

        // An array to store a partition
        int[] p = new int[n];

        // Index of last element in a
        // partition
        int k = 0;

        // Initialize first partition as
        // number itself
        p[k] = n;

        // This loop first prints current
        // partition, then generates next
        // partition. The loop stops when
        // the current partition has all 1s
        while (true)
        {

            // print current partition
            printArray(p, k+1);

            // Generate next partition

            // Find the rightmost non-one
            // value in p[]. Also, update
            // the rem_val so that we know
            // how much value can be
            // accommodated
            int rem_val = 0;

            while (k >= 0 && p[k] == 1)
            {
                rem_val += p[k];
                k--;
            }

            // if k < 0, all the values are 1 so
            // there are no more partitions
            if (k < 0)
                return;

            // Decrease the p[k] found above
            // and adjust the rem_val
            p[k]--;
            rem_val++;

            // If rem_val is more, then the sorted
            // order is violated. Divide rem_val in
            // different values of size p[k] and copy
            // these values at different positions
            // after p[k]
            while (rem_val > p[k])
            {
                p[k+1] = p[k];
                rem_val = rem_val - p[k];
                k++;
            }

            // Copy rem_val to next position and
            // increment position
            p[k+1] = rem_val;
            k++;
        }
    }

    // Driver program
    public static void Main ()
    {
        Console.WriteLine("All Unique Partitions of 2");
        printAllUniqueParts(2);

        Console.WriteLine("All Unique Partitions of 3");
        printAllUniqueParts(3);

        Console.WriteLine("All Unique Partitions of 4");
        printAllUniqueParts(4);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate
// all unique partitions
// of an integer

// A utility function to
// print an array p[] of
// size 'n'
function printArray( $p, $n)
{
    for ($i = 0; $i < $n; $i++)
    echo $p[$i] , " ";
    echo "\n";
}

function printAllUniqueParts($n)
{
    // An array to store
    // a partition
    $p[$n] = array(0);

    // Index of last element
    // in a partition
    $k = 0;

    // Initialize first
    // partition as number
    // itself
    $p[$k] = $n;

    // This loop first prints
    // current partition, then
    // generates next partition.
    // The loop stops when the
    // current partition has all 1s
    while (true)
    {
        // print current partition
        printArray($p, $k + 1);

        // Generate next partition

        // Find the rightmost non-one
        // value in p[]. Also, update
        // the rem_val so that we know
        // how much value can be accommodated
        $rem_val = 0;
        while ($k >= 0 && $p[$k] == 1)
        {
            $rem_val += $p[$k];
            $k--;
        }

        // if k < 0, all the values
        // are 1 so there are no
        // more partitions
        if ($k < 0) return;

        // Decrease the p[k] found
        // above and adjust the
        // rem_val
        $p[$k]--;
        $rem_val++;

        // If rem_val is more, then
        // the sorted order is violated.
        // Divide rem_val in different
        // values of size p[k] and copy
        // these values at different
        // positions after p[k]
        while ($rem_val > $p[$k])
        {
            $p[$k + 1] = $p[$k];
            $rem_val = $rem_val - $p[$k];
            $k++;
        }

        // Copy rem_val to next
        // position and increment
        // position
        $p[$k + 1] = $rem_val;
        $k++;
    }
}

// Driver Code
echo "All Unique Partitions of 2 \n";
printAllUniqueParts(2);

echo "\nAll Unique Partitions of 3 \n";
printAllUniqueParts(3);

echo "\nAll Unique Partitions of 4 \n";
printAllUniqueParts(4);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to generate all unique
// partitions of an integer

// Function to print an array p[]
// of size n
function printArray(p, n)
{
    for(let i = 0; i < n; i++)
        document.write(p[i] + " ");

    document.write("</br>");
}

// Function to generate all unique
// partitions of an integer
function printAllUniqueParts(n)
{

    // An array to store a partition
    let p = new Array(n);

    // Index of last element in a
    // partition
    let k = 0;

    // Initialize first partition as
    // number itself
    p[k] = n;

    // This loop first prints current
    // partition, then generates next
    // partition. The loop stops when
    // the current partition has all 1s
    while (true)
    {

        // print current partition
        printArray(p, k + 1);

        // Generate next partition

        // Find the rightmost non-one
        // value in p[]. Also, update
        // the rem_val so that we know
        // how much value can be
        // accommodated
        let rem_val = 0;

        while (k >= 0 && p[k] == 1)
        {
            rem_val += p[k];
            k--;
        }

        // If k < 0, all the values are 1 so
        // there are no more partitions
        if (k < 0)
            return;

        // Decrease the p[k] found above
        // and adjust the rem_val
        p[k]--;
        rem_val++;

        // If rem_val is more, then the sorted
        // order is violated. Divide rem_val in
        // different values of size p[k] and copy
        // these values at different positions
        // after p[k]
        while (rem_val > p[k])
        {
            p[k + 1] = p[k];
            rem_val = rem_val - p[k];
            k++;
        }

        // Copy rem_val to next position and
        // increment position
        p[k + 1] = rem_val;
        k++;
    }
}

// Driver code
document.write("All Unique Partitions of 2" + "</br>");
printAllUniqueParts(2);

document.write("All Unique Partitions of 3" + "</br>");
printAllUniqueParts(3);

document.write("All Unique Partitions of 4" + "</br>");
printAllUniqueParts(4);

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
All Unique Partitions of 2
2
1 1

All Unique Partitions of 3
3
2 1
1 1 1

All Unique Partitions of 4
4
3 1
2 2
2 1 1
1 1 1 1
```

***时间复杂度:** O(n * k)*

***辅助空间:** O(n)*
本文由 **Hariprasad NG** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息