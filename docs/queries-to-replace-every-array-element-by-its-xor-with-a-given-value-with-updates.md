# 查询通过更新将每个数组元素与其给定值进行异或替换

> 原文:[https://www . geeksforgeeks . org/query-以更新替换每个数组元素与给定值的异或运算/](https://www.geeksforgeeks.org/queries-to-replace-every-array-element-by-its-xor-with-a-given-value-with-updates/)

给定一个数组，最初由作为唯一存在元素的 **0** 和以下两种类型的 **Q** 操作组成:

*   **加(X):** 将 **X** 插入阵中。
*   **更新(X):** 将每个数组元素**a<sub>I</sub>t5】替换为 **A <sub>i</sub> ^ X** ，其中^是[异或](https://www.geeksforgeeks.org/tag/xor/)运算。**

**示例:**

> **输入:**q = 2
> add(5)
> update(2)
> **输出:**2 7
> t8】解释:
> 最初，Array = {0}
> 查询 1: Array = {0，5}
> 查询 2: Array = {0^2，5^2} = > {2，7}
> 
> **输入:** Q = 2
> 加(3)
> 加(5)
> T5】输出: 0 3 5

**方法:**的思想是存储一个变量，该变量存储将与每个数组元素进行[异或](https://www.geeksforgeeks.org/tag/xor/)的值，在数组中插入元素时，为了消除异或值的影响，对其本身应用**异或**运算。按照以下步骤解决问题:

*   维护一个变量，比如*效果*，来存储最终的异或值。
*   对于操作**添加(X):** 在列表末尾添加 **X** ，并用*X ^效应* **更新其值。**
*   对于操作**更新(X):** 用*效果^ X 更新“*效果”* 的值。*这是为了得到一个更新后的 **XOR** 效果。
*   完成上述所有操作后，用其**异或**与*效果*更新所有数组元素，即对于所有**a<sub>I</sub>T7】，更新 **A <sub>i</sub> = A <sub>i</sub> ^效果**。**

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

#define int long long

// Function to insert an element
// into the array
void add(vector<int>& arr, int x)
{
    arr.push_back(x);
}

// Function to update every array
// element a[i] by a[i] ^ x
void update(int& effect, int x)
{
    effect = effect ^ x;
}

// Function to compute the final
// results after the operations
void computeResults(vector<int>& arr,
                    int effect)
{
    for (int i = 0; i < arr.size(); i++) {
        arr[i] = arr[i] ^ effect;
        cout << arr[i] << " ";
    }
}

// Driver Code
signed main()
{
    vector<int> arr = { 0 };
    int effect = 0;

    // Queries
    add(arr, 5);
    update(effect, 2);

    // Function Call
    computeResults(arr, effect);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of
// the above approach
import java.util.*;
class GFG{

static Vector<Integer> arr =
              new Vector<Integer>();
static int effect;

// Function to insert an element
// into the array
static void add(int x)
{
  arr.add(x);
}

// Function to update every array
// element a[i] by a[i] ^ x
static void update(int x)
{
  effect = effect ^ x;
}

// Function to compute the final
// results after the operations
static void computeResults()
{
  for (int i = 0; i < arr.size(); i++)
  {
    arr.set(i, arr.get(i) ^ effect);
    System.out.print(arr.get(i) + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  arr = new Vector<Integer>();
  arr.add(0);
  effect = 0;

  // Queries
  add(5);
  update(2);

  // Function Call
  computeResults();
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function to insert an element
# into the array
def add(arr, x):

    arr.append(x)

# Function to update every array
# element a[i] by a[i] ^ x
def update(effect, x):

    effect = effect ^ x
    return effect

# Function to compute the final
# results after the operations
def computeResults(arr, effect):

    for i in range(len(arr)):
        arr[i] = arr[i] ^ effect
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [0]
    effect = 0

    # Queries
    add(arr, 5)
    effect = update(effect, 2)

    # Function call
    computeResults(arr, effect)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program of
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static List<int> arr = new List<int>();
static int effect;

// Function to insert an element
// into the array
static void add(int x)
{
  arr.Add(x);
}

// Function to update every array
// element a[i] by a[i] ^ x
static void update(int x)
{
  effect = effect ^ x;
}

// Function to compute the final
// results after the operations
static void computeResults()
{
  for (int i = 0; i < arr.Count; i++)
  {
    arr[i] = arr[i] ^ effect;
    Console.Write(arr[i] + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  arr = new List<int>();
  arr.Add(0);
  effect = 0;

  // Queries
  add(5);
  update(2);

  // Function Call
  computeResults();
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// Function to insert an element
// into the array
function add(arr, x)
{
    arr.push(x);
}

// Function to update every array
// element a[i] by a[i] ^ x
function update(effect, x)
{
    effect = effect ^ x;
    return effect;
}

// Function to compute the final
// results after the operations
function computeResults(arr, effect) {
    for (let i = 0; i < arr.length; i++) {
        arr[i] = arr[i] ^ effect;
        document.write(arr[i] + " ");
    }
}

// Driver Code
let arr = [0];
let effect = 0;

// Queries
add(arr, 5);
effect = update(effect, 2)

// Function Call
computeResults(arr, effect);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
2 7
```

***时间复杂度:**O(Q)*
T5**辅助空间:** O(1)