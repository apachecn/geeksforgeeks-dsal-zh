# 在位数乘积最大的范围内找到数字

> 原文:[https://www . geeksforgeeks . org/find-范围内的数字-具有最大位数的乘积/](https://www.geeksforgeeks.org/find-the-number-in-a-range-having-maximum-product-of-the-digits/)

给定一个由两个正整数 L 和 r 表示的范围，找出这个范围内具有最大位数乘积的数。
**例:**

```
Input : L = 1, R = 10
Output : 9

Input : L = 51, R = 62
Output : 59
```

**方法:**这里的关键思想是从最高有效数字开始迭代数字 R 的数字。从左到右，即从最高有效数字到最低有效数字，用比当前数字少一个的数字替换当前数字，用 9 替换数字中当前数字之后的所有数字，因为数字在当前位置已经变得小于 R，所以我们可以安全地将任何数字放在后面的数字中，以最大化数字的乘积。此外，检查结果数是否大于 L，以保持在该范围内，并更新最大乘积。
以下是上述办法的实施情况:

## C++

```
// CPP Program to find the number in a
// range having maximum product of the
// digits

#include <bits/stdc++.h>
using namespace std;

// Returns the product of digits of number x
int product(int x)
{
    int prod = 1;
    while (x) {
        prod *= (x % 10);
        x /= 10;
    }
    return prod;
}

// This function returns the number having
// maximum product of the digits
int findNumber(int l, int r)
{
    // Converting both integers to strings
    string a = to_string(l);
    string b = to_string(r);

    // Let the current answer be r
    int ans = r;
    for (int i = 0; i < b.size(); i++) {
        if (b[i] == '0')
            continue;

        // Stores the current number having
        // current digit one less than current
        // digit in b
        string curr = b;
        curr[i] = ((curr[i] - '0') - 1) + '0';

        // Replace all following digits with 9
        // to maximise the product
        for (int j = i + 1; j < curr.size(); j++)
            curr[j] = '9';

        // Convert string to number
        int num = 0;
        for (auto c : curr)
            num = num * 10 + (c - '0');

        // Check if it lies in range and its product
        // is greater than max product
        if (num >= l && product(ans) < product(num))
            ans = num;
    }

    return ans;
}

// Driver Code
int main()
{
    int l = 1, r = 10;
    cout << findNumber(l, r) << endl;

    l = 51, r = 62;
    cout << findNumber(l, r) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the number in a
// range having maximum product of the
// digits

class GFG
{

// Returns the product of digits of number x
static int product(int x)
{
    int prod = 1;
    while (x > 0)
    {
        prod *= (x % 10);
        x /= 10;
    }
    return prod;
}

// This function returns the number having
// maximum product of the digits
static int findNumber(int l, int r)
{
    // Converting both integers to strings
    //string a = l.ToString();
    String b = Integer.toString(r);

    // Let the current answer be r
    int ans = r;
    for (int i = 0; i < b.length(); i++)
    {
        if (b.charAt(i) == '0')
            continue;

        // Stores the current number having
        // current digit one less than current
        // digit in b
        char[] curr = b.toCharArray();
        curr[i] = (char)(((int)(curr[i] -
                    (int)'0') - 1) + (int)('0'));

        // Replace all following digits with 9
        // to maximise the product
        for (int j = i + 1; j < curr.length; j++)
            curr[j] = '9';

        // Convert string to number
        int num = 0;
        for (int j = 0; j < curr.length; j++)
            num = num * 10 + (curr[j] - '0');

        // Check if it lies in range and its product
        // is greater than max product
        if (num >= l && product(ans) < product(num))
            ans = num;
    }

    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int l = 1, r = 10;
    System.out.println(findNumber(l, r));

    l = 51;
    r = 62;
    System.out.println(findNumber(l, r));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 Program to find the number
# in a range having maximum product
# of the digits

# Returns the product of digits
# of number x
def product(x) :

    prod = 1
    while (x) :
        prod *= (x % 10)
        x //= 10;

    return prod

# This function returns the number having
# maximum product of the digits
def findNumber(l, r) :

    # Converting both integers to strings
    a = str(l);
    b = str(r);

    # Let the current answer be r
    ans = r

    for i in range(len(b)) :
        if (b[i] == '0') :
            continue

        # Stores the current number having
        # current digit one less than current
        # digit in b
        curr = list(b)
        curr[i] = str(((ord(curr[i]) -
                        ord('0')) - 1) + ord('0'))

        # Replace all following digits with 9
        # to maximise the product
        for j in range(i + 1, len(curr)) :
            curr[j] = str(ord('9'))

        # Convert string to number
        num = 0
        for c in curr :
            num = num * 10 + (int(c) - ord('0'))

        # Check if it lies in range and its
        # product is greater than max product
        if (num >= l and product(ans) < product(num)) :
            ans = num

    return ans

# Driver Code
if __name__ == "__main__" :

    l, r = 1, 10
    print(findNumber(l, r))

    l, r = 51, 62
    print(findNumber(l, r))

# This code is contributed by Ryuga
```

## C#

```
// C# Program to find the number in a
// range having maximum product of the
// digits
using System;

class GFG
{

// Returns the product of digits of number x
static int product(int x)
{
    int prod = 1;
    while (x > 0)
    {
        prod *= (x % 10);
        x /= 10;
    }
    return prod;
}

// This function returns the number having
// maximum product of the digits
static int findNumber(int l, int r)
{
    // Converting both integers to strings
    //string a = l.ToString();
    string b = r.ToString();

    // Let the current answer be r
    int ans = r;
    for (int i = 0; i < b.Length; i++)
    {
        if (b[i] == '0')
            continue;

        // Stores the current number having
        // current digit one less than current
        // digit in b
        char[] curr = b.ToCharArray();
        curr[i] = (char)(((int)(curr[i] -
                    (int)'0') - 1) + (int)('0'));

        // Replace all following digits with 9
        // to maximise the product
        for (int j = i + 1; j < curr.Length; j++)
            curr[j] = '9';

        // Convert string to number
        int num = 0;
        for (int j = 0; j < curr.Length; j++)
            num = num * 10 + (curr[j] - '0');

        // Check if it lies in range and its product
        // is greater than max product
        if (num >= l && product(ans) < product(num))
            ans = num;
    }

    return ans;
}

// Driver Code
static void Main()
{
    int l = 1, r = 10;
    Console.WriteLine(findNumber(l, r));

    l = 51;
    r = 62;
    Console.WriteLine(findNumber(l, r));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the number
// in a range having maximum product
// of the digits

// Returns the product of digits
// of number x
function product($x)
{
    $prod = 1;
    while ($x)
    {
        $prod *= ($x % 10);
        $x = (int)($x / 10);
    }

    return $prod;
}

// This function returns the number
// having maximum product of the digits
function findNumber($l, $r)
{
    // Let the current answer be r
    $ans = $r;

    // Converting both integers
    // to strings
    $a = strval($l);
    $b = strval($r);

    for ($i = 0; $i < strlen($b); $i++)
    {
        if ($b[$i] == '0')
            continue;

        // Stores the current number having
        // current digit one less than
        // current digit in b
        $curr = $b;
        $curr[$i] = chr(((ord($curr[$i]) -
                          ord('0')) - 1) +
                          ord('0'));

        // Replace all following digits
        // with 9 to maximise the product
        for ($j = $i + 1; $j < strlen($curr); $j++)
            $curr[$j] = '9';

        // Convert string to number
        $num = 0;
        for ($c = 0; $c < strlen($curr); $c++)
            $num = $num * 10 + (ord($curr[$c]) -
                                ord('0'));

        // Check if it lies in range and its
        // product is greater than max product
        if ($num >= $l and
            product($ans) < product($num))
            $ans = $num;
    }

    return $ans;
}

// Driver Code
$l = 1;
$r = 10;
print(findNumber($l, $r) . "\n");

$l = 51;
$r = 62;
print(findNumber($l, $r));

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find the number in a
    // range having maximum product of the
    // digits

    // Returns the product of digits of number x
    function product(x)
    {
        let prod = 1;
        while (x > 0)
        {
            prod *= (x % 10);
            x = parseInt(x / 10, 10);
        }
        return prod;
    }

    // This function returns the number having
    // maximum product of the digits
    function findNumber(l, r)
    {
        // Converting both integers to strings
        //string a = l.ToString();
        let b = r.toString();

        // Let the current answer be r
        let ans = r;
        for (let i = 0; i < b.length; i++)
        {
            if (b[i] == '0')
                continue;

            // Stores the current number having
            // current digit one less than current
            // digit in b
            let curr = b.split('');
            curr[i] = String.fromCharCode(((curr[i].charCodeAt() - '0'.charCodeAt()) - 1) + '0'.charCodeAt());

            // Replace all following digits with 9
            // to maximise the product
            for (let j = i + 1; j < curr.length; j++)
                curr[j] = '9';

            // Convert string to number
            let num = 0;
            for (let j = 0; j < curr.length; j++)
                num = num * 10 + (curr[j].charCodeAt() - '0'.charCodeAt());

            // Check if it lies in range and its product
            // is greater than max product
            if (num >= l && product(ans) < product(num))
                ans = num;
        }

        return ans;
    }

    let l = 1, r = 10;
    document.write(findNumber(l, r) + "</br>");

    l = 51;
    r = 62;
    document.write(findNumber(l, r));

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
9
59
```

**时间复杂度** : O(18 * 18)，如果我们处理的数字是 10 <sup>18</sup> 。

**另一种方法:**可以用[数字 Dp](https://www.geeksforgeeks.org/digit-dp-introduction/) 解决

**观察要点:-**

**1。**众所周知，我们在数字 dp 中使用**紧密**来检查该数字的范围是否受限，同样在这里我们将使用**紧密 ta** 和**紧密 tb** ( **基本上是两个紧密条件**)，ta 会告诉我们

数字和 tb 的**下限**将告诉我们数字的**上限**，使用两个严格值的原因是我们必须计算最大乘积，情况可能如下:-

**max(l，r)≠max(r)–max(l-1)**我们的整数应该在 l 到 r 的范围内。

**2。**假设范围值为，l=5，r=15，为了使大小相等，我们应该在转换为字符串并在计算答案时注意前导零后，在数字前面添加零，

**Dp 状态包括:-**

**1)位置**

*   它将从整数的左边告诉索引的位置

**2) ta**

*   它代表一个数字的下限，我们必须确保数字应该大于或等于{ l }
*   假设我们正在构建一个大于或等于 0055 的数字，并且我们已经创建了一个像 005 这样的序列，所以在第 4 位，我们不能放小于 5 的数字，那将只有 5 到 9 之间的数字。所以为了检查这个界限，我们需要 ta。

```
Example : Consider the value of  l = 005
Index   : 0 1 2
digits  : 0 0 5
valid numbers like: 005,006,007,008...
invalid numbers like: ...001,002,003,004
```

3)TB

*   数字的上限，我们必须确保数字应小于或等于{ r }
*   再次假设我们正在构建一个小于等于 526 的数字，我们已经创建了一个像 52 这样的序列，所以在第三个位置，我们不能放大于 6 的数字，在那里我们只能放 0 到 6 之间的数字。所以为了检查这个界限，我们需要肺结核

```
Example : Consider the value of  r = 150
Index   : 0 1 2
digits  : 1 5 0
valid numbers like: ...148,149,150
invalid numbers like: 151,152,153...
```

**4) st**

*   用于检查前导零(如 005 ~ 5)

**3。约束:l 和 r (1 ≤ l ≤ r ≤ 10^18)**

**算法:**

*   我们将在**紧 ta** 和**紧 tb** 的基础上从头到尾遍历 I，如下:

```
start = ta == 1 ? l[ pos ] - '0' : 0;
end = tb ==1 ? r[ pos ] -'0'  : 9;
```

*   首先我们将检查**前导零**为:

```
if ( st == 0 and i = 0) then multiply with 1,else multiply with i
```

*   对于每个位置，我们将计算序列的乘积，并检查它是否是最大乘积，并存储相应的数字

```
int ans = 0;
for(int i = start; i <= end; i++){
  int val = i;
  if (st==0 and i==0) val = 1;
  ans = max (ans, val * solve (pos+1, ta&(i==start),tb&(i==end) ,st|i>0);
}
```

**C++实现:**

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define int long long int

// pair of array to store product and number
// dp[pos][tight1][tight2][start]
pair<int, string> dp[20][2][2][2];

pair<int, string> recur(string l, string r, int pos, int ta,
                        int tb, int st)
{

    // Base case if pos is equal
    // to l or r size return
    // pair{1,""}
    if (pos == l.size()) {
        return { 1, "" };
    }

    // look up condition
    if (dp[pos][ta][tb][st].first != -1)
        return dp[pos][ta][tb][st];

    // Lower bound condition
    int start = ta ? l[pos] - '0' : 0;

    // Upper bound condition
    int end = tb ? r[pos] - '0' : 9;

    // To store the maximum product
    // initially its is set to -1
    int ans = -1;

    // To store the corresponding
    // number as number is large
    // so store it as a string
    string s = "";

    for (int i = start; i <= end; i++) {

        // Multiply with this val
        int val = i;

        // check for leading zeroes as 00005
        if (st == 0 and i == 0) {

            val = 1;
        }

        // Recursive call for next
        // position and store it in
        // a pair pair first gives
        // maximum product pair
        // second gives number which
        // gave maximum product
        pair<int, string> temp

            = recur(l, r, pos + 1, ta & (i == start),

                    tb & (i == end), st | i > 0);

        // check if calculated product is greater than
        // previous calculated ans
        if (temp.first * val > ans) {

            ans = temp.first * val;

            // update string only if no leading zeroes
            // becoz no use to append the leading zeroes
            if (i == 0 and st == 0) {

                s = temp.second;
            }

            else {

                s = temp.second;

                s.push_back('0' + i);
            }
        }
    }

    // while returning memoize the ans
    return dp[pos][ta][tb][st] = { ans, s };
}

pair<int, string> solve(int a, int b)

{

    // convert int l to sting L and int r to string R ,
    // as integer value should be large
    string L = to_string(a);

    string R = to_string(b);

    // to make the size of strings
    // equal append zeroes in
    // front of string L
    if (L.size() < R.size()) {

        reverse(L.begin(), L.end());

        while (L.size() < R.size()) {

            L.push_back('0');
        }

        reverse(L.begin(), L.end());
    }

    // initialize dp
    // as it is pair of array so memset will not work
    for (int i = 0; i < 20; i++) {

        for (int j = 0; j < 2; j++) {

            for (int k = 0; k < 2; k++) {

                for (int l = 0; l < 2; l++) {

                    dp[i][j][k][l].first = -1;
                }
            }
        }
    }

    // as we have to return pair second value
    // it's that number which gaves maximum product
    // initially pos=0,ta=1,tb=1,start=0(becoz number is not
    // started yet)

    pair<int, string> ans = recur(L, R, 0, 1, 1, 0);

    // reverse it becoz we were appending from right to left
    // in recursive call
    reverse(ans.second.begin(), ans.second.end());

    return { ans.first, ans.second };
}

signed main()

{

    // take l and r as input

    int l = 52, r = 62;
    cout << "l= " << l << "\n";
    cout << "r= " << r << "\n";
    pair<int, string> ans = solve(l, r);
    cout << "Maximum Product: " << ans.first << "\n";
    cout << "Number which gave maximum product: "
         << ans.second;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.util.*;
import java.io.*;
import java.math.*;
class GFG
{

// pair of array to store product and number
// dp[pos][tight1][tight2][start]
static class pair
 {
    int first;
    String second;
    pair(int first,String second)
      {
         this.first=first;
         this.second=second;
      }
 }

static pair dp[][][][];

static pair recur(String l, String r, int pos, int ta,
                        int tb, int st)
{

    // Base case if pos is equal
    // to l or r size return
    // pair{1,""}
    if (pos == l.length()) {
        return new pair(1,"");
    }

    // look up condition
    if (dp[pos][ta][tb][st].first != -1)
        return dp[pos][ta][tb][st];

    // Lower bound condition
    int start = ta ==1 ? l.charAt(pos) - '0' : 0;

    // Upper bound condition
    int end = tb ==1 ? r.charAt(pos)  - '0' : 9;

    // To store the maximum product
    // initially its is set to -1
    int ans = -1;

    // To store the corresponding
    // number as number is large
    // so store it as a string
    String s = "";

    for (int i = start; i <= end; i++) {

        // Multiply with this val
        int val = i;

        // check for leading zeroes as 00005
        if (st == 0 && i == 0) {

            val = 1;
        }

        // Recursive call for next
        // position and store it in
        // a pair pair first gives
        // maximum product pair
        // second gives number which
        // gave maximum product
        pair temp

            = recur(l, r, pos + 1, ta==1 ?  (i == start ? 1 : 0) : 0,

                    tb==1  ? (i == end ? 1 : 0) : 0, (st | i) > 0 ? 1 : 0);

        // check if calculated product is greater than
        // previous calculated ans
        if (temp.first * val > ans) {

            ans = temp.first * val;

            // update string only if no leading zeroes
            // becoz no use to append the leading zeroes
            if (i == 0 && st == 0) {

                s = temp.second;
            }

            else {

                s = temp.second;

                s+=(i);
            }
        }
    }

    // while returning memoize the ans
    return dp[pos][ta][tb][st] = new pair(ans, s );
}
static String reverse(String x)
 {
    StringBuilder sb=new StringBuilder("");
    sb.append(x);
    sb.reverse();
    return sb.toString();
 }
static pair solve(int a, int b)

{

    // convert int l to sting L and int r to string R ,
    // as integer value should be large
    String L = Integer.toString(a);
    String R = Integer.toString(b);

    // to make the size of strings
    // equal append zeroes in
    // front of string L
    if (L.length() < R.length()) {

        L=reverse(L);

        while (L.length() < R.length()) {

            L += "0";
        }

        L=reverse(L);
    }

    // initialize dp
    // as it is pair of array so memset will not work
    for (int i = 0; i < 20; i++) {

        for (int j = 0; j < 2; j++) {

            for (int k = 0; k < 2; k++) {

                for (int l = 0; l < 2; l++) {

                    dp[i][j][k][l] = new pair(-1,"");
                }
            }
        }
    }

    // as we have to return pair second value
    // it's that number which gaves maximum product
    // initially pos=0,ta=1,tb=1,start=0(becoz number is not
    // started yet)

    pair ans = recur(L, R, 0, 1, 1, 0);

    // reverse it becoz we were appending from right to left
    // in recursive call
    ans.second = reverse(ans.second);
   pair result = new pair(ans.first, ans.second);
    return result;
}

public static void main(String args[])
{

    // take l and r as input
    int l = 52, r = 62;
    System.out.println("l= "+l );
    System.out.println("r= "+r );

    // creation of dp table
    dp = new pair[20][2][2][2];

    // call function
    pair ans = solve(l, r);
    System.out.println("Maximum Product: "+ans.first);
    System.out.println("Number which gave maximum product: "+ans.second);
}
}

// This code is contributed by Debojyoti Mandal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# pair of array to store product and number
# dp[pos][tight1][tight2][start]
dp=[[[[[0,0] for _ in range(2)] for _ in range(2)]for _ in range(2)]for _ in range(20)]

def recur(l, r, pos, ta, tb, st):

    # Base case if pos is equal
    # to l or r size return
    # pair:1,""
    if (pos == len(l)) :
        return (1, "")

    # look up condition
    if (dp[pos][ta][tb][st][0] != -1):
        return dp[pos][ta][tb][st]

    # Lower bound condition
    start = ord(l[pos]) - ord('0') if ta else  0

    # Upper bound condition
    end = ord(r[pos]) - ord('0') if tb  else 9

    # To store the maximum product
    # initially its is set to -1
    ans = -1

    # To store the corresponding
    # number as number is large
    # so store it as a
    s = []

    for i in range(start,end+1) :

        # Multiply with this val
        val = i

        # check for leading zeroes as 00005
        if (st == 0 and i == 0) :

            val = 1

        # Recursive call for next
        # position and store it in
        # a pair pair first gives
        # maximum product pair
        # second gives number which
        # gave maximum product
        temp = recur(l, r, pos + 1, ta & (i == start),tb & (i == end), st | i > 0)

        # check if calculated product is greater than
        # previous calculated ans
        if (temp[0] * val > ans) :

            ans = temp[0] * val

            # update only if no leading zeroes
            # becoz no use to append the leading zeroes
            if (i == 0 and st == 0) :

                s = list(temp[1])

            else :

                s = list(temp[1])

                s.append(chr(ord('0') + i))
    s=''.join(s)

    # while returning memoize the ans
    dp[pos][ta][tb][st] = [ans, s]
    return dp[pos][ta][tb][st]

def solve(a, b):

    # convert l to sting L and r to R ,
    # as eger value should be large
    L = list(str(a))

    R = str(b)

    # to make the size of s
    # equal append zeroes in
    # front of L
    if (len(L) < len(R)) :

        L=L[::-1]

        while (len(L) < len(R)) :

            L.append('0')

        L=L[::-1]
    L=''.join(L)

    # initialize dp
    # as it is pair of array so memset will not work
    for i in range(20) :

        for j in range(2) :

            for k in range(2) :

                for l in range(2):

                    dp[i][j][k][l][0] = -1

    # as we have to return pair second value
    # it's that number which gaves maximum product
    # initially pos=0,ta=1,tb=1,start=0(becoz number is not
    # started yet)

    ans = recur(L, R, 0, 1, 1, 0)

    # reverse it becoz we were appending from right to left
    # in recursive call
    ans[1]=ans[1][::-1]

    return [ans[0], ans[1]]

if __name__=='__main__':

    # take l and r as input

    l = 52; r = 62
    print("l=",l)
    print("r=",r)
    ans = solve(l, r)
    print("Maximum Product:",ans[0])
    print("Number which gave maximum product:",ans[1])
```

**Output**

```
l= 52
r= 62
Maximum Product: 45
Number which gave maximum product: 59
```

**时间复杂度:** O(logN)，其中 N 是 L 和 r 之间的最大值
T3】辅助空间: O(logN)