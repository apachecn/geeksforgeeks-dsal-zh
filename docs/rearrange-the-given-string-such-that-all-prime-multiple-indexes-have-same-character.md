# 重新排列给定的字符串，使所有质数索引具有相同的字符

> 原文:[https://www . geeksforgeeks . org/重排给定字符串，以便所有质数多索引都具有相同的字符/](https://www.geeksforgeeks.org/rearrange-the-given-string-such-that-all-prime-multiple-indexes-have-same-character/)

给定一根大小为 **N** 的绳子**绳子**。任务是找出是否可能重新排列字符串中的字符，以便对于任何质数 p < = N 和范围从 1 到 N/p 的任何整数 I，必须满足条件字符串 <sub>p</sub> =字符串 <sub>p*i</sub> 。如果不可能进行任何这样的重新排列，则打印-1。

**示例:**

> **输入:**str = " aabaaa "
> T3】输出:baaaaa
> 字符串大小为 7。
> 索引 2、4、6 包含相同的字符。
> 索引 3、6 包含相同的字符。
> 
> **输入:** str = "abcd"
> **输出:** -1

**进场:**

*   除了第一个位置和质数大于 N/2 的位置之外，所有位置都必须有相同的符号。
*   剩余位置可以有任何符号。该位置保持使用[筛](https://www.geeksforgeeks.org/sieve-eratosthenes-0n-time-complexity/)。
*   如果字符串中出现次数最多的元素少于这些位置，则打印-1。

以下是上述方法的实现:

## C++

```
// CPP program to rearrange the given 
// string such that all prime multiple
// indexes have same character
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// To store answer
char ans[N];
int sieve[N];

// Function to rearrange the given string
// such that all prime multiple indexes
// have the same character.
void Rearrange(string s, int n)
{
    // Initially assume that we can kept
    // any symbol at any positions.
    // If at any index contains one then it is not
    // counted in our required positions
    fill(sieve + 1, sieve + n + 1, 1);

    // To store number of positions required
    // to store elements of same kind
    int sz = 0;

    // Start sieve
    for (int i = 2; i <= n / 2; i++) {
        if (sieve[i]) {
            // For all multiples of i
            for (int j = 1; i * j <= n; j++) {
                if (sieve[i * j])
                    sz++;
                sieve[i * j] = 0;
            }
        }
    }

    // map to store frequency of each character
    map<char, int> m;
    for (auto it : s)
        m[it]++;

    // Store all characters in the vector and
    // sort the vector to find the character with
    // highest frequency
    vector<pair<int, char> > v;
    for (auto it : m)
        v.push_back({ it.second, it.first });
    sort(v.begin(), v.end());

    // If most occured character is less than
    // required positions
    if (v.back().first < sz) {
        cout << -1;
        return;
    }

    // In all required positions keep
    // character which occured most times
    for (int i = 2; i <= n; i++) {
        if (!sieve[i]) {

            ans[i] = v.back().second;
        }
    }

    // Fill all other indexes with
    // remaining characters
    int idx = 0;
    for (int i = 1; i <= n; i++) {
        if (sieve[i]) {
            ans[i] = v[idx].second;
            v[idx].first--;
            // If character frequency becomes
            // zero then go to next character
            if (v[idx].first == 0)
                idx++;
        }
        cout << ans[i];
    }
}

// Driver code
int main()
{
    string str = "aabaaaa";

    int n = str.size();

    // Function call
    Rearrange(str, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to rearrange the given 
# string such that all prime multiple 
# indexes have same character 

N = 100005

# To store answer 
ans = [0]*N; 
# sieve = [1]*N; 

# Function to rearrange the given string 
# such that all prime multiple indexes 
# have the same character. 
def Rearrange(s, n) : 

    # Initially assume that we can kept 
    # any symbol at any positions. 
    # If at any index contains one then it is not 
    # counted in our required positions 
    sieve = [1]*(N+1);

    # To store number of positions required 
    # to store elements of same kind
    sz = 0;

    # Start sieve
    for i in range(2, n//2 + 1) :
        if (sieve[i]) :

            # For all multiples of i
            for j in range(1, n//i + 1) :
                if (sieve[i * j]) :
                    sz += 1;
                sieve[i * j] = 0;

    # map to store frequency of each character 
    m = dict.fromkeys(s,0);

    for it in s :
        m[it] += 1;

    # Store all characters in the vector and 
    # sort the vector to find the character with 
    # highest frequency
    v = [];
    for key,value in m.items() :
        v.append([ value, key] );

    v.sort();

    # If most occured character is less than
    # required positions
    if (v[-1][0] < sz) :
        print(-1,end="");
        return;

    # In all required positions keep
    # character which occured most times
    for i in range(2, n + 1) :
        if (not sieve[i]) :
            ans[i] = v[-1][1];

    # Fill all other indexes with 
    # remaining characters 
    idx = 0;

    for i in range(1, n + 1) :
        if (sieve[i]):
            ans[i] = v[idx][1];
            v[idx][0] -= 1;

            # If character frequency becomes 
            # zero then go to next character
            if (v[idx][0] == 0) :
                idx += 1;

        print(ans[i],end= ""); 

# Driver code 
if __name__ == "__main__" : 

    string = "aabaaaa"; 

    n = len(string); 

    # Function call 
    Rearrange(string, n); 

# This code is contributed by AnkitRai01
```

**Output:**

```
baaaaaa

```