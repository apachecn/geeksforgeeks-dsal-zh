# 打印分母小于等于 N 的所有正确分数

> 原文:[https://www . geeksforgeeks . org/print-all-perfect-带分母的分数-小于等于 n/](https://www.geeksforgeeks.org/print-all-proper-fractions-with-denominators-less-than-equal-to-n/)

给定一个整数 **N** ，任务是打印所有合适的分数，使分母小于或等于 N

> **适当分数:**如果分子小于分母，则称分数为适当分数。

**示例:**

> **输入:**N = 3
> T3】输出: 1/2，1/3，2/3
> 
> **输入:**N = 4
> T3】输出: 1/2、1/3、1/4、2/3、3/4

**方法:**
遍历**【1，N-1】**上的所有记数器，对于每个记数器，遍历**【分子+1，N】**范围内的所有分母，检查分子和分母是否互质。如果发现是互质，那么打印分数。

下面是上述方法的实现:

## C++14

```
// C++ program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all
// proper fractions
void printFractions(int n)
{
    for (int i = 1; i < n; i++) {
        for (int j = i + 1; j <= n; j++) {

            // If the numerator and the
            // denominator are coprime
            if (__gcd(i, j) == 1) {

                string a = to_string(i);
                string b = to_string(j);

                cout << a + "/" + b << ", ";
            }
        }
    }
}

// Driver Code
int main()
{
    int n = 3;
    printFractions(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
class GFG{

// Function to print all
// proper fractions
static void printFractions(int n)
{
    for(int i = 1; i < n; i++)
    {
        for(int j = i + 1; j <= n; j++)
        {

            // If the numerator and the
            // denominator are coprime
            if (__gcd(i, j) == 1)
            {
                String a = String.valueOf(i);
                String b = String.valueOf(j);

                System.out.print(a + "/" +
                                 b + ", ");
            }
        }
    }
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    printFractions(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to print
# all proper functions
def printfractions(n):

  for i in range(1, n):
    for j in range(i + 1, n + 1):

      # If the numerator and
      # denominator are coprime
      if __gcd(i, j) == 1:
        a = str(i)
        b = str(j)
        print(a + '/' + b, end = ", ")

def __gcd(a, b):

  if b == 0:
    return a
  else:
    return __gcd(b, a % b)

# Driver code
if __name__=='__main__':

  n = 3
  printfractions(n)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program to implement the
// above approach
using System;

class GFG{

// Function to print all
// proper fractions
static void printFractions(int n)
{
    for(int i = 1; i < n; i++)
    {
        for(int j = i + 1; j <= n; j++)
        {

            // If the numerator and the
            // denominator are coprime
            if (__gcd(i, j) == 1)
            {
                string a = i.ToString();
                string b = j.ToString();

                Console.Write(a + "/" +
                              b + ", ");
            }
        }
    }
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(string[] args)
{
    int n = 3;

    printFractions(n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print all proper functions
const printFractions = (n) => {
  for (var i = 1; i < n; i++) {
      for (var j = i + 1; j <= n; j++) {

      // If the numerator and denominator are coprime

      if(__gcd(i, j) == 1){
        let a = `${i}`;
        let b = `${j}`;
        document.write(`${a}/${b}, `)
      }
    }
  }
}

const __gcd = (a, b) => {
  if(b == 0){
    return a;
  }else{
    return __gcd(b, a % b);
  }
}

// Driver code
let n = 3;
printFractions(n);

// This article is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
1/2, 1/3, 2/3,
```

***时间复杂度:**O(N<sup>2</sup>log N)*
***辅助空间:** O(1)*