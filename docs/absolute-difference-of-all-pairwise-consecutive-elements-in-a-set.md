# 集合中所有成对连续元素的绝对差

> 原文:[https://www . geeksforgeeks . org/所有成对连续元素的绝对差集/](https://www.geeksforgeeks.org/absolute-difference-of-all-pairwise-consecutive-elements-in-a-set/)

给定一组 **N** 元素的整数。任务是打印集合中所有成对连续元素的绝对差值。使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)访问一组大小为 N 的成对连续对。

**示例:**

> **输入:** s = {8，5，4，3，15，20}
> 
> **输出:** 1 1 3 7 5
> 
> **说明:**
> 
> 设定为:3 4 5 8 15 20
> 4 和 3 的差为 1
> 5 和 4 的差为 1
> 8 和 5 的差为 3
> 15 和 8 的差为 7
> 20 和 15 的差为 5
> 
> **输入:** s = {5，10，15，20}
> 
> **输出:** 5 5 5
> 
> **说明:**
> 设定为:5 10 15 20
> 10 和 5 的差为 5
> 15 和 10 的差为 5
> 20 和 15 的差为 5

文章[数组中所有成对连续元素的绝对差](https://www.geeksforgeeks.org/absolute-difference-of-all-pairwise-consecutive-elements-in-an-array/)涵盖了寻找数组中所有成对连续元素的绝对差的方法。

**方法:**这个问题可以使用 [**两指针算法**](https://www.geeksforgeeks.org/two-pointers-technique/) 来解决。我们将使用迭代器作为两个指针来迭代集合并检查给定的条件。按照以下步骤理解上述问题的解决方案:

1.  声明两个迭代器 **itr1 和 itr2** ，它们都指向集合的开始元素。
2.  在循环开始时增加 **itr2** ，即 **itr2++** 。
3.  减去 itr1 和 itr2 所指向的值，即*** itr 2 –* itr 1**。
4.  循环结束时递增 itr1，这意味着 ***itr1++。**
5.  如果 itr2 到达集合的末尾，则中断循环并退出。

在 [C++](http://www.geeksforgeeks.org/c-plus-plus/) 中，集合元素被排序，在存储到内存中之前，重复的元素被移除。因此，在下面的 C++程序中，成对连续元素之间的差异是在排序的集合上计算的，如上面的例子中所解释的。

下面是上述方法的 C++程序实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// difference of consecutive pairwise
// elements in a set
void display_difference(set<int> s)
{
    // Declaring the set iterator
    set<int>::iterator itr;

    // Printing difference between
    // consecutive elements in a set
    set<int>::iterator itr1 = s.begin();
    set<int>::iterator itr2 = s.begin();
    while (1) {
        itr2++;
        if (itr2 == s.end())
            break;
        cout << (*itr2 - *itr1) << " ";
        itr1++;
    }
}
// Driver code
int main()
{
    // Declaring the set
    set<int> s{ 8, 5, 4, 3, 15, 20 };

    // Invoking the display_difference()
    // function
    display_difference(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.TreeSet;

// Function to calculate the
// difference of consecutive pairwise
// elements in a set
class GFG {
  static void display_difference(HashSet<Integer> S) {

    // Printing difference between
    // consecutive elements in a set
    TreeSet<Integer> s = new TreeSet<Integer>(S);

    int itr1 = 0;
    int itr2 = 0;
    while (true) {
      itr2 += 1;
      ;
      if (itr2 >= s.size()) {
        break;
      }
      List<Integer> temp = new ArrayList<Integer>();
      temp.addAll(s);
      System.out.print((temp.get(itr2) - temp.get(itr1)) + " ");
      itr1 += 1;
    }
  }

  // Driver code

  public static void main(String args[])
  {

    // Declaring the set
    HashSet<Integer> s = new HashSet<Integer>();
    s.add(8);
    s.add(5);
    s.add(4);
    s.add(3);
    s.add(15);
    s.add(20);

    // Invoking the display_difference()
    // function
    display_difference(s);

  }
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to calculate the
# difference of consecutive pairwise
# elements in a set
def display_difference(s):

    # Printing difference between
    # consecutive elements in a set
    itr1 = 0
    itr2 = 0
    while (1):
        itr2 += 1
        if (itr2 >= len(s)):
            break
        print((list(s)[itr2] - list(s)[itr1]), end=" ")
        itr1 += 1

# Driver code
if __name__ == "__main__":

    # Declaring the set
    s = set([8, 5, 4, 3, 15, 20])

    # Invoking the display_difference()
    # function
    display_difference(s)

    # This code is contributed by ukasp.
```

## C#

```
// C# program to implement
// the above approach

// Function to calculate the
// difference of consecutive pairwise
// elements in a set
using System;
using System.Collections.Generic;
public class GFG
{
  static void display_difference(HashSet<int> S)
  {

    // Printing difference between
    // consecutive elements in a set
    SortedSet<int> s = new SortedSet<int>(S);

    int itr1 = 0;
    int itr2 = 0;
    while (true) {
      itr2 += 1;
      ;
      if (itr2 >= s.Count) {
        break;
      }
      List<int> temp = new List<int>();
      temp.AddRange(s);
      Console.Write((temp[itr2] - temp[itr1]) + " ");
      itr1 += 1;
    }
  }

  // Driver code
  public static void Main(String []args)
  {

    // Declaring the set
    HashSet<int> s = new HashSet<int>();
    s.Add(8);
    s.Add(5);
    s.Add(4);
    s.Add(3);
    s.Add(15);
    s.Add(20);

    // Invoking the display_difference()
    // function
    display_difference(s);
  }
}

// This code is contributed by Rajput-Ji.
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to calculate the
// difference of consecutive pairwise
// elements in a set
function display_difference(s) {

    // Printing difference between
    // consecutive elements in a set
    s = new Set([...s].sort((a, b) => a - b));

    let itr1 = 0
    let itr2 = 0
    while (1) {
        itr2 += 1
        if (itr2 >= s.size) {
            break
        }
        document.write(([...s][itr2] - [...s][itr1]) + " ")
        itr1 += 1
    }
}

// Driver code

// Declaring the set
let s = new Set([8, 5, 4, 3, 15, 20]);

// Invoking the display_difference()
// function
display_difference(s)

// This code is contributed by Saurabh Jaiswal
</script>
```

**输出:**

> 1 1 3 7 5

**时间复杂度:**O(n)
T3】辅助空间: O(n)