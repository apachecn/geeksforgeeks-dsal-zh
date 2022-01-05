# N 位二进制数

> 原文:[https://www.geeksforgeeks.org/binary-numbers-of-n-digits/](https://www.geeksforgeeks.org/binary-numbers-of-n-digits/)

给定一个正整数 **N** 。任务是生成 **N 位**的所有二进制数。这些二进制数应该按照**升序**排列。

**示例:**

> **输入:**2
> T3】输出:T5】00
> 01
> 10
> 11
> T10】说明:这 4 个是仅有的 2 位数二进制数。
> 
> **输入:**3
> T3】输出:T5】0 0 0
> 0 0 1
> 0 1 0
> 0 1 1
> 1 0 0
> 1 0 1
> 1 1 0
> 1 1 1 1

**逼近:**对于任意位数长度 N，都会有**2<sup>N</sup>T5】二进制数。**

*   因此从 **0 到 2 <sup>N</sup>** 遍历，并将每个数字转换为二进制。
*   存储每个数字，并在最后打印出来。

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert number
// to binary of N bits
vector<int> convertToBinary(int num,
                            int length)
{
    // Vector to store the number
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

// Function to generate all
// N bit binary numbers
vector<vector<int> > getAllBinary(int n)
{
    vector<vector<int> > binary_nos;

    // Loop to generate the binary numbers
    for (int i = 0; i < pow(2, n); i++) {
        vector<int> bits =
            convertToBinary(i, n);
        binary_nos.push_back(bits);
    }

    return binary_nos;
}

// Driver code
int main()
{
    int N = 3;
    vector<vector<int> > binary_nos =
        getAllBinary(N);
    for (int i = 0; i < binary_nos.size();
           i++) {
        for (int j = 0;
                j < binary_nos[i].size(); j++)
            cout << binary_nos[i][j];
        cout << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG {

  // Function to convert number
  // to binary of N bits
  static int[] convertToBinary(int num,
                               int length)
  {

    // Vector to store the number
    int[] bits = new int[length];
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

  // Function to generate all
  // N bit binary numbers
  static int[][] getAllBinary(int n)
  {
    int[][] binary_nos = new int[(int)Math.pow(2,n)][];
    int k = 0;

    // Loop to generate the binary numbers
    for (int i = 0; i < Math.pow(2, n); i++) {
      int[] bits = convertToBinary(i, n);
      binary_nos[k++]= bits;
    }

    return binary_nos;
  }

  // Driver code
  public static void main (String[] args)
  {
    int N = 3;
    int[][] binary_nos = getAllBinary(N);
    for (int i = 0; i < binary_nos.length; i++) {
      for (int j = 0; j < binary_nos[i].length; j++)
        System.out.print(binary_nos[i][j]);
      System.out.println();
    }

  }
};

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 code to implement above approach

# Function to convert number
# to binary of N bits
def convertToBinary(num,
                    length):

    # Vector to store the number
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

# Function to generate all
# N bit binary numbers
def getAllBinary(n):

    binary_nos = []

    # Loop to generate the binary numbers
    for i in range(pow(2, n)):
        bits = convertToBinary(i, n)
        binary_nos.append(bits)

    return binary_nos

# Driver code
if __name__ == "__main__":

    N = 3
    binary_nos = getAllBinary(N)
    for i in range(len(binary_nos)):
        for j in range(len(binary_nos[i])):
            print(binary_nos[i][j], end="")
        print()

        # This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript code to implement above approach

    // Function to convert number
    // to binary of N bits
    const convertToBinary = (num, length) => {
        // Vector to store the number
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

    // Function to generate all
    // N bit binary numbers
    const getAllBinary = (n) => {
        let binary_nos = [];

        // Loop to generate the binary numbers
        for (let i = 0; i < parseInt(Math.pow(2, n)); i++) {
            let bits = convertToBinary(i, n);
            binary_nos.push(bits);
        }

        return binary_nos;
    }

    // Driver code

    let N = 3;
    let binary_nos = getAllBinary(N);
    for (let i = 0; i < binary_nos.length;
        i++) {
        for (let j = 0;
            j < binary_nos[i].length; j++)
            document.write(binary_nos[i][j]);
        document.write("<br/>");
    }

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
000
001
010
011
100
101
110
111
```

**时间复杂度:**O(2<sup>N</sup>)
T5】辅助空间: O(2 <sup>N</sup>