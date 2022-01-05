# 检查所有数组元素串联形成的数字是否为 Harshad 数

> 原文:[https://www . geesforgeks . org/check-如果通过串联所有数组元素形成的数字是一个-harshad-number-or-not/](https://www.geeksforgeeks.org/check-if-the-number-formed-by-concatenating-all-array-elements-is-a-harshad-number-or-not/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是检查通过连接所有数组元素形成的数字是否为 [Harshad 数字](https://www.geeksforgeeks.org/harshad-or-niven-number/)。

**示例:**

> **输入** : arr[] = { 1，35，69，60}
> **输出:**是
> **说明:**
> 数组元素串联形成的个数为“1356960”。
> 数字的位数之和= 1 + 3 + 5 + 6 + 9 + 6 + 0 = 30。
> 由于数字可被其位数的和整除，所以该数字是“哈沙德数”。
> 
> **输入:** arr[] = {1，563，9，59，7，8 }
> T3】输出:是

**方法:**想法是[将所有数组元素转换为它们的等价字符串并连接这些字符串。](https://www.geeksforgeeks.org/python-program-to-concatenate-two-integer-values-into-one/)按照以下步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并将每个数组元素转换为其等价字符串。
2.  连接变量中的所有字符串，比如 **S.**
3.  初始化一个变量，说**和，**存储生成数的[位数和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)。
4.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 并将 **sum** 更新为 **sum += int (s[i])。**
5.  初始化一个变量，比如说 **N = 0，**来存储由字符串 **S** mod **sum 的所有字符连接而成的数字。**
6.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 并将 **N** 更新为 **N = (N * 10 + int (S[i]))的% sum。**
7.  打印**是，**如果 **N = 0。**
8.  否则，打印**否**。

下面是上述方法的实现:

## C++

```
// CPP implementation
// of above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check whether n
// is a harshad number or not
int checkHarshad(string n)
{

  // Stores the sum of digits
  int sum = 0;

  // Stores the remainder
  int N = 0;

  // Increment sum
  for (int c = 0; c < n.length(); c++)
    sum += (n);

  for (int c = 0; c < n.length(); c++)
  {
    N = N + (N * 10 + (n));
    N %= sum;
  }
  return (N != 0);
}

// Function to check if concatenation
// of elements from the array arr[]
// is a harshad number or not
bool combineArray(vector<int> lis)
{

  // Stores the concatenated number
  string st = "";

  // Traverse the array
  for(auto el: lis)
  {

    // Concatenate the string
    st += to_string(el);
  }

  if(checkHarshad(st))
    return true;
  else
    return false;
}

// Driver Code
int main()
{

  // Input
  vector<int>arr{1, 35, 69, 60};

  // Function call to check if
  // concatenation of elements of
  // arr[] is a harshad number
  if(combineArray(arr))
    cout << "Yes";
  else
    cout << "No";
}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.ArrayList;

class GFG {

  // Function to check whether n
  // is a harshad number or not
  public static boolean checkHarshad(String n)
  {

    // Stores the sum of digits
    int sum = 0;

    // Stores the remainder
    int N = 0;

    // Increment sum
    for (int c = 0; c < n.length(); c++) {
      sum += Character.getNumericValue(n.charAt(c));
    }
    for (int c = 0; c < n.length(); c++) {
      N = N
        + (N * 10
           + (Character.getNumericValue(
             n.charAt(c))));
      N %= sum;
    }
    if (N == 0) {
      return true;
    }
    return false;
  }

  // Function to check if concatenation
  // of elements from the array arr[]
  // is a harshad number or not
  public static boolean
    combineArray(ArrayList<Integer> list)
  {

    // Stores the concatenated number
    String st = "";

    // Traverse the array
    for (int i = 0; i < list.size(); i++)
    {

      // Concatenate the string
      st += Integer.toString(list.get(i));
    }

    if (checkHarshad(st)) {
      return true;
    }
    return false;
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Input
    ArrayList<Integer> list = new ArrayList<>();
    list.add(1);
    list.add(35);
    list.add(69);
    list.add(60);

    // Function call to check if
    // concatenation of elements of
    // arr[] is a harshad number
    if (combineArray(list))
      System.out.println("Yes");
    else
      System.out.println("No");
  }
}

// This code is contributed by aditya7409
```

## 蟒蛇 3

```
# Python implementation
# of above approach

# Function to check whether n
# is a harshad number or not
def checkHarshad(n):

    # Stores the sum of digits
    sum = 0

    # Stores the remainder
    N = 0

    # Increment sum
    for c in n:
        sum += int(c)

    for c in n:
        N = N + (N*10+int(c))
        N %= sum

    return N == 0

# Function to check if concatenation
# of elements from the array arr[]
# is a harshad number or not
def combineArray(lis):

    # Stores the concatenated number
    string=""

    # Traverse the array
    for el in lis:

        # Convert to equivalent string
        el = str(el)

        # Concatenate the string
        string = string + el

    if(checkHarshad(string)):
        return True
    else:
        return False

# Driver Code

# Input
arr=[1, 35, 69, 60]

# Function call to check if
# concatenation of elements of
# arr[] is a harshad number
if(combineArray(arr)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to check whether n
  // is a harshad number or not
  public static bool checkHarshad(string n)
  {

    // Stores the sum of digits
    int sum = 0;

    // Stores the remainder
    int N = 0;

    // Increment sum
    for (int c = 0; c < n.Length; c++) {
      sum += (int)Char.GetNumericValue(n);
    }
    for (int c = 0; c < n.Length; c++) {
      N = N
        + (N * 10
           + (int)(Char.GetNumericValue(
             n)));
      N %= sum;
    }
    if (N == 0) {
      return true;
    }
    return false;
  }

  // Function to check if concatenation
  // of elements from the array arr[]
  // is a harshad number or not
  static bool
    combineArray(List<int> list)
  {

    // Stores the concatenated number
    string st = "";

     st += string.Join("", list);

    if (checkHarshad(st)) {
      return true;
    }
    return false;
  }

// Driver code
static void Main()
{
    List<int> list = new List<int>();
    list.Add(1);
    list.Add(35);
    list.Add(69);
    list.Add(60);

    // Function call to check if
    // concatenation of elements of
    // arr[] is a harshad number
    if (combineArray(list))
      Console.WriteLine("Yes");
    else
      Console.WriteLine("No");
}
}

// This code is contributed susmitakundugoaldanga.
```

## java 描述语言

```
<script>
// Javascript implementation
// of above approach

// Function to check whether n
// is a harshad number or not
function checkHarshad(n)
{

  // Stores the sum of digits
  var sum = 0;

  // Stores the remainder
  var N = 0;

  // Increment sum
  for (var c = 0; c < n.length; c++)
    sum += (n);

  for (var c = 0; c < n.length; c++)
  {
    N = N + (N * 10 + (n));
    N %= sum;
  }
  return (N != 0);
}

// Function to check if concatenation
// of elements from the array arr[]
// is a harshad number or not
function combineArray(lis)
{

  // Stores the concatenated number
  var st = "";

  // Traverse the array
  for(var el in lis)
  {

    // Concatenate the string
    st += (el.toString());
  }

  if(checkHarshad(st))
    return true;
  else
    return false;
}

// Driver Code
// Input
var arr = [1, 35, 69, 60];
// Function call to check if
// concatenation of elements of
// arr[] is a harshad number
if(combineArray(arr))
  document.write( "Yes");
else
  document.write( "No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)