# 计算数组元素的频率

> 原文:[https://www . geesforgeks . org/counting-frequency-of-array-elements/](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

给定一个可能包含重复的数组，打印所有元素及其频率。

**例:**

```
Input :  arr[] = {10, 20, 20, 10, 10, 20, 5, 20}
Output : 10 3
         20 4
         5  1

Input : arr[] = {10, 20, 20}
Output : 10 1
         20 2 
```

一个**简单的解决方案**就是跑两个圈。对于每个项目计数次数，它都会发生。为了避免重复打印，请跟踪已处理的项目。

## c++

```
// CPP program to count frequencies of array items
#include <bits/stdc++.h>
using namespace std;

void countFreq(int arr[], int n)
{
    // Mark all array elements as not visited
    vector<bool> visited(n, false);

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++) {

        // Skip this element if already processed
        if (visited[i] == true)
            continue;

        // Count frequency
        int count = 1;
        for (int j = i + 1; j < n; j++) {
            if (arr[i] == arr[j]) {
                visited[j] = true;
                count++;
            }
        }
        cout << arr[i] << " " << count << endl;
    }
}

int main()
{
    int arr[] = { 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    countFreq(arr, n);
    return 0;
}
```

## Java

```
// Java program to count frequencies of array items
import java.util.Arrays;

class GFG
{
public static void countFreq(int arr[], int n)
{
    boolean visited[] = new boolean[n];

    Arrays.fill(visited, false);

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++) {

        // Skip this element if already processed
        if (visited[i] == true)
            continue;

        // Count frequency
        int count = 1;
        for (int j = i + 1; j < n; j++) {
            if (arr[i] == arr[j]) {
                visited[j] = true;
                count++;
            }
        }
        System.out.println(arr[i] + " " + count);
    }
}

// Driver code
public static void main(String []args)
{
    int arr[] = new int[]{ 10, 20, 20, 10, 10, 20, 5, 20 };
    int n = arr.length;
    countFreq(arr, n);
}
}

// This code contributed by Adarsh_Verma.
```

## python 3

```
# Python 3 program to count frequencies
# of array items
def countFreq(arr, n):

    # Mark all array elements as not visited
    visited = [False for i in range(n)]

    # Traverse through array elements
    # and count frequencies
    for i in range(n):

        # Skip this element if already
        # processed
        if (visited[i] == True):
            continue

        # Count frequency
        count = 1
        for j in range(i + 1, n, 1):
            if (arr[i] == arr[j]):
                visited[j] = True
                count += 1

        print(arr[i], count)

# Driver Code
if __name__ == '__main__':
    arr = [10, 20, 20, 10, 10, 20, 5, 20]
    n = len(arr)
    countFreq(arr, n)

# This code is contributed by
# Shashank_Sharma
```

## c#

```
// C# program to count frequencies of array items
using System;

class GFG
{
    public static void countFreq(int []arr, int n)
    {
        bool []visited = new bool[n];

        // Traverse through array elements and
        // count frequencies
        for (int i = 0; i < n; i++)
        {

            // Skip this element if already processed
            if (visited[i] == true)
                continue;

            // Count frequency
            int count = 1;
            for (int j = i + 1; j < n; j++)
            {
                if (arr[i] == arr[j])
                {
                    visited[j] = true;
                    count++;
                }
            }
            Console.WriteLine(arr[i] + " " + count);
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = new int[]{ 10, 20, 20, 10, 10, 20, 5, 20 };
        int n = arr.Length;
        countFreq(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## Javascript

```
<script>

// JavaScript program to count frequencies of array items

function countFreq(arr, n)
{
    let visited = Array.from({length: n}, (_, i) => false);

    // Traverse through array elements and
    // count frequencies
    for (let i = 0; i < n; i++) {

        // Skip this element if already processed
        if (visited[i] == true)
            continue;

        // Count frequency
        let count = 1;
        for (let j = i + 1; j < n; j++) {
            if (arr[i] == arr[j]) {
                visited[j] = true;
                count++;
            }
        }
           document.write(arr[i] + " " + count + "<br/>");
    }
}

// Driver Code

    let arr = [ 10, 20, 20, 10, 10, 20, 5, 20 ];
    let n = arr.length;
    countFreq(arr, n);   

</script>
```

**输出:**

```
10 3
20 4
5 1
```