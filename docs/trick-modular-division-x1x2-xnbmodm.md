# 模除法的技巧((x1 * x2 …)。xn) / b ) mod (m)

> 原文:[https://www . geesforgeks . org/trick-modular-division-x1x 2-xnbmodm/](https://www.geeksforgeeks.org/trick-modular-division-x1x2-xnbmodm/)

给定整数 x1，x2，x3…xn，b 和 m，我们应该找到((x1*x2…xn)/b)mod(m)。
**例 1:** 假设要求我们求(55 C5)%(10000000007)即((55 * 54 * 53 * 52 * 51)/120)% 10000000007
**天真法:**

1.  简单计算乘积(55*54*53*52*51)=比如 x，
2.  将 x 除以 120，然后取它的模 1000000007

**使用模乘逆:**
上述方法只有在 x1，x2，x3……。xn 值很小。
假设我们需要找到 x1，x2，…的结果。xn 落在~1000000(10^6).范围内因此，我们将不得不利用模块化数学的规则，它说:
(a * b)mod(m)=(a(mod(m))* b(mod(m)))mod(m)
请注意，上述公式对模块化乘法有效。类似的除法公式不存在。
即(a/b)mod(m)！= a(mod(m))/b(mod(m))

1.  所以我们需要找出 b 的[模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)说 I，然后用 a 乘 I。
2.  此后，我们将不得不取所得结果的模。
    即((x1*x2…)。xn)/b)mod(m)=((x1*x2…xn)* I)mod(m)=((x1)mod(m)*(x2)mod(m)*…。(xn)mod(m) * (i)mod(m))mod(m)

注:要找到模乘逆，我们可以使用[扩展欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)或费马小定理。
**例 2 :** 假设我们要找到(55555 C5)%(10000000007)即((55555 * 55554 * 55553 * 55552 * 55551)/120)% 100000000007。

## C++

```
// To run this code, we need to copy modular inverse
// from below post.
// https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/

int main()
{
    // naive method-calculating the result in a single line
    long int naive_answer = ((long int)(55555 * 55554 *
                55553 * 55552 * 55551) / 120) % 1000000007;

    long int ans = 1;

    // modular_inverse() is a user defined function
    // that calculates inverse of a number
    long int i = modular_inverse(120, 10000007);

    // it will use extended Eucledian algorithm or
    // Fermat’s Little Theorem for calculation.
    // MMI of 120 under division by 1000000007
    // will be 808333339
    for (int i = 0; i < 5; i++)
        ans = (ans * (55555 - i)) % 1000000007;

    ans = (ans * i) % 1000000007;
    cout << "Answer using naive method: " << naive_answer << endl;
    cout << "Answer using multiplicative"
         << " modular inverse concept: " << ans;

    return 0;
}
```