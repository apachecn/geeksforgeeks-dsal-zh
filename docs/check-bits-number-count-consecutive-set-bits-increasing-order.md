# 检查一个数字的位是否具有递增顺序的连续设置位的计数

> 原文:[https://www . geesforgeks . org/check-bits-number-count-continuous-set-bits-递增-order/](https://www.geeksforgeeks.org/check-bits-number-count-consecutive-set-bits-increasing-order/)

给定一个整数 n > 0，任务是找出在整数计数的位模式中连续的 1 是否在从左向右增加。

**例:**

```
Input:19
Output:Yes
Explanation: Bit-pattern of 19 = 10011,
Counts of continuous 1's from left to right 
are 1, 2 which are in increasing order.

Input  : 183
Output : yes
Explanation: Bit-pattern of 183 = 10110111,
Counts of continuous 1's from left to right 
are 1, 2, 3 which are in increasing order.
```

一个**简单的解决方案**是将给定数字的二进制表示存储到一个字符串中，然后从左向右遍历并计算连续 1 的数量。对于每次遇到 0，检查连续 1 的先前计数的值与当前值的值，如果先前计数的值大于当前计数的值，则返回假，否则当字符串结束时返回真。

## c++

```
// C++ program to find if bit-pattern
// of a number has increasing value of
// continuous-1 or not.
#include<bits/stdc++.h>
using namespace std;

// Returns true if n has increasing count of
// continuous-1 else false
bool findContinuous1(int n)
{
    const int bits = 8*sizeof(int);

    // store the bit-pattern of n into
    // bit bitset- bp
    string bp = bitset <bits>(n).to_string();

    // set prev_count = 0 and curr_count = 0.
    int prev_count = 0, curr_count = 0;

    int i = 0;
    while (i < bits)
    {
        if (bp[i] == '1')
        {
            // increment current count of continuous-1
            curr_count++;
            i++;
        }

        // traverse all continuous-0
        else if (bp[i-1] == '0')
        {
            i++;
            curr_count = 0;
            continue;
        }

        // check  prev_count and curr_count
        // on encounter of first zero after
        // continuous-1s
        else
        {
            if (curr_count < prev_count)
                return 0;
            i++;
            prev_count=curr_count;
            curr_count = 0;
        }
    }

    // check for last sequence of continuous-1
    if (prev_count > curr_count && (curr_count != 0))
        return 0;

    return 1;
}

// Driver code
int main()
{
    int n = 179;
    if (findContinuous1(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## python 3

```
# Python3 program to find if bit-pattern
# of a number has increasing value of
# continuous-1 or not.

# Returns true if n has increasing count of
# continuous-1 else false
def findContinuous1(n):

    # store the bit-pattern of n into
    # bit bitset- bp
    bp = list(bin(n))

    bits = len(bp)

    # set prev_count = 0 and curr_count = 0.
    prev_count = 0
    curr_count = 0

    i = 0
    while (i < bits):
        if (bp[i] == '1'):

            # increment current count of continuous-1
            curr_count += 1
            i += 1

        # traverse all continuous-0
        elif (bp[i - 1] == '0'):
            i += 1
            curr_count = 0
            continue

        # check prev_count and curr_count
        # on encounter of first zero after
        # continuous-1s
        else:
            if (curr_count < prev_count):
                return 0
            i += 1
            prev_count = curr_count
            curr_count = 0

    # check for last sequence of continuous-1
    if (prev_count > curr_count and (curr_count != 0)):
        return 0

    return 1

# Driver code
n = 179
if (findContinuous1(n)):
    print( "Yes")
else:
    print( "No")

# This code is contributed by SHUBHAMSINGH10
```

## Javascript

```
<script>
// JavaScript program to find if bit-pattern
// of a number has increasing value of
// continuous-1 or not.
function dec2bin(dec) {
  return (dec >>> 0).toString(2);
}
// Returns true if n has increasing count of
// continuous-1 else false
function findContinuous1(n){
    // store the bit-pattern of n into
    // bit bitset- bp
    let bp = dec2bin(n)
    let bits = bp.length

    // set prev_count = 0 and curr_count = 0.
    let prev_count = 0
    let curr_count = 0

    let i = 0
    while (i < bits){
        if (bp[i] == '1'){
            // increment current count of continuous-1
            curr_count += 1;
            i += 1;
        }
        // traverse all continuous-0
        else if (bp[i - 1] == '0'){
            i += 1
            curr_count = 0
            continue
        }
        // check prev_count and curr_count
        // on encounter of first zero after
        // continuous-1s
        else{
            if (curr_count < prev_count)
                return 0
            i += 1
            prev_count = curr_count
            curr_count = 0
        }
    }
    // check for last sequence of continuous-1
    if (prev_count > curr_count && (curr_count != 0))
        return 0

    return 1
}
// Driver code
n = 179
if (findContinuous1(n))
    document.write( "Yes")
else
    document.write( "No")

</script>
```

**输出:**

```
Yes
```