# 将[L，R]范围内的所有数字转换为二进制数

> 原文:[https://www . geesforgeks . org/convert-all-numbers-in-range-l-r-to-binary-number/](https://www.geeksforgeeks.org/convert-all-numbers-in-range-l-r-to-binary-number/)

给定两个正整数 **L** 和 **R** 。任务是把 L 到 R 的所有数字转换成二进制数。

**示例:**

> **输入:** L = 1，R = 4
> **输出:**
> 1
> 10
> 11
> 100
> **解释:**数字 1、2、3、4 的二进制表示为:
> 1 =(1)<sub>2</sub>
> 2 =(10)<sub>2</sub>
> 3 =(11)<sub>2【T20</sub>
> 
> **输入:** L = 2，R = 8
> **输出:**
> 10
> 11
> 100
> 101
> 110
> 111
> 1000

**方法:**问题可以用以下方法解决。

*   从左到右遍历，将每个数字转换为二进制数。
*   存储每个数字，并在最后打印出来。

下面是上述方法的实现。

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert a number
// to its binary equivalent
vector<int> convertToBinary(int num)
{
    vector<int> bits;
    if (num == 0) {
        bits.push_back(0);
        return bits;
    }

    while (num != 0) {
        bits.push_back(num % 2);

        // Integer division
        // gives quotient
        num = num / 2;
    }
    reverse(bits.begin(), bits.end());
    return bits;
}

// Function to convert all numbers
// in range [L, R] to binary
vector<vector<int> > getAllBinary(int l,
                                  int r)
{
    // Vector to store the binary
    // representations of the numbers
    vector<vector<int> > binary_nos;
    for (int i = l; i <= r; i++) {
        vector<int> bits =
            convertToBinary(i);
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
        for (int j = 0; j < binary_nos[i].size();
            j++)
            cout << binary_nos[i][j];
        cout << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.ArrayList;
import java.util.Collections;

class GFG {

  // Function to convert a number
  // to its binary equivalent
  public static ArrayList<Integer> convertToBinary(int num) {
    ArrayList<Integer> bits = new ArrayList<Integer>();
    if (num == 0) {
      bits.add(0);
      return bits;
    }

    while (num != 0) {
      bits.add(num % 2);

      // Integer division
      // gives quotient
      num = num / 2;
    }
    Collections.reverse(bits);
    return bits;
  }

  // Function to convert all numbers
  // in range [L, R] to binary
  public static ArrayList<ArrayList<Integer>> getAllBinary(int l, int r)
  {

    // Vector to store the binary
    // representations of the numbers
    ArrayList<ArrayList<Integer>> binary_nos = new ArrayList<ArrayList<Integer>>();
    for (int i = l; i <= r; i++)
    {
      ArrayList<Integer> bits = convertToBinary(i);
      binary_nos.add(bits);
    }
    return binary_nos;
  }

  // Driver code
  public static void main(String args[])
  {
    int L = 2, R = 8;
    ArrayList<ArrayList<Integer>> binary_nos = getAllBinary(L, R);
    for (int i = 0; i < binary_nos.size(); i++) {
      for (int j = 0; j < binary_nos.get(i).size(); j++)
        System.out.print(binary_nos.get(i).get(j));
      System.out.println("");
    }
  }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 code to implement the above approach

# Function to convert a number
# to its binary equivalent
def convertToBinary(num):

    bits = []
    if (num == 0):
        bits.append(0)
        return bits

    while (num != 0):
        bits.append(num % 2)

        # Integer division
        # gives quotient
        num = num // 2

    bits.reverse()
    return bits

# Function to convert all numbers
# in range [L, R] to binary
def getAllBinary(l, r):

    # Vector to store the binary
    # representations of the numbers
    binary_nos = []
    for i in range(l, r+1):
        bits = convertToBinary(i)
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

## C#

```
// C# code to implement the above approach
using System;
using System.Collections.Generic;

public class GFG {

  // Function to convert a number
  // to its binary equivalent
  public static List<int> convertToBinary(int num) {
    List<int> bits = new List<int>();
    if (num == 0) {
      bits.Add(0);
      return bits;
    }

    while (num != 0) {
      bits.Add(num % 2);

      // int division
      // gives quotient
      num = num / 2;
    }
    bits.Reverse();
    return bits;
  }

  // Function to convert all numbers
  // in range [L, R] to binary
  public static List<List<int>> getAllBinary(int l, int r)
  {

    // List to store the binary
    // representations of the numbers
    List<List<int>> binary_nos = new List<List<int>>();
    for (int i = l; i <= r; i++)
    {
      List<int> bits = convertToBinary(i);
      binary_nos.Add(bits);
    }
    return binary_nos;
  }

  // Driver code
  public static void Main(String []args)
  {
    int L = 2, R = 8;
    List<List<int>> binary_nos = getAllBinary(L, R);
    for (int i = 0; i < binary_nos.Count; i++) {
      for (int j = 0; j < binary_nos[i].Count; j++)
        Console.Write(binary_nos[i][j]);
      Console.WriteLine("");
    }
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // JavaScript code to implement the above approach

    // Function to convert a number
    // to its binary equivalent
    const convertToBinary = (num) => {
        let bits = [];
        if (num == 0) {
            bits.push(0);
            return bits;
        }

        while (num != 0) {
            bits.push(num % 2);

            // Integer division
            // gives quotient
            num = parseInt(num / 2);
        }
        bits.reverse()
        return bits;
    }

    // Function to convert all numbers
    // in range [L, R] to binary
    const getAllBinary = (l, r) => {

        // Vector to store the binary
        // representations of the numbers
        let binary_nos = [];
        for (let i = l; i <= r; i++) {
            let bits = convertToBinary(i);
            binary_nos.push(bits);
        }
        return binary_nos;
    }

    // Driver code
    let L = 2, R = 8;
    let binary_nos = getAllBinary(L, R);
    for (let i = 0; i < binary_nos.length;
        i++) {
        for (let j = 0; j < binary_nos[i].length;
            j++)
            document.write(`${binary_nos[i][j]}`);
        document.write("<br/>");
    }

    // This code is contributed by rakeshsahni
</script>
```

**Output**

```
10
11
100
101
110
111
1000
```

**时间复杂度:** O(N * LogR)其中 N 是范围【L，R】
**内数字的计数辅助空间:** O(N * logR)