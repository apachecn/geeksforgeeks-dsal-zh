# 生成范围【L，R】内所有长度相同的二进制数

> 原文:[https://www . geesforgeks . org/generate-all-binary-numbers-in-range-l-r-同长/](https://www.geeksforgeeks.org/generate-all-binary-numbers-in-range-l-r-with-same-length/)

给定两个正整数 **L** 和 **R** 。任务是把 L 到 R 的所有数字转换成二进制数。所有二进制数的长度应该相同。

**示例:**

> **输入:** L = 2，R = 4
> **输出:**
> 010
> 011
> 100
> **说明:**数字的二进制表示:2 = 10，3 = 11，4 = 100。
> 对于长度相同的数字，在 3 和 4 的二进制表示中加一个 0。
> 
> **输入:** L = 2，R = 8
> **输出:**
> 0010
> 0011
> 0100
> 0101
> 0110
> 0111
> 1000

**方法:**按照下面提到的方法解决问题。

*   要确定结果二进制数的长度，取 **R+1** 的对数为基数 2。
*   然后从 L 到 R 遍历**，将每个数字转换成确定长度的二进制。**
*   **存储每个数字，并在最后打印出来。**

**下面是上述方法的实现**

## **C++**

```
// C++ code to implement the approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert a number to binary
vector<int> convertToBinary(int num,
                            int length)
{
    vector<int> bits(length, 0);
    if (num == 0) {
        return bits;
    }

    int i = length - 1;
    while (num != 0) {
        bits[i--] = (num % 2);

        // Integer division
        // gives quotient
        num = num / 2;
    }
    return bits;
}

// Function to convert all numbers
// in range [L, R] to binary of
// same length
vector<vector<int> > getAllBinary(int l,
                                  int r)
{

    // Length of the binary numbers
    int n = (int) ceil(log(r+1) / log (2));

    vector<vector<int> > binary_nos;

    for (int i = l; i <= r; i++) {
        vector<int> bits =
            convertToBinary(i, n);
        binary_nos.push_back(bits);
    }

    return binary_nos;
}

// Driver code
int main()
{
    int L = 2, R = 8;
    vector<vector<int> > binary_nos =
        getAllBinary(L, R);
    for (int i = 0; i < binary_nos.size();
        i++) {
        for (int j = 0; j <
            binary_nos[i].size(); j++)
            cout << binary_nos[i][j];
        cout << endl;
    }
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to implement the approach
import java.util.*;
public class GFG
{

  // Function to convert a number to binary
  static ArrayList<Integer> convertToBinary(int num,
                                            int length)
  {
    ArrayList<Integer> bits= new ArrayList<Integer>();
    for(int i = 0; i < length; i++) {
      bits.add(0);
    }
    if (num == 0) {
      return bits;
    }

    int i = length - 1;
    while (num != 0) {
      bits.set(i, (num % 2));
      i = i - 1;

      // Integer division
      // gives quotient
      num = num / 2;
    }

    return bits;
  }

  // Function to convert all numbers
  // in range [L, R] to binary of
  // same length
  static ArrayList<ArrayList<Integer> > getAllBinary(int l,
                                                     int r)
  {

    // Length of the binary numbers
    double x = Math.log(r+1);
    double y = Math.log (2);
    int n = (int) Math.ceil(x / y);

    ArrayList<ArrayList<Integer> > binary_nos =
      new ArrayList<ArrayList<Integer> >();

    for (int i = l; i <= r; i++) {
      ArrayList<Integer> bits =
        convertToBinary(i, n);
      binary_nos.add(bits);
    }

    return binary_nos;
  }

  // Driver code
  public static void main(String args[])
  {
    int L = 2, R = 8;
    ArrayList<ArrayList<Integer> > binary_nos =
      getAllBinary(L, R);
    for (int i = 0; i < binary_nos.size(); i++) {
      for (int j = 0; j < binary_nos.get(i).size(); j++) {
        System.out.print(binary_nos.get(i).get(j));
      }
      System.out.println();
    }
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## **蟒蛇 3**

```
# Python 3 code to implement the approach
import math

# Function to convert a number to binary
def convertToBinary(num, length):

    bits = [0]*(length)
    if (num == 0):
        return bits

    i = length - 1
    while (num != 0):
        bits[i] = (num % 2)
        i -= 1

        # Integer division
        # gives quotient
        num = num // 2

    return bits

# Function to convert all numbers
# in range [L, R] to binary of
# same length
def getAllBinary(l, r):

    # Length of the binary numbers
    n = int(math.ceil(math.log(r+1)/ math.log(2)))

    binary_nos = []

    for i in range(l, r + 1):
        bits = convertToBinary(i, n)
        binary_nos.append(bits)

    return binary_nos

# Driver code
if __name__ == "__main__":

    L = 2
    R = 8
    binary_nos = getAllBinary(L, R)
    for i in range(len(binary_nos)):
        for j in range(len(binary_nos[i])):
            print(binary_nos[i][j], end="")
        print()

        # This code is contributed by ukasp.
```

## **C#**

```
// C# code to implement the approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Function to convert a number to binary
  static List<int> convertToBinary(int num, int length)
  {
    List<int> bits = new List<int>();
    int i;
    for (i = 0; i < length; i++)
    {
      bits.Add(0);
    }
    if (num == 0)
    {
      return bits;
    }

    i = length - 1;
    while (num != 0)
    {
      bits[i] = (num % 2);
      i = i - 1;

      // Integer division
      // gives quotient
      num = num / 2;
    }

    return bits;
  }

  // Function to convert all numbers
  // in range [L, R] to binary of
  // same length
  static List<List<int>> getAllBinary(int l, int r)
  {

    // Length of the binary numbers
    double x = Math.Log(r + 1);
    double y = Math.Log(2);
    int n = (int)Math.Ceiling(x / y);

    List<List<int>> binary_nos = new List<List<int>>();

    for (int i = l; i <= r; i++)
    {
      List<int> bits = convertToBinary(i, n);
      binary_nos.Add(bits);
    }

    return binary_nos;
  }

  // Driver code
  public static void Main()
  {
    int L = 2, R = 8;
    List<List<int>> binary_nos = getAllBinary(L, R);
    for (int i = 0; i < binary_nos.Count; i++)
    {
      for (int j = 0; j < binary_nos[i].Count; j++)
      {
        Console.Write(binary_nos[i][j]);
      }
      Console.WriteLine("");
    }
  }
}

// This code is contributed by Saurabh Jaiswal
```

## **java 描述语言**

```
<script>
    // JavaScript code to implement the approach

    // Function to convert a number to binary
    const convertToBinary = (num, length) => {
        let bits = new Array(length).fill(0);
        if (num == 0) {
            return bits;
        }

        let i = length - 1;
        while (num != 0) {
            bits[i--] = (num % 2);

            // Integer division
            // gives quotient
            num = parseInt(num / 2);
        }
        return bits;
    }

    // Function to convert all numbers
    // in range [L, R] to binary of
    // same length
    const getAllBinary = (l, r) => {

        // Length of the binary numbers
        let n = Math.ceil(Math.log(r + 1) / Math.log(2));

        let binary_nos = [];

        for (let i = l; i <= r; i++) {
            let bits = convertToBinary(i, n);
            binary_nos.push(bits);
        }

        return binary_nos;
    }

    // Driver code

    let L = 2, R = 8;
    let binary_nos = getAllBinary(L, R);
    for (let i = 0; i < binary_nos.length;
        i++) {
        for (let j = 0; j <
            binary_nos[i].length; j++)
            document.write(binary_nos[i][j]);
        document.write("<br/>");
    }

    // This code is contributed by rakeshsahni

</script>
```

****Output**

```
0010
0011
0100
0101
0110
0111
1000
```** 

****时间复杂度:** O(N * logR)其中 N =(R–L+1)
T3】辅助空间: O(N * logR)**