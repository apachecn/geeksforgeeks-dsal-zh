# 11 次查询的子串可分性

> 原文:[https://www . geesforgeks . org/sub-string-可分性-11-查询/](https://www.geeksforgeeks.org/sub-string-divisibility-11-queries/)

给定一个大的数字，n(具有直到 10^6 的数字)和以下形式的各种查询:

```
Query(l, r) :  find if the sub-string between the 
               indices l and r (Both inclusive) 
               are divisible by 11\. 
```

**示例:**

```
Input: n = 122164154695
Queries: l = 0 r = 3, l = 1 r = 2, l = 5 r = 9,
         l = 0 r = 11
Output:
True
False
False
True

Explanation:
In the first query, 1221 is divisible by 11
In the second query, 22 is divisible by 11 and so on.
```

我们知道，任何数字如果奇数索引数字之和与偶数索引数字之和之差能被 11 整除，即
*Sum(奇数位数字)–Sum(偶数位数字)应能被 11 整除*。
因此，我们的想法是预处理一个辅助数组，该数组将存储奇数和偶数位置的数字总和。
为了评估一个查询，我们可以在 O(1)中使用辅助数组来回答它。

## C++

```
// C++ program to check divisibility by 11 in
// substrings of a number string
#include <iostream>
using namespace std;

const int MAX = 1000005;

// To store sums of even and odd digits
struct OddEvenSums
{
    // Sum of even placed digits
    int e_sum;

    // Sum of odd placed digits
    int o_sum;
};

// Auxiliary array
OddEvenSums sum[MAX];

// Utility function to evaluate a character's
// integer value
int toInt(char x)
{
    return int(x) - 48;
}

// This function receives the string representation
// of the number and precomputes the sum array
void preCompute(string x)
{
    // Initialize everb
    sum[0].e_sum = sum[0].o_sum = 0;

    // Add the respective digits depending on whether
    // they're even indexed or odd indexed
    for (int i=0; i<x.length(); i++)
    {
        if (i%2==0)
        {
            sum[i+1].e_sum = sum[i].e_sum+toInt(x[i]);
            sum[i+1].o_sum = sum[i].o_sum;
        }
        else
        {
            sum[i+1].o_sum = sum[i].o_sum+toInt(x[i]);
            sum[i+1].e_sum = sum[i].e_sum;
        }
    }
}

// This function receives l and r representing
// the indices and prints the required output
bool query(int l,int r)
{
    int diff = (sum[r+1].e_sum - sum[r+1].o_sum) -
               (sum[l].e_sum - sum[l].o_sum);

    return (diff%11==0);
}

//driver function to check the program
int main()
{
    string s = "122164154695";

    preCompute(s);

    cout << query(0, 3) << endl;
    cout << query(1, 2) << endl;
    cout << query(5, 9) << endl;
    cout << query(0, 11) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check divisibility by 11 in
// subStrings of a number String
class GFG
{

static int MAX = 1000005;

// To store sums of even and odd digits
static class OddEvenSums
{
    // Sum of even placed digits
    int e_sum;

    // Sum of odd placed digits
    int o_sum;
};

// Auxiliary array
static OddEvenSums []sum = new OddEvenSums[MAX];

// Utility function to evaluate a character's
// integer value
static int toInt(char x)
{
    return x - 48;
}

// This function receives the String representation
// of the number and precomputes the sum array
static void preCompute(String x)
{
    // Initialize everb
    sum[0].e_sum = sum[0].o_sum = 0;

    // Add the respective digits depending on whether
    // they're even indexed or odd indexed
    for (int i = 0; i < x.length(); i++)
    {
        if (i % 2 == 0)
        {
            sum[i + 1].e_sum = sum[i].e_sum + toInt(x.charAt(i));
            sum[i + 1].o_sum = sum[i].o_sum;
        }
        else
        {
            sum[i + 1].o_sum = sum[i].o_sum + toInt(x.charAt(i));
            sum[i + 1].e_sum = sum[i].e_sum;
        }
    }
}

// This function receives l and r representing
// the indices and prints the required output
static boolean query(int l, int r)
{
    int diff = (sum[r + 1].e_sum - sum[r + 1].o_sum) -
               (sum[l].e_sum - sum[l].o_sum);

    return (diff % 11 == 0);
}

//driver function to check the program
public static void main(String[] args)
{
    for (int i = 0; i < MAX; i++) {
        sum[i] = new OddEvenSums();
    }
    String s = "122164154695";

    preCompute(s);

    System.out.println(query(0, 3) ? 1 : 0);
    System.out.println(query(1, 2) ? 1 : 0);
    System.out.println(query(5, 9) ? 1 : 0);
    System.out.println(query(0, 11) ? 1 : 0);

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check divisibility by
# 11 in subStrings of a number String
MAX = 1000005

# To store sums of even and odd digits
class OddEvenSums:

    def __init__(self, e_sum, o_sum):

        # Sum of even placed digits
        self.e_sum = e_sum

        # Sum of odd placed digits
        self.o_sum = o_sum

sum = [OddEvenSums(0, 0) for i in range(MAX)]

# This function receives the String
# representation of the number and
# precomputes the sum array
def preCompute(x):

    # Initialize everb
    sum[0].e_sum = sum[0].o_sum = 0

    # Add the respective digits
    # depending on whether
    # they're even indexed or
    # odd indexed
    for i in range(len(x)):
        if (i % 2 == 0):
            sum[i + 1].e_sum = (sum[i].e_sum +
                              int(x[i]))
            sum[i + 1].o_sum = sum[i].o_sum

        else:
            sum[i + 1].o_sum = (sum[i].o_sum +
                              int(x[i]))
            sum[i + 1].e_sum = sum[i].e_sum

# This function receives l and r representing
# the indices and prints the required output
def query(l, r):

    diff = ((sum[r + 1].e_sum -
             sum[r + 1].o_sum) -
            (sum[l].e_sum -
             sum[l].o_sum))

    if (diff % 11 == 0):
        return True
    else:
        return False

# Driver code
if __name__=="__main__":

    s = "122164154695"

    preCompute(s)

    print(1 if query(0, 3) else 0)
    print(1 if query(1, 2) else 0)
    print(1 if query(5, 9) else 0)
    print(1 if query(0, 11) else 0)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to check
// divisibility by 11 in
// subStrings of a number String
using System;
class GFG{

static int MAX = 1000005;

// To store sums of even
// and odd digits 
public class OddEvenSums
{
  // Sum of even placed digits
  public int e_sum;

  // Sum of odd placed digits
  public int o_sum;
};

// Auxiliary array
static OddEvenSums []sum =
       new OddEvenSums[MAX];

// Utility function to
// evaluate a character's
// integer value
static int toInt(char x)
{
  return x - 48;
}

// This function receives the
// String representation of the
// number and precomputes the sum array
static void preCompute(String x)
{
  // Initialize everb
  sum[0].e_sum = sum[0].o_sum = 0;

  // Add the respective digits
  // depending on whether they're
  // even indexed or odd indexed
  for (int i = 0; i < x.Length; i++)
  {
    if (i % 2 == 0)
    {
      sum[i + 1].e_sum = sum[i].e_sum +
                         toInt(x[i]);
      sum[i + 1].o_sum = sum[i].o_sum;
    }
    else
    {
      sum[i + 1].o_sum = sum[i].o_sum +
                         toInt(x[i]);
      sum[i + 1].e_sum = sum[i].e_sum;
    }
  }
}

// This function receives l and r
// representing the indices and
// prints the required output
static bool query(int l, int r)
{
  int diff = (sum[r + 1].e_sum -
              sum[r + 1].o_sum) -
             (sum[l].e_sum -
              sum[l].o_sum);

  return (diff % 11 == 0);
}

// Driver function to check the program
public static void Main(String[] args)
{
  for (int i = 0; i < MAX; i++)
  {
    sum[i] = new OddEvenSums();
  }

  String s = "122164154695";
  preCompute(s);

  Console.WriteLine(query(0, 3) ? 1 : 0);
  Console.WriteLine(query(1, 2) ? 1 : 0);
  Console.WriteLine(query(5, 9) ? 1 : 0);
  Console.WriteLine(query(0, 11) ? 1 : 0);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to check divisibility by 11 in
// subStrings of a number String
let MAX = 1000005;

// To store sums of even and odd digits
class OddEvenSums
{
    constructor()
    {
        this.e_sum = 0;
        this.o_sum = 0;

    }
}

// Auxiliary array
let sum = new Array(MAX);

// Utility function to evaluate a character's
// integer value
function toInt(x)
{
    return x.charCodeAt(0) -     48;
}

// This function receives the String representation
// of the number and precomputes the sum array
function preCompute(x)
{

    // Initialize everb
    sum[0].e_sum = sum[0].o_sum = 0;

    // Add the respective digits depending on whether
    // they're even indexed or odd indexed
    for (let i = 0; i < x.length; i++)
    {
        if (i % 2 == 0)
        {
            sum[i + 1].e_sum = sum[i].e_sum + parseInt(x[i]);
            sum[i + 1].o_sum = sum[i].o_sum;
        }
        else
        {
            sum[i + 1].o_sum = sum[i].o_sum + parseInt(x[i]);
            sum[i + 1].e_sum = sum[i].e_sum;
        }
    }
}

// This function receives l and r representing
// the indices and prints the required output
function query(l,r)
{
    let diff = (sum[r + 1].e_sum - sum[r + 1].o_sum) -
               (sum[l].e_sum - sum[l].o_sum);

    return (diff % 11 == 0);
}

// driver function to check the program
for (let i = 0; i < MAX; i++) {
    sum[i] = new OddEvenSums();
}
let s = "122164154695";

preCompute(s);

document.write((query(0, 3) ? 1 : 0)+"<br>");
document.write((query(1, 2) ? 1 : 0)+"<br>");
document.write((query(5, 9) ? 1 : 0)+"<br>");
document.write((query(0, 11) ? 1 :0)+"<br>");

// This code is contributed by unknown2108
</script>
```

**输出:**

```
1
1
0
1
```

本文由 [**阿舒托什·库马尔**](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。