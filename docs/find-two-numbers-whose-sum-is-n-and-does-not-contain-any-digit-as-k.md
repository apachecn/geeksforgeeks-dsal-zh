# 找出两个和为 N 且不含任何数字的数作为 K

> 原文:[https://www . geesforgeks . org/find-two-numbers-其和为-n-且-不包含任何数字-as-k/](https://www.geeksforgeeks.org/find-two-numbers-whose-sum-is-n-and-does-not-contain-any-digit-as-k/)

给定一个整数***N*****任务是找到两个数字 *a 和 b* ，使得 ***a + b = N*** ，其中 *a 和 b* 不包含任何与 **K** 相同的数字。如果不可能，打印 **-1** 。**

****示例:****

> ****输入:** N = 100，K = 0
> **输出:** 1 99
> **说明:**
> 1 + 99 = 100，其中没有一个数字是 0。**
> 
> ****输入:** N = 123456789，K = 2
> **输出:** 3456790 119999999
> **说明:**
> 3456790+11999999999 = 123456789，没有一个数字里面有 2。**

****方法:**思路是迭代一个从 **i = 1 到 n-1** 的循环，检查 **i** 和**(n–I)**是否不包含 **K** 。如果它不包含任何数字，那么打印这两个数字，并打破循环。**

> **例如: **N = 11，k = 0**
> i = 1，N–1 = 10 但是 10 包含 0，所以增量 i
> i = 2，N–1 = 9，所以打印这个 I 和 N–I**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for
// the above approach
#include<bits/stdc++.h>
using namespace std;

int freqCount(string str, char k)
{
    int count = 0;
    for(int i = 0;
            i < str.size(); i++)
    {
        if (str[i] == k)
        count++;
    }
    return count;
}

// Function to find two
// numbers whose sum
// is N and do not
// contain any digit as k
void findAandB(int n, int k)
{
    int flag = 0;

    // Check every number i and (n-i)
    for(int i = 1; i < n; i++)
    {
        // Check if i and n-i doesn't
        // contain k in them print i and n-i
        if (freqCount(to_string(i),
                     (char)(k + 48)) == 0 and
            freqCount(to_string(n - i),
                     (char)(k + 48)) == 0)
        {
            cout << "(" << i << ", "
                 << n - i << ")";
            flag = 1;
            break;
        }
    }

    // Check if flag is 0
    // then print -1
    if (flag == 0)
        cout << -1;
}

// Driver Code
int main()
{

    // Given N and K
    int N = 100;
    int K = 0;

    // Function call
    findAandB(N, K);
    return 0;
}

// This code is contributed by Rajput-Ji
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

static int freqCount(String str, char k)
{
    int count = 0;
    for(int i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) == k)
            count++;
    }
    return count;
}

// Function to find two numbers
// whose sum is N and do not
// contain any digit as k
static void findAandB(int n, int k)
{
    int flag = 0;

    // Check every number i and (n-i)
    for(int i = 1; i < n; i++)
    {

        // Check if i and n-i doesn't
        // contain k in them print i and n-i
        if (freqCount(Integer.toString(i),
                     (char)(k + 48)) == 0 &&
            freqCount(Integer.toString(n - i),
                     (char)(k + 48)) == 0)
        {
            System.out.print("(" + i + ", " +
                              (n - i) + ")");
            flag = 1;
            break;
        }
    }

    // Check if flag is 0
    // then print -1
    if (flag == 0)
        System.out.print(-1);
}

// Driver code
public static void main(String[] args)
{

    // Given N and K
    int N = 100;
    int K = 0;

    // Function call
    findAandB(N, K);
}
}

// This code is contributed by offbeat
```

## **计算机编程语言**

```
# Python program for the above approach

# Function to find two numbers whose sum
# is N and do not contain any digit as k
def findAandB(n, k):

    flag = 0

    # Check every number i and (n-i)
    for i in range(1, n):

        # Check if i and n-i doesn't
        # contain k in them print i and n-i
        if str(i).count(chr(k + 48)) == 0 \
        and str(n-i).count(chr(k + 48)) == 0:
            print(i, n-i)
            flag = 1
            break

    # check if flag is 0 then print -1
    if(flag == 0):
        print(-1)

# Driver Code
if __name__ == '__main__':

  # Given N and K
    N = 100
    K = 0

    # Function Call
    findAandB(N, K)
```

## **C#**

```
// C# program for the
// above approach
using System;
class GFG{

static int freqCount(String str,
                     char k)
{
  int count = 0;

  for(int i = 0; i < str.Length; i++)
  {
    if (str[i] == k)
      count++;
  }

  return count;
}

// Function to find two numbers
// whose sum is N and do not
// contain any digit as k
static void findAandB(int n, int k)
{
  int flag = 0;

  // Check every number i and (n-i)
  for(int i = 1; i < n; i++)
  {
    // Check if i and n-i doesn't
    // contain k in them print i and n-i
    if (freqCount(i.ToString(),
                 (char)(k + 48)) == 0 &&
        freqCount((n-i).ToString(),
                  (char)(k + 48)) == 0)
    {
      Console.Write("(" + i + ", " +
                    (n - i) + ")");
      flag = 1;
      break;
    }
  }

  // Check if flag is 0
  // then print -1
  if (flag == 0)
    Console.Write(-1);
}

// Driver code
public static void Main(String[] args)
{
  // Given N and K
  int N = 100;
  int K = 0;

  // Function call
  findAandB(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript program for
// the above approach

function freqCount(str, k)
{
    var count = 0;
    for(var i = 0;
            i < str.length; i++)
    {
        if (str[i] == k)
        count++;
    }
    return count;
}

// Function to find two
// numbers whose sum
// is N and do not
// contain any digit as k
function findAandB(n, k)
{
    var flag = 0;

    // Check every number i and (n-i)
    for(var i = 1; i < n; i++)
    {
        // Check if i and n-i doesn't
        // contain k in them print i and n-i
        if (freqCount(i.toString(),
                     String.fromCharCode(k + 48)) == 0 &&
            freqCount((n - i).toString(),
                     String.fromCharCode(k + 48)) == 0)
        {
            document.write( "(" + i + ", "
                 + (n - i) + ")");
            flag = 1;
            break;
        }
    }

    // Check if flag is 0
    // then print -1
    if (flag == 0)
        cout + -1;
}

// Driver Code
// Given N and K
var N = 100;
var K = 0;

// Function call
findAandB(N, K);

// This code is contributed by rrrtnx.
</script>
```

****Output:** 

```
(1, 99)
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**