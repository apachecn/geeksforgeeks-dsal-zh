# 给定一个大数，检查一个数字子序列是否能被 8 整除

> 原文:[https://www . geesforgeks . org/给定-大数-校验-子序列-数字-可分-8/](https://www.geeksforgeeks.org/given-large-number-check-subsequence-digits-divisible-8/)

给定一个最多 100 位数的数字。我们必须检查在去掉某些数字后，是否有可能得到至少一个可被 8 整除的数字。我们被禁止重新排列数字。

**示例:**

```
Input : 1787075866
Output : Yes
There exist more one or more subsequences
divisible by 8\. Example subsequences are
176, 16 and 8.

Input : 6673177113
Output : No 
No subsequence is divisible by 8.

Input : 3144
Output : Yes
The subsequence 344 is divisible by 8.
```

[除以八](https://www.geeksforgeeks.org/check-large-number-divisible-8-not/)的性质:当且仅当一个数的最后三位数字形成一个可被八除的数时，该数可被八除。因此，只测试那些可以通过划掉从原始数字中获得的最多包含三位数的数字就足够了，也就是说，我们检查所有一位数、两位数和三位数的数字组合。

***方法 1(蛮力):***
我们采用蛮力的方法。我们使用迭代阶梯排列所有可能的一位数、两位数和三位数组合。如果我们遇到一个可被 8 整除的一位数或一个可被 8 整除的两位数组合或一个可被 8 整除的三位数组合，那么这就是我们问题的解决方案。

## C++

```
// C++ program to check if a subsequence of digits
// is divisible by 8.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate any permutation divisible
// by 8\. If such permutation exists, the function
// will return that permutation else it will return -1
bool isSubSeqDivisible(string str)
{
    // Converting string to integer array for ease
    // of computations (Indexing in arr[] is
    // considered to be starting from 1)
    int l = str.length();
    int arr[l];
    for (int i = 0; i < l; i++)
        arr[i] = str[i] - '0';

    // Generating all possible permutations and checking
    // if any such permutation is divisible by 8
    for (int i = 0; i < l; i++) {
        for (int j = i; j < l; j++) {
            for (int k = j; k < l; k++) {
                if (arr[i] % 8 == 0)
                    return true;

                else if ((arr[i] * 10 + arr[j]) % 8 == 0 && i != j)
                    return true;

                else if ((arr[i] * 100 + arr[j] * 10 + arr[k]) % 8 == 0 && i != j && j != k && i != k)
                    return true;
            }
        }
    }
    return false;
}

// Driver function
int main()
{
    string str = "3144";
    if (isSubSeqDivisible(str))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a subsequence
// of digits is divisible by 8.
import java.io.*;

class GFG {

    // Function to calculate any permutation
    // divisible by 8\. If such permutation
    // exists, the function will return
    // that permutation else it will return -1
    static boolean isSubSeqDivisible(String str)
    {

        int i, j, k, l = str.length();
        int arr[] = new int[l];

        // Converting string to integer array for ease
        // of computations (Indexing in arr[] is
        // considered to be starting from 1)
        for (i = 0; i < l; i++)
            arr[i] = str.charAt(i) - '0';

        // Generating all possible permutations
        // and checking if any such
        // permutation is divisible by 8
        for (i = 0; i < l; i++) {
            for (j = i; j < l; j++) {
                for (k = j; k < l; k++) {
                    if (arr[i] % 8 == 0)
                        return true;

                    else if ((arr[i] * 10 + arr[j]) % 8 == 0 && i != j)
                        return true;

                    else if ((arr[i] * 100 + arr[j] * 10 + arr[k]) % 8 == 0
                             && i != j && j != k && i != k)
                        return true;
                }
            }
        }
        return false;
    }

    // Driver function
    public static void main(String args[])
    {

        String str = "3144";
        if (isSubSeqDivisible(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to
# check if a subsequence of digits
# is divisible by 8.

# Function to calculate any
# permutation divisible
# by 8\. If such permutation
# exists, the function
# will return that permutation
# else it will return -1
def isSubSeqDivisible(st) :

    l = len(st)
    arr = [int(ch) for ch in st]

    # Generating all possible
    # permutations and checking
    # if any such permutation
    # is divisible by 8
    for i in range(0, l) :
        for j in range(i, l) :
            for k in range(j, l) :
                if (arr[i] % 8 == 0) :
                    return True

                elif ((arr[i]*10 + arr[j])% 8 == 0 and i != j) :
                    return True

                elif ((arr[i] * 100 + arr[j] * 10 + arr[k]) % 8 == 0 and i != j and j != k and i != k) :
                    return True

    return False

# Driver function

st = "3144"
if (isSubSeqDivisible(st)) :
    print("Yes")
else :
    print("No")

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to check if a subsequence
// of digits is divisible by 8.
using System;

class GFG {

    // Function to calculate any permutation
    // divisible by 8\. If such permutation
    // exists, the function will return
    // that permutation else it will return -1
    static bool isSubSeqDivisible(string str)
    {
        int i, j, k, l = str.Length;
        int[] arr = new int[l];

        // Converting string to integer array for ease
        // of computations (Indexing in arr[] is
        // considered to be starting from 1)
        for (i = 0; i < n; i++)
           arr[i] = str[i] - '0';

        // Generating all possible permutations
        // and checking if any such
        // permutation is divisible by 8
        for (i = 0; i < l; i++) {
            for (j = i; j < l; j++) {
                for (k = j; k < l; k++) {
                    if (arr[i] % 8 == 0)
                        return true;

                    else if ((arr[i] * 10 + arr[j])
                                     % 8
                                 == 0
                             && i != j)
                        return true;

                    else if ((arr[i] * 100 + arr[j] * 10 + arr[k]) % 8 == 0
                             && i != j && j != k
                             && i != k)
                        return true;
                }
            }
        }

        return false;
    }

    // Driver function
    public static void Main()
    {
        string str = "3144";

        if (isSubSeqDivisible(str))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to check if a subsequence
// of digits is divisible by 8.

// Function to calculate any permutation
// divisible by 8\. If such permutation
// exists, the function will return
// that permutation else it will return -1
function isSubSeqDivisible(str)
{
    let i, j, k, l = str.length;
    let arr = [];

    // Converting string to integer array for ease
    // of computations (Indexing in arr[] is
    // considered to be starting from 1)
    for(i = 0; i < l; i++)
       arr[i] = str[i] - '0';

    // Generating all possible permutations
    // and checking if any such
    // permutation is divisible by 8
    for(i = 0; i < l; i++)
    {
        for(j = i; j < l; j++)
        {
            for(k = j; k < l; k++)
            {
                if (arr[i] % 8 == 0)
                    return true;

                else if ((arr[i] * 10 + arr[j]) %
                               8 == 0 && i != j)
                    return true;

                else if ((arr[i] * 100 + arr[j] * 10 +
                         arr[k]) % 8 == 0 && i != j &&
                              j != k && i != k)
                    return true;
            }
        }
    }
    return false;
}

// Driver Code
let str = "3144";
if (isSubSeqDivisible(str))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by susmitakundugoaldanga    

</script>
```

**Output**

```
Yes
```

**方法 2(动态编程):**
虽然我们只有 100 位数字，但是对于比这更长的例子，我们的程序可能会超过给定的时间限制。
因此，我们通过使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法优化我们的代码。
让

![a_{i}              ](img/cfe2d4d5a0db7d4d9aa2986fab6dfce0.png "Rendered by QuickLaTeX.com")

是样本的第一个数字。我们生成一个矩阵 dp[i][j]，1<=i<=n 和 0<=j<8。如果我们能从长度为 I 的前缀中划掉一些数字，使得剩余的数字给出模 8，dp 的值为真，否则为假。为了更广泛地理解这个概念，如果在一个索引处，我们找到该索引的模 8 元素，我们把

![dp[i][a_{i}mod8] = 1              ](img/d0026087064a491c03b97c532578749c.png "Rendered by QuickLaTeX.com")

对于所有其他数字，我们建立在一个简单的概念上，即该数字的加法将提供可被 8 整除的数字的信息，或者它将被忽略。

**注意:**我们也要记住不能改变顺序
现在，

![dp[i][(j*10+a_{i}) mod 8]=max(dp[i][(j*10+a_{i}) mod 8], dp[i-1][j])              ](img/17cb01bc136df5a6366723cd85d50154.png "Rendered by QuickLaTeX.com")

如果我们把当前数字加到前面的结果上。

![dp[i][(j*10) mod 8]=max(dp[i][(j*10) mod 8], dp[i-1][j])              ](img/6f540d750e3c10824b49868a194d8d5e.png "Rendered by QuickLaTeX.com")

如果我们排除当前数字。
现在，如果这样一个数字存在，我们将得到 dp[i][0]中任何 *i* 的“真”

## C++

```
// C++ program to find if there is a subsequence
// of digits divisible by 8.
#include <bits/stdc++.h>
using namespace std;

// Function takes in an array of numbers,
// dynamically goes on the location and
// makes combination of numbers.
bool isSubSeqDivisible(string str)
{
    int n = str.length();
    int dp[n + 1][10];
    memset(dp, 0, sizeof(dp));

    // Converting string to integer array for ease
    // of computations (Indexing in arr[] is
    // considered to be starting from 1)
    int arr[n + 1];
    for (int i = 1; i <= n; i++)
        arr[i] = str[i - 1] - '0';

    for (int i = 1; i <= n; i++) {

        dp[i][arr[i] % 8] = 1;
        for (int j = 0; j < 8; j++) {

            // If we consider the number in our combination,
            // we add it to the previous combination
            if (dp[i - 1][j] > dp[i][(j * 10 + arr[i]) % 8])
                dp[i][(j * 10 + arr[i]) % 8] = dp[i - 1][j];

            // If we exclude the number from our combination
            if (dp[i - 1][j] > dp[i][j])
                dp[i][j] = dp[i - 1][j];
        }
    }

    for (int i = 1; i <= n; i++) {

        // If at dp[i][0], we find value 1/true, it shows
        // that the number exists at the value of 'i'
        if (dp[i][0] == 1)
            return true;
    }

    return false;
}

// Driver function
int main()
{
    string str = "3144";
    if (isSubSeqDivisible(str))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there is a
// subsequence of digits divisible by 8.
import java.io.*;
import java.util.*;

class GFG {

    // Function takes in an array of numbers,
    // dynamically goes on the location and
    // makes combination of numbers.
    static boolean isSubSeqDivisible(String str)
    {

        int n = str.length();
        int dp[][] = new int[n + 1][10];

        // Converting string to integer array
        // for ease of computations (Indexing in
        // arr[] is considered to be starting
        // from 1)
        int arr[] = new int[n + 1];
        for (int i = 1; i <= n; i++)
            arr[i] = (int)(str.charAt(i - 1) - '0');

        for (int i = 1; i <= n; i++) {

            dp[i][arr[i] % 8] = 1;
            for (int j = 0; j < 8; j++) {

                // If we consider the number in
                // our combination, we add it to
                // the previous combination
                if (dp[i - 1][j] > dp[i][(j * 10
                                          + arr[i])
                                         % 8])
                    dp[i][(j * 10 + arr[i]) % 8]
                        = dp[i - 1][j];

                // If we exclude the number from
                // our combination
                if (dp[i - 1][j] > dp[i][j])
                    dp[i][j] = dp[i - 1][j];
            }
        }

        for (int i = 1; i <= n; i++) {

            // If at dp[i][0], we find value 1/true,
            // it shows that the number exists at
            // the value of 'i'
            if (dp[i][0] == 1)
                return true;
        }

        return false;
    }

    // Driver function
    public static void main(String args[])
    {
        String str = "3144";
        if (isSubSeqDivisible(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 program to find
# if there is a subsequence
# of digits divisible by 8.

# Function takes in an array of numbers,
# dynamically goes on the location and
# makes combination of numbers.
def isSubSeqDivisible(str):
    n = len(str)
    dp = [[0 for i in range(10)]
             for i in range(n + 1)]

    # Converting string to integer
    # array for ease of computations
    # (Indexing in arr[] is considered
    # to be starting from 1)
    arr = [0 for i in range(n + 1)]
    for i in range(1, n + 1):
        arr[i] = int(str[i - 1]);

    for i in range(1, n + 1):
        dp[i][arr[i] % 8] = 1;
        for j in range(8):

            # If we consider the number
            # in our combination, we add
            # it to the previous combination
            if (dp[i - 1][j] > dp[i][(j * 10 + arr[i]) % 8]):
                dp[i][(j * 10 + arr[i]) % 8] = dp[i - 1][j]

            # If we exclude the number
            # from our combination
            if (dp[i - 1][j] > dp[i][j]):
                dp[i][j] = dp[i - 1][j]

    for i in range(1, n + 1):

        # If at dp[i][0], we find
        # value 1/true, it shows
        # that the number exists
        # at the value of 'i'
        if (dp[i][0] == 1):
            return True
    return False

# Driver Code
str = "3144"
if (isSubSeqDivisible(str)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to find if there is a
// subsequence of digits divisible by 8.
using System;

class GFG {

    // Function takes in an array of numbers,
    // dynamically goes on the location and
    // makes combination of numbers.
    static bool isSubSeqDivisible(String str)
    {

        int n = str.Length;
        int[, ] dp = new int[n + 1, 10];

        // Converting string to integer array
        // for ease of computations (Indexing in
        // arr[] is considered to be starting
        // from 1)
        int[] arr = new int[n + 1];
        for (int i = 1; i <= n; i++)
            arr[i] = (int)(str[i - 1] - '0');

        for (int i = 1; i <= n; i++) {
            dp[i, arr[i] % 8] = 1;
            for (int j = 0; j < 8; j++) {

                // If we consider the number in
                // our combination, we add it to
                // the previous combination
                if (dp[i - 1, j] > dp[i, (j * 10
                                          + arr[i])
                                             % 8])
                    dp[i, (j * 10 + arr[i]) % 8]
                        = dp[i - 1, j];

                // If we exclude the number from
                // our combination
                if (dp[i - 1, j] > dp[i, j])
                    dp[i, j] = dp[i - 1, j];
            }
        }

        for (int i = 1; i <= n; i++) {

            // If at dp[i][0], we find value
            // 1/true, it shows that the number
            // exists at the value of 'i'
            if (dp[i, 0] == 1)
                return true;
        }

        return false;
    }

    // Driver function
    public static void Main()
    {
        string str = "3144";

        if (isSubSeqDivisible(str))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if there
// is a subsequence of digits
// divisible by 8.

// Function takes in an array of numbers,
// dynamically goes on the location and
// makes combination of numbers.
function isSubSeqDivisible($str)
{
    $n = strlen($str);
    $dp = array_fill(0, $n + 1,
          array_fill(0, 10, NULL));

    // Converting string to integer
    // array for ease of computations
    // (Indexing in arr[] is considered
    // to be starting from 1)
    $arr = array_fill(0, ($n + 1), NULL);
    for ($i = 1; $i <= $n; $i++)
        $arr[$i] = $str[$i - 1] - '0';

    for ($i = 1; $i <= $n; $i++)
    {
        $dp[$i][$arr[$i] % 8] = 1;
        for ($j = 0; $j < 8; $j++)
        {

            // If we consider the number in
            // our combination, we add it to
            // the previous combination
            if ($dp[$i - 1][$j] > $dp[$i][($j * 10 +
                                           $arr[$i]) % 8])
                $dp[$i][($j * 10 +
                         $arr[$i]) % 8] = $dp[$i - 1][$j];

            // If we exclude the number
            // from our combination
            if ($dp[$i - 1][$j] > $dp[$i][$j])
                $dp[$i][$j] = $dp[$i - 1][$j];
        }
    }

    for ($i = 1; $i <= $n; $i++)
    {

        // If at dp[i][0], we find value 1/true,
        // it shows that the number exists at
        // the value of 'i'
        if ($dp[$i][0] == 1)
            return true;
    }

    return false;
}

// Driver Code
$str = "3144";
if (isSubSeqDivisible($str))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
    // Javascript program to find if there is a
    // subsequence of digits divisible by 8.

    // Function takes in an array of numbers,
    // dynamically goes on the location and
    // makes combination of numbers.
    function isSubSeqDivisible(str)
    {

        let n = str.length;
        let dp = new Array(n + 1);
        for(let i = 0; i < 10; i++)
        {
            dp[i] = new Array(10);
            for(let j = 0; j < 10; j++)
            {
                dp[i][j] = 0;
            }
        }

        // Converting string to integer array
        // for ease of computations (Indexing in
        // arr[] is considered to be starting
        // from 1)
        let arr = new Array(n + 1);
        for (let i = 1; i <= n; i++)
            arr[i] = (str[i - 1].charCodeAt() - '0'.charCodeAt());

        for (let i = 1; i <= n; i++) {

            dp[i][arr[i] % 8] = 1;
            for (let j = 0; j < 8; j++) {

                // If we consider the number in
                // our combination, we add it to
                // the previous combination
                if (dp[i - 1][j] > dp[i][(j * 10 + arr[i]) % 8])
                    dp[i][(j * 10 + arr[i]) % 8] = dp[i - 1][j];

                // If we exclude the number from
                // our combination
                if (dp[i - 1][j] > dp[i][j])
                    dp[i][j] = dp[i - 1][j];
            }
        }

        for (let i = 1; i <= n; i++) {

            // If at dp[i][0], we find value 1/true,
            // it shows that the number exists at
            // the value of 'i'
            if (dp[i][0] == 1)
                return true;
        }

        return false;
    }

    let str = "3144";
    if (isSubSeqDivisible(str))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output**

```
Yes
```

使用动态方法，我们的时间复杂度降低到 O(8*n)，其中 8 是可以整除的数，n 是我们输入的长度。因此，整体复杂度为 O(n)。

**方法 3**
对于这个问题，我们只需要检查是否存在可被 8 整除的两位数子序列(8 整除性检验)
我们首先找出所有可被 8 整除的 2 位数，并将十位数字映射为单位位数字
，即:- 16，24，32，40，48，56，64，72，80，88， 96
忽略 48，因为 8 总是能被 8 整除类似地，80 和 88 中有 8，这使得这样的子序列总是能被 8 整除
所以我们在 C++中使用 map(即 stl map)来映射 1 到 6、2 到 4、3 到 2 等等。
在构建映射之后，我们遍历来自最后一个索引的字符串，并检查当前索引号的映射值是否被访问，因此我们需要一个访问数组，如果该索引号被访问，该数组将存储 true，否则存储 false
例如:- 3769
来自最后一个索引的第一个字符是 9，因此我们检查是否访问了 6(即 96 是否是子序列)， 我们在访问数组
中标记 9，下一个字符是 6，所以我们检查是 4 访问(即 64)，我们在访问数组
中标记 6，下一个字符是 7，所以我们检查是 2 访问(即 72)，我们在访问数组
中标记 7，下一个字符是 3，所以我们检查是 6 访问(即 36)，是 6 被标记，因此我们打印是。

## C++

```
// C++ program to check if given string
// has a subsequence divisible by 8
#include<bits/stdc++.h>
using namespace std;
// Driver function
int main(){

    string str = "129365";

    // map key will be tens place digit of number
        // that is divisible by 8 and value will
        // be units place digit
    map<int, int> mp;

    // For filling the map let start
        // with initial value 8
    int no = 8;

    while(no < 100){
        no = no + 8;

        // key is digit at tens place and value is
            // digit at units place mp.insert({key, value})
        mp.insert({(no / 10) % 10, no % 10});
    }

    // Create a hash to check if we visited a number
    vector<bool> visited(10, false);

    int i;
    // Iterate from last index to 0th index
    for(i = str.length() - 1; i >= 0; i--){

        // If 8 is present in string then
            // 8 divided 8 hence print yes
        if(str[i] == '8')
           {
               cout << "Yes";
                break;
           }

        // considering present character as the second
        // digit of two digits no we check if the value
        // of this key is marked in hash or not
        // If marked then we a have a number divisible by 8
        if(visited[mp[str[i] - '0']]){
            cout << "Yes";
            break;
        }
        visited[str[i] - '0'] = true;     

    }
    // If no subsequence divisible by 8 
    if(i == -1)
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// given String has a subsequence
// divisible by 8
import java.util.*;
class GFG{

// Driver code
public static void main(String[] args)
{
  String str = "129365";

  // map key will be tens place
  // digit of number that is
  // divisible by 8 and value will
  // be units place digit
  HashMap<Integer,
          Integer> mp = new HashMap<Integer,
                                    Integer>();

  // For filling the map let start
  // with initial value 8
  int no = 8;

  while(no < 100)
  {
    no = no + 8;

    // key is digit at tens place
    // and value is digit at units
    // place mp.add({key, value})
    //if(mp.containsKey((no / 10) % 10))
    mp.put((no / 10) % 10, no % 10);
  }

  // Create a hash to check if
  // we visited a number
  boolean[] visited = new boolean[10];

  int i;

  // Iterate from last index
  // to 0th index
  for(i = str.length() - 1;
      i >= 0; i--)
  {
    // If 8 is present in String then
    // 8 divided 8 hence print yes
    if(str.charAt(i) == '8')
    {
      System.out.print("Yes");
      break;
    }

    // considering present character
    // as the second digit of two
    // digits no we check if the value
    // of this key is marked in hash or not
    // If marked then we a have a number
    // divisible by 8
    if(visited[mp.get(str.charAt(i)- '0')])
    {
      System.out.print("Yes");
      break;
    }
    visited[str.charAt(i) - '0'] = true;    

  }
  // If no subsequence divisible
  // by 8
  if(i == -1)
    System.out.print("No");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to check if given string
# has a subsequence divisible by 8
Str = "129365"

# map key will be tens place digit of number
# that is divisible by 8 and value will
# be units place digit
mp = {}

# For filling the map let start
# with initial value 8
no = 8

while(no < 100) :
    no = no + 8

    # key is digit at tens place and value is
    # digit at units place mp.insert({key, value})
    mp[(no // 10) % 10] = no % 10

# Create a hash to check if we visited a number
visited = [False] * 10

# Iterate from last index to 0th index
for i in range(len(Str) - 1, -1, -1) :

    # If 8 is present in string then
    # 8 divided 8 hence print yes
    if(Str[i] == '8') :

        print("Yes", end = "")
        break

    # considering present character as the second
    # digit of two digits no we check if the value
    # of this key is marked in hash or not
    # If marked then we a have a number divisible by 8
    if visited[mp[ord(Str[i]) - ord('0')]] :
        print("Yes", end = "")
        break

    visited[ord(Str[i]) - ord('0')] = True

# If no subsequence divisible by 8
if(i == -1) :
    print("No")

    # This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to check if given
// String has a subsequence
// divisible by 8
using System;
using System.Collections.Generic;

class GFG{

// Driver code
public static void Main(String[] args)
{
    String str = "129365";

    // Map key will be tens place
    // digit of number that is
    // divisible by 8 and value will
    // be units place digit
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // For filling the map let start
    // with initial value 8
    int no = 8;

    while (no < 100)
    {
        no = no + 8;

        // Key is digit at tens place
        // and value is digit at units
        // place mp.Add({key, value})
        if (mp.ContainsKey((no / 10) % 10))
            mp[(no / 10) % 10] = no % 10;
        else
            mp.Add((no / 10) % 10, no % 10);
    }

    // Create a hash to check if
    // we visited a number
    bool[] visited = new bool[10];

    int i;

    // Iterate from last index
    // to 0th index
    for(i = str.Length - 1; i >= 0; i--)
    {

        // If 8 is present in String then
        // 8 divided 8 hence print yes
        if (str[i] == '8')
        {
            Console.Write("Yes");
            break;
        }

        // Considering present character
        // as the second digit of two
        // digits no we check if the value
        // of this key is marked in hash or not
        // If marked then we a have a number
        // divisible by 8
        if (visited[mp[str[i] - '0']])
        {
            Console.Write("Yes");
            break;
        }
        visited[str[i] - '0'] = true;
    }

    // If no subsequence divisible
    // by 8
    if (i == -1)
        Console.Write("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to check if
// given String has a subsequence
// divisible by 8

    // Driver code
    let str = "129365";

    // map key will be tens place
  // digit of number that is
  // divisible by 8 and value will
  // be units place digit
  let mp = new Map();

  // For filling the map let start
  // with initial value 8
  let no = 8;

  while(no < 100)
  {
    no = no + 8;

    // key is digit at tens place
    // and value is digit at units
    // place mp.add({key, value})
    //if(mp.containsKey((no / 10) % 10))
    mp.set((Math.floor(no / 10)) % 10, no % 10);
  }

  // Create a hash to check if
  // we visited a number
  let visited = new Array(10);
  for(let i=0;i<visited.length;i++)
  {
      visited[i]=false;
  }

  let i;

  // Iterate from last index
  // to 0th index
  for(i = str.length - 1;
      i >= 0; i--)
  {
    // If 8 is present in String then
    // 8 divided 8 hence print yes
    if(str[i] == '8')
    {
      document.write("Yes");
      break;
    }

    // considering present character
    // as the second digit of two
    // digits no we check if the value
    // of this key is marked in hash or not
    // If marked then we a have a number
    // divisible by 8
    if(visited[mp.get(str[i].charCodeAt(0)-
    '0'.charCodeAt(0))])
    {
      document.write("Yes");
      break;
    }
    visited[str[i].charCodeAt(0) -
    '0'.charCodeAt(0)] = true;   

  }
  // If no subsequence divisible
  // by 8
  if(i == -1)
    document.write("No");

    // This code is contributed by rag2127

</script>
```

**Output**

```
Yes
```

如果仔细观察，被访问的数组将始终有 10 个字段，并且映射将始终具有相同的大小，因此空间复杂度将为 0(1)，遍历字符串的时间复杂度将为 0(n)。