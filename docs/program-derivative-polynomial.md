# 多项式导数程序

> 原文:[https://www . geesforgeks . org/program-导数-多项式/](https://www.geeksforgeeks.org/program-derivative-polynomial/)

给定一个多项式作为字符串和值。求给定值的多项式导数。
**注意:**输入格式是术语和“+”符号之间有一个空格

> p(x) = ax^n 的导数是 p'(x) = a*n*x^(n-1)
> 同样，如果 p(x) = p1(x) + p2(x)
> 这里 p1 和 p2 也是多项式
> p '(x)= P1′(x)+p2′(x)

```
Input : 3x^3 + 4x^2 + 6x^1 + 89x^0
        2             
Output :58 
Explanation : Derivative of given
polynomial is : 9x^2 + 8x^1 + 6
Now put x = 2
9*4 + 8*2 + 6 = 36 + 16 + 6 = 58  

Input : 1x^3
        3
Output : 27
```

我们将输入字符串分割成标记，并为每个项分别计算每个项的导数，然后将它们相加得到结果。

## C++

```
// C++ program to find value of derivative of
// a polynomial.
#include <bits/stdc++.h>
using namespace std;

long long derivativeTerm(string pTerm, long long val)
{
    // Get coefficient
    string coeffStr = "";
    int i;
    for (i = 0; pTerm[i] != 'x'; i++)
        coeffStr.push_back(pTerm[i]);
    long long coeff = atol(coeffStr.c_str());

    // Get Power (Skip 2 characters for x and ^)
    string powStr = "";
    for (i = i + 2; i != pTerm.size(); i++)
        powStr.push_back(pTerm[i]);
    long long power = atol(powStr.c_str());

    // For ax^n, we return anx^(n-1)
    return coeff * power * pow(val, power - 1);
}

long long derivativeVal(string& poly, int val)
{
    long long ans = 0;

    // We use istringstream to get input in tokens
    istringstream is(poly);

    string pTerm;
    while (is >> pTerm) {

        // If the token is equal to '+' then
        // continue with the string
        if (pTerm == "+")
            continue;

        // Otherwise find the derivative of that
        // particular term
        else
            ans = (ans + derivativeTerm(pTerm, val));
    }
    return ans;
}

// Driver code
int main()
{
    string str = "4x^3 + 3x^1 + 2x^2";
    int val = 2;
    cout << derivativeVal(str, val);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find value of derivative of
// a polynomial
import java.io.*;
class GFG
{

  static long derivativeTerm(String pTerm, long val)
  {

    // Get coefficient
    String coeffStr = "";
    int i;
    for (i = 0; pTerm.charAt(i) != 'x' ; i++)
    {
      if(pTerm.charAt(i)==' ')
        continue;
      coeffStr += (pTerm.charAt(i));
    }

    long coeff = Long.parseLong(coeffStr);

    // Get Power (Skip 2 characters for x and ^)
    String powStr = ""; 
    for (i = i + 2; i != pTerm.length() && pTerm.charAt(i) != ' '; i++)
    {
      powStr += pTerm.charAt(i);
    }

    long power=Long.parseLong(powStr);

    // For ax^n, we return a(n)x^(n-1)
    return coeff * power * (long)Math.pow(val, power - 1);
  }
  static long derivativeVal(String poly, int val)
  {
    long ans = 0;

    int i = 0;
    String[] stSplit = poly.split("\\+");
    while(i<stSplit.length)
    {
      ans = (ans +derivativeTerm(stSplit[i], val));
      i++;
    }
    return ans;
  }

  // Driver code
  public static void main (String[] args) {

    String str = "4x^3 + 3x^1 + 2x^2";
    int val = 2;

    System.out.println(derivativeVal(str, val));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to find
# value of derivative of
# a polynomial.
def derivativeTerm(pTerm, val):

    # Get coefficient
    coeffStr = ""

    i = 0
    while (i < len(pTerm) and
           pTerm[i] != 'x'):
        coeffStr += (pTerm[i])
        i += 1

    coeff = int(coeffStr)

    # Get Power (Skip 2 characters
    # for x and ^)
    powStr = ""
    j = i + 2
    while j < len(pTerm):
        powStr += (pTerm[j])
        j += 1

    power = int(powStr)

    # For ax^n, we return
    # a(n)x^(n-1)
    return (coeff * power *
            pow(val, power - 1))

def derivativeVal(poly, val):

    ans = 0
    i = 0
    stSplit = poly.split("+")

    while (i < len(stSplit)):     
        ans = (ans +
               derivativeTerm(stSplit[i],
                              val))
        i += 1

    return ans

# Driver code
if __name__ == "__main__":

    st = "4x^3 + 3x^1 + 2x^2"
    val = 2   
    print(derivativeVal(st, val))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find value of derivative of
// a polynomial
using System;

class GFG{

static long derivativeTerm(string pTerm, long val)
{

    // Get coefficient
    string coeffStr = "";
    int i;

    for(i = 0; pTerm[i] != 'x'; i++)
    {
        if (pTerm[i] == ' ')
            continue;

        coeffStr += (pTerm[i]);
    }

    long coeff = long.Parse(coeffStr);

    // Get Power (Skip 2 characters for x and ^)
    string powStr = ""; 
    for(i = i + 2;
        i != pTerm.Length && pTerm[i] != ' ';
        i++)
    {
        powStr += pTerm[i];
    }

    long power = long.Parse(powStr);

    // For ax^n, we return a(n)x^(n-1)
    return coeff * power * (long)Math.Pow(val, power - 1);
}

static long derivativeVal(string poly, int val)
{
    long ans = 0;

    int i = 0;
    String[] stSplit = poly.Split("+");

    while (i < stSplit.Length)
    {
        ans = (ans +derivativeTerm(stSplit[i], val));
        i++;
    }
    return ans;
}

// Driver code
static public void Main()
{
    String str = "4x^3 + 3x^1 + 2x^2";
    int val = 2;

    Console.WriteLine(derivativeVal(str, val));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program to find value of derivative of
// a polynomial

function derivativeTerm( pTerm,val)
{
    // Get coefficient
    let coeffStr = "";
    let i;
    for (i = 0; pTerm[i] != 'x' ; i++)
    {
      if(pTerm[i]==' ')
        continue;
      coeffStr += (pTerm[i]);
    }

    let coeff = parseInt(coeffStr);

    // Get Power (Skip 2 characters for x and ^)
    let powStr = "";
    for (i = i + 2; i != pTerm.length && pTerm[i] != ' '; i++)
    {
      powStr += pTerm[i];
    }

    let power=parseInt(powStr);

    // For ax^n, we return a(n)x^(n-1)
    return coeff * power * Math.pow(val, power - 1);
}

function derivativeVal(poly,val)
{
    let ans = 0;

    let i = 0;
    let stSplit = poly.split("+");
    while(i<stSplit.length)
    {
      ans = (ans +derivativeTerm(stSplit[i], val));
      i++;
    }
    return ans;
}

 // Driver code
let str = "4x^3 + 3x^1 + 2x^2";
let val = 2;
document.write(derivativeVal(str, val));

// This code is contributed by ab2127
</script>
```

**输出:**

```
59
```

本文由 [**安基特·贾恩**](https://www.facebook.com/profile.php?id=100000412091676) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。