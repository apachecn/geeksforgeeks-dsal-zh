# 由给定的两位数组成的从 1 到 N 的共质数对的数量

> 原文:[https://www . geeksforgeeks . org/co-prime-pairs-number-from-1-n-由给定的两位数组成/](https://www.geeksforgeeks.org/number-of-co-prime-pairs-from-1-to-n-which-consists-of-given-two-digits/)

给定一个整数 **N** 和两个整数 **D1** 和 **D2** ( *< 10* )，任务是找出小于或等于 **N** 的[共质数对](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)的个数，该个数只由数字 **D1** 和 **D2** 组成。

**示例:**

> **输入:** N = 30，D1 = 2，D2 = 3
> **输出:** 5
> **解释:**
> 30 以下所有可能的数字对，数字 2 和 3 互为素数，它们是(2，3)，(2，23)，(3，22)，(3，23)，(22，23)。
> 
> **输入:** N = 100，D1 = 5，D2 = 6
> **输出:** 8
> **解释:**
> 100 以内所有可能的数字对，数字 5 和 6 互为质数，它们是(5，6)，(5，56)，(5，66)，(6，55)，(6，65)，(55，56)，(56，65)，(65，66)，(65，66)。

**方法:**解决这个问题的思路基于以下观察:

> **观察:**
> 
> *   查找并向列表中追加每个仅包含两个小于或等于 **N** 的数字**。**
> *   现在很容易找到共素数的无序对的数量。
> *   请注意，列表中最多可以有**1+2+2<sup>2</sup>+2<sup>3</sup>+2<sup>4</sup>+……2<sup>10</sup>= 2047**个数字，即整体时间复杂度不能超过 **O(2047 * 2047)，**作为可能的最大位数为 9。

按照以下步骤解决问题:

*   初始化一个空的[列表](https://www.geeksforgeeks.org/python-list/)，说 **l** 、**T5】并将给定的两位数字作为添加到列表中。**
*   [排序列表](https://www.geeksforgeeks.org/python-list-sort/)。
*   初始化两个列表，说**总计**和**温度 2** 以备后用。
*   迭代直到 **l[0] < 10:**
    *   将给定的两位数字作为字符串附加到列表中的所有元素 **l.**
    *   按照如下所示的方式继续更新 **l** :
        *   [2，3] -> **['2' + '2 '，' 2' + '3 '，' 3' + '2 '，' 3' + '3']**
        *   [22，23，32，33]–>**[' 22 '+' 2 '，' 22' + '3 '，' 23' + '2 '，' 23' + '3 '，' 32' + '2 '，' 32' + '3 '，' 33' + '2 '，' 33' + '3']** 等等。
*   定义一个函数**NumofParks()**，该函数返回无序的同素对的计数。
*   打印上述函数返回的计数作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check whether given
// integers are co-prime or not
int coprime(int a, int b) { return (__gcd(a, b) == 1); }

// Utility function to count
// number of co-prime pairs
int numOfPairs(vector<string> arr, int N)
{
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {
        for (int j = i + 1; j < N; j++) {

            // If co-prime
            if (coprime(stoi(arr[i]), stoi(arr[j]))) {

                // Increment count
                count = count + 1;
            }
        }
    }
    // Return count
    return count;
}

// Function to count number
// of co-prime pairs
int noOfCoPrimePairs(int N, int d1, int d2)
{

    // Stores digits in string form
    vector<string> l;
    l.push_back(to_string(d1));
    l.push_back(to_string(d2));

    // Sort the list
    sort(l.begin(), l.end());

    if (N < stoi(l[1]))
        return 0;

    // Keep two copies of list l
    vector<string> total = l;
    vector<string> temp2 = l;
    int flag = 0;
    vector<string> temp3;

    // Generate 2 digit numbers
    // using d1 and d2
    while (l[0].length() < 10) {
        for (int i = 0; i < l.size(); i++) {
            for (int j = 0; j < 2; j++) {

                // If current number
                // does not exceed N
                if (stoi(l[i] + temp2[j]) > N) {
                    flag = 1;
                    break;
                }
                total.push_back(l[i] + temp2[j]);
                temp3.push_back(l[i] + temp2[j]);
            }
            if (flag == 1)
                break;
        }
        if (flag == 1)
            break;
        l = temp3;
        vector<string> temp3;
    }

    // Stores length of list
    int lenOfTotal = total.size();

    // Stores number of co-prime pairs
    int ans = numOfPairs(total, lenOfTotal);

    // Print number of co-prime pairs
    cout << (ans);
}

// Driver Code
int main()
{

    // Given value of N, d1, d2
    int N = 30, d1 = 2, d2 = 3;

    // Function call to count
    // number of co-prime pairs
    noOfCoPrimePairs(N, d1, d2);
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;       

class GFG{

static int GCD(int a, int b)
{
    return b == 0 ? a : GCD(b, a % b);
}

// Function to check whether given
// integers are co-prime or not
static boolean coprime(int a, int b)
{
    if (GCD(a, b) == 1)
        return true;

    return false;
}

// Utility function to count
// number of co-prime pairs
static int numOfPairs(ArrayList<String> arr, int N)
{
    int count = 0;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // If co-prime
            if (coprime(Integer.parseInt(arr.get(i)),
                        Integer.parseInt(arr.get(j))))
            {

                // Increment count
                count = count + 1;
            }
        }
    }

    // Return count
    return count;
}

// Function to count number
// of co-prime pairs
static void noOfCoPrimePairs(int N, int d1, int d2)
{

    // Stores digits in string form
    ArrayList<String> l = new ArrayList<String>();  
    l.add(Integer.toString(d1));
    l.add(Integer.toString(d2));

    // Sort the list
    Collections.sort(l);

    if (N < Integer.parseInt(l.get(1)))
        return;

    // Keep two copies of list l
    ArrayList<String> total = new ArrayList<String>(l);  
    ArrayList<String> temp2 = new ArrayList<String>(l);  
    int flag = 0;
    ArrayList<String> temp3 = new ArrayList<String>(l); 

    // Generate 2 digit numbers
    // using d1 and d2
    while (l.get(0).length() < 10)
    {
        for(int i = 0; i < l.size(); i++)
        {
            for(int j = 0; j < 2; j++)
            {

                // If current number
                // does not exceed N
                if (Integer.parseInt(l.get(i) +
                                 temp2.get(j)) > N)
                {
                    flag = 1;
                    break;
                }
                total.add(l.get(i) + temp2.get(j));
                temp3.add(l.get(i) + temp2.get(j));
            }
            if (flag == 1)
                break;
        }
        if (flag == 1)
            break;

        l = temp3;
        temp3.clear();
    }

    // Stores length of list
    int lenOfTotal = total.size();

    // Stores number of co-prime pairs
    int ans = numOfPairs(total, lenOfTotal);

    // Print number of co-prime pairs
    System.out.print(ans);
}

// Driver Code
public static void main(String args[])
{

    // Given value of N, d1, d2
    int N = 30, d1 = 2, d2 = 3;

    // Function call to count
    // number of co-prime pairs
    noOfCoPrimePairs(N, d1, d2);
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach

from copy import deepcopy
import math

# Function to check whether given
# integers are co-prime or not
def coprime(a, b):
    return (math.gcd(a, b)) == 1

# Utility function to count
# number of co-prime pairs
def numOfPairs(arr, N):
    count = 0

    # Traverse the array
    for i in range(0, N-1):
        for j in range(i+1, N):

            # If co-prime
            if (coprime(int(arr[i]), int(arr[j]))):

                # Increment count
                count = count + 1

    # Return count
    return count

# Function to count number
# of co-prime pairs
def noOfCoPrimePairs(N, d1, d2):

    # Stores digits in string form
    l = []
    l.append(str(d1))
    l.append(str(d2))

    # Sort the list
    l.sort()

    if int(N) < int(l[1]):
        return 0

    # Keep two copies of list l
    total = temp2 = deepcopy(l)
    flag = 0
    temp3 = []

    # Generate 2 digit numbers
    # using d1 and d2
    while len(l[0]) < 10:
        for i in range(len(l)):
            for j in range(2):

                # If current number
                # does not exceed N
                if int(l[i]+temp2[j]) > int(N):
                    flag = 1
                    break

                total.append(l[i]+temp2[j])
                temp3.append(l[i]+temp2[j])

            if flag == 1:
                break
        if flag == 1:
            break
        l = deepcopy(temp3)
        temp3 = []

    # Stores length of list
    lenOfTotal = len(total)

    # Stores number of co-prime pairs
    ans = numOfPairs(total, lenOfTotal)

    # Print number of co-prime pairs
    print(ans)

# Driver Code
if __name__ == "__main__":

    # Given value of N, d1, d2
    N = 30
    d1 = 2
    d2 = 3

    # Function call to count
    # number of co-prime pairs
    noOfCoPrimePairs(N, d1, d2)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;       

class GFG{

static int GCD(int a, int b)
{
    return b == 0 ? a : GCD(b, a % b);
}

// Function to check whether given
// integers are co-prime or not
static bool coprime(int a, int b)
{
    if (GCD(a, b) == 1)
        return true;

    return false;
}

// Utility function to count
// number of co-prime pairs
static int numOfPairs(List<string> arr, int N)
{
    int count = 0;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // If co-prime
            if (coprime(Int32.Parse(arr[i]),
                        Int32.Parse(arr[j])))
            {

                // Increment count
                count = count + 1;
            }
        }
    }

    // Return count
    return count;
}

// Function to count number
// of co-prime pairs
static void noOfCoPrimePairs(int N, int d1, int d2)
{

    // Stores digits in string form
    List<string> l = new List<string>();
    l.Add(d1.ToString());
    l.Add(d2.ToString());

    // Sort the list
    l.Sort();

    if (N < Int32.Parse(l[1]))
        return;

    // Keep two copies of list l
    List<string> total = new List<string>(l);
    List<string> temp2 = new List<string>(l);
    int flag = 0;
    List<string> temp3 = new List<string>();

    // Generate 2 digit numbers
    // using d1 and d2
    while (l[0].Length < 10)
    {
        for(int i = 0; i < l.Count; i++)
        {
            for(int j = 0; j < 2; j++)
            {

                // If current number
                // does not exceed N
                if (Int32.Parse(l[i] + temp2[j]) > N)
                {
                    flag = 1;
                    break;
                }
                total.Add(l[i] + temp2[j]);
                temp3.Add(l[i] + temp2[j]);
            }
            if (flag == 1)
                break;
        }
        if (flag == 1)
            break;

        l = temp3;
        temp3.Clear();
    }

    // Stores length of list
    int lenOfTotal = total.Count;

    // Stores number of co-prime pairs
    int ans = numOfPairs(total, lenOfTotal);

    // Print number of co-prime pairs
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{

    // Given value of N, d1, d2
    int N = 30, d1 = 2, d2 = 3;

    // Function call to count
    // number of co-prime pairs
    noOfCoPrimePairs(N, d1, d2);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

function GCD(a,b)
{
    return b == 0 ? a : GCD(b, a % b);
}

// Function to check whether given
// integers are co-prime or not
function coprime(a,b)
{
    if (GCD(a, b) == 1)
        return true;

    return false;
}

// Utility function to count
// number of co-prime pairs
function numOfPairs(arr,N)
{
    let count = 0;

    // Traverse the array
    for(let i = 0; i < N - 1; i++)
    {
        for(let j = i + 1; j < N; j++)
        {

            // If co-prime
            if (coprime(parseInt(arr[i]),
                        parseInt(arr[j])))
            {

                // Increment count
                count = count + 1;
            }
        }
    }

    // Return count
    return count;
}

// Function to count number
// of co-prime pairs
function noOfCoPrimePairs(N,d1,d2)
{
    // Stores digits in string form
    let l = [];
    l.push(d1.toString());
    l.push(d2.toString());

    // Sort the list
    l.sort();

    if (N < parseInt(l[1]))
        return;

    // Keep two copies of list l
    let total = [...l];
    let temp2 = [...l];
    let flag = 0;
    let temp3 = [];

    // Generate 2 digit numbers
    // using d1 and d2
    while (l[0].length < 10)
    {
        for(let i = 0; i < l.length; i++)
        {
            for(let j = 0; j < 2; j++)
            {

                // If current number
                // does not exceed N
                if (parseInt(l[i] +
                                 temp2[j]) > N)
                {
                    flag = 1;
                    break;
                }
                total.push(l[i] + temp2[j]);
                temp3.push(l[i] + temp2[j]);
            }
            if (flag == 1)
                break;
        }
        if (flag == 1)
            break;

        l = [...temp3];
        temp3=[];
    }

    // Stores length of list
    let lenOfTotal = total.length;

    // Stores number of co-prime pairs
    let ans = numOfPairs(total, lenOfTotal);

    // Print number of co-prime pairs
    document.write(ans);
}

// Driver Code
// Given value of N, d1, d2
let N = 30, d1 = 2, d2 = 3;

// Function call to count
// number of co-prime pairs
noOfCoPrimePairs(N, d1, d2);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(2<sup>logN</sup>)*
***辅助空间:** O(2 <sup>logN</sup> )*