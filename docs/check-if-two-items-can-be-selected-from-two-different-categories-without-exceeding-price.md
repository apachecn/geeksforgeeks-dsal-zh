# 检查是否可以从两个不同的类别中选择两个项目而不超过价格

> 原文:[https://www . geesforgeks . org/check-if-two-items-可以从两个不同的类别中选择-不超过价格/](https://www.geeksforgeeks.org/check-if-two-items-can-be-selected-from-two-different-categories-without-exceeding-price/)

给定两个数组**prices【】**、**type【】**和一个整数 **S** ，任务是检查是否可以从两个不同的类别中选择两个项目而不超出总价 S，**type【】**数组中的每个元素表示第 i <sup>个</sup>元素的类别，**prices【】**数组中的每个元素表示第 i <sup>个</sup>元素的价格。

**示例:**

> **输入:** S = 10，类型[] = {0，1，1，0}，价格[] = {3，8，6，5}
> **输出:**是
> **说明:**
> 可以选择要素价格【0】和价格【2】
> 总价=价格【0】+价格【2】= 3+6 = 9
> 
> **输入:** S = 15，类型[] = {0，1，1，0}，价格[] = {5，7，6，5}
> **输出:**否
> **说明:**
> 不存在总价小于 15 的可能解。

**方法:**想法是使用两个嵌套的[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)迭代选择每一个可能的对。对于每一对，检查它们的类别是否不同，它们的总价是否小于 S，如果是，那么有一种方法可以选择两个项目，否则就没有这样的成对项目。

下面是上述方法的实现:

## C++14

```
// C++ implementation to check if
// two items can be selected from
// two different categories without
// exceeding the total price

#include <bits/stdc++.h>
using namespace std;

// Function to check if
// two items can be selected from
// two different categories without
// exceeding the total price
string check(int S, int prices[],
             int type[], int n)
{

    // Loop to choose two different
    // pairs using two nested loops
    for (int j = 0; j < n; j++) {
        for (int k = j + 1; k < n; k++) {

            // Condition to check if the price
            // of these two elements is less than S
            if ((type[j] == 0 && type[k] == 1)
                || (type[j] == 1 && type[k] == 0)) {

                if (prices[j] + prices[k] <= S) {
                    return "Yes";
                }
            }
        }
    }
    return "No";
}

int main()
{
    int prices[] = { 3, 8, 6, 5 };
    int type[] = { 0, 1, 1, 0 };
    int S = 10;
    int n = 4;

    // Function Call
    cout << check(S, prices, type, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// two items can be selected from
// two different categories without
// exceeding the total price
import java.util.*;
class GFG{

// Function to check if
// two items can be selected from
// two different categories without
// exceeding the total price
static String check(int S, int prices[],
                    int type[], int n)
{

    // Loop to choose two different
    // pairs using two nested loops
    for (int j = 0; j < n; j++)
    {
        for (int k = j + 1; k < n; k++)
        {

            // Condition to check if the price
            // of these two elements is less than S
            if ((type[j] == 0 && type[k] == 1) ||
                (type[j] == 1 && type[k] == 0))
            {
                if (prices[j] + prices[k] <= S)
                {
                    return "Yes";
                }
            }
        }
    }
    return "No";
}

// Driver Code
public static void main(String[] args)
{
    int prices[] = { 3, 8, 6, 5 };
    int type[] = { 0, 1, 1, 0 };
    int S = 10;
    int n = 4;

    // Function Call
    System.out.print(check(S, prices, type, n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to check if
# two items can be selected from
# two different categories without
# exceeding the total price

# Function to check if
# two items can be selected from
# two different categories without
# exceeding the total price
def check(S, prices, type1, n):

    # Loop to choose two different
    # pairs using two nested loops
    for j in range(0, n):
        for k in range(j + 1, n):

            # Condition to check if the price
            # of these two elements is less than S
            if ((type1[j] == 0 and type1[k] == 1) or
                (type1[j] == 1 and type1[k] == 0)):

                if (prices[j] + prices[k] <= S):
                    return "Yes";

    return "No";

# Driver Code
prices = [ 3, 8, 6, 5 ];
type1 = [ 0, 1, 1, 0 ];
S = 10;
n = 4;

# Function Call
print(check(S, prices, type1, n));

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to check if
// two items can be selected from
// two different categories without
// exceeding the total price
using System;

class GFG{

// Function to check if two items 
// can be selected from two
// different categories without
// exceeding the total price
static String check(int S, int []prices,
                    int []type, int n)
{

    // Loop to choose two different
    // pairs using two nested loops
    for(int j = 0; j < n; j++)
    {
       for(int k = j + 1; k < n; k++)
       { 

          // Condition to check if the price
          // of these two elements is less than S
          if ((type[j] == 0 && type[k] == 1) ||
              (type[j] == 1 && type[k] == 0))
          {
              if (prices[j] + prices[k] <= S)
              {
                  return "Yes";
              }
          }
       }
    }
    return "No";
}

// Driver Code
public static void Main(String[] args)
{
    int []prices = { 3, 8, 6, 5 };
    int []type = { 0, 1, 1, 0 };
    int S = 10;
    int n = 4;

    // Function call
    Console.Write(check(S, prices, type, n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to check if
// two items can be selected from
// two different categories without
// exceeding the total price

// Function to check if two items 
// can be selected from two
// different categories without
// exceeding the total price
function check(S, prices, type, n)
{

    // Loop to choose two different
    // pairs using two nested loops
    for(let j = 0; j < n; j++)
    {
       for(let k = j + 1; k < n; k++)
       { 

          // Condition to check if the price
          // of these two elements is less than S
          if ((type[j] == 0 && type[k] == 1) ||
              (type[j] == 1 && type[k] == 0))
          {
              if (prices[j] + prices[k] <= S)
              {
                  return "Yes";
              }
          }
       }
    }
    return "No";
}

// Driver code
let prices = [ 3, 8, 6, 5 ];
let type = [ 0, 1, 1, 0 ];
let S = 10;
let n = 4;

// Function call
document.write(check(S, prices, type, n));

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
Yes
```