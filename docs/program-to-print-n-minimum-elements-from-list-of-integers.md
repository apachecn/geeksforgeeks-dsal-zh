# 从整数列表中打印 N 个最小元素的程序

> 原文:[https://www . geesforgeks . org/program-to-print-n-从整数列表中选择最小元素/](https://www.geeksforgeeks.org/program-to-print-n-minimum-elements-from-list-of-integers/)

给定一个整数列表，任务是生成另一个包含 N 个最小元素的列表。

**示例:**

```
Input: {23, 1, 6, 2, 90}
Output: {1, 2}

Input: {34, 21, 56, 42, 89, 90, -1}
Output: {-1, 21}
```

**方法:**想法是使用[中使用的概念，在数组](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)中找到最小和第二小的元素。

*   首先，在给定的列表中找到最小的数字。
*   然后将当前的最小元素添加到另一个包含 N 个最小元素的列表中。
*   从给定列表中移除当前最小元素。
*   继续相同的过程，直到找到 N 个最小元素。

下面是上述方法的实现:

## C++

```
// C++ program to find N
// minimum elements
#include <bits/stdc++.h>
using namespace std;

void Nminelements(vector<int>list1, int N)
{
    vector<int> final_list;
    int n = list1.size();
    for (int i = 0; i < N; i++)
    {
        int min1 = 9999999;
        for (int j = 0; j < n; j++)
        {
            if (list1[j] < min1)
                min1 = list1[j];
        }

        // remove minimum element
        // from list so that it do
        // not come in calculation again        
        list1.erase(remove(list1.begin(),
                           list1.end(), min1),
                           list1.end());
        final_list.push_back(min1);
    }
    for(int i = 0; i < final_list.size(); i++)
    cout << final_list[i] << " ";
}

// Driver code
int main()
{
    vector<int> list1 = {4, 78, 34, 10,
                         8, 21, 11, 231};
    int N = 2;
    Nminelements(list1, N);
}

// This code is contributed by Subhadeep
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N
// minimum elements
import java.io.*;
import java.util.*;

class GFG{

static void Nminelements(ArrayList<Integer> list1, int N)
{
    ArrayList<Integer> final_list = new ArrayList<Integer>();

    for(int i = 0; i < N; i++)
    {
        int min1 = 9999999;
        int index = 0;
        for(int j = 0; j < list1.size(); j++)
        {
            if ((int)list1.get(j) < min1)
            {    min1 = (int)list1.get(j);
                index = j;
            }
        }

        // Remove minimum element
        // from list so that it do
        // not come in calculation again
        list1.remove(index);
        final_list.add(min1);
    }
    for(int i = 0; i < final_list.size(); i++)
        System.out.print(final_list.get(i) + " ");
}

// Driver code
public static void main (String[] args)
{
    ArrayList<Integer> list1 = new ArrayList<Integer>(
        Arrays.asList(4, 78, 34, 10, 8, 21, 11, 231 ));
    int N = 2;

    Nminelements(list1, N);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to find N minimum elements
def Nminelements(list1, N):
    final_list =[];

    for i in range(0, N):   
        min1 = 9999999;

        for j in range(len(list1)):     
            if list1[j]<min1:
                min1 = list1[j];

        # remove minimum element from list so
        # that it do not come in calculation again        
        list1.remove(min1);
        final_list.append(min1)

    print(final_list)

# Driver code
list1 = [4, 78, 34, 10, 8, 21, 11, 231];
N = 2;
Nminelements(list1, N)
```

## C#

```
// C# program to find N
// minimum elements
using System;
using System.Collections;

class GFG{

static void Nminelements(ArrayList list1, int N)
{
    ArrayList final_list = new ArrayList();

    for(int i = 0; i < N; i++)
    {
        int min1 = 9999999;
        for(int j = 0; j < list1.Count; j++)
        {
            if ((int)list1[j] < min1)
                min1 = (int)list1[j];
        }

        // Remove minimum element
        // from list so that it do
        // not come in calculation again
        list1.Remove(min1);

        final_list.Add(min1);
    }
    for(int i = 0; i < final_list.Count; i++)
        Console.Write(final_list[i] + " ");
}

// Driver code
public static void Main()
{
    ArrayList list1 = new ArrayList(){ 4, 78, 34, 10,
                                       8, 21, 11, 231 };
    int N = 2;

    Nminelements(list1, N);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// Javascript program to find N
// minimum elements

function Nminelements(list1,N)
{
    let final_list = [];

    for(let i = 0; i < N; i++)
    {
        let min1 = 9999999;
        let index = 0;
        for(let j = 0; j < list1.length; j++)
        {
            if (list1[j] < min1)
            {    min1 = list1[j];
                index = j;
            }
        }

        // Remove minimum element
        // from list so that it do
        // not come in calculation again
        list1.splice(index, 1);
        final_list.push(min1);
    }
    for(let i = 0; i < final_list.length; i++)
        document.write(final_list[i] + " ");
}

// Driver code
let list1=[4, 78, 34, 10, 8, 21, 11, 231 ];
let N = 2;
Nminelements(list1, N);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
4 8
```