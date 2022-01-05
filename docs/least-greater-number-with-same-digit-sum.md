# 具有相同数字和的最小较大数字

> 原文:[https://www . geeksforgeeks . org/同位数总和最小-最大-数/](https://www.geeksforgeeks.org/least-greater-number-with-same-digit-sum/)

给定一个以数组形式表示的数字，使得数组的每个元素存储该数字的一个位数。也就是说，数字 1234 的数组将是 arr[] = {1，2，3，4}。任务是找到比给定数字大但位数总和等于给定数字的最小数字。

**简单来说**:考虑数字的长度最多可以是 20。

**示例**:

> **输入** : arr[] = {0，0，0，0，0，0，0，0，3，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，8 }；
> **输出**:000000047999999999
> **说明**:位数之和= 110
> 
> **输入** : arr[] = {0，0，0，0，0，0，0，0，3，9，7，0，0，2，9，8，9，5，9，9，0 }；
> **输出**:00000003970029896089
> **说明**:位数之和= 70

一种**蛮力方法**是:

1.  从那个数字开始，把数字加 1。
2.  检查总数。如果总和相同，则返回数字。
3.  否则回到第一步。

A **更好的做法**是跳到 O(n)时间复杂度中的下一个数字，其中 n 是字符串的长度。

> 我们将数字分成 4 个区域:
> **第 1 个**:尾随零。
> **第二位**:最低位不在 1 区。
> **第三个**:从区域 2 上方的数字开始连续 9 秒。
> **第 4 位**:所有剩余数字。
> 
> 那么下一个数字是:
> 【区域 4+1】【区域 1】【区域 2-1】【区域 3】。
> 
> **示例** :
> 输入编号= 548995000
> 区域 1 : 000
> 区域 2 : 5
> 区域 3 : 99
> 区域 4 : 548
> 
> 下一个数字= 549000499

以下是上述方法的实现:

## C++

```
// CPP program to find next greater number with
// same sum of digits.
#include <bits/stdc++.h>
using namespace std;

#define pb push_back

void getnext(int arr[], int n)
{
    // for storing 4 regions
    vector<int> a1, a2, a3, a4;

    // trailing zeros region1
    int i = n - 1; // last index
    while (arr[i] == 0) 
    {
        a1.pb(0);
        i--;
    }

    // lowest region(region 2) not in region 1
    a2.pb(arr[i--]); 

    // Consecutive 9's   (region 3)
    while (arr[i] == 9) 
    {
        a3.pb(9);
        i--;
    }

    int j = 0;
    while (arr[j] == 0)
        j++; // Starting zeros

    while (j <= i) // 4th region
    {
        a4.pb(arr[j]);
        j++;
    }

    // Calculation of result
    j = a4.size() - 1;

    a4[j]++; // Region4 + 1

    a2[0]--; // Region2 -1

    int l = a1.size() + a2.size() + a3.size() + a4.size();

    // Calculating the result
    j = n-1;
    i = a3.size() - 1;

    // Copying the third region
    while (i >= 0)
    {
        arr[j--] = a3[i--];
    }

    // Copying the 2nd region
    i = a2.size() - 1;
    while (i >= 0) 
    {
        arr[j--] = a2[i--];
    }

    // Copying the 1st region
    i = a1.size() - 1;
    while (i >= 0) 
    {
        arr[j--] = a1[i--];
    }

    // Copying the 4th region
    i = a4.size() - 1;
    while (i >= 0) 
    {
        arr[j--] = a4[i--];
    }

    while (j >= 0)
        arr[j--] = 0;
}

int main()
{
    int arr[] = { 0, 0, 0, 0, 0, 0, 0, 3, 9, 7, 
                0, 0, 2, 9, 8, 9, 5, 9, 9, 0 };
    int n = sizeof(arr)/sizeof(arr[0]);

    getnext(arr, n); // Calling the function

    for (int i = 0; i < n; i++)
        cout << arr[i];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next greater number with
// same sum of digits.
import java.util.*;

class GFG
{

static void getnext(int []arr, int n)
{
    // for storing 4 regions
    ArrayList<Integer> a1 = new ArrayList<Integer>();
    ArrayList<Integer> a2 = new ArrayList<Integer>();
    ArrayList<Integer> a3 = new ArrayList<Integer>();
    ArrayList<Integer> a4 = new ArrayList<Integer>();

    // trailing zeros region1
    int i = n - 1; // last index
    while (arr[i] == 0) 
    {
        a1.add(0);
        i--;
    }

    // lowest region(region 2) not in region 1
    a2.add(arr[i--]); 

    // Consecutive 9's (region 3)
    while (arr[i] == 9) 
    {
        a3.add(9);
        i--;
    }

    int j = 0;
    while (arr[j] == 0)
        j++; // Starting zeros

    while (j <= i) // 4th region
    {
        a4.add(arr[j]);
        j++;
    }

    // Calculation of result
    j = a4.size() - 1;

    a4.set(j,a4.get(j) + 1); // Region4 + 1

    a2.set(0,a2.get(0) - 1); // Region2 -1

    //int l = a1.size() + a2.size() + a3.size() + a4.size();

    // Calculating the result
    j = n - 1;
    i = a3.size() - 1;

    // Copying the third region
    while (i >= 0)
    {
        arr[j--] = (int)a3.get(i);
        i--;
    }

    // Copying the 2nd region
    i = a2.size() - 1;
    while (i >= 0) 
    {
        arr[j--] = (int)a2.get(i);
        i--;
    }

    // Copying the 1st region
    i = a1.size() - 1;
    while (i >= 0) 
    {
        arr[j--] = a1.get(i);
        i--;
    }

    // Copying the 4th region
    i = a4.size() - 1;
    while (i >= 0) 
    {
        arr[j--] = a4.get(i);
        i--;
    }

    while (j >= 0)
        arr[j--] = 0;
}

// Driver code
public static void main (String[] args) 
{
    int []arr = { 0, 0, 0, 0, 0, 0, 0, 3, 9, 7, 
                0, 0, 2, 9, 8, 9, 5, 9, 9, 0 };
    int n = arr.length;

    getnext(arr, n); // Calling the function

    for (int i = 0; i < n; i++)
        System.out.print(arr[i]);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find next greater number with
# same sum of digits.

def getnext(arr, n):

    # for storing 4 regions
    a1=[];
    a2=[];
    a3=[];
    a4=[];

    # trailing zeros region1
    i = n - 1; # last index
    while (arr[i] == 0):
        a1.append(0);
        i-=1;

    # lowest region(region 2) not in region 1
    a2.append(arr[i]);
    i-=1;

    # Consecutive 9's (region 3)
    while (arr[i] == 9):
        a3.append(9);
        i-=1;

    j = 0;
    while (arr[j] == 0):
        j+=1; # Starting zeros

    while (j <= i): # 4th region
        a4.append(arr[j]);
        j+=1;

    # Calculation of result
    j = len(a4) - 1;

    a4[j]+=1; # Region4 + 1

    a2[0]-=1; # Region2 -1

    l = len(a1) + len(a2) + len(a3) + len(a4);

    # Calculating the result
    j = n-1;
    i = len(a3) - 1;

    # Copying the third region
    while (i >= 0):
        arr[j] = a3[i];
        j-=1;
        i-=1;

    # Copying the 2nd region
    i = len(a2) - 1;
    while (i >= 0):
        arr[j] = a2[i];
        j-=1;
        i-=1;

    # Copying the 1st region
    i = len(a1) - 1;
    while (i >= 0):
        arr[j] = a1[i];
        j-=1;
        i-=1;

    # Copying the 4th region
    i = len(a4) - 1;
    while (i >= 0):
        arr[j] = a4[i];
        j-=1;
        i-=1;

    while (j >= 0):
        arr[j] = 0;
        j-=1;

# Driver code
arr = [ 0, 0, 0, 0, 0, 0, 0, 3, 9, 7, 0,
            0, 2, 9, 8, 9, 5, 9, 9, 0 ];
n = len(arr);

getnext(arr, n); # Calling the function

for i in range(0,n):
    print(arr[i],end="");

# This code is contributed by mits
```

## C#

```
// C# program to find next greater number with
// same sum of digits.
using System;
using System.Collections;

class GFG
{

static void getnext(int []arr, int n)
{
    // for storing 4 regions
    ArrayList a1 = new ArrayList();
    ArrayList a2 = new ArrayList();
    ArrayList a3 = new ArrayList();
    ArrayList a4 = new ArrayList();

    // trailing zeros region1
    int i = n - 1; // last index
    while (arr[i] == 0) 
    {
        a1.Add(0);
        i--;
    }

    // lowest region(region 2) not in region 1
    a2.Add(arr[i--]); 

    // Consecutive 9's (region 3)
    while (arr[i] == 9) 
    {
        a3.Add(9);
        i--;
    }

    int j = 0;
    while (arr[j] == 0)
        j++; // Starting zeros

    while (j <= i) // 4th region
    {
        a4.Add(arr[j]);
        j++;
    }

    // Calculation of result
    j = a4.Count - 1;

    a4[j] = (int)a4[j] + 1; // Region4 + 1

    a2[0] = (int)a2[0] - 1; // Region2 -1

    //int l = a1.Count + a2.Count + a3.Count + a4.Count;

    // Calculating the result
    j = n - 1;
    i = a3.Count - 1;

    // Copying the third region
    while (i >= 0)
    {
        arr[j--] = (int)a3[i];
        i--;
    }

    // Copying the 2nd region
    i = a2.Count - 1;
    while (i >= 0) 
    {
        arr[j--] = (int)a2[i];
        i--;
    }

    // Copying the 1st region
    i = a1.Count - 1;
    while (i >= 0) 
    {
        arr[j--] = (int)a1[i];
        i--;
    }

    // Copying the 4th region
    i = a4.Count - 1;
    while (i >= 0) 
    {
        arr[j--] = (int)a4[i];
        i--;
    }

    while (j >= 0)
        arr[j--] = 0;
}

// Driver code
static void Main()
{
    int []arr = { 0, 0, 0, 0, 0, 0, 0, 3, 9, 7, 
                0, 0, 2, 9, 8, 9, 5, 9, 9, 0 };
    int n = arr.Length;

    getnext(arr, n); // Calling the function

    for (int i = 0; i < n; i++)
        Console.Write(arr[i]);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find next greater number with
// same sum of digits.

function getnext(&$arr, $n)
{
    // for storing 4 regions
    $a1=array();
    $a2=array();
    $a3=array();
    $a4=array();

    // trailing zeros region1
    $i = $n - 1; // last index
    while ($arr[$i] == 0) 
    {
        array_push($a1,0);
        $i--;
    }

    // lowest region(region 2) not in region 1
    array_push($a2,$arr[$i--]); 

    // Consecutive 9's (region 3)
    while ($arr[$i] == 9) 
    {
        array_push($a3,9);
        $i--;
    }

    $j = 0;
    while ($arr[$j] == 0)
        $j++; // Starting zeros

    while ($j <= $i) // 4th region
    {
        array_push($a4,$arr[$j]);
        $j++;
    }

    // Calculation of result
    $j = count($a4) - 1;

    $a4[$j]++; // Region4 + 1

    $a2[0]--; // Region2 -1

    $l = count($a1) + count($a2) + count($a3) + count($a4);

    // Calculating the result
    $j = $n-1;
    $i = count($a3) - 1;

    // Copying the third region
    while ($i >= 0)
    {
        $arr[$j--] = $a3[$i--];
    }

    // Copying the 2nd region
    $i = count($a2) - 1;
    while ($i >= 0) 
    {
        $arr[$j--] = $a2[$i--];
    }

    // Copying the 1st region
    $i = count($a1) - 1;
    while ($i >= 0) 
    {
        $arr[$j--] = $a1[$i--];
    }

    // Copying the 4th region
    $i = count($a4) - 1;
    while ($i >= 0) 
    {
        $arr[$j--] = $a4[$i--];
    }

    while ($j >= 0)
        $arr[$j--] = 0;
}

        // Driver code
    $arr = array( 0, 0, 0, 0, 0, 0, 0, 3, 9, 7, 
                0, 0, 2, 9, 8, 9, 5, 9, 9, 0 );
    $n = count($arr);

    getnext($arr, $n); // Calling the function

    for ($i = 0; $i < $n; $i++)
        echo $arr[$i];

// This code is contributed by mits
?>
```

**Output:**

```
00000003970029896089

```