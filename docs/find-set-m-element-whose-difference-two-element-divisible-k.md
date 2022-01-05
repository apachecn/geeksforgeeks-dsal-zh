# 求任意两个元素之差可被 k 整除的 m 元素集合

> 原文:[https://www . geesforgeks . org/find-set-m-element-what-difference-two-element-整除-k/](https://www.geeksforgeeks.org/find-set-m-element-whose-difference-two-element-divisible-k/)

给定一个由 n 个正整数和一个正整数 k 组成的数组，找到一组正好为 m 的元素，使得任意两个元素之差等于 k。

**示例:**

```
Input : arr[] = {4, 7, 10, 6, 9},
        k = 3, m = 3
Output : Yes 
         4 7 10

Input : arr[] = {4, 7, 10, 6, 9}, 
        k = 12, m = 4
Output : No

Input : arr[] = {4, 7, 10, 6, 9}, 
        k = 3, m = 4
Output : No
```

**方法:**要解决这个问题，只需记录一个元素被 k 除时的余数。创建一个大小为 k 的多维数组余数集[][]，其索引显示余数，当被 k 除时，该数组的元素将按照它们相应的余数排列。例如，如果 arr[i] % k = 3，那么 arr[i]将是所有元素的余数集[3]的元素，依此类推。现在，遍历余数集，可以很容易地得到一个大于或等于所需大小 m(如果存在)的集。当然，集合中任何元素的差都可以被 k 整除。

## C++

```
// C++ program for finding remainder set
#include <bits/stdc++.h>
using namespace std;

// function to find remainder set
void findSet(int arr[], int n, int k, int m) {

  vector<int> remainder_set[k];

  // calculate remainder set array
  // and push element as per their remainder
  for (int i = 0; i < n; i++) {
    int rem = arr[i] % k;
    remainder_set[rem].push_back(arr[i]);
  }

  // check whether sizeof any remainder set
  // is equal or greater than m
  for (int i = 0; i < k; i++) {
    if (remainder_set[i].size() >= m) {
      cout << "Yes \n";
      for (int j = 0; j < m; j++)
        cout << remainder_set[i][j] << " ";     
      return;
    }
  }

  cout << "No";
}

// driver program
int main() {
  int arr[] = {5, 8, 9, 12, 13, 7, 11, 15};
  int k = 4;
  int m = 3;
  int n = sizeof(arr) / sizeof(arr[0]);
  findSet(arr, n, k, m);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding remainder set
import java.util.*;
class GFG
{

// function to find remainder set
static void findSet(int arr[], int n,
                    int k, int m)
{
    Vector<Integer> []remainder_set = new Vector[k];
    for (int i = 0; i < k; i++)
    {
        remainder_set[i] = new Vector<Integer>();
    }

    // calculate remainder set array
    // and push element as per their remainder
    for (int i = 0; i < n; i++)
    {
        int rem = arr[i] % k;
        remainder_set[rem].add(arr[i]);
    }

    // check whether sizeof any remainder set
    // is equal or greater than m
    for (int i = 0; i < k; i++)
    {
        if (remainder_set[i].size() >= m)
        {
            System.out.println("Yes");
            for (int j = 0; j < m; j++)
                    System.out.print(remainder_set[i].get(j) + " ");    
            return;
        }
    }
    System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {5, 8, 9, 12, 13, 7, 11, 15};
    int k = 4;
    int m = 3;
    int n = arr.length;
    findSet(arr, n, k, m);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find exactly m-element set
# where difference of any two is divisible by k
def findSet( arr, k, m):

    arr_size = len(arr);
    remainder_set=[0]*k;

    # initialize remainder set with blank array
    for i in range(k):
        remainder_set[i] = [];

    # calculate remainder set array
    # and push element as per their reainder
    for i in range(arr_size):
        rem = arr[i] % k;
        remainder_set[rem].append(arr[i]);

    # check whether sizeof any remainder set
    # is equal or greater than m
    for i in range(k):
        # if size exist then print yes and all elements
        if(len(remainder_set[i]) >= m):
            print("Yes");
            for j in range(m):
                print(remainder_set[i][j],end="");
                print(" ",end="");

            # return if remainder set found
            return;

    # print no if no remiander set found
    print("No");

arr = [5, 8, 9, 12, 13, 7, 11, 15];
k = 4; # constant k
m = 3; # size of set required
findSet(arr, k, m);

# This code is contributed by mits.
```

## C#

```
// C# program for finding
// remainder set
using System;
using System.Collections.Generic;

class GFG
{
// function to find
// remainder set
static void findSet(int []arr, int n,
                    int k, int m)
{
    List<int>[] remainder_set =
                       new List<int>[k];
    for(int i = 0; i < k; i++)
        remainder_set[i] =
                       new List<int>();

    // calculate remainder set
    // array and push element
    // as per their remainder
    for (int i = 0; i < n; i++)
    {
        int rem = arr[i] % k;
        remainder_set[rem].Add(arr[i]);
    }

    // check whether sizeof
    // any remainder set is
    // equal or greater than m
    for (int i = 0; i < k; i++)
    {
        if (remainder_set[i].Count >= m)
        {
        Console.Write("Yes \n");
        for (int j = 0; j < m; j++)
            Console.Write(remainder_set[i][j] +
                                          " ");    
        return;
        }
    }

    Console.Write("No");
    }

// Driver Code
static void Main()
{
    int []arr = new int[]{5, 8, 9, 12,
                          13, 7, 11, 15};
    int k = 4;
    int m = 3;
    int n = arr.Length;
    findSet(arr, n, k, m);
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find exactly m-element set
// where difference of any two is divisible by k
function findSet( $arr, $k, $m)
{
    $arr_size = sizeof($arr);

    // initialize remainder set with blank array
    for ($i = 0; $i < $k; $i++)
    {
        $remainder_set[$i] = array();
    }

    // calculate remainder set array
    // and push element as per their reainder
    for ($i = 0; $i < $arr_size; $i++)
    {
        $rem = $arr[$i] % $k;
        array_push($remainder_set[$rem], $arr[$i]);
    }

    // check whether sizeof any remainder set
    // is equal or greater than m
    for($i = 0; $i < $k; $i++)
    {
        // if size exist then print yes and all elements
        if(sizeof($remainder_set[$i]) >= $m)
        {
            print("Yes\n");
            for($j = 0; $j < $m; $j++)
            {
                print($remainder_set[$i][$j]);
                print(" ");
            }

            // return if remainder set found
            return;
        }
    }

    // print no if no remiander set found
    print("No");
}

$arr = array(5, 8, 9, 12, 13, 7, 11, 15);
$k = 4; // constant k
$m = 3; // size of set required
findset($arr, $k, $m);
?>
```

## java 描述语言

```
<script>

// Javascript program to find exactly m-element set
// where difference of any two is divisible by k

function findSet(arr, k, m)
{
    let arr_size = arr.length;
    let remainder_set = []
    // initialize remainder set with blank array
    for (let i = 0; i < k; i++)
    {
        remainder_set[i] = new Array();
    }

    // calculate remainder set array
    // and push element as per their reainder
    for (let i = 0; i < arr_size; i++)
    {
        let rem = arr[i] % k;
        remainder_set[rem].push(arr[i]);
    }

    // check whether sizeof any remainder set
    // is equal or greater than m
    for(let i = 0; i < k; i++)
    {
        // if size exist then print yes and all elements
        if(remainder_set[i].length >= m)
        {
            document.write("Yes<br>");
            for(let j = 0; j < m; j++)
            {
                document.write(remainder_set[i][j]);
                document.write(" ");
            }

            // return if remainder set found
            return;
        }
    }

    // print no if no remiander set found
    document.write("No");
}

let arr = [5, 8, 9, 12, 13, 7, 11, 15];
let k = 4; // constant k
let m = 3; // size of set required
findSet(arr, k, m);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
Yes 
5 9 13
```