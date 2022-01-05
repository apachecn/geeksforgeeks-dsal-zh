# 求每次迭代后剩余棒的总和

> 原文:[https://www . geeksforgeeks . org/find-每次迭代后剩余棒数之和/](https://www.geeksforgeeks.org/find-the-sum-of-remaining-sticks-after-each-iterations/)

给定阵列中不同长度的棒的数量，任务是确定每次迭代后剩余棒的总数。每次迭代时，从剩余的棒中剪下最短的棒。

**示例:**

```
Input: N = 6, arr = {5, 4, 4, 2, 2, 8}
Output: 7
Explanation:
Iteration 1: 
Initial arr = {5, 4, 4, 2, 2, 8}
Shortest stick = 2
arr with reduced length = {3, 2, 2, 0, 0, 6}
Remaining sticks = 4

Iteration 2: 
arr = {3, 2, 2, 4}
Shortest stick = 2
Left stick = 2

Iteration 3: 
arr = {1, 2}
Shortest stick = 1
Left stick = 1

Iteration 4: 
arr = {1}
Min length = 1
Left stick = 0

Input: N = 8, arr = {1, 2, 3, 4, 3, 3, 2, 1}
Output: 11
```

**方法:**解决这个问题的方法是对数组进行排序，然后在遍历时找到相同长度的最小长度棒的数量，并在每一步相应地更新总和，最后返回总和。

## C++

```
// C++ program to find the sum of
// remaining sticks after each iterations

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// sum of remaining sticks
// after each iteration
int sum(vector<int> &arr, int n)
{
    int sum = 0;
    sort(arr.begin(),arr.end());
    int prev=0,count=1,s=arr.size();
    int i=1;
    while(i<arr.size()){
        if(arr[i]==arr[prev]){
            count++;
        }else{
            prev=i;
            sum+=s-count;
              s-=count;
            count=1;
        }
        i++;
    }
    return sum;
}

// Driver code
int main()
{

    int n = 6;
    vector<int> ar{ 5, 4, 4, 2, 2, 8 };

    int ans = sum(ar, n);

    cout << ans << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// remaining sticks after each iterations
import java.io.*;
import java.util.*;

class GFG{

// Function to calculate
// sum of remaining sticks
// after each iteration
public static int sum(int arr[], int n)
{
    int sum = 0;
    Arrays.sort(arr);

    int prev = 0, count = 1, s = n;
    int i = 1;

    while (i < n)
    {
        if (arr[i] == arr[prev])
        {
            count++;
        }
        else
        {
            prev = i;
            sum += s - count;
            s -= count;
            count = 1;
        }
        i++;
    }
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    int ar[] = { 5, 4, 4, 2, 2, 8 };
    int ans = sum(ar, n);

    System.out.println(ans);
}
}

// This code is contributed by Manu Pathria
```

## java 描述语言

```
<script>
// Java Script program to find the sum of
// remaining sticks after each iterations

// Function to calculate
// sum of remaining sticks
// after each iteration
function sum(arr,n)
{
    let sum = 0;
    arr.sort();

    let prev = 0, count = 1, s = n;
    let i = 1;

    while (i < n)
    {
        if (arr[i] == arr[prev])
        {
            count++;
        }
        else
        {
            prev = i;
            sum += s - count;
            s -= count;
            count = 1;
        }
        i++;
    }
    return sum;
}

// Driver code

    let n = 6;
    let ar = [ 5, 4, 4, 2, 2, 8 ];
    let ans = sum(ar, n);

    document.write(ans);

// This code is contributed by manoj
</script>
```

**<u>时间复杂度</u> :** **O(Nlog(N))** 其中 N 为棍棒数。

**<u>另一种方法:</u>**

*   将杆长的频率存储在地图中
*   在每次迭代中，
    *   找出最小长度棒的频率
    *   从每个杆的频率中降低最小长度杆的频率
    *   将非零棒数加到合成棒上。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of
// remaining sticks after each iterations

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// sum of remaining sticks
// after each iteration
int sum(int ar[], int n)
{
    map<int, int> mp;

    // storing frequency of stick length
    for (int i = 0; i < n; i++) {
        mp[ar[i]]++;
    }

    int sum = 0;

    for (auto p : mp) {
        n -= p.second;
        sum += n;
    }

    return sum;
}

// Driver code
int main()
{

    int n = 6;
    int ar[] = { 5, 4, 4, 2, 2, 8 };

    int ans = sum(ar, n);

    cout << ans << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// remaining sticks after each iterations
import java.util.HashMap;
import java.util.Map;

class GFG
{

    // Function to calculate
    // sum of remaining sticks
    // after each iteration
    static int sum(int ar[], int n)
    {
        HashMap<Integer,
                Integer> mp = new HashMap<>();

        for (int i = 0; i < n; i++)
        {
            mp.put(ar[i], 0);
        }

        // storing frequency of stick length
        for (int i = 0; i < n; i++)
        {
            mp.put(ar[i], mp.get(ar[i]) + 1) ;
        }

        int sum = 0;

        for(Map.Entry p : mp.entrySet())
        {
            n -= (int)p.getValue();
            sum += n;
        }
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 6;
        int ar[] = { 5, 4, 4, 2, 2, 8 };

        int ans = sum(ar, n);

        System.out.println(ans);

    }
}

// This code is contributed by kanugargng
```

## 蟒蛇 3

```
# Python proagram to find sum
# of remaining sticks

# Function to calculate
# sum of remaining sticks
# after each iteration
def sum(ar, n):
  mp = dict()

  for i in ar:
    if i in mp:
      mp[i]+= 1
    else:
      mp[i] = 1

  mp = sorted(list(mp.items()))

  sum = 0

  for pair in mp:
    n-= pair[1]
    sum+= n

  return sum
# Driver code
def main():
  n = 6
  ar = [5, 4, 4, 2, 2, 8]
  ans = sum(ar, n)
  print(ans)

main()
```

## C#

```
// C# program to find the sum of
// remaining sticks after each iterations
using System;
using System.Collections.Generic;            

class GFG
{

    // Function to calculate
    // sum of remaining sticks
    // after each iteration
    static int sum(int []ar, int n)
    {
        SortedDictionary<int,
                         int> mp = new SortedDictionary<int,
                                                        int>();

        // storing frequency of stick length
        for (int i = 0; i < n; i++)
        {
            if(!mp.ContainsKey(ar[i]))
                mp.Add(ar[i], 0);
            else
                mp[ar[i]] = 0;
        }

        // storing frequency of stick length
        for (int i = 0; i < n; i++)
        {
            if(!mp.ContainsKey(ar[i]))
                mp.Add(ar[i], 1);
            else
                mp[ar[i]] = ++mp[ar[i]];
        }

        int sum = 0;

        foreach(KeyValuePair<int, int> p in mp)
        {
            n -= p.Value;
            sum += n;
        }
        return sum;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 6;
        int []ar = { 5, 4, 4, 2, 2, 8 };

        int ans = sum(ar, n);

        Console.WriteLine(ans);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find the sum of
// remaining sticks after each iterations

// Function to calculate
// sum of remaining sticks
// after each iteration
function sum(ar, n)
{
    let mp = new Map();

    for (let i = 0; i < n; i++)
    {
        mp.set(ar[i], 0);
    }

    // storing frequency of stick length
    for (let i = 0; i < n; i++)
    {
        mp.set(ar[i], mp.get(ar[i]) + 1);
    }

     mp = new Map([...mp].sort((a, b) => String(a[0]).localeCompare(b[0])))
    let sum = 0;

    for (let p of mp)
    {
        n -= p[1]
        sum += n;
    }
    return sum;
}

// Driver code
let n = 6;
let ar = [5, 4, 4, 2, 2, 8];
let ans = sum(ar, n);
document.write(ans + '<br>');

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
7
```

**时间复杂度:** ![O(Nlog(N))       ](img/8459d5125627c72150b0e8630e2453e5.png "Rendered by QuickLaTeX.com")其中 N 为棍棒数