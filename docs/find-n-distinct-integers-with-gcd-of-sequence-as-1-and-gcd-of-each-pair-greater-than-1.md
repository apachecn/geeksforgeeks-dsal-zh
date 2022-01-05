# 找出 N 个不同的整数，序列的 GCD 为 1，每对的 GCD 大于 1

> 原文:[https://www . geesforgeks . org/find-n-distinct-integers-with-gcd-of-sequence-as-1 和-gcd-of-每对-大于-1/](https://www.geeksforgeeks.org/find-n-distinct-integers-with-gcd-of-sequence-as-1-and-gcd-of-each-pair-greater-than-1/)

给定一个整数 **N** ，任务是找到一个由 **N** 个不同正整数组成的序列，使得该序列的[最大公约数](http://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)为 1，并且所有可能的元素对的 GCD 大于 1。

> **输入:** N = 4
> **输出:** 84 60 105 70
> **说明:**GCD(84、60、105、70)为 1，所有可能的元素对即{(84、60)、(84、105)、(84、70)、(60、105)、(60、70)、(105、70)}的 GCD 大于 1。
> 
> **输入:**N = 3
> T3】输出: 6 10 15

**方法:**这个问题可以通过使用[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)来解决。想法是选择三个形式为 **(a*b，b*c，c*a)** 的整数，因为三者中的 [GCD](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 1，两两之间 **GCD** 总是大于 1。此外，只需将三个整数的倍数相加，直到序列包含所需数量的整数。形式为 **(a*b，b*c，c*a)** 的一组整数为 **(6，10，15)** 。因此，将 **6** 、 **10、**和 **15** 的倍数添加到序列中，打印所需的整数个数。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sequence of
// distinct integers with GCD equal
// to 1 and every pair has GCD > 1.
void findSequence(int N)
{
    // Special case
    if (N == 3) {
        cout << "6 10 15" << endl;
        return;
    }

    // Set to avoid duplicates
    set<int> s;
    s.insert(6);
    s.insert(10);
    s.insert(15);

    // Add multiples of 6
    for (int i = 12; i <= 10000; i += 6)
        s.insert(i);

    // Add multiples of 10
    for (int i = 20; i <= 10000; i += 10)
        s.insert(i);

    // Add multiples of 15
    for (int i = 30; i <= 10000; i += 15)
        s.insert(i);

      int cnt = 0;

    // Print first N numbers of set
    for (int x : s) {
        cout << x << " ";
        cnt++;
        if (cnt == N) {
            break;
        }
    }
}

// Driver Code
int main()
{
    int N = 3;
    findSequence(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Function to find the sequence of
// distinct integers with GCD equal
// to 1 and every pair has GCD > 1.
static void findSequence(int N)
{

    // Special case
    if (N == 3)
    {
        System.out.println("6 10 15");
        return;
    }

    // Set to avoid duplicates
    Set<Integer> s = new HashSet<Integer>();
    s.add(6);
    s.add(10);
    s.add(15);

    // Add multiples of 6
    for(int i = 12; i <= 10000; i += 6)
        s.add(i);

    // Add multiples of 10
    for(int i = 20; i <= 10000; i += 10)
        s.add(i);

    // Add multiples of 15
    for(int i = 30; i <= 10000; i += 15)
        s.add(i);

    int cnt = 0;

    // Print first N numbers of set
    for(Integer x : s)
    {
        System.out.print(x + " ");
        cnt++;

        if (cnt == N)
        {
            break;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;

    findSequence(N);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for above approach

# Function to find the sequence of
# distinct integers with GCD equal
# to 1 and every pair has GCD > 1.
def findSequence(N):

    # Special case
    if (N == 3):
        print("6 10 15")
        return

    # Set to avoid duplicates
    s = set()
    s.add(6)
    s.add(10)
    s.add(15)

    # Add multiples of 6
    for i in range(12, 10001, 6):
        s.add(i)

    # Add multiples of 10
    for i in range(20, 10001, 10):
        s.add(i)

    # Add multiples of 15
    for i in range(30, 10001, 15):
        s.add(i)

    cnt = 0

    # Print first N numbers of set
    for x in s:
        print(x, end=" ")
        cnt += 1
        if (cnt == N):
            break

# Driver Code
if __name__ == "__main__":

    N = 3
    findSequence(N)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the sequence of
    // distinct integers with GCD equal
    // to 1 and every pair has GCD > 1.
    static void findSequence(int N)
    {

        // Special case
        if (N == 3) {
            Console.WriteLine("6 10 15");
            return;
        }

        // Set to avoid duplicates
        HashSet<int> s = new HashSet<int>();
        s.Add(6);
        s.Add(10);
        s.Add(15);

        // Add multiples of 6
        for (int i = 12; i <= 10000; i += 6)
            s.Add(i);

        // Add multiples of 10
        for (int i = 20; i <= 10000; i += 10)
            s.Add(i);

        // Add multiples of 15
        for (int i = 30; i <= 10000; i += 15)
            s.Add(i);

        int cnt = 0;

        // Print first N numbers of set
        foreach(int x in s)
        {
            Console.Write(x + " ");
            cnt++;

            if (cnt == N) {
                break;
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 3;

        findSequence(N);
    }
}

// Thiss code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to find the sequence of
// distinct integers with GCD equal
// to 1 and every pair has GCD > 1.
function findSequence(N)
{

    // Special case
    if (N == 3) {
        document.write("6 10 15");
        return;
    }

    // Set to avoid duplicates
    let s = new Set();
    s.add(6);
    s.add(10);
    s.add(15);

    // Add multiples of 6
    for (let i = 12; i <= 10000; i += 6)
        s.add(i);

    // Add multiples of 10
    for (let i = 20; i <= 10000; i += 10)
        s.add(i);

    // Add multiples of 15
    for (let i = 30; i <= 10000; i += 15)
        s.add(i);

    let cnt = 0;

    // Print first N numbers of set
    for (x of s) {
        document.write(x + " ");
        cnt++;
        if (cnt == N) {
            break;
        }
    }
}

// Driver Code
let N = 3;
findSequence(N);

// This code is contributed by gfgking.
</script>
```

**Output**

```
6 10 15
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*