# 在数组中找到其和已经存在于数组中的对

> 原文:[https://www . geesforgeks . org/find-pairs-in-array-其和已经存在于数组中/](https://www.geeksforgeeks.org/find-pairs-in-array-whose-sums-already-exist-in-array/)

给定一个由 n 个不同的正元素组成的数组，任务是找到其和已经存在于给定数组中的对。
**例:**

```
Input : arr[] = {2, 8, 7, 1, 5};
Output : 2 5
         7 1    

Input : arr[] = {7, 8, 5, 9, 11};
Output : Not Exist
```

一种**天真的方法**是运行三个循环来寻找其和存在于数组中的对。

## C++

```
// A simple C++ program to find pair whose sum
// already exists in array
#include <bits/stdc++.h>
using namespace std;

// Function to find pair whose sum exists in arr[]
void findPair(int arr[], int n)
{
    bool found = false;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = 0; k < n; k++) {
                if (arr[i] + arr[j] == arr[k]) {
                    cout << arr[i] << " " << arr[j] << endl;
                    found = true;
                }
            }
        }
    }

    if (found == false)
        cout << "Not exist" << endl;
}

// Driven code
int main()
{
    int arr[] = { 10, 4, 8, 13, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findPair(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to find
// pair whose sum already exists
// in array
import java.io.*;

public class GFG {

    // Function to find pair whose
    // sum exists in arr[]
    static void findPair(int[] arr, int n)
    {
        boolean found = false;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = 0; k < n; k++) {
                    if (arr[i] + arr[j] == arr[k]) {
                        System.out.println(arr[i] +
                                      " " + arr[j]);
                        found = true;
                    }
                }
            }
        }

        if (found == false)
            System.out.println("Not exist");
    }

    // Driver code
    static public void main(String[] args)
    {
        int[] arr = {10, 4, 8, 13, 5};
        int n = arr.length;
        findPair(arr, n);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# A simple python program to find pair
# whose sum already exists in array

# Function to find pair whose sum
# exists in arr[]
def findPair(arr, n):
    found = False
    for i in range(0, n):
        for j in range(i + 1, n):
            for k in range(0, n):
                if (arr[i] + arr[j] == arr[k]):
                    print(arr[i], arr[j])
                    found = True

    if (found == False):
        print("Not exist")

# Driver code
if __name__ == '__main__':
    arr = [ 10, 4, 8, 13, 5 ]
    n = len(arr)
    findPair(arr, n)

# This code contributed by 29AjayKumar
```

## C#

```
// A simple C# program to find
// pair whose sum already exists
// in array
using System;

public class GFG {

    // Function to find pair whose
    // sum exists in arr[]
    static void findPair(int[] arr, int n)
    {
        bool found = false;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = 0; k < n; k++) {
                    if (arr[i] + arr[j] == arr[k]) {
                        Console.WriteLine(arr[i] +
                                      " " + arr[j]);
                        found = true;
                    }
                }
            }
        }

        if (found == false)
            Console.WriteLine("Not exist");
    }

    // Driver code
    static public void Main(String []args)
    {
        int[] arr = {10, 4, 8, 13, 5};
        int n = arr.Length;
        findPair(arr, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple php program to
// find pair whose sum
// already exists in array

// Function to find pair whose
// sum exists in arr[]
function findPair($arr, $n)
{
    $found = false;
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = $i + 1; $j < $n; $j++)
        {
            for ($k = 0; $k < $n; $k++)
            {
                if ($arr[$i] + $arr[$j] == $arr[$k])
                {
                    echo $arr[$i] , " " , $arr[$j] ;
                    $found = true;
                }
            }
        }
    }

    if ($found == false)
        echo "Not exist" ;
}

// Driver code
$arr = array( 10, 4, 8, 13, 5 );
$n = sizeof($arr) / sizeof($arr[0]);
findPair($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// A simple Javascript program to find
// pair whose sum already exists
// in array

    // Function to find pair whose
    // sum exists in arr[]
    function findPair(arr,n)
    {
        let found = false;
        for (let i = 0; i < n; i++) {
            for (let j = i + 1; j < n; j++) {
                for (let k = 0; k < n; k++) {
                    if (arr[i] + arr[j] == arr[k]) {
                        document.write(arr[i] +
                                      " " + arr[j]+"<br>");
                        found = true;
                    }
                }
            }
        }

        if (found == false)
            document.write("Not exist");
    }

    // Driver code
    let arr=[10, 4, 8, 13, 5];
    let n = arr.length;
    findPair(arr, n);

// This code is contributed by patel2127
</script>
```

**输出:**

```
8 5
```

一个**高效的解决方案**是将所有元素存储在一个哈希表中(【C++ 中的[无序 _ 集合)，并逐一检查所有对，并检查其和是否存在于集合中。如果它存在于集合中，则打印对。如果在阵列中没有找到配对，则打印不存在。](https://www.geeksforgeeks.org/unorderd_set-stl-uses/) 

## C++

```
// C++ program to find pair whose sum already
// exists in array
#include <bits/stdc++.h>
using namespace std;

// Function to find pair whose sum exists in arr[]
void findPair(int arr[], int n)
{
    // Hash to store all element of array
    unordered_set<int> s;
    for (int i = 0; i < n; i++)
        s.insert(arr[i]);

    bool found = false;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            // Check sum already exists or not
            if (s.find(arr[i] + arr[j]) != s.end()) {
                cout << arr[i] << " " << arr[j] << endl;
                found = true;
            }
        }
    }

    if (found == false)
        cout << "Not exist" << endl;
}

// Driven code
int main()
{
    int arr[] = { 10, 4, 8, 13, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findPair(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pair whose sum
// already exists in array
import java.util.*;
import java.lang.*;
import java.io.*;

class Getpairs {
    // Function to find pair whose sum
    // exists in arr[]
    public static void findPair(int[] arr, int n)
    {
        /* store all the array elements as a
        Hash value*/
        HashSet<Integer> s = new HashSet<Integer>();

        for (Integer i : arr) {
            s.add(i);
        }

        /* Run two loop and check for the sum
    in the Hashset*/
        /* if not a single pair exist then found
    will be false else true*/
        boolean found = false;

        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                int sum = arr[i] + arr[j];
                if (s.contains(sum)) {
                    /* if the sum is present in
                 hashset then found become
                true*/
                    found = true;

                    System.out.println(arr[i] + " "
                                       + arr[j]);
                }
            }
        }

        if (found == false)
            System.out.println("Not Exist ");
    }

    // driver function
    public static void main(String args[])
    {
        int[] arr = { 10, 4, 8, 13, 5 };
        int n = arr.length;
        findPair(arr, n);
    }
}

// This code is contributed by Smarak Chopdar
```

## 蟒蛇 3

```
# Python3 program to find pair whose
# sum already exist in arrar

# Function to find pair whose
# sum sxists in arr[]
def findPair(arr, n):

    # hash to store all element of array
    s = {i : 1 for i in arr}

    found = False

    for i in range(n):
        for j in range(i + 1, n):

            # check if sum already exists or not
            if arr[i] + arr[j] in s.keys():
                print(arr[i], arr[j])
                found = True
    if found == False:
        print("Not exist")

# Driver code
arr = [10, 4, 8, 13, 5]

n = len(arr)

findPair(arr, n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find pair whose sum
// already exists in array
using System;
using System.Collections.Generic;

class Getpairs
{
    // Function to find pair whose sum
    // exists in arr[]
    public static void findPair(int[] arr, int n)
    {
        /* store all the array elements as a
        Hash value*/
        HashSet<int> s = new HashSet<int>();

        foreach (int i in arr)
        {
            s.Add(i);
        }

        /* Run two loop and check for the sum
    in the Hashset*/
        /* if not a single pair exist then found
    will be false else true*/
        bool found = false;

        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                int sum = arr[i] + arr[j];
                if (s.Contains(sum))
                {
                    /* if the sum is present in
                    hashset then found become
                    true*/
                    found = true;

                    Console.WriteLine(arr[i] + " "
                                    + arr[j]);
                }
            }
        }

        if (found == false)
            Console.WriteLine("Not Exist ");
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 10, 4, 8, 13, 5 };
        int n = arr.Length;
        findPair(arr, n);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find pair whose sum
// already exists in array   

    // Function to find pair whose sum
    // exists in arr[]
    function findPair(arr,n)
    {
        /* store all the array elements as a
        Hash value*/
        let s = new Set();

        for (let i=0;i<arr.length;i++) {
            s.add(arr[i]);
        }

        /* Run two loop and check for the sum
    in the Hashset*/
        /* if not a single pair exist then found
    will be false else true*/
        let found = false;

        for (let i = 0; i < n - 1; i++) {
            for (let j = i + 1; j < n; j++) {
                let sum = arr[i] + arr[j];
                if (s.has(sum)) {
                    /* if the sum is present in
                 hashset then found become
                true*/
                    found = true;

                    document.write(arr[i] + " "
                                  + arr[j]+"<br>");
                }
            }
        }

        if (found == false)
            document.write("Not Exist ");
    }

    // driver function
    let arr=[10, 4, 8, 13, 5 ];
    let n = arr.length;
    findPair(arr, n);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
8 5
```

**时间复杂度:** O(n <sup>2</sup> )
本文由**丹麦语 _RAZA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。