# 大于 X 的最小数，为 K 周期

> 原文:[https://www . geesforgeks . org/minist-number-behind-x-is-k-periodic/](https://www.geeksforgeeks.org/smallest-number-greater-than-x-which-is-k-periodic/)

给定一个由 **N** 数字和一个整数 **K** 组成的字符串整数 **X** ，任务是找出大于或等于 **X** 的最小整数，它是[T9】K 周期](https://www.geeksforgeeks.org/check-if-the-given-string-is-k-periodic/) **(K < = N)** 。

**示例:**

> **输入:** K = 2，X =“1215”
> **输出:** 1313
> **解释:**
> 1313 是 2 周期的，因为位置 1、3 的数字是‘1’，位置 2、4 的数字是‘3’。这是大于或等于“1215”的最小 2 周期整数。
> 
> **输入:** K = 3，X =“299398”
> **输出:** 300300
> **说明:**
> 300300 是最小可能的 3 周期数。

**做法:**
要解决问题，思路是让**X<sub>I</sub>= X<sub>I-K</sub>T8】为所有 **i > K** 。然后按照以下步骤解决问题:**

*   检查 **X** 是否大于或等于初始整数。如果是，则打印当前字符串作为答案。
*   否则，从右向左遍历，找到不等于 **9** 的第一个数字。然后将该数字增加 **1** ，并用一个名为 ***的变量标记该位置。***
*   然后将**后的所有数字设置为 ***K <sup>th</sup>*** 数字至 **0** 。再次使**X<sub>I</sub>= X<sub>I-K</sub>**为所有 **i > K** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to find the
// smallest K periodic
// integer greater than X
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// smallest K periodic
// integer greater than X
string Kperiodicinteger(string X, int N,
                        int K)
{
    // Stores the number
    // in a temporary string
    string temp = X;

    // Set X[i]=X[i-k] for
    // i>k
    for (int i = 0; i < K; i++)

    {
        // Start from
        // the current
        // index
        int j = i;

        // Loop upto N
        // change
        // X[j] to X[i]
        while (j < N) {
            X[j] = X[i];
            j += K;
        }
    }

    // Return X if current
    // Value is greater
    // than original value
    if (X >= temp) {

        return X;
    }

    int POS;

    // Find the first
    // digit not equal to 9
    for (int i = K - 1; i >= 0; i--) {
        if (X[i] != '9') {

        // Increment X[i]
            X[i]++;

            // Set POS to
            // current index
            POS = i;

            break;
        }
    }

    // Change X[i] to 0
    // for all indices
    // from POS+1 to K
    for (int i = POS + 1; i < K; i++) {
        X[i] = '0';
    }

    // Set X[i]=X[i-k] for
    // i>k
    for (int i = 0; i < K; i++)

    {
        int j = i;
        // Loop upto N
        // change
        // X[j] to X[i]

        while (j < N) {
            X[j] = X[i];
            j += K;
        }
    }

    // Return the
    // final string
    return X;
}

// Driver Code
int main()
{

    int N = 4, K = 2;

    string X = "1215";

    cout << Kperiodicinteger(X, N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the smallest
// K periodic integer greater than X
import java.util.*;

class GFG{

// Function to find the
// smallest K periodic
// integer greater than X
static String Kperiodicinteger(char []X,
                            int N, int K)
{

    // Stores the number
    // in a temporary String
    String temp = String.valueOf(X);

    // Set X[i]=X[i-k] for
    // i>k
    for(int i = 0; i < K; i++)
    {

        // Start from the current
        // index
        int j = i;

        // Loop upto N change
        // X[j] to X[i]
        while (j < N)
        {
            X[j] = X[i];
            j += K;
        }
    }

    // Return X if current
    // Value is greater
    // than original value
    if (String.valueOf(X).compareTo(temp) >= 0)
    {
        return String.valueOf(X);
    }

    int POS = 0;

    // Find the first
    // digit not equal to 9
    for(int i = K - 1; i >= 0; i--)
    {
        if (X[i] != '9')
        {

            // Increment X[i]
            X[i]++;

            // Set POS to
            // current index
            POS = i;
            break;
        }
    }

    // Change X[i] to 0
    // for all indices
    // from POS+1 to K
    for(int i = POS + 1; i < K; i++)
    {
        X[i] = '0';
    }

    // Set X[i]=X[i-k] for
    // i>k
    for(int i = 0; i < K; i++)
    {
        int j = i;

        // Loop upto N change
        // X[j] to X[i]
        while (j < N)
        {
            X[j] = X[i];
            j += K;
        }
    }

    // Return the
    // final String
    return String.valueOf(X);
}

// Driver Code
public static void main(String[] args)
{
    int N = 4, K = 2;
    String X = "1215";

    System.out.print(Kperiodicinteger(
            X.toCharArray(), N, K));
}
}

// This code is contributed by sapnasingh4991
```

## **蟒蛇 3**

```
# Python3 program to find the smallest
# K periodic integer greater than X

# Function to find the 
# smallest K periodic 
# integer greater than X
def Kperiodicinteger(X, N, K):

    X = list(X)

    # Stores the number 
    # in a temporary string 
    temp = X.copy()

    # Set X[i]=X[i-k] for 
    # i>k
    for i in range(K):

        # Start from the current 
        # index 
        j = i

        # Loop upto N change 
        # X[j] to X[i]
        while (j < N):
            X[j] = X[i]
            j += K

    # Return X if current 
    # Value is greater 
    # than original value 
    if (X >= temp):
        return X

    POS = 0

    # Find the first digit
    # not equal to 9
    for i in range(K - 1, -1, -1):
        if (X[i] != '9'):

            # Increment X[i] 
            X[i] = str(int(X[i]) + 1)

            # Set POS to 
            # current index
            POS = i
            break

    # Change X[i] to 0 
    # for all indices 
    # from POS+1 to K 
    for i in range(POS + 1, K):
        X[i] = '0'

    # Set X[i]=X[i-k] for 
    # i>k
    for i in range(K):
        j = i

        # Loop upto N 
        # change 
        # X[j] to X[i]
        while (j < N):
            X[j] = X[i]
            j += K

    # Return the 
    # final string 
    return X

# Driver Code
N = 4
K = 2
X = "1215"

print(*Kperiodicinteger(X, N, K), sep = '')

# This code is contributed by avanitrachhadiya2155
```

## **C#**

```
// C# program to find the smallest
// K periodic integer greater than X
using System;

class GFG{

// Function to find the
// smallest K periodic
// integer greater than X
static String Kperiodicinteger(char[] X,
                               int N, int K)
{

    // Stores the number
    // in a temporary String
    String temp = String.Join("", X);

    // Set X[i]=X[i-k] for
    // i>k
    for(int i = 0; i < K; i++)
    {

        // Start from the current
        // index
        int j = i;

        // Loop upto N change
        // X[j] to X[i]
        while (j < N)
        {
            X[j] = X[i];
            j += K;
        }
    }

    // Return X if current
    // Value is greater
    // than original value
    if (String.Join("", X).CompareTo(temp) >= 0)
    {
        return String.Join("", X);
    }

    int POS = 0;

    // Find the first
    // digit not equal to 9
    for(int i = K - 1; i >= 0; i--)
    {
        if (X[i] != '9')
        {

            // Increment X[i]
            X[i]++;

            // Set POS to
            // current index
            POS = i;
            break;
        }
    }

    // Change X[i] to 0
    // for all indices
    // from POS+1 to K
    for(int i = POS + 1; i < K; i++)
    {
        X[i] = '0';
    }

    // Set X[i]=X[i-k] for
    // i>k
    for(int i = 0; i < K; i++)
    {
        int j = i;

        // Loop upto N change
        // X[j] to X[i]
        while (j < N)
        {
            X[j] = X[i];
            j += K;
        }
    }

    // Return the
    // readonly String
    return String.Join("", X);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4, K = 2;
    String X = "1215";

    Console.Write(Kperiodicinteger(
          X.ToCharArray(), N, K));
}
}

// This code is contributed by sapnasingh4991
```

## **java 描述语言**

```
<script>

// Javascript Program to find the
// smallest K periodic
// integer greater than X

// Function to find the
// smallest K periodic
// integer greater than X
function Kperiodicinteger(X, N, K)
{
    // Stores the number
    // in a temporary string
    var temp = X

    // Set X[i]=X[i-k] for
    // i>k
    for (var i = 0; i < K; i++)

    {
        // Start from
        // the current
        // index
        var j = i;

        // Loop upto N
        // change
        // X[j] to X[i]
        while (j < N) {
            X[j] = X[i];
            j += K;
        }
    }

    // Return X if current
    // Value is greater
    // than original value
    if (parseInt(X.join('')) < parseInt(temp.join(''))) {

        return X.join('');
    }

    var POS;

    // Find the first
    // digit not equal to 9
    for (var i = K - 1; i >= 0; i--) {
        if (X[i] != '9') {

        // Increment X[i]
            X[i] = String.fromCharCode(X[i].charCodeAt(0) + 1);

            // Set POS to
            // current index
            POS = i;

            break;
        }
    }

    // Change X[i] to 0
    // for all indices
    // from POS+1 to K
    for (var i = POS + 1; i < K; i++) {
        X[i] = '0';
    }

    // Set X[i]=X[i-k] for
    // i>k
    for (var i = 0; i < K; i++)

    {
        var j = i;
        // Loop upto N
        // change
        // X[j] to X[i]

        while (j < N) {
            X[j] = X[i];
            j += K;
        }
    }

    // Return the
    // final string
    return X.join('');
}

// Driver Code
var N = 4, K = 2;
var X = "1215";
document.write( Kperiodicinteger(X.split(''), N, K));

// This code is contributed by itsok.
</script>
```

****Output:** 

```
1313
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**