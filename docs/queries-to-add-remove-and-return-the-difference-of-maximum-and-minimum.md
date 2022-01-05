# 查询添加、删除和返回最大值和最小值的差值。

> 原文:[https://www . geesforgeks . org/query-to-add-remove-return-最大值与最小值之差/](https://www.geeksforgeeks.org/queries-to-add-remove-and-return-the-difference-of-maximum-and-minimum/)

给定 Q 个查询。查询有三种类型，描述如下:

*   将数字 ***num*** 添加到列表中。
*   从列表中删除编号 ***num*** 。
*   返回列表中最大值和最小值之间的差值。

任务是编写一个执行上述查询的程序。
**注意:**数字是不同的，每次调用 query-3 时，列表中至少会有 1 个元素。
**示例:**

> **输入:**
> Q = 5
> 类型 1 的查询:num = 3
> 类型 1 的查询:num = 5
> 类型 1 的查询:num = 6
> 类型 2 的查询:num = 6
> 类型 1 的查询:num = 2
> 类型 3 的查询:
> **输出:** 4
> 由于类型 3 的查询只被调用过一次，瞬间的答案是 4。
> 第一次查询类型-1 后，列表为{3}
> 第二次查询类型-1 后，列表为{3，5}
> 第三次查询类型-1 后，列表为{3，5，6}
> 第四次查询类型-2 后，列表为{3，5}
> 第五次查询类型-1 后，列表为{2，3，5}
> 第六次查询类型-3 时，答案为 5-2。

一**简单**的解决方法是按照以下步骤:

*   将数字存储在向量数组中。
*   对于**的查询，键入-1** 向数组中添加一个元素。
*   对于**查询，键入-2** 从向量或数组中移除元素。
*   对于**类型-3 的查询，**遍历数组，找到数组中的最小值和最大值，并返回它们的差值。

**时间复杂度:** O(1)用于类型-2 的查询的插入，O(N)用于最坏情况下的类型-2 的查询，O(N)用于类型-3 的查询。
**辅助空间:** O(N)
一个**高效的解决方案**是使用一个自平衡的二叉查找树(实现为 C++中的 [set](https://www.geeksforgeeks.org/set-in-cpp-stl/) 容器或者 Java 中的 [TreeSet](https://www.geeksforgeeks.org/treeset-in-java-with-examples/) )。按照以下步骤解决上述问题。

*   使用 [insert()](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) 功能将元素插入容器中。
*   使用[擦除()](https://www.geeksforgeeks.org/seterase-c-stl/)功能从容器中删除元素。
*   最小值总是在开始，最大值总是在结束。可以使用 [begin()](https://www.geeksforgeeks.org/setbegin-setend-c-stl/) 和 [rbegin()](https://www.geeksforgeeks.org/setrbegin-and-setrend-in-c-stl/) 功能检索它们。

下面是高效方法的实现:

## C++

```
// C++ program to perform Queries to
// add, remove and return
// the difference of maximum and minimum.
#include <bits/stdc++.h>
    using namespace std;
set<int> s;

// function to perform query 1
void performQueryOne(int num)
{
    // insert the element
    s.insert(num);
}

// function to perform query 2
void performQueryTwo(int num)
{
    // erase the element
    s.erase(num);
}

// function to perform query 3
int performQueryThree()
{
    int mini = *(s.begin());
    int maxi = *(s.rbegin());

    return maxi - mini;
}

// Driver Code
int main()
{

    // query type-1
    int num = 3;
    performQueryOne(num);

    // query type-1
    num = 5;
    performQueryOne(num);

    // query type-1
    num = 6;
    performQueryOne(num);

    // query type-2
    num = 5;
    performQueryTwo(num);

    // query type-1
    num = 2;
    performQueryOne(num);

    // query type-3
    cout << performQueryThree();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform Queries
// to add, remove and return
// the difference of maximum and
// minimum using TreeSet.
import java.util.*;
class GFG
{
static SortedSet<Integer> t = new TreeSet<Integer>();

// function to perform query 1
static void performQueryOne(int num)
{
    // insert the element
    t.add(num);
}

// function to perform query 2
static void performQueryTwo(int num)
{
    // erase the element
    t.remove(num);
}

// function to perform query 3
static int performQueryThree()
{
    int mini = t.first();
    int maxi = t.last();

    return maxi - mini;
}

// Driver Code
public static void main(String[] args)
{
    // query type-1
    int num = 3;
    performQueryOne(num);

    // query type-1
    num = 5;
    performQueryOne(num);

    // query type-1
    num = 6;
    performQueryOne(num);

    // query type-2
    num = 5;
    performQueryTwo(num);

    // query type-1
    num = 2;
    performQueryOne(num);

    // query type-3
    System.out.println(performQueryThree());
}
}

// This code is contributed by debjitdbb
```

## 蟒蛇 3

```
# Python3 program to perform Queries
# to add, remove and return
# difference of maximum and minimum.

# Function to perform query 1
def performQueryOne(num):

    # insert the element
    s.add(num)

# Function to perform query 2
def performQueryTwo(num):

    # erase the element
    s.remove(num)

# function to perform query 3
def performQueryThree():

    mini = min(s)
    maxi = max(s)

    return maxi - mini

# Driver Code
if __name__ == "__main__":

    s = set()

    # query type-1
    num = 3
    performQueryOne(num)

    # query type-1
    num = 5
    performQueryOne(num)

    # query type-1
    num = 6
    performQueryOne(num)

    # query type-2
    num = 5
    performQueryTwo(num)

    # query type-1
    num = 2
    performQueryOne(num)

    # query type-3
    print(performQueryThree())

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to perform Queries
// to add, remove and return
// the difference of maximum and
// minimum using TreeSet.
using System;
using System.Collections.Generic;

class GFG
{

static SortedSet<int> t = new SortedSet<int>();

// function to perform query 1
static void performQueryOne(int num)
{
    // insert the element
    t.Add(num);
}

// function to perform query 2
static void performQueryTwo(int num)
{
    // erase the element
    t.Remove(num);
}

// function to perform query 3
static int performQueryThree()
{
    int mini = t.Min;
    int maxi = t.Max;

    return maxi - mini;
}

// Driver Code
public static void Main(String[] args)
{
    // query type-1
    int num = 3;
    performQueryOne(num);

    // query type-1
    num = 5;
    performQueryOne(num);

    // query type-1
    num = 6;
    performQueryOne(num);

    // query type-2
    num = 5;
    performQueryTwo(num);

    // query type-1
    num = 2;
    performQueryOne(num);

    // query type-3
    Console.WriteLine(performQueryThree());
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to perform Queries to
// add, remove and return
// the difference of maximum and minimum.
var s = new Set();

// function to perform query 1
function performQueryOne( num)
{
    // insert the element
    s.add(num);
}

// function to perform query 2
function performQueryTwo( num)
{
    // erase the element
    s.delete(num);
}

// function to perform query 3
function performQueryThree()
{
    var tmp = [...s].sort((a,b)=>a-b);
    var mini = tmp[0];
    var maxi = tmp[tmp.length-1];

    return maxi - mini;
}

// Driver Code
// query type-1
var num = 3;
performQueryOne(num);
// query type-1
num = 5;
performQueryOne(num);
// query type-1
num = 6;
performQueryOne(num);
// query type-2
num = 5;
performQueryTwo(num);
// query type-1
num = 2;
performQueryOne(num);
// query type-3
document.write( performQueryThree());

</script>
```

**Output:** 

```
4
```

**时间复杂度:**每个查询 O(log N)。
**辅助空间:** O(N)