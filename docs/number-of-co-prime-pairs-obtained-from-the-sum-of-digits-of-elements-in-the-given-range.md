# 从给定范围内元素的位数之和得到的同素对的个数

> 原文:[https://www . geeksforgeeks . org/从给定范围内元素的位数总和中获得的同素对数/](https://www.geeksforgeeks.org/number-of-co-prime-pairs-obtained-from-the-sum-of-digits-of-elements-in-the-given-range/)

给定两个数字 A 和 B，其中 1 <= A <= B。任务是计算元素为同素的对的数量，其中对是由给定范围内元素的位数之和形成的。

**注意:**如果两对中至少有一个数字不同，则视为不同。可以假设最大数字总和可以是 162。

**示例:**

```
Input: 12 15
Output: 4
12 = 1+2 = 3
13 = 1+3 = 4
14 = 1+4 = 5
15 = 1+5 = 6
Thus pairs who are co-prime to each other are 
(3, 4), (3, 5), (4, 5), (5, 6) 
i.e the answer is 4.

Input: 7 10
Output: 6
```

**方法-1:**

*   考虑从 a 到 b 的每一个元素。
*   找出每个元素的数字总和，并将其存储到一个向量中。
*   逐一考虑每一对，并检查该对元素的 gcd 是否为 1。
*   如果是的话，把那一对算作同素的。
*   打印共质数对的计数。

下面是上述方法的实现:

## C++

```
// C++ program to count the pairs
// whose sum of digits is co-prime
#include <bits/stdc++.h>
using namespace std;

// Function to find the elements
// after doing the sum of digits
int makePairs(vector<int> &pairs, int a, int b)
{

    // Traverse from a  to b
    for (int i = a; i <= b; i++)
    {

    // Find the sum of the digits of the elements
    // in the given range one by one
      int sumOfDigits = 0, k = i;
      while(k>0)
      {
          sumOfDigits += k%10;
          k /= 10;
      }
      if (sumOfDigits <= 162)
      pairs.push_back(sumOfDigits);
    }
}

// Function to count the co-prime pairs
int countCoPrime(int a, int b){
    vector<int> pairs;

    // Function to make the pairs
    // by doing the sum of digits
    makePairs(pairs, a, b);
    int count = 0;

    // Count pairs that are co-primes
    for(int i = 0; i < pairs.size(); i++)
       for (int j = i+1; j < pairs.size(); j++)
          if (__gcd(pairs[i], pairs[j]) == 1)
                 count++;

   return count;

}

// Driver code
int main()
{
    int a = 12, b = 15;

    // Function to count the pairs
    cout << countCoPrime(a, b) ;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the pairs
// whose sum of digits is co-prime
import java.util.*;

class GFG
{
static int GCD(int a, int b)
{
if (b == 0) return a;
return GCD(b, a % b);
}
// Function to find the elements
// after doing the sum of digits
static void makePairs(Vector<Integer> pairs,
                      int a, int b)
{

    // Traverse from a to b
    for (int i = a; i <= b; i++)
    {

    // Find the sum of the digits
    // of the elements in the given
    // range one by one
    int sumOfDigits = 0, k = i;
    while(k > 0)
    {
        sumOfDigits += k % 10;
        k /= 10;
    }
    if (sumOfDigits <= 162)
        pairs.add(sumOfDigits);
    }
}

// Function to count
// the co-prime pairs
static int countCoPrime(int a, int b)
{
    Vector<Integer> pairs = new Vector<Integer>();

    // Function to make the pairs
    // by doing the sum of digits
    makePairs(pairs, a, b);
    int count = 0;

    // Count pairs that are co-primes
    for(int i = 0; i < pairs.size(); i++)
    for (int j = i+1; j < pairs.size(); j++)
        if (GCD(pairs.get(i),
                pairs.get(j)) == 1)
                count++;

return count;

}

// Driver code
public static void main(String args[])
{
    int a = 12, b = 15;

    // Function to count the pairs
    System.out.println(countCoPrime(a, b));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to count the pairs
# whose sum of digits is co-prime
from math import gcd
# Function to find the elements
# after doing the sum of digits
def makePairs(pairs, a, b):
    # Traverse from a to b
    for i in range(a,b+1,1):
        # Find the sum of the digits of the elements
        # in the given range one by one
        sumOfDigits = 0
        k = i
        while(k>0):
            sumOfDigits += k%10
            k = int(k / 10)

        if (sumOfDigits <= 162):
            pairs.append(sumOfDigits)

# Function to count the co-prime pairs
def countCoPrime(a, b):
    pairs = []

    # Function to make the pairs
    # by doing the sum of digits
    makePairs(pairs, a, b)
    count = 0

    # Count pairs that are co-primes
    for i in range(0,len(pairs),1):
            for j in range(i+1,len(pairs),1):
                if (gcd(pairs[i], pairs[j]) == 1):
                    count += 1

    return count

# Driver code
if __name__ == '__main__':
    a = 12
    b = 15

    # Function to count the pairs
    print (countCoPrime(a, b))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count the pairs
// whose sum of digits is co-prime
using System;
using System.Collections.Generic;

class GFG
{
public static int GCD(int a, int b)
{
    if (b == 0)
    {
        return a;
    }
    return GCD(b, a % b);
}

// Function to find the elements
// after doing the sum of digits
public static void makePairs(List<int> pairs,
                                int a, int b)
{

    // Traverse from a to b
    for (int i = a; i <= b; i++)
    {

    // Find the sum of the digits
    // of the elements in the given
    // range one by one
    int sumOfDigits = 0, k = i;
    while (k > 0)
    {
        sumOfDigits += k % 10;
        k /= 10;
    }
    if (sumOfDigits <= 162)
    {
        pairs.Add(sumOfDigits);
    }
    }
}

// Function to count
// the co-prime pairs
public static int countCoPrime(int a, int b)
{
    List<int> pairs = new List<int>();

    // Function to make the pairs
    // by doing the sum of digits
    makePairs(pairs, a, b);
    int count = 0;

    // Count pairs that are co-primes
    for (int i = 0;
             i < pairs.Count; i++)
    {
    for (int j = i + 1;
             j < pairs.Count; j++)
    {
        if (GCD(pairs[i], pairs[j]) == 1)
        {
                count++;
        }
    }
    }

    return count;

}

// Driver code
public static void Main(string[] args)
{
    int a = 12, b = 15;

    // Function to count the pairs
    Console.WriteLine(countCoPrime(a, b));
}
}

// This code is contributed
// by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to count the pairs
// whose sum of digits is co-prime
function GCD(a, b)
{
    if (b == 0)
        return a;

    return GCD(b, a % b);
}

// Function to find the elements
// after doing the sum of digits
function makePairs(pairs, a, b)
{

    // Traverse from a to b
    for(i = a; i <= b; i++)
    {

        // Find the sum of the digits
        // of the elements in the given
        // range one by one
        var sumOfDigits = 0, k = i;

        while (k > 0)
        {
            sumOfDigits += k % 10;
            k = parseInt(k / 10);
        }
        if (sumOfDigits <= 162)
            pairs.push(sumOfDigits);
    }
}

// Function to count
// the co-prime pairs
function countCoPrime(a, b)
{
    var pairs = [];

    // Function to make the pairs
    // by doing the sum of digits
    makePairs(pairs, a, b);
    var count = 0;

    // Count pairs that are co-primes
    for(i = 0; i < pairs.length; i++)
        for(j = i + 1; j < pairs.length; j++)
            if (GCD(pairs[i], pairs[j]) == 1)
                count++;

    return count;

}

// Driver code
var a = 12, b = 15;

// Function to count the pairs
document.write(countCoPrime(a, b));

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
4
```

**方法-2:**
如题所述，最大和可以是 162。所以，找出数字和从 1 到 162 在 A 到 B 范围内的频率，并将频率存储在数组中。以后，用这个频率找到答案。
自，

> 数字，频率
> 1，0
> 2，0
> 3，1
> 4，1
> 5，1
> 6，1
> 7，0
> 8，0
> 。, .
> 。, .
> 162，0
> 因此 gcd 对的数量= freq(3)* freq(4)+freq(3)* freq(5)+freq(4)* freq(5)+freq(5)* freq(6)
> = 1+1+1+1
> = 4

因此，相互同素的对是(3，4)，(3，5)，(4，5)，(5，6)，即答案是 4。

以下是所需的实现:

## C++

```
// C++ program to count the pairs
// whose sum of digits is co-prime
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Recursive function to return the frequency
// of numbers having their sum of digits i
ll recursive(ll idx, ll sum, ll tight, string st,
             ll dp[20][2][166], ll num)
{
    if (idx == num)
        // Returns 1 or 0
        return sum == 0;

    // Returns value of the dp if already stored
    if (dp[idx][tight][sum] != -1)
        return dp[idx][tight][sum];

    bool newTight;
    ll ans = 0;
    ll d;

    // Loop from digit 0 to 9
    for (d = 0; d < 10; ++d) {
        newTight = false;
        if (tight && st[idx] - '0' < d)
            continue;

        // To change the tight to 1
        if (tight && st[idx] - '0' == d)
            newTight = true;

        // Calling the recursive function to find the frequency
        if (sum >= d)
            ans += recursive(idx + 1, sum - d,
                             newTight, st, dp, num);
    }

    return dp[idx][tight][sum] = ans;
}

// Function to find out frequency of numbers
// from 1 to N having their sum of digits
// from 1 to 162 and store them in array
vector<ll> formArray(ll N)
{
    ll dp[20][2][166];
    memset(dp, -1, sizeof dp);

    // Number to string conversion
    ostringstream x;
    x << N;
    string st = x.str();
    ll num = st.size();

    vector<ll> arr;
    for (int i = 1; i <= 162; ++i) {

        // Calling the recursive function
        // and pushing it into array
        arr.push_back(recursive(0, i, 1, st, dp, num));
    }

    return arr;
}

// Function to find the pairs
ll findPair(ll a, ll b)
{
    // Calling the  formArray function of a-1 numbers
    vector<ll> arr_smaller = formArray(a - 1);

    // Calling the  formArray function of b numbers
    vector<ll> arr_greater = formArray(b);

    // Subtracting the frequency of higher number array with lower
    // number array and thus finding the range of
    // numbers from a to b having sum from 1 to 162
    for (int i = 0; i < arr_greater.size(); ++i)
        arr_greater[i] -= arr_smaller[i];

    int ans = 0;
    for (int i = 1; i <= 162; ++i) {
        for (int j = i + 1; j <= 162; ++j) {

            // To find out total number of pairs
            // which are co-prime
            if (__gcd(i, j) == 1)
                ans = (ans + arr_greater[i - 1] * arr_greater[j - 1]);
        }
    }

    return ans;
}

// Driver code
int main()
{
    ll a = 12, b = 15;

    // Function to count the pairs
    cout << findPair(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the pairs
// whose sum of digits is co-prime
import java.io.*;
import java.util.*;
class GFG
{

  static int gcd(int a, int b)
  {
    if (b == 0)
      return a;
    return gcd(b, a % b);        
  }

  // Recursive function to return the frequency
  // of numbers having their sum of digits i
  static long recursive(long idx, long sum, long tight,
                        String st, long[][][] dp, long num)
  {
    if (idx == num)
    {

      // Returns 1 or 0
      return sum == 0 ? 1 : 0;
    }

    // Returns value of the dp if already stored
    if (dp[(int)idx][(int)tight][(int)sum] != -1)
      return dp[(int)idx][(int)tight][(int)sum];

    long newTight;
    long ans = 0;
    long d;

    // Loop from digit 0 to 9
    for (d = 0; d < 10; ++d)
    {
      newTight = 0;
      if (tight == 1 && st.charAt((int)idx) - '0' < d)
        continue;

      // To change the tight to 1
      if (tight == 1 && st.charAt((int)idx) - '0' == d)
        newTight = 1;

      // Calling the recursive function to find the frequency
      if (sum >= d)
        ans += recursive(idx + 1, sum - d,
                         (int)newTight, st, dp, num);
    }
    return dp[(int)idx][(int)tight][(int)sum] = ans;
  }

  // Function to find out frequency of numbers
  // from 1 to N having their sum of digits
  // from 1 to 162 and store them in array
  static ArrayList<Long> formArray(long N)
  {
    long[][][] dp = new long[20][2][166];
    for (long[][] innerRow: dp)
    {
      for (long[] innerInnerRow: innerRow)
      {
        Arrays.fill(innerInnerRow, -1);
      }
    }

    // Number to string conversion
    String st = String.valueOf(N);
    long num = st.length();

    ArrayList<Long> arr = new ArrayList<Long>();
    for (int i = 1; i <= 162; ++i)
    {
      // Calling the recursive function
      // and pushing it into array
      arr.add(recursive(0, i, 1, st, dp, num));
    }
    return arr;
  }

  // Function to find the pairs
  static long findPair(long a, long b)
  {

    // Calling the  formArray function of a-1 numbers
    ArrayList<Long> arr_smaller = formArray(a - 1);

    // Calling the  formArray function of b numbers
    ArrayList<Long> arr_greater = formArray(b);

    // Subtracting the frequency of higher number array with lower
    // number array and thus finding the range of
    // numbers from a to b having sum from 1 to 162
    for (int i = 0; i < arr_greater.size(); ++i)
    {
      arr_greater.set(i,arr_greater.get(i)-arr_smaller.get(i));
    }
    long ans = 0;
    for (int i = 1; i <= 162; ++i)
    {
      for (int j = i + 1; j <= 162; ++j)
      {
        // To find out total number of pairs
        // which are co-prime
        if (gcd(i, j) == 1)
        {
          ans = (ans + arr_greater.get(i-1) * arr_greater.get(j-1));
        }
      }
    }
    return ans;
  }

  // Driver code
  public static void main (String[] args)
  {
    long a = 12, b = 15;

    // Function to count the pairs
    System.out.println(findPair(a, b));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to count
# the pairs whose sum of
# digits is co-prime
import math

# Recursive function to
# return the frequency of
# numbers having their sum
# of digits i
def recursive(idx, sum,
              tight, st,
              dp, num):

    if (idx == num):

        # Returns 1 or 0
        return sum == 0

    # Returns value of the dp
    # if already stored
    if (dp[idx][tight][sum] != -1):
        return dp[idx][tight][sum]

    ans = 0

    # Loop from digit 0 to 9
    for d in range(10):
        newTight = False
        if (tight and ord(st[idx]) -
            ord('0') < d):
            continue

        # To change the tight to 1
        if (tight and ord(st[idx]) -
            ord('0') == d):
            newTight = True

        # Calling the recursive
        # function to find the
        # frequency
        if (sum >= d):
            ans += recursive(idx + 1,
                             sum - d,
                             newTight,
                             st, dp, num)

    dp[idx][tight][sum] = ans
    return dp[idx][tight][sum]

# Function to find out frequency
# of numbers from 1 to N having
# their sum of digits from 1 to
# 162 and store them in array
def formArray(N):

    dp = [[[-1 for x in range(166)]
               for y in range(2)]
               for z in range(20)]

    # Number to string conversion
    st = str(N)
    num = len(st)

    arr = []
    for i in range(1, 163):

        # Calling the recursive function
        # and pushing it into array
        arr.append(recursive(0, i, 1,
                             st, dp, num))
    return arr

# Function to find the pairs
def findPair(a, b):

    # Calling the  formArray
    # function of a-1 numbers
    arr_smaller = formArray(a - 1)

    # Calling the  formArray
    # function of b numbers
    arr_greater = formArray(b)

    # Subtracting the frequency of
    # higher number array with lower
    # number array and thus finding
    # the range of numbers from a to
    # b having sum from 1 to 162
    for i in range(len(arr_greater)):
        arr_greater[i] -= arr_smaller[i]

    ans = 0
    for i in range(1, 163):
        for j in range(i + 1, 163):

            # To find out total number
            # of pairs which are co-prime
            if (math.gcd(i, j) == 1):
                ans = (ans + arr_greater[i - 1] *
                       arr_greater[j - 1])
    return ans

# Driver code
if __name__ == "__main__":
    a = 12
    b = 15

    # Function to count the pairs
    print(findPair(a, b))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to count the pairs
// whose sum of digits is co-prime
using System;
using System.Collections.Generic;

class GFG{

static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);        
}

// Recursive function to return the frequency
// of numbers having their sum of digits i
static long recursive(long idx, long sum, long tight,
                      string st, long[,,] dp, long num)
{
    if (idx == num)
    {

        // Returns 1 or 0
        return sum == 0 ? 1 : 0;
    }

    // Returns value of the dp if already stored
    if (dp[(int)idx, (int)tight, (int)sum] != -1)
        return dp[(int)idx, (int)tight, (int)sum];

    long newTight;
    long ans = 0;
    long d;

    // Loop from digit 0 to 9
    for (d = 0; d < 10; ++d)
    {
        newTight = 0;

        if (tight == 1 && st[((int)idx)] - '0' < d)
            continue;

        // To change the tight to 1
        if (tight == 1 && st[((int)idx)] - '0' == d)
            newTight = 1;

        // Calling the recursive function to
        // find the frequency
        if (sum >= d)
            ans += recursive(idx + 1, sum - d,
                   (int)newTight, st, dp, num);
    }
    return dp[(int)idx, (int)tight, (int)sum] = ans;
}

// Function to find out frequency of numbers
// from 1 to N having their sum of digits
// from 1 to 162 and store them in array
static List<long> formArray(long N)
{
    long[,,] dp = new long[20, 2, 166];
    for(int i = 0; i < 20; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            for(int k = 0; k < 166; k++)
            {
                dp[i, j, k] = -1;
            }
        }
    }

    // Number to string conversion
    string st = N.ToString();
    long num = st.Length;

    List<long> arr = new List<long>();
    for (int i = 1; i <= 162; ++i)
    {

        // Calling the recursive function
        // and pushing it into array
        arr.Add(recursive(0, i, 1, st, dp, num));
    }
    return arr;
}

// Function to find the pairs
static long findPair(long a, long b)
{

    // Calling the  formArray function of a-1 numbers
    List<long> arr_smaller = formArray(a - 1);

    // Calling the  formArray function of b numbers
    List<long> arr_greater = formArray(b);

    // Subtracting the frequency of higher number
    // array with lower number array and thus
    // finding the range of numbers from a to b
    // having sum from 1 to 162
    for(int i = 0; i < arr_greater.Count; ++i)
    {
        arr_greater[i] = arr_greater[i] -
                         arr_smaller[i];
    }
    long ans = 0;

    for(int i = 1; i <= 162; ++i)
    {
        for(int j = i + 1; j <= 162; ++j)
        {

            // To find out total number of pairs
            // which are co-prime
            if (gcd(i, j) == 1)
            {
                ans = (ans + arr_greater[i - 1] *
                             arr_greater[j - 1]);
            }
        }
    }
    return ans;
}

// Driver code
static public void Main()
{
    long a = 12, b = 15;

    // Function to count the pairs
    Console.WriteLine(findPair(a, b));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program to count the pairs
// whose sum of digits is co-prime

function gcd(a,b)
{
    if (b == 0)
      return a;
    return gcd(b, a % b);     
}

// Recursive function to return the frequency
// of numbers having their sum of digits i
function recursive(idx,sum,tight,st,dp, num)
{
    if (idx == num)
    {

      // Returns 1 or 0
      return sum == 0 ? 1 : 0;
    }

    // Returns value of the dp if already stored
    if (dp[idx][tight][sum] != -1)
      return dp[idx][tight][sum];

    let newTight;
    let ans = 0;
    let d;

    // Loop from digit 0 to 9
    for (d = 0; d < 10; ++d)
    {
      newTight = 0;
      if (tight == 1 && st[idx].charCodeAt(0) - '0'.charCodeAt(0) < d)
        continue;

      // To change the tight to 1
      if (tight == 1 && st[idx].charCodeAt(0) - '0'.charCodeAt(0) == d)
        newTight = 1;

      // Calling the recursive function to find the frequency
      if (sum >= d)
        ans += recursive(idx + 1, sum - d,
                         newTight, st, dp, num);
    }
    return dp[idx][tight][sum] = ans;
}

// Function to find out frequency of numbers
  // from 1 to N having their sum of digits
  // from 1 to 162 and store them in array
function formArray(N)
{
    let dp = new Array(20);
    for(let i=0;i<20;i++)
    {
        dp[i]=new Array(2);
        for(let j=0;j<2;j++)
        {
            dp[i][j]=new Array(166);
            for(let k=0;k<166;k++)
            {
                dp[i][j][k]=-1;
            }
        }
    }

    // Number to string conversion
    let st = (N).toString();
    let num = st.length;

    let arr = [];
    for (let i = 1; i <= 162; ++i)
    {
      // Calling the recursive function
      // and pushing it into array
      arr.push(recursive(0, i, 1, st, dp, num));
    }
    return arr;
}

// Function to find the pairs
function findPair(a,b)
{
    // Calling the  formArray function of a-1 numbers
    let arr_smaller = formArray(a - 1);

    // Calling the  formArray function of b numbers
    let arr_greater = formArray(b);

    // Subtracting the frequency of higher number array with lower
    // number array and thus finding the range of
    // numbers from a to b having sum from 1 to 162
    for (let i = 0; i < arr_greater.length; ++i)
    {
      arr_greater[i] -= arr_smaller[i];
    }
    let ans = 0;
    for (let i = 1; i <= 162; ++i)
    {
      for (let j = i + 1; j <= 162; ++j)
      {
        // To find out total number of pairs
        // which are co-prime
        if (gcd(i, j) == 1)
        {
          ans = (ans + arr_greater[i-1] * arr_greater[j-1]);
        }
      }
    }
    return ans;
}

// Driver code
let a = 12, b = 15;

// Function to count the pairs
document.write(findPair(a, b));

// This code is contributed by ab2127
</script>
```

**Output:** 

```
4
```