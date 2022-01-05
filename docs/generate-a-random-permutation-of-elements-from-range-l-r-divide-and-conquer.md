# 从范围【L，R】(分而治之)

生成元素的随机排列

> 原文:[https://www . geesforgeks . org/generate-a-random-arrange-from-l-r-分治法/](https://www.geeksforgeeks.org/generate-a-random-permutation-of-elements-from-range-l-r-divide-and-conquer/)

给定范围**【L，R】****L≤R**，任务是生成序列**【L，L + 1，L + 2，…，R】**的随机排列。
**举例:**

> **输入:** L = 5，R = 15
> **输出:** 11 9 6 5 8 7 10 12 13 15 14
> **输入:** L = 10，R = 20
> **输出:** 16 14 11 10 13 12 15 17 18 20 19

**方法:**我们将使用[分治](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)算法进行求解。我们将创建一个全局[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，它将存储由我们的递归函数**生成的随机数。
我们将把两个参数 **L** (开始)和 **R** (结束)传递给我们的递归函数。在函数内部，它将调用另一个函数 ***给 _random_number*** ，该函数将返回一个介于 **X** 和 **Y** 之间的数字。让我们称之为 **N** 。我们将把这个随机数存储在我们的向量中，然后我们将对范围**【L，N–1】**递归调用**generate _ random _ replacement()**函数，然后对范围**【N+1，R】**递归调用。
如果 **L** 变得大于 **R** ，那么我们将从功能中返回，不执行任何任务，因为这是我们的基础条件。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// To store the random permutation
vector<int> permutation;

// Utility function to print
// the generated permutation
void printPermutation()
{
    for (auto i : permutation)
        cout << i << " ";
}

// Function to return a random
// number between x and y
int give_random_number(int l, int r)
{
    int x = rand() % (r - l + 1) + l;
    return x;
}

// Recursive function to generate
// the random permutation
void generate_random_permutation(int l, int r)
{

    // Base condition
    if (l > r)
        return;

    // Random number returned from the function
    int n = give_random_number(l, r);

    // Inserting random number in vector
    permutation.push_back(n);

    // Recursion call for [l, n - 1]
    generate_random_permutation(l, n - 1);

    // Recursion call for [n + 1, r]
    generate_random_permutation(n + 1, r);
}

// Driver code
int main()
{
    int l = 5;
    int r = 15;

    // Generate permutation
    generate_random_permutation(l, r);

    // Print the generated permutation
    printPermutation();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Vector;

class GFG
{

// To store the random permutation
static Vector<Integer> permutation = new Vector<>();

// Utility function to print
// the generated permutation
static void printPermutation()
{
    permutation.stream().forEach((i) ->
    {
        System.out.print(i+" ");
    });
}

// Function to return a random
// number between x and y
static int give_random_number(int l, int r)
{
    int x = (int) (Math.random()% (r - l + 1) + l);
    return x;
}

// Recursive function to generate
// the random permutation
static void generate_random_permutation(int l, int r)
{

    // Base condition
    if (l > r)
        return;

    // Random number returned from the function
    int n = give_random_number(l, r);

    // Inserting random number in vector
    permutation.add(n);

    // Recursion call for [l, n - 1]
    generate_random_permutation(l, n - 1);

    // Recursion call for [n + 1, r]
    generate_random_permutation(n + 1, r);
}

// Driver code
public static void main(String[] args)
{
    int l = 5;
    int r = 15;

    // Generate permutation
    generate_random_permutation(l, r);

    // Print the generated permutation
    printPermutation();
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import random

# To store the random permutation
permutation = []

# Utility function to print
# the generated permutation
def printPermutation() :

    for i in permutation:
        print(i, end = " ")

# Function to return a random
# number between x and y
def give_random_number(l, r) :

    x = random.randint(l, r)
    return x

# Recursive function to generate
# the random permutation
def generate_random_permutation(l, r) :

    # Base condition
    if (l > r) :
        return

    # Random number returned from the function
    n = give_random_number(l, r)

    # Inserting random number in vector
    permutation.append(n)

    # Recursion call for [l, n - 1]
    generate_random_permutation(l, n - 1)

    # Recursion call for [n + 1, r]
    generate_random_permutation(n + 1, r)

# Driver code
l = 5
r = 15

# Generate permutation
generate_random_permutation(l, r)

# Print the generated permutation
printPermutation()

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// To store the random permutation
static List<int> permutation = new List<int>();

// Utility function to print
// the generated permutation
static void printPermutation()
{
    foreach(int i in permutation)
        Console.Write(i+" ");
}

// Function to return a random
// number between x and y
static int give_random_number(int l, int r)
{
    Random rnd = new Random();
    int num = rnd.Next(l, r);
    int x = (int) (num % (r - l + 1) + l);
    return x;
}

// Recursive function to generate
// the random permutation
static void generate_random_permutation(int l, int r)
{

    // Base condition
    if (l > r)
        return;

    // Random number returned from the function
    int n = give_random_number(l, r);

    // Inserting random number in vector
    permutation.Add(n);

    // Recursion call for [l, n - 1]
    generate_random_permutation(l, n - 1);

    // Recursion call for [n + 1, r]
    generate_random_permutation(n + 1, r);
}

// Driver code
public static void Main(String[] args)
{
    int l = 5;
    int r = 15;

    // Generate permutation
    generate_random_permutation(l, r);

    // Print the generated permutation
    printPermutation();
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// To store the random permutation
$permutation = array();

// Utility function to print
// the generated permutation
function printPermutation()
{
    global $permutation;
    foreach ($permutation as $i)
        echo $i . " ";
}

// Function to return a random
// number between x and y
function give_random_number($l, $r)
{
    $x = rand() % ($r - $l + 1) + $l;
    return $x;
}

// Recursive function to generate
// the random permutation
function generate_random_permutation($l, $r)
{
    global $permutation;

    // Base condition
    if ($l > $r)
        return;

    // Random number returned from the function
    $n = give_random_number($l, $r);

    // Inserting random number in vector
    array_push($permutation, $n);

    // Recursion call for [l, n - 1]
    generate_random_permutation($l, $n - 1);

    // Recursion call for [n + 1, r]
    generate_random_permutation($n + 1, $r);
}

// Driver code
$l = 5;
$r = 15;

// Generate permutation
generate_random_permutation($l, $r);

// Print the generated permutation
printPermutation();

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// To store the random permutation
var permutation = [];

// Utility function to print
// the generated permutation
function printPermutation()
{
    for (var i of permutation)
        document.write(i + " ");
}

// Function to return a random
// number between x and y
function give_random_number(l, r)
{
    var x = Math.floor(Math.random() * l + r) % (r - l + 1) + l;
    return x;
}

// Recursive function to generate
// the random permutation
function generate_random_permutation(l, r)
{

    // Base condition
    if (l > r)
        return;

    // Random number returned from the function
    var n = give_random_number(l, r);

    // Inserting random number in vector
    permutation.push(n);

    // Recursion call for [l, n - 1]
    generate_random_permutation(l, n - 1);

    // Recursion call for [n + 1, r]
    generate_random_permutation(n + 1, r);
}

// Driver code
var l = 5;
var r = 15;

// Generate permutation
generate_random_permutation(l, r);

// Print the generated permutation
printPermutation();

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
11 9 6 5 8 7 10 12 13 15 14
```

**时间复杂度:** O(n)