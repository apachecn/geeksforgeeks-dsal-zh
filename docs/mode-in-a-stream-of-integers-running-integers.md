# 整数流中的模式(运行整数)

> 原文:[https://www . geesforgeks . org/整数流运行模式/整数/](https://www.geeksforgeeks.org/mode-in-a-stream-of-integers-running-integers/)

假设从数据流中读取整数。找到从第一个整数开始到最后一个整数为止所读取的所有元素的[](https://www.geeksforgeeks.org/mode/)****模式。****

> ****[**模式**](https://www.geeksforgeeks.org/mode/) 定义为出现时间最长的元素。如果两个或多个元素具有相同的最大频率，则取最后出现的元素。****

******示例:******

> ******输入:**流[] = {2，7，3，2，5 }
> T3】输出:2 7 3 2
> T6】解释:
> 运行流的模式计算如下:
> 模式({2}) = 2
> 模式({2，7}) = 7
> 模式({2，7，3}) = 3
> 模式({2，7，3，2}) = 2
> 模式({ 0****
> 
>  ******输入:**流[] = {3，5，9，9，2，3，3，4}
> 输出:3 5 9 9 3 3 3 3****

******逼近**:想法是使用[哈希映射](https://www.geeksforgeeks.org/hashing-data-structure/) 将元素映射到其[频率](https://www.geeksforgeeks.org/sort-elements-by-frequency/)。在逐个读取元素的同时，更新映射中元素的频率，并且还更新模式，该模式将是运行整数流的模式。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function that prints
// the Mode values
void findMode(int a[], int n)
{

    // Map used to mp integers
    // to its frequency
    map<int, int> mp; 

    // To store the maximum frequency
    int max = 0;

    // To store the element with
    // the maximum frequency
    int mode = 0;

    // Loop used to read the
    // elements one by one
    for(int i = 0; i < n; i++) 
    {

        // Updates the frequency of
        // that element
        mp[a[i]]++;

        // Checks for maximum Number
        // of occurrence
        if (mp[a[i]] >= max) 
        {

            // Updates the maximum frequency
            max = mp[a[i]];

            // Updates the Mode
            mode = a[i];
        }
        cout << mode << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 7, 3, 2, 5 };
    int n = sizeof(arr)/sizeof(arr[0]);

    // Function call
    findMode(arr, n);

    return 0;
} 

// This code is contributed by rutvik_56**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java implementation of the
// above approach

import java.util.*;

public class GFG {

    // Function that prints
    // the Mode values
    public static void findMode(int[] a, int n)
    {
        // Map used to map integers
        // to its frequency
        Map<Integer, Integer> map
            = new HashMap<>();

        // To store the maximum frequency
        int max = 0;

        // To store the element with
        // the maximum frequency
        int mode = 0;

        // Loop used to read the
        // elements one by one
        for (int i = 0; i < n; i++) {

            // Updates the frequency of
            // that element
            map.put(a[i],
                    map.getOrDefault(a[i], 0) + 1);

            // Checks for maximum Number
            // of occurrence
            if (map.get(a[i]) >= max) {

                // Updates the maximum frequency
                max = map.get(a[i]);

                // Updates the Mode
                mode = a[i];
            }

            System.out.print(mode);
            System.out.print(" ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, 7, 3, 2, 5 };

        int n = arr.length;

        // Function Call
        findMode(arr, n);
    }
}**
```

## ****蟒蛇 3****

```
**# Python3 implementation of the 
# above approach

# Function that prints 
# the Mode values 
def findMode(a, n):

    # Map used to mp integers 
    # to its frequency 
    mp = {}

    # To store the maximum frequency 
    max = 0

    # To store the element with 
    # the maximum frequency 
    mode = 0

    # Loop used to read the 
    # elements one by one 
    for i in range(n):
        if a[i] in mp:
            mp[a[i]] += 1
        else:
            mp[a[i]] = 1

        # Checks for maximum Number 
        # of occurrence     
        if (mp[a[i]] >= max):

            # Updates the maximum 
            # frequency 
            max = mp[a[i]]

            # Updates the Mode 
            mode = a[i]

        print(mode, end = " ")

# Driver Code
arr = [ 2, 7, 3, 2, 5 ]
n = len(arr)

# Function call 
findMode(arr,n)

# This code is contributed by divyeshrabadiya07**
```

## ****C#****

```
**// C# implementation of the
// above approach
using System;
using System.Collections.Generic;
class GFG{

    // Function that prints
    // the Mode values
    public static void findMode(int[] a, int n)
    {
        // Map used to map integers
        // to its frequency
        Dictionary<int, int> map = new Dictionary<int, int>();

        // To store the maximum frequency
        int max = 0;

        // To store the element with
        // the maximum frequency
        int mode = 0;

        // Loop used to read the
        // elements one by one
        for (int i = 0; i < n; i++) 
        {

            // Updates the frequency of
            // that element
            if (map.ContainsKey(a[i])) 
            {
                map[a[i]] = map[a[i]] + 1;
            }
            else
            {
                map.Add(a[i], 1);
            }

            // Checks for maximum Number
            // of occurrence
            if (map[a[i]] >= max) 
            {

                // Updates the maximum frequency
                max = map[a[i]];

                // Updates the Mode
                mode = a[i];
            }
            Console.Write(mode);
            Console.Write(" ");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = {2, 7, 3, 2, 5};
        int n = arr.Length;

        // Function Call
        findMode(arr, n);
    }
}

// This code is contributed by Amit Katiyar**
```

******Output:** 

```
2 7 3 2 2

```**** 

******性能分析:******

*   ******时间复杂度:** O(N)****
*   ******辅助空间:** O(N)****