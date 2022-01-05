# 数组中每个元素右侧的天花板

> 原文:[https://www . geesforgeks . org/数组中每个元素右侧天花板/](https://www.geeksforgeeks.org/ceiling-in-right-side-for-every-element-in-an-array/)

给定一个整数数组，为每个元素找到最接近的大元素。如果没有更大的元素，则打印-1

示例:

> 输入:arr[] = {10，5，11，10，20，12}
> 输出:10 10 12 12 -1 -1
> 
> 输入:arr[] = {50，20，200，100，30}
> 输出:100 30 -1 -1 -1

一个简单的解决方案是运行两个嵌套循环。我们一个接一个地挑选外部元素。对于每个拾取的元素，我们遍历右侧数组并找到最近的大于或等于的元素。该方案的时间复杂度为 O(n*n)

一个**更好的解决方案**是使用排序。我们对所有元素进行排序，然后对每个元素向右遍历，直到找到一个更大的元素(请注意，一个元素可以多次出现)。

一个**高效的解决方案**是使用自平衡 BST(实现为 C++中的[集和 Java 中的](https://www.geeksforgeeks.org/set-in-cpp-stl/)[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/))。在自平衡 BST 中，我们可以在 O(Log n)时间内完成插入和上限操作。

## C++

```
// C++ program to find ceiling on right side for
// every element.
#include <bits/stdc++.h>
using namespace std;

void closestGreater(int arr[], int n)
{
    set<int> s;
    vector<int> ceilings;

    // Find smallest greater or equal element
    // for every array element
    for (int i = n - 1; i >= 0; i--) {
        auto greater = s.lower_bound(arr[i]);
        if (greater == s.end())
            ceilings.push_back(-1);
        else
            ceilings.push_back(*greater);
        s.insert(arr[i]);
    }

    for (int i = n - 1; i >= 0; i--)
        cout << ceilings[i] << " ";
}

int main()
{
    int arr[] = { 50, 20, 200, 100, 30 };
    closestGreater(arr, 5);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find ceiling on right side for
// every element.
import java.util.*;

class TreeSetDemo {
    public static void closestGreater(int[] arr)
    {
        int n = arr.length;
        TreeSet<Integer> ts = new TreeSet<Integer>();
        ArrayList<Integer> ceilings = new ArrayList<Integer>(n);

        // Find smallest greater or equal element
        // for every array element
        for (int i = n - 1; i >= 0; i--) {
            Integer greater = ts.ceiling(arr[i]);
            if (greater == null)
                ceilings.add(-1);
            else
                ceilings.add(greater);
            ts.add(arr[i]);
        }

        for (int i = n - 1; i >= 0; i--)
            System.out.print(ceilings.get(i) + " ");
    }

    public static void main(String[] args)
    {
        int[] arr = { 50, 20, 200, 100, 30 };
        closestGreater(arr);
    }
}
```

**Output:**

```
100 30 -1 -1 -1

```

时间复杂度:0(对数 n)