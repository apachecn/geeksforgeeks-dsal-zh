# 检查一个数字是否可以表示为 a^b |集合 2

> 原文:[https://www . geesforgeks . org/check-if-a-number-can-express-as-ab-set-2/](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-ab-set-2/)

你给了一个数 n。检查一个数是否可以用幂(a，b)来表示(a^b).

**例:**

```
Input : 4
Output : Yes
22 = 4

Input : 12
Output : No
```

我们在[中讨论了两种方法，检查一个数是否可以表示为 x^y (x 的幂为 y)](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-xy-x-raised-to-power-y/) 。在这篇文章中，讨论了一个更有效的解决方案。这个想法是基于对数的。

```
Consider a no. N which needs 
to be expressed in the form (a^b).
N = ab
Taking log both sides:
log (N) = b.log (a)
b = log(N)/log(a)
```

牢记这一逻辑，开发出下面提到的最高效的解决方案:

## c++

```
// CPP program to check if a number
// can be expressed as a^b.
#include <bits/stdc++.h>
using namespace std;

bool isPower(int a)
{
    if (a == 1)
        return true;

    for (int i = 2; i * i <= a; i++) {
        double val = log(a) / log(i);
        if ((val - (int)val) < 0.00000001)
            return true;
    }

    return false;
}

// Driver code
int main()
{
    int n = 16;
    cout << (isPower(n) ? "Yes" : "No");
    return 0;
}
```

## Java

```
//Java program to check if a number
//can be expressed as a^b.

public class GFG {

    static boolean isPower(int a)
    {
    if (a == 1)
        return true;

    for (int i = 2; i * i <= a; i++) {
        double val = Math.log(a) / Math.log(i);
        if ((val - (int)val) < 0.00000001)
            return true;
    }

    return false;
    }

    // Driver code
    public static void main(String[] args) {

        int n = 16;
        System.out.println(isPower(n) ? "Yes" : "No");

    }
}
```

## Python 3

T2

## c#

T3】PHPT4

## Javascript

```
<script>
//Javascript program to check if a number
//can be expressed as a^b.

    function isPower(a)
    {
        if (a == 1)
        return true;

    for (let i = 2; i * i <= a; i++) {
        let val = Math.log(a) / Math.log(i);
        if ((val - Math.floor(val)) < 0.00000001)
            return true;

    }

    return false;

    }

    // Driver code
    let n = 16;
    document.write(isPower(n) ? "Yes" : "No");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**时间复杂度:** O(sqrt(n))