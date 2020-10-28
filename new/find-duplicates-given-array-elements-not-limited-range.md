# 当元素不限于范围时，查找给定数组中的重复项

> 原文：[https://www.geeksforgeeks.org/find-duplicates-given-array-elements-not-limited-range/](https://www.geeksforgeeks.org/find-duplicates-given-array-elements-not-limited-range/)

给定 n 个整数数组。 任务是在给定数组中打印重复项。 如果没有重复，则打印-1。

**范例**：

```
Input: {2, 10,10, 100, 2, 10, 11,2,11,2}
Output: 2 10 11

Input: {5, 40, 1, 40, 100000, 1, 5, 1}
Output: 5 40 1

```

**注意**：可以按任何顺序打印重复的元素。

**简单方法**：想法是使用嵌套循环，并对每个元素检查数组中元素是否存在多次。 如果存在，则将其存储在哈希图中。 否则，请继续检查其他元素。

下面是上述方法的实现：

## Java

```java

// Java implementation of the
// above approach

import java.util.ArrayList;

public class GFG {

    // Function to find the Duplicates,
    // if duplicate occurs 2 times or
    // more than 2 times in
    // array so, it will print duplicate
    // value only once at output
    static void findDuplicates(
      int arr[], int len)
    {

        // initialize ifPresent as false
        boolean ifPresent = false;

        // ArrayList to store the output
        ArrayList<Integer> al = new ArrayList<Integer>();

        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                if (arr[i] == arr[j]) {
                    // checking if element is
                    // present in the ArrayList
                    // or not if present then break
                    if (al.contains(arr[i])) {
                        break;
                    }

                    // if element is not present in the
                    // ArrayList then add it to ArrayList
                    // and make ifPresent at true
                    else {
                        al.add(arr[i]);
                        ifPresent = true;
                    }
                }
            }
        }

        // if duplicates is present
        // then print ArrayList
        if (ifPresent == true) {

            System.out.print(al + " ");
        }
        else {
            System.out.print(
                "No duplicates present in arrays");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        int arr[] = { 12, 11, 40, 12, 5, 6, 5, 12, 11 };
        int n = arr.length;

        findDuplicates(arr, n);
    }
}

```

**Output**

```
[12, 11, 5] 
```

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（N）*

**有效方法**：使用 [unordered_map](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) 进行哈希处理。 打印每个元素的出现频率和频率大于 1 的元素。 **unordered_map** 因为整数范围未知而被使用。 对于 Python，使用字典将数字存储为键，将频率存储为值。 字典可以用作整数范围是未知的。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find
// duplicates in the given array
#include <bits/stdc++.h>
using namespace std;

// function to find and print duplicates
void printDuplicates(int arr[], int n)
{
    // unordered_map to store frequencies
    unordered_map<int, int> freq;
    for (int i=0; i<n; i++)
        freq[arr[i]]++;

    bool dup = false;
    unordered_map<int, int>:: iterator itr;
    for (itr=freq.begin(); itr!=freq.end(); itr++)
    {
        // if frequency is more than 1
        // print the element
        if (itr->second > 1)
        {
            cout << itr->first << " ";
            dup = true;
        }
    }

    // no duplicates present
    if (dup == false)
        cout << "-1";
}

// Driver program to test above
int main()
{
    int arr[] = {12, 11, 40, 12, 5, 6, 5, 12, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    printDuplicates(arr, n);
    return 0;
}

```

## Java

```java

// Java program to find
// duplicates in the given array
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;

public class FindDuplicatedInArray
{
    // Driver program
    public static void main(String[] args)
    {
        int arr[] = {12, 11, 40, 12, 5, 6, 5, 12, 11};
        int n = arr.length;
        printDuplicates(arr, n);
    }
    // function to find and print duplicates
    private static void printDuplicates(int[] arr, int n) 
    {
        Map<Integer,Integer> map = new HashMap<>();
        int count = 0;
        boolean dup = false;
        for(int i = 0; i < n; i++){
            if(map.containsKey(arr[i])){
                count = map.get(arr[i]);
                map.put(arr[i], count + 1);
            }
            else{
                map.put(arr[i], 1);
            }
        }

        for(Entry<Integer,Integer> entry : map.entrySet())
        {
            // if frequency is more than 1
            // print the element
            if(entry.getValue() > 1){
                System.out.print(entry.getKey()+ " ");
                dup = true;
            }
        }
        // no duplicates present
        if(!dup){
            System.out.println("-1");
        }
    }
}

```

## Python3

```py

# Python 3 code to find duplicates 
# using dictionary approach.
def printDuplicates(arr):
    dict = {}

    for ele in arr:
        try:
            dict[ele] += 1
        except:
            dict[ele] = 1

    for item in dict:

         # if frequency is more than 1
         # print the element
        if(dict[item] > 1):
            print(item, end=" ")

    print("\n")

# Driver Code
if __name__ == "__main__":
    list = [12, 11, 40, 12, 
            5, 6, 5, 12, 11]
    printDuplicates(list)

# This code is contributed
# by Sushil Bhile

```

## C#

```cs

// C# program to find 
// duplicates in the given array 
using System;
using System.Collections.Generic;

class GFG
{
    // function to find and print duplicates
    static void printDuplicates(int[] arr, int n)
    {
        Dictionary<int, 
                   int> map = new Dictionary<int, 
                                             int>();
        int count = 0;
        bool dup = false;
        for (int i = 0; i < n; i++)
        {
            if (map.ContainsKey(arr[i]))
            {
                count = map[arr[i]];
                map[arr[i]]++;
            }
            else
                map.Add(arr[i], 1);
        }

        foreach (KeyValuePair<int, 
                              int> entry in map)
        {
            // if frequency is more than 1 
            // print the element
            if (entry.Value > 1)
                Console.Write(entry.Key + " ");
            dup = true;
        }

        // no duplicates present
        if (!dup)
            Console.WriteLine("-1");
    }

    // Driver Code 
    public static void Main(String[] args)
    {
        int[] arr = { 12, 11, 40, 12, 
                     5, 6, 5, 12, 11 };
        int n = arr.Length;
        printDuplicates(arr, n);
    }
}

// This code is contributed by
// sanjeev2552

```

**Output**

```
5 12 11 
```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*

**相关文章**：

[打印给定整数数组的所有不同元素](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)

[查找 O（n）时间和 O（1）多余空间中的重复项| 设置 1](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/)

[在 O（n）中的数组中重复并通过使用 O（1）多余空间| Set-2](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-2/)

[打印输入字符串](https://www.geeksforgeeks.org/print-all-the-duplicates-in-the-input-string/)中的所有重复项

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

