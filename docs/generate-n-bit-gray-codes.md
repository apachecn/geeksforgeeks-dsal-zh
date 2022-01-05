# 生成 n 位格雷码

> 原文:[https://www.geeksforgeeks.org/generate-n-bit-gray-codes/](https://www.geeksforgeeks.org/generate-n-bit-gray-codes/)

给定一个数字 **N** ，生成从 0 到 2^N-1 的位模式，使得连续的模式相差一位。

**示例:**

```
Input: N = 2
Output: 00 01 11 10

Input: N = 3
Output: 000 001 011 010 110 111 101 100
```

**方法-1**

以上序列是不同宽度的[格雷码](http://en.wikipedia.org/wiki/Gray_code)。以下是格雷码中一个有趣的模式。
**可以使用以下步骤从(n-1)位格雷码列表中生成 n 位格雷码。**

1.  让(n-1)位格雷码的列表是 L1。创建另一个与 L1 相反的 L2 名单。
2.  通过在 L1 的所有代码中加前缀“0”来修改 L1 列表。
3.  通过在 L2 的所有代码中加前缀“1”来修改 L2 列表。
4.  连接 L1 和 L2。级联列表是 n 位格雷码的必需列表

例如，以下是从 2 位格雷码列表中生成 3 位格雷码列表的步骤。
L1 = {00，01，11，10 }(2 位格雷码列表)
L2 = {10，11，01，00}(与 L1 相反)
L1 的所有条目前加“0”，L1 变为{000，001，011，010 }
L2 的所有条目前加“1”，L2 变为{110，111，101，100}
连接 L1 和 L2，我们得到{0001 位格雷码列表为{0，1}。我们重复上述步骤，从 1 位格雷码生成 2 位格雷码，然后从 2 位格雷码生成 3 位格雷码，直到位数等于 n

下面是上述方法的实现:

## C++

```
// C++ program to generate n-bit Gray codes
#include <iostream>
#include <string>
#include <vector>
using namespace std;

// This function generates all n bit Gray codes and prints the
// generated codes
void generateGrayarr(int n)
{
    // base case
    if (n <= 0)
        return;

    // 'arr' will store all generated codes
    vector<string> arr;

    // start with one-bit pattern
    arr.push_back("0");
    arr.push_back("1");

    // Every iteration of this loop generates 2*i codes from previously
    // generated i codes.
    int i, j;
    for (i = 2; i < (1<<n); i = i<<1)
    {
        // Enter the prviously generated codes again in arr[] in reverse
        // order. Nor arr[] has double number of codes.
        for (j = i-1 ; j >= 0 ; j--)
            arr.push_back(arr[j]);

        // append 0 to the first half
        for (j = 0 ; j < i ; j++)
            arr[j] = "0" + arr[j];

        // append 1 to the second half
        for (j = i ; j < 2*i ; j++)
            arr[j] = "1" + arr[j];
    }

    // print contents of arr[]
    for (i = 0 ; i < arr.size() ; i++ )
        cout << arr[i] << endl;
}

// Driver program to test above function
int main()
{
    generateGrayarr(3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate n-bit Gray codes
import java.util.*;
class GfG {

// This function generates all n bit Gray codes and prints the
// generated codes
static void generateGrayarr(int n)
{
    // base case
    if (n <= 0)
        return;

    // 'arr' will store all generated codes
    ArrayList<String> arr = new ArrayList<String> ();

    // start with one-bit pattern
    arr.add("0");
    arr.add("1");

    // Every iteration of this loop generates 2*i codes from previously
    // generated i codes.
    int i, j;
    for (i = 2; i < (1<<n); i = i<<1)
    {
        // Enter the prviously generated codes again in arr[] in reverse
        // order. Nor arr[] has double number of codes.
        for (j = i-1 ; j >= 0 ; j--)
            arr.add(arr.get(j));

        // append 0 to the first half
        for (j = 0 ; j < i ; j++)
            arr.set(j, "0" + arr.get(j));

        // append 1 to the second half
        for (j = i ; j < 2*i ; j++)
            arr.set(j, "1" + arr.get(j));
    }

    // print contents of arr[]
    for (i = 0 ; i < arr.size() ; i++ )
        System.out.println(arr.get(i));
}

// Driver program to test above function
public static void main(String[] args)
{
    generateGrayarr(3);
}
}
```

## 蟒蛇 3

```
# Python3 program to generate n-bit Gray codes
import math as mt

# This function generates all n bit Gray
# codes and prints the generated codes
def generateGrayarr(n):

    # base case
    if (n <= 0):
        return

    # 'arr' will store all generated codes
    arr = list()

    # start with one-bit pattern
    arr.append("0")
    arr.append("1")

    # Every iteration of this loop generates
    # 2*i codes from previously generated i codes.
    i = 2
    j = 0
    while(True):

        if i >= 1 << n:
            break

        # Enter the prviously generated codes
        # again in arr[] in reverse order.
        # Nor arr[] has double number of codes.
        for j in range(i - 1, -1, -1):
            arr.append(arr[j])

        # append 0 to the first half
        for j in range(i):
            arr[j] = "0" + arr[j]

        # append 1 to the second half
        for j in range(i, 2 * i):
            arr[j] = "1" + arr[j]
        i = i << 1

    # prcontents of arr[]
    for i in range(len(arr)):
        print(arr[i])

# Driver Code
generateGrayarr(3)

# This code is contributed
# by Mohit kumar 29
```

## C#

```
using System;
using System.Collections.Generic;

// C# program to generate n-bit Gray codes 
public class GfG
{

// This function generates all n bit Gray codes and prints the 
// generated codes 
public static void generateGrayarr(int n)
{
    // base case 
    if (n <= 0)
    {
        return;
    }

    // 'arr' will store all generated codes 
    List<string> arr = new List<string> ();

    // start with one-bit pattern 
    arr.Add("0");
    arr.Add("1");

    // Every iteration of this loop generates 2*i codes from previously 
    // generated i codes. 
    int i, j;
    for (i = 2; i < (1 << n); i = i << 1)
    {
        // Enter the prviously generated codes again in arr[] in reverse 
        // order. Nor arr[] has double number of codes. 
        for (j = i - 1 ; j >= 0 ; j--)
        {
            arr.Add(arr[j]);
        }

        // append 0 to the first half 
        for (j = 0 ; j < i ; j++)
        {
            arr[j] = "0" + arr[j];
        }

        // append 1 to the second half 
        for (j = i ; j < 2 * i ; j++)
        {
            arr[j] = "1" + arr[j];
        }
    }

    // print contents of arr[] 
    for (i = 0 ; i < arr.Count ; i++)
    {
        Console.WriteLine(arr[i]);
    }
}

// Driver program to test above function 
public static void Main(string[] args)
{
    generateGrayarr(3);
}
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// Javascript program to generate n-bit Gray codes

    // This function generates all n bit Gray codes and prints the
    // generated codes
    function generateGrayarr(n)
    {
        // base case
    if (n <= 0)
        return;

    // 'arr' will store all generated codes
    let arr = [];

    // start with one-bit pattern
    arr.push("0");
    arr.push("1");

    // Every iteration of this loop generates 2*i codes from previously
    // generated i codes.
    let i, j;
    for (i = 2; i < (1<<n); i = i<<1)
    {
        // Enter the prviously generated codes again in arr[] in reverse
        // order. Nor arr[] has double number of codes.
        for (j = i-1 ; j >= 0 ; j--)
            arr.push(arr[j]);

        // append 0 to the first half
        for (j = 0 ; j < i ; j++)
            arr[j]= "0" + arr[j];

        // append 1 to the second half
        for (j = i ; j < 2*i ; j++)
            arr[j]= "1" + arr[j];
    }

    // print contents of arr[]
    for (i = 0 ; i < arr.length ; i++ )
        document.write(arr[i]+"<br>");
    }

    // Driver program to test above function
    generateGrayarr(3);

    // This code is contributed by unknown2108
</script>
```

**Output**

```
000
001
011
010
110
111
101
100
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*

**方法 2:递归方法**

其思想是每次递归追加位 0 和 1，直到位数不等于 n。

**基本条件:**这个问题的基本情况是当 N = 0 或 1 时。

> If (N == 0)
> 返回{“0”}
> if(N = = 1)
> 返回{“0”、“1”}

**递归条件:**否则，对于任何大于 1 的值，递归生成 N–1 位的格雷码，然后为生成的每个格雷码添加前缀 0 和 1。

下面是上述方法的实现:

## C++

```
// C++ program to generate
// n-bit Gray codes

#include <bits/stdc++.h>
using namespace std;

// This function generates all n
// bit Gray codes and prints the
// generated codes
vector<string> generateGray(int n)
{
    // Base case
    if (n <= 0)
        return {"0"};

    if (n == 1)
    {
      return {"0","1"};
    }

    //Recursive case
    vector<string> recAns=
          generateGray(n-1);
    vector<string> mainAns;

    // Append 0 to the first half
    for(int i=0;i<recAns.size();i++)
    {
      string s=recAns[i];
      mainAns.push_back("0"+s);
    }

     // Append 1 to the second half
    for(int i=recAns.size()-1;i>=0;i--)
    {
       string s=recAns[i];
       mainAns.push_back("1"+s);
    }
    return mainAns;
}

// Function to generate the
// Gray code of N bits
void generateGrayarr(int n)
{
    vector<string> arr;
    arr=generateGray(n);
    // print contents of arr
    for (int i = 0 ; i < arr.size();
         i++ )
        cout << arr[i] << endl;
}

// Driver Code
int main()
{
    generateGrayarr(3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate
// n-bit Gray codes
import java.io.*;
import java.util.*;
class GFG
{

  // This function generates all n
  // bit Gray codes and prints the
  // generated codes
  static ArrayList<String> generateGray(int n)
  {

    // Base case
    if (n <= 0)
    {
      ArrayList<String> temp =
        new ArrayList<String>(){{add("0");}};
      return temp;
    }
    if(n == 1)
    {
      ArrayList<String> temp =
        new ArrayList<String>(){{add("0");add("1");}};
      return temp;
    }

    // Recursive case
    ArrayList<String> recAns = generateGray(n - 1);
    ArrayList<String> mainAns = new ArrayList<String>();

    // Append 0 to the first half
    for(int i = 0; i < recAns.size(); i++)
    {
      String s = recAns.get(i);
      mainAns.add("0" + s);

    }

    // Append 1 to the second half
    for(int i = recAns.size() - 1; i >= 0; i--)
    {
      String s = recAns.get(i);
      mainAns.add("1" + s);
    }
    return mainAns;
  }

  // Function to generate the
  // Gray code of N bits
  static void generateGrayarr(int n)
  {
    ArrayList<String> arr = new ArrayList<String>();
    arr = generateGray(n);

    // print contents of arr
    for (int i = 0 ; i < arr.size(); i++)
    {
      System.out.println(arr.get(i));   
    }
  }

  // Driver Code
  public static void main (String[] args)
  {
    generateGrayarr(3);
  }
}

// This code is contributed by rag2127.
```

## 蟒蛇 3

```
# Python3 program to generate
# n-bit Gray codes

# This function generates all n
# bit Gray codes and prints the
# generated codes
def generateGray(n):

    # Base case
    if (n <= 0):
        return ["0"]
    if (n == 1):
        return [ "0", "1" ]

    # Recursive case
    recAns = generateGray(n - 1)

    mainAns = []

    # Append 0 to the first half
    for i in range(len(recAns)):
        s = recAns[i]
        mainAns.append("0" + s)

    # Append 1 to the second half
    for i in range(len(recAns) - 1, -1, -1):
        s = recAns[i]
        mainAns.append("1" + s)

    return mainAns

# Function to generate the
# Gray code of N bits
def generateGrayarr(n):

    arr = generateGray(n)

    # Print contents of arr
    print(*arr, sep = "\n")

# Driver Code
generateGrayarr(3)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// Java program to generate
// n-bit Gray codes
using System;
using System.Collections.Generic;
class GFG {

  // This function generates all n
  // bit Gray codes and prints the
  // generated codes
  static List<String> generateGray(int n)
  {

    // Base case
    if (n <= 0) {
      List<String> temp = new List<String>();
      temp.Add("0");
      return temp;
    }
    if (n == 1) {
      List<String> temp = new List<String>();
      temp.Add("0");
      temp.Add("1");
      return temp;
    }

    // Recursive case
    List<String> recAns = generateGray(n - 1);
    List<String> mainAns = new List<String>();

    // Append 0 to the first half
    for (int i = 0; i < recAns.Count; i++) {
      String s = recAns[i];
      mainAns.Add("0" + s);
    }

    // Append 1 to the second half
    for (int i = recAns.Count - 1; i >= 0; i--) {
      String s = recAns[i];
      mainAns.Add("1" + s);
    }
    return mainAns;
  }

  // Function to generate the
  // Gray code of N bits
  static void generateGrayarr(int n)
  {
    List<String> arr = new List<String>();
    arr = generateGray(n);

    // print contents of arr
    for (int i = 0; i < arr.Count; i++)
    {
      Console.WriteLine(arr[i]);
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    generateGrayarr(3);
  }
}

// This code is contributed by grand_master.
```

## java 描述语言

```
<script>
// Javascript program to generate
// n-bit Gray codes

// This function generates all n
  // bit Gray codes and prints the
  // generated codes
function generateGray(n)
{
    // Base case
    if (n <= 0)
    {
      let temp =["0"];
      return temp;
    }
    if(n == 1)
    {
      let temp =["0","1"];

      return temp;
    }

    // Recursive case
    let recAns = generateGray(n - 1);
    let mainAns = [];

    // Append 0 to the first half
    for(let i = 0; i < recAns.length; i++)
    {
      let s = recAns[i];
      mainAns.push("0" + s);

    }

    // Append 1 to the second half
    for(let i = recAns.length - 1; i >= 0; i--)
    {
      let s = recAns[i];
      mainAns.push("1" + s);
    }
    return mainAns;
}

// Function to generate the
  // Gray code of N bits
function generateGrayarr(n)
{
    let arr = [];
    arr = generateGray(n);

    // print contents of arr
    for (let i = 0 ; i < arr.length; i++)
    {
      document.write(arr[i]+"<br>");  
    }
}

// Driver Code
generateGrayarr(3);

// This code is contributed by ab2127
</script>
```

**Output**

```
000
001
011
010
110
111
101
100
```