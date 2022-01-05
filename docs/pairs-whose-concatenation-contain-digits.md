# 串联包含所有数字的对

> 原文:[https://www . geesforgeks . org/pairs-what-concation-contain-digits/](https://www.geeksforgeeks.org/pairs-whose-concatenation-contain-digits/)

给定一组 **n 个**数字。任务是找出可以从给定的中得到的对的数量，这些对在连接时将包含从 0 到 9 的所有数字。
**例:**

> 输入:num[][]= {“129300455”、“5559948277”、“012334556”、“56789”、“123456879”}
> 输出:5
> {“129300455”、“56789”}、{“129300455”、“123456879”}、{“5559948277”、“0123337”

注意:每个数字中的数字可以是 10^6.

其思想是将每个数字表示为 10 位的掩码，这样如果它包含数字 **i** 至少一次，那么在掩码中将设置 **i <sup>第</sup>T5】位。
例如
让 n = 4556120 然后 0 <sup>th</sup> ，1 <sup>st</sup> ，2 <sup>nd</sup> ，4 <sup>th</sup> ，5 <sup>th</sup> ，6 <sup>th</sup> 位将被设置在掩码中。
因此，mask =(0001110111)<sub>2</sub>=(119)<sub>10</sub>
现在，对于从 0 到 2^10–1 的每个 mask **m** ，我们将存储其编号的掩码等于 **m** 的编号的计数。
那么，我们来做一个数组，比如 cnt[]，其中 cnt[i]存储掩码等于 I 的数字个数的计数，这个的伪代码:** 

```
for (i = 0; i < (1 << 10); i++)
  cnt[i] = 0;

for (i = 1; i <= n; i++)
{
  string x = p[i];
  int mask  = 0;
  for (j = 0; j < x.size(); j++)  
    mask |= (1 << (x[j] - '0';);

  cnt[mask]++;
}
```

如果 0 到 9 的每一位都在 maskof 的位 OR 中设置，即如果它等于(11111111111)<sub>2</sub)=(1023)10</sub>
，则一对数字将具有从 0 到 9 的所有数字

现在，我们将迭代所有按位“或”等于 1023 的掩码对，并添加多种方法。
以下是该方法的实现:

## C++

```
// C++ Program to find number of pairs whose
// concatenation contains all digits from 0 to 9.
#include <bits/stdc++.h>
using namespace std;
#define N 20

// Function to return number of pairs whose
// concatenation contain all digits from 0 to 9
int countPair(char str[N][N], int n)
{
    int cnt[1 << 10] = { 0 };

    // making the mask for each of the number.
    for (int i = 0; i < n; i++) {

        int mask = 0;
        for (int j = 0; str[i][j] != '\0'; ++j)
            mask |= (1 << (str[i][j] - '0'));       
        cnt[mask]++;
    }

    // for each of the possible pair which can
    // make OR value equal to 1023
    int ans = 0;
    for (int m1 = 0; m1 <= 1023; m1++)
        for (int m2 = 0; m2 <= 1023; m2++)
            if ((m1 | m2) == 1023) {

                // finding the count of pair
                // from the given numbers.
                ans += ((m1 == m2) ?
                       (cnt[m1] * (cnt[m1] - 1)) :
                       (cnt[m1] * cnt[m2]));
            }

    return ans / 2;
}

// Driven Program
int main()
{
    int n = 5;
    char str[][N] = { "129300455", "5559948277",
               "012334556", "56789", "123456879" };
    cout << countPair(str, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find number of pairs whose
// concatenation contains all digits from 0 to 9.
class GFG
{
    static final int N = 20;

    // Function to return number of pairs whose
    // concatenation contain all digits from 0 to 9
    static int countPair(char str[][], int n)
    {
        int[] cnt = new int[1 << 10];

        // making the mask for each of the number.
        for (int i = 0; i < n; i++)
        {
            int mask = 0;
            for (int j = 0; j < str[i].length; ++j)
                mask |= (1 << (str[i][j] - '0'));
            cnt[mask]++;
        }

        // for each of the possible pair which can
        // make OR value equal to 1023
        int ans = 0;
        for (int m1 = 0; m1 <= 1023; m1++)
            for (int m2 = 0; m2 <= 1023; m2++)
                if ((m1 | m2) == 1023)
                {

                    // finding the count of pair
                    // from the given numbers.
                    ans += ((m1 == m2) ? (cnt[m1] * (cnt[m1] - 1)) :
                                          (cnt[m1] * cnt[m2]));
                }
        return ans / 2;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        char str[][] = { "129300455".toCharArray(),
                         "5559948277".toCharArray(),
                         "012334556".toCharArray(),
                         "56789".toCharArray(),
                         "123456879".toCharArray() };
        System.out.print(countPair(str, n) + "\n");
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Program to find
# number of pairs whose
# concatenation contains
# all digits from 0 to 9.
N = 20

# Function to return number
# of pairs whose concatenation
# contain all digits from 0 to 9
def countPair(st, n):

    cnt = [0] * (1 << 10)

    # Making the mask for
    # each of the number.
    for i in range (n):
        mask = 0
        for j in range (len(st[i])):
            mask |= (1 << (ord(st[i][j]) - ord('0')))      
        cnt[mask] += 1

    # for each of the possible
    # pair which can make OR
    # value equal to 1023
    ans = 0
    for m1 in range(1024):
        for m2 in range (1024):
            if ((m1 | m2) == 1023):

                # Finding the count of pair
                # from the given numbers.
                if (m1 == m2):
                      ans += (cnt[m1] * (cnt[m1] - 1))
                else:
                      ans += (cnt[m1] * cnt[m2])

    return ans // 2

# Driven Program
if __name__ == "__main__":

    n = 5
    st = ["129300455", "5559948277",
          "012334556", "56789", "123456879"]
    print(countPair(st, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to find number of pairs whose
// concatenation contains all digits from 0 to 9.
using System;

class GFG
{
    static readonly int N = 20;

    // Function to return number of pairs whose
    // concatenation contain all digits from 0 to 9
    static int countPair(String []str, int n)
    {
        int[] cnt = new int[1 << 10];

        // making the mask for each of the number.
        for (int i = 0; i < n; i++)
        {
            int mask = 0;
            for (int j = 0; j < str[i].Length; ++j)
                mask |= (1 << (str[i][j] - '0'));
            cnt[mask]++;
        }

        // for each of the possible pair which can
        // make OR value equal to 1023
        int ans = 0;
        for (int m1 = 0; m1 <= 1023; m1++)
            for (int m2 = 0; m2 <= 1023; m2++)
                if ((m1 | m2) == 1023)
                {

                    // finding the count of pair
                    // from the given numbers.
                    ans += ((m1 == m2) ? (cnt[m1] * (cnt[m1] - 1)) :
                                         (cnt[m1] * cnt[m2]));
                }
        return ans / 2;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 5;
        String []str = {"129300455",
                        "5559948277",
                        "012334556",
                        "56789",
                        "123456879" };
        Console.Write(countPair(str, n) + "\n");
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript Program to find number of pairs whose
// concatenation contains all digits from 0 to 9.

    let N = 20;

    // Function to return number of pairs whose
    // concatenation contain all digits from 0 to 9
    function countPair(str,n)
    {
        let cnt = new Array(1 << 10);
        for(let i=0;i<cnt.length;i++)
        {
            cnt[i]=0;
        }

        // making the mask for each of the number.
        for (let i = 0; i < n; i++)
        {
            let mask = 0;
            for (let j = 0; j < str[i].length; ++j)
                mask |= (1 << (str[i][j] - '0'));
            cnt[mask]++;
        }

        // for each of the possible pair which can
        // make OR value equal to 1023
        let ans = 0;
        for (let m1 = 0; m1 <= 1023; m1++)
            for (let m2 = 0; m2 <= 1023; m2++)
                if ((m1 | m2) == 1023)
                {

                    // finding the count of pair
                    // from the given numbers.
                    ans += ((m1 == m2) ? (cnt[m1] * (cnt[m1] - 1)) :
                                          (cnt[m1] * cnt[m2]));
                }
        return Math.floor(ans / 2);
    }

    // Driver Code
    let n = 5;
    let st = ["129300455", "5559948277",
          "012334556", "56789", "123456879"];
    document.write(countPair(st, n))    

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
5
```

**复杂度:** O(n + 2^10 * 2^10)