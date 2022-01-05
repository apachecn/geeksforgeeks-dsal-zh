# 可被其整除的数的重排

> 原文:[https://www . geesforgeks . org/重排-数也可分/](https://www.geeksforgeeks.org/rearrangement-number-also-divisible/)

给定一个数字 n，我们需要重新排列它的所有数字，这样新的排列可以被 n 整除。此外，新的数字不应该等于 x。如果不可能这样重新排列，请打印-1。

**示例:**

```
Input : n = 1035
Output : 3105
The result 3105 is divisible by
given n and has the same set of digits.

Input : n = 1782
Output : m = 7128

```

**简单方法:**找出给定 n 的所有排列，然后检查它是否能被 n 整除，还要检查新的排列不应该等于 n。

**有效方法:**假设 y 是我们的结果，那么 y = m * n，我们也知道 y 一定是 n 位数的重排，所以我们可以说现在根据给定的条件限制 m(乘数)。
1) y 和 n 的位数相同。所以，m 必须小于 10。
2) y 一定不等于 n，所以 m 会大于 1。
所以我们得到范围[2，9]内的乘数 m。所以我们会找到所有可能的 y，然后检查 y 是否和 n 有相同的数字。

## C++

```
// CPP program for finding rearrangement of n
// that is divisible  by n
#include<bits/stdc++.h>
using namespace std;

// perform hashing for given n
void storeDigitCounts(int n, vector<int> &hash)
{
    // perform hashing
    while (n)
    {
        hash[n%10]++;
        n /= 10;
    }
}

// check whether any arrangement exists
int rearrange (int n)
{
    // Create a hash for given number n
    // The hash is of size 10 and stores
    // count of each digit in n.
    vector<int> hash_n(10, 0);
    storeDigitCounts(n, hash_n);

    // check for all possible multipliers
    for (int mult=2; mult<10; mult++)
    {
        int curr = n*mult;

        vector<int> hash_curr(10, 0);
        storeDigitCounts(curr, hash_curr);

        // check hash table for both. 
        // Please refer below link for help 
        // of equal()
        // https://www.geeksforgeeks.org/stdequal-in-cpp/
        if (equal(hash_n.begin(), hash_n.end(),
                             hash_curr.begin()))
            return curr;
    }
    return -1;
}

// driver program
int main()
{
    int n = 10035;
    cout << rearrange(n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for finding rearrangement 
# of n that is divisible by n 

# Perform hashing for given n 
def storeDigitCounts(n, Hash): 

    # perform hashing 
    while n > 0: 

        Hash[n % 10] += 1
        n //= 10

# check whether any arrangement exists 
def rearrange(n): 

    # Create a hash for given number n 
    # The hash is of size 10 and stores 
    # count of each digit in n. 
    hash_n = [0] * 10
    storeDigitCounts(n, hash_n) 

    # check for all possible multipliers 
    for mult in range(2, 10): 

        curr = n * mult 

        hash_curr = [0] * 10
        storeDigitCounts(curr, hash_curr) 

        # check hash table for both. 
        if hash_n == hash_curr: 
            return curr 

    return -1

# Driver Code
if __name__ == "__main__": 

    n = 10035
    print(rearrange(n))

# This code is contributed by Rituraj Jain
```

**输出:**

```
30105

```

本文由**[Shivam Pradhan(anuj _ charm)](http://www.facebook.com/ma5ter6it)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。