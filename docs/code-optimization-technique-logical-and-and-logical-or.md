# 代码优化技术(逻辑与和逻辑或)

> 原文:[https://www . geesforgeks . org/code-optimization-technology-logic-and-and-logic-or/](https://www.geeksforgeeks.org/code-optimization-technique-logical-and-and-logical-or/)

## 逻辑与(&&)

在使用&&(逻辑与)时，我们必须将获得**假**概率高的条件放在第一位，这样如果第一个条件为假，编译器就不需要检查第二个条件。

## C++14

```
#include <bits/stdc++.h>
using namespace std;
// Function to check whether n is odd
bool isOdd(int n) { return (n & 1); }

// Function to check whether n is prime
bool isPrime(int n)
{
    if (n <= 1)
        return false;
    for (int i = 2; i <= sqrt(n); i++)
        if ((n % i) == 0)
            return false;
    return true;
}

int main()
{
    int cnt = 0, n = 10;

    // Implementation 1
    for (int i = 2; i <= n; i++) {
        if (isOdd(i) && isPrime(i))
            cnt++;
    }

    cnt = 0;
    n = 10;

    // Implementation 2
    for (int i = 2; i <= n; i++) {
        if (isPrime(i) && isOdd(i))
            cnt++;
    }
}
```

## 蟒蛇 3

```
# Function to check whether n is odd
def isOdd(n):
    pass

# Function to check whether n is prime
def isPrime(n):
    pass

if __name__ == '__main__':
    cnt = 0; n = 10

    # Implementation 1
    for i in range(2,n) :
        if isOdd(i) and isPrime(i):
            cnt+=1

    cnt = 0
    n = 10

    # Implementation 2
    for i in range(2,n):
        if isPrime(i) and isOdd(i):
            cnt+=1

```

考虑上面的实现:

> **在实现 1** 中，我们避免检查偶数是否是素数，因为素数测试需要比检查偶数/奇数更多的计算。
> 一个数变得奇数的概率大于它是质数的概率，这就是为什么我们首先检查这个数是否是奇数，然后再检查它是否是质数。

> 另一方面**在实现 2** 中，我们在检查一个数是否为素数之前，先检查这个数是否为奇数，这使得不必要的计算，因为除了 **2** 之外的所有偶数都不是素数，但是实现仍然检查它们是否为素数。

## 逻辑或(||)

在使用||(逻辑 OR)时，我们必须将条件放在第一位，其得到**为真**的概率很高，这样如果第一个条件为真，编译器就不需要检查第二个条件。

## C

```
#include <iostream.h>

// Function to check whether n is odd
bool isEven(int n);

// Function to check whether n is prime
bool isPrime(int n);

int main()
{
    int cnt = 0, n = 10;

    // Implementation 1
    for (int i = 3; i <= n; i++) {
        if (isEven(i) || !isPrime(i))
            cnt++;
    }
}
```

## 蟒蛇 3

```
# Function to check whether n is even
def isEven(n):
    pass

# Function to check whether n is prime
def isPrime(n):
    pass

if __name__ == '__main__':
    cnt = 0; n = 10

    # Implementation 1
    for i in range(3,n) :
        if isOdd(i) or not isPrime(i):
            cnt+=1
```

> 如前所述，一个数为偶数的概率大于它为非素数的概率。语句的当前执行顺序不允许检查大于 2 的偶数是否为非素数(因为它们都是非素数)。

**注意:**对于较大的输入，语句的执行顺序会影响程序的整体执行时间。