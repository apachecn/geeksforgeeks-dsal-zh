# 生成 1 到 N 的随机排列

> 原文:[https://www . geesforgeks . org/generate-a-random-置换-1 到-n/](https://www.geeksforgeeks.org/generate-a-random-permutation-of-1-to-n/)

给定一个整数 **N** ，任务是生成 **N** 个不重复的随机数。

**示例:**

> **输入:**N = 5
> T3】输出: 1 5 2 4 3
> 
> **输入:**N = 8
> T3】输出: 7 2 1 8 3 6 4 5

**方法:**创建一个由 **N** 元素组成的数组，并将这些元素初始化为 **1，2，3，4，…，N** ，然后使用 Fisher-Yates 洗牌算法对数组元素进行洗牌。

[费希尔-耶茨洗牌算法](https://www.geeksforgeeks.org/shuffle-a-given-array-using-fisher-yates-shuffle-algorithm/)在 0(n)时间复杂度下工作。这里的假设是，给我们一个函数 rand()，它在 O(1)时间内生成一个随机数。

想法是从最后一个元素开始，用从整个数组中随机选择的元素(包括最后一个)替换它。现在考虑从 0 到 n-2(大小减少 1)的数组，重复这个过程，直到我们遇到第一个元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the next random number
int getNum(vector<int>& v)
{

    // Size of the vector
    int n = v.size();

    // Generate a random number
    srand(time(NULL));

    // Make sure the number is within
    // the index range
    int index = rand() % n;

    // Get random number from the vector
    int num = v[index];

    // Remove the number from the vector
    swap(v[index], v[n - 1]);
    v.pop_back();

    // Return the removed number
    return num;
}

// Function to generate n non-repeating random numbers
void generateRandom(int n)
{
    vector<int> v(n);

    // Fill the vector with the values
    // 1, 2, 3, ..., n
    for (int i = 0; i < n; i++)
        v[i] = i + 1;

    // While vector has elements
    // get a random number from the vector and print it
    while (v.size()) {
        cout << getNum(v) << " ";
    }
}

// Driver code
int main()
{
    int n = 8;
    generateRandom(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.Math;

class GfG
{

    // Function to return the next random number
    static int getNum(ArrayList<Integer> v)
    {
        // Size of the vector
        int n = v.size();

        // Make sure the number is within
        // the index range
        int index = (int)(Math.random() * n);

        // Get random number from the vector
        int num = v.get(index);

        // Remove the number from the vector
        v.set(index, v.get(n - 1));
        v.remove(n - 1);

        // Return the removed number
        return num;
    }

    // Function to generate n
    // non-repeating random numbers
    static void generateRandom(int n)
    {
        ArrayList<Integer> v = new ArrayList<>(n);

        // Fill the vector with the values
        // 1, 2, 3, ..., n
        for (int i = 0; i < n; i++)
            v.add(i + 1);

        // While vector has elements
        // get a random number from the vector and print it
        while (v.size() > 0)
        {
            System.out.print(getNum(v) + " ");
        }
    }

    // Driver code
    public static void main(String []args)
    {

        int n = 8;
        generateRandom(n);
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# import random module
import random

# Function to return the next
# random number
def getNum(v) :

    # Size of the vector
    n = len(v)

    # Generate a random number within
    # the index range
    index = random.randint(0, n - 1)

    # Get random number from the vector
    num = v[index]

    # Remove the number from the vector
    v[index], v[n - 1] = v[n - 1], v[index]
    v.pop()

    # Return the removed number
    return num

# Function to generate n non-repeating
# random numbers
def generateRandom(n) :

    v = [0] * n

    # Fill the vector with the values
    # 1, 2, 3, ..., n
    for i in range(n) :
        v[i] = i + 1

    # While vector has elements get a 
    # random number from the vector
    # and print it
    while (len(v)) :
        print(getNum(v), end = " ")

# Driver code
if __name__ == "__main__" :

    n = 8
    generateRandom(n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GfG{

// Function to return the next random number
static int getNum(ArrayList v)
{

    // Size of the vector
    int n = v.Count;

    Random rand = new Random();

    // Make sure the number is within
    // the index range
    int index = (rand.Next() % n);

    // Get random number from the vector
    int num = (int)v[index];

    // Remove the number from the vector
    v[index] = (int)v[n - 1];
    v.Remove(v[n - 1]);

    // Return the removed number
    return num;
}

// Function to generate n
// non-repeating random numbers
static void generateRandom(int n)
{
    ArrayList v = new ArrayList(n);

    // Fill the vector with the values
    // 1, 2, 3, ..., n
    for(int i = 0; i < n; i++)
        v.Add(i + 1);

    // While vector has elements get a
    // random number from the vector
    // and print it
    while (v.Count > 0)
    {
        Console.Write(getNum(v) + " ");
    }
}

// Driver code
public static void Main(string []args)
{
    int n = 8;

    generateRandom(n);
}
}

// This code is contributed by rutvik_56
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the next random number
function getNum(&$v)
{

    // Size of the vector
    $n = sizeof($v);

    // Generate a random number
    srand(time(NULL));

    // Make sure the number is within
    // the index range
    $index = rand() % $n;

    // Get random number from the vector
    $num = $v[$index];

    // Remove the number from the vector
    $t = $v[$index];
    $v[$index] = $v[$n - 1];
    $v[$n - 1] = $t;
    array_pop($v);

    // Return the removed number
    return $num;
}

// Function to generate n non-repeating
// random numbers
function generateRandom($n)
{
    $v = array(0, $n, NULL);

    // Fill the vector with the values
    // 1, 2, 3, ..., n
    for ($i = 0; $i < $n; $i++)
        $v[$i] = $i + 1;

    // While vector has elements
    // get a random number from the
    // vector and print it
    while (sizeof($v))
    {
        echo getNum($v) . " ";
    }
}

// Driver code
$n = 8;
generateRandom($n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the next random number
function getNum(v)
{
        // Size of the vector
        let n = v.length;

        // Make sure the number is within
        // the index range
        let index = Math.floor(Math.random() % n);

        // Get random number from the vector
        let num = v[index];

        // Remove the number from the vector
        v[index] = v[n - 1];
        v.splice(n - 1,1);

        // Return the removed number
        return num;
}

// Function to generate n
// non-repeating random numbers
function generateRandom(n)
{
        let v = [];

        // Fill the vector with the values
        // 1, 2, 3, ..., n
        for (let i = 0; i < n; i++)
            v.push(i + 1);

        // While vector has elements
        // get a random number from the vector and print it
        while (v.length > 0)
        {
            document.write(getNum(v) + " ");
        }
}

// Driver code
let n = 8;
generateRandom(n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
3 4 5 8 6 2 1 7
```