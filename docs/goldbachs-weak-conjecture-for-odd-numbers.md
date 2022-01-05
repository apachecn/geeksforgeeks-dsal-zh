# 奇数的哥德巴赫弱猜想

> 原文:[https://www . geeksforgeeks . org/goldbachs-奇数弱猜想/](https://www.geeksforgeeks.org/goldbachs-weak-conjecture-for-odd-numbers/)

给定一个奇数 N，任务是找出这个数是否可以表示为 3 个素数之和。
**例:**

```
Input: N = 7
Output: Yes
Explanation:
2 + 2 + 3 = 7

Input: N = 17
Output: Yes
Explanation:
2 + 2 + 13 = 17
```

**方法:**
在数论中，哥德巴赫的弱猜想，也称为[奇哥德巴赫猜想](https://en.wikipedia.org/wiki/Goldbach%27s_weak_conjecture)，三元哥德巴赫问题，或 3-素数问题，指出每一个大于 5 的奇数都可以表示为三个素数之和。(一个素数在同一个和中可以多次使用。).
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// if a number can
// be represent as
// as a sum of 3 prime
void check(int n)
{
    if (n % 2 == 1 && n > 5)
        cout << "Yes\n";
    else
        cout << "No\n";
}

// Driver code
int main()
{
    int a = 3;
    int b = 7;
    check(a);
    check(b);
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
    // Function to check
    // if a number can
    // be represent as
    // as a sum of 3 prime

    static void check(int n)
    {
        if (n % 2 == 1 && n > 5)
        {
            System.out.println("YES");
        }
        else
        {
            System.out.println("NO");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 3;
        int b = 7;
        check(a);
        check(b);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Function to check
# if a number can
# be represent as
# as a sum of 3 prime
def check(n):
  if n % 2 == 1 and n > 5:
    print('YES')
  else:
    print('NO')

# Driver code
def main():
  a = 3
  b = 7
  check(a)
  check(b)

main()
```

## C#

```
using System;
class GFG
{
    // Function to check
    // if a number can
    // be represent as
    // as a sum of 3 prime

    static void check(int n)
    {
        if (n % 2 == 1 && n > 5)
        {
            Console.Write("YES");
        }
        else
        {
            Console.WriteLine("NO");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int a = 3;
        int b = 7;
        check(a);
        check(b);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
    // Function to check
    // if a number can
    // be represent as
    // as a sum of 3 prime

    function check(n)
    {
        if (n % 2 == 1 && n > 5)
        {
            document.write("YES");
        }
        else
        {
            document.write("NO" + "<br>");
        }
    }

    // Driver code

        var a = 3;
        var b = 7;
        check(a);
        check(b);

// This code is contributed by shivanisinghss2110
```

**Output:** 

```
NO
YES
```