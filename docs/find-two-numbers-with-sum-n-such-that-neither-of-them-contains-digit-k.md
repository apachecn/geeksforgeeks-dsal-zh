# 找出两个和为 N 的数字，使得它们都不包含数字 K

> 原文:[https://www . geesforgeks . org/find-两个数字加和-n-so-它们都不包含数字-k/](https://www.geeksforgeeks.org/find-two-numbers-with-sum-n-such-that-neither-of-them-contains-digit-k/)

给定一个数字 **N** 和一个数字 **K** (1 < K < = 9)，任务是找到两个整数 **A** 和 **B** ，使得 **A + B = N** 和数字 K 在 A 或 B 中不存在

****示例:****

> ****输入:** N = 443，K = 4
> **输出:** 256，187
> **解释:**
> Sum = 256 + 187 = 443 = N
> 同样，K(4)在 256 或 187
> 中不存在因此，256 和 187 是有效输出。**
> 
> ****输入:** N = 678，K = 9
> **输出:** 311，367
> **解释:**
> Sum = 311 + 367 = 678 = N
> 同样，K(9)在 311 或 367
> 中不存在因此，311 和 367 是有效输出。**

****天真的方法:**
一个简单的方法是运行一个循环，从 1 到 N-1 考虑每个元素(比如 A)。由于 A 和 B 的和必须是 N，相应的 B 将是(N–A)。现在检查 A 和 B 是否都包含 K，如果不包含，则打印 A 和 B。对于更大的输入，如 N = 10 <sup>18</sup> ，这种方法将失败。**

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**

****有效方法:**
给定的问题可以更有效地解决。想法是将 N 的每个数字 **D** 分成两个部分 **D1** 和 **D2** 这样 D1 + D2 = D .取两个字符串 **A** 和 **B** ，A 将包含所有 D1 的，字符串 B 将包含所有 D2 的.
例如 N = 4467，K = 4**

```
**D    D1    D2**
4    2    2
4    2    2
6    6    0
7    7    0 
```

**这里，A 是 2267，B 是 2200。
本办法具体步骤如下:
**1。**遍历 **N** 并考虑其每个数字 **D** 。
**2。**如果数字 D 与 K 相同，将其拆分为 D1 = D / 2 和 D2 = D / 2 + D % 2。
将 D % 2 添加到 D2，以确保 D1 + D2 = D 为偶数和奇数 D。
**3。**否则，将其分解为 D1 = D，D2 = 0。
**4。**继续将 D1 的追加到字符串 A，将 D2 的追加到字符串 b。
**5。**最后，在去掉前导零(如果有)后，打印字符串 A 和 B。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of
// the above approach

#include <iostream>
using namespace std;

string removeLeadingZeros(string str)
{
    // Count leading zeros
    int i = 0;
    int n = str.length();
    while (str[i] == '0' && i < n)
        i++;

    // It removes i characters
    // starting from index 0
    str.erase(0, i);

    return str;
}

void findPairs(int sum, int K)
{

    string A, B;
    A = "";
    B = "";

    string N = to_string(sum);
    int n = N.length();

    // Check each digit of the N
    for (int i = 0; i < n; i++) {

        int D = N[i] - '0';

        // If digit is K break it
        if (D == K) {
            int D1, D2;
            D1 = D / 2;

            // For odd numbers
            D2 = D / 2 + D % 2;

            // Add D1 to A and D2 to B
            A = A + char(D1 + '0');
            B = B + char(D2 + '0');
        }

        // If the digit is not K,
        // no need to break
        // string D in A and 0 in B
        else {
            A = A + char(D + '0');
            B = B + '0';
        }
    }

    // Remove leading zeros
    A = removeLeadingZeros(A);
    B = removeLeadingZeros(B);

    // Print the answer
    cout << A << ", " << B << endl;
}

// Driver code
int main()

{
    int N = 33673;
    int K = 3;

    findPairs(N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
class GFG{

static String removeLeadingZeros(String str)
{

    // Count leading zeros
    int i = 0;
    int n = str.length();

    while (str.charAt(i) == '0' && i < n)
        i++;

    // It removes i characters
    // starting from index 0
    str = str.substring(i);

    return str;
}

static void findPairs(int sum, int K)
{

    String A, B;
    A = "";
    B = "";

    String N = String.valueOf(sum);
    int n = N.length();

    // Check each digit of the N
    for(int i = 0; i < n; i++)
    {
       int D = N.charAt(i) - '0';

       // If digit is K break it
       if (D == K)
       {
           int D1, D2;
           D1 = D / 2;

           // For odd numbers
           D2 = D / 2 + D % 2;

           // Add D1 to A and D2 to B
           A = A + (char)(D1 + '0');
           B = B + (char)(D2 + '0');
       }

       // If the digit is not K,
       // no need to break
       // String D in A and 0 in B
       else
       {
           A = A + (char)(D + '0');
           B = B + '0';
       }
    }

    // Remove leading zeros
    A = removeLeadingZeros(A);
    B = removeLeadingZeros(B);

    // Print the answer
    System.out.print(A + ", " + B + "\n");
}

// Driver code
public static void main(String[] args)
{
    int N = 33673;
    int K = 3;

    findPairs(N, K);
}
}

// This code is contributed by sapnasingh4991
```

## **蟒蛇 3**

```
# Python3 implementation of the
# above approach
def removeLeadingZeros(Str):

    # Count leading zeros
    i = 0
    n = len(Str)

    while (Str[i] == '0' and i < n):
        i += 1

    # It removes i characters
    # starting from index 0
    Str = Str[i:]
    return Str

def findPairs(Sum, K):

    A = ""
    B = ""

    N = str(Sum)
    n = len(N)

    # Check each digit of the N
    for i in range(n):

       D = int(N[i]) - int('0')

       # If digit is K break it
       if (D == K):
           D1 = D // 2;

           # For odd numbers
           D2 = (D // 2) + (D % 2)

           # Add D1 to A and D2 to B
           A = A + (str)(D1 + int('0'))
           B = B + (str)(D2 + int('0'))

       # If the digit is not K,
       # no need to break
       # String D in A and 0 in B
       else:
           A = A + (str)(D + int('0'))
           B = B + '0'

    # Remove leading zeros
    A = removeLeadingZeros(A)
    B = removeLeadingZeros(B)

    # Print the answer
    print(A + ", " + B)

# Driver code
N = 33673
K = 3

findPairs(N, K)

# This code is contributed divyeshrabadiya07
```

## **C#**

```
// C# implementation of the above approach
using System;

class GFG{

static String removeLeadingZeros(String str)
{

    // Count leading zeros
    int i = 0;
    int n = str.Length;

    while (str[i] == '0' && i < n)
        i++;

    // It removes i characters
    // starting from index 0
    str = str.Substring(i);

    return str;
}

static void findPairs(int sum, int K)
{

    String A, B;
    A = "";
    B = "";

    String N = String.Join("", sum);
    int n = N.Length;

    // Check each digit of the N
    for(int i = 0; i < n; i++)
    {
       int D = N[i] - '0';

       // If digit is K break it
       if (D == K)
       {
           int D1, D2;
           D1 = D / 2;

           // For odd numbers
           D2 = D / 2 + D % 2;

           // Add D1 to A and D2 to B
           A = A + (char)(D1 + '0');
           B = B + (char)(D2 + '0');
       }

       // If the digit is not K,
       // no need to break
       // String D in A and 0 in B
       else
       {
           A = A + (char)(D + '0');
           B = B + '0';
       }
    }

    // Remove leading zeros
    A = removeLeadingZeros(A);
    B = removeLeadingZeros(B);

    // Print the answer
    Console.Write(A + ", " + B + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int N = 33673;
    int K = 3;

    findPairs(N, K);
}
}

// This code is contributed by sapnasingh4991
```

## **java 描述语言**

```
<script>

// JavaScript implementation of
// the above approach

function removeLeadingZeros(str)
{
    // Count leading zeros
    var i = 0;
    var n = str.length;
    while (str[i] == '0' && i < n)
        i++;

    return str;
}

function findPairs(sum, K)
{

    var A, B;
    A = "";
    B = "";

    var N = (sum.toString());
    var n = N.length;

    // Check each digit of the N
    for (var i = 0; i < n; i++) {

        var D = N[i] - '0';

        // If digit is K break it
        if (D == K) {
            var D1, D2;
            D1 = parseInt(D / 2);

            // For odd numbers
            D2 = parseInt(D / 2) + D % 2;

            // Add D1 to A and D2 to B
            A = A +
            String.fromCharCode(D1 + '0'.charCodeAt(0));

            B = B +
            String.fromCharCode(D2 + '0'.charCodeAt(0));
        }

        // If the digit is not K,
        // no need to break
        // string D in A and 0 in B
        else {
            A = A +
            String.fromCharCode(D + '0'.charCodeAt(0));
            B = B + '0';
        }
    }

    // Remove leading zeros
    A = removeLeadingZeros(A);
    B = removeLeadingZeros(B);

    // Print the answer
    document.write( A + ", " + B );
}

// Driver code
var N = 33673;
var K = 3;
findPairs(N, K);

</script>
```

****Output:** 

```
11671, 22002
```** 

*****时间复杂度:** O(M)*
***辅助空间:** O(M)*
这里，M 是 n 中的位数。**