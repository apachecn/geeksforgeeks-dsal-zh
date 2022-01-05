# 频率大于或等于某个元素的数组中的元素的和

> 原文:[https://www . geesforgeks . org/频率大于或等于该元素的数组元素总和/](https://www.geeksforgeeks.org/sum-of-elements-in-an-array-with-frequencies-greater-than-or-equal-to-that-element/)

给定一个由 N 个整数组成的数组 arr[]。任务是找出频率大于或等于数组中那个元素的元素的和。
**例**:

```
Input: arr[] = {2, 1, 1, 2, 1, 6}
Output: 3
The elements in the array are {2, 1, 6}
Where,
 2 appear 2 times which is greater than equal to 2 itself.
 1 appear 3 times which is greater than 1 itself.
 But 6 appears 1 time which is not greater than or equals to 6.
So, sum = 2 + 1 = 3.

Input: arr[] = {1, 2, 3, 3, 2, 3, 2, 3, 3}
Output: 6
```

**进场:**

*   遍历数组，将所有元素的频率存储在 C++中的[无序 _map 中](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)或任何其他编程语言中的等效数据结构中。
*   计算频率大于或等于该元素的元素的总和。

下面是上述方法的实现:

## C++

```
// C++ program to find sum of elements
// in an array having frequency greater
// than or equal to that element

#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of elements
// in an array having frequency greater
// than or equal to that element
int sumOfElements(int arr[], int n)
{
    bool prime[n + 1];
    int i, j;

    // Map is used to store
    // element frequencies
    unordered_map<int, int> m;
    for (i = 0; i < n; i++)
        m[arr[i]]++;

    int sum = 0;

    // Traverse the map using iterators
    for (auto it = m.begin(); it != m.end(); it++) {

        // Calculate the sum of elements
        // having frequencies greater than
        // or equal to the element itself
        if ((it->second) >= (it->first)) {
            sum += (it->first);
        }
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 3, 2, 3, 2, 3, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sumOfElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of elements
// in an array having frequency greater
// than or equal to that element
import java.util.*;
class Solution
{

// Function to return the sum of elements
// in an array having frequency greater
// than or equal to that element
static int sumOfElements(int arr[], int n)
{
    boolean prime[] = new boolean[n + 1];
    int i, j;

    // Map is used to store
    // element frequencies
    HashMap<Integer, Integer> m= new HashMap<Integer,Integer>();
    for (i = 0; i < n; i++)
        {
            if(m.get(arr[i])==null)
            m.put(arr[i],1);
            else
            m.put(arr[i],m.get(arr[i])+1);
        }

    int sum = 0;
        // Getting an iterator
        Iterator hmIterator = m.entrySet().iterator();

    // Traverse the map using iterators
        while (hmIterator.hasNext()) {
            Map.Entry mapElement = (Map.Entry)hmIterator.next();

        // Calculate the sum of elements
        // having frequencies greater than
        // or equal to the element itself
        if (((int)mapElement.getValue()) >= ((int)mapElement.getKey())) {
            sum += ((int)mapElement.getKey());
        }
    }

    return sum;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 3, 2, 3, 2, 3, 3 };
    int n = arr.length;

    System.out.println(sumOfElements(arr, n));

 }
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find sum of elements
# in an array having frequency greater
# than or equal to that element

# Function to return the sum of elements
# in an array having frequency greater
# than or equal to that element
def sumOfElements(arr, n) :

    # dictionary is used to store
    # element frequencies
    m = dict.fromkeys(arr, 0)

    for i in range(n) :
            m[arr[i]] += 1

    sum = 0

    # traverse the dictionary
    for key,value in m.items() :

        # Calculate the sum of elements
        # having frequencies greater than
        # or equal to the element itself
        if value >= key :
                sum += key

    return sum

# Driver code
if __name__ == "__main__" :

    arr = [1, 2, 3, 3, 2, 3, 2, 3, 3]
    n = len(arr)

    print(sumOfElements(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find sum of elements
// in an array having frequency greater
// than or equal to that element
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the sum of elements
    // in an array having frequency greater
    // than or equal to that element
    static int sumOfElements(int []arr, int n)
    {
        bool []prime = new bool[n + 1];
        int i;

        // Map is used to store
        // element frequencies
        Dictionary<int, int> m= new Dictionary<int,int>();
        for (i = 0; i < n; i++)
            {
                if(!m.ContainsKey(arr[i]))
                    m.Add(arr[i],1);
                else
                {
                    var val = m[arr[i]];
                    m.Remove(arr[i]);
                    m.Add(arr[i], val + 1);
                }

            }

            int sum = 0;
            // Calculate the sum of elements
            // having frequencies greater than
            // or equal to the element itself
            foreach(KeyValuePair<int, int> entry in m)
            {
                if(entry.Value >= entry.Key)
                {
                    sum+=entry.Key;
                }
            }

        return sum;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 1, 2, 3, 3, 2, 3, 2, 3, 3 };
        int n = arr.Length;

        Console.WriteLine(sumOfElements(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to find sum of elements
// in an array having frequency greater
// than or equal to that element

// Function to return the sum of elements
// in an array having frequency greater
// than or equal to that element
function sumOfElements(arr, n) {
    let prime = new Array(n + 1);
    let i, j;

    // Map is used to store
    // element frequencies
    let m = new Map();
    for (i = 0; i < n; i++) {
        if (m.has(arr[i])) {
            m.set(arr[i], m.get(arr[i]) + 1)
        } else[
            m.set(arr[i], 1)
        ]
    }

    let sum = 0;

    // Traverse the map using iterators
    for (let it of m) {

        // Calculate the sum of elements
        // having frequencies greater than
        // or equal to the element itself
        if ((it[1]) >= (it[0])) {
            sum += (it[0]);
        }
    }

    return sum;
}

// Driver code
let arr = [1, 2, 3, 3, 2, 3, 2, 3, 3];
let n = arr.length;

document.write(sumOfElements(arr, n));

// This code is contributed by gfgking.
</script>
```

**Output**

```
6
```