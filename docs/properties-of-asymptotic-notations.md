# 渐近符号的性质

> 原文:[https://www . geeksforgeeks . org/properties-of-渐近符号/](https://www.geeksforgeeks.org/properties-of-asymptotic-notations/)

**前提:** [渐近符号](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)
假设 f(n)、g(n)和 h(n)是渐近函数，数学定义为:

1.  如果**f(n)=θ(g(n))**，则存在正常数 c1、c2、n0，使得 **0 ≤ c1.g(n) ≤ f(n) ≤ c2.g(n)** ，对于所有 n ≥ n0
2.  如果 **f(n) = O(g(n))** ，则存在正常数 c，n0，使得 **0 ≤ f(n) ≤ c.g(n)** ，对于所有 n ≥ n0
3.  如果**f(n)=ω(g(n))**，则存在正常数 c，n0，使得 **0 ≤ c.g(n) ≤ f(n)** ，对于所有 n ≥ n0
4.  如果 **f(n) = o(g(n))** ，则存在正常数 c，n0，使得 **0 ≤ f(n) < c.g(n)** ，对于所有 n ≥ n0
5.  如果 **f(n) = ω(g(n))** ，则存在正常数 c，n0，使得 **0 ≤ c.g(n) < f(n)** ，对于所有 n ≥ n0

**属性:**

1.  **Reflexivity:**
    If f(n) is given then

    ```
    f(n) = O(f(n))
    ```

    *例:*
    若 f(n)= n<sup>3</sup>O(n<sup>3</sup>)
    同理，

    ```
    f(n) = Ω(f(n)) 
    f(n) = Θ(f(n)) 
    ```

2.  **Symmetry:**

    ```
    f(n) = Θ(g(n)) if and only if g(n) = Θ(f(n))
    ```

    *例:*
    如果 f(n) = n <sup>2</sup> 和 g(n) = n <sup>2</sup> 那么 f(n)=θ(n<sup>2</sup>和 g(n)=θ(n<sup>2</sup>)
    ***证明:***

    *   ***必要部分:***
        f(n)=θ(g(n))【g(n)=θ(f(n))
        根据θ的定义，存在正常数 c1，c2，不存在 c1.g(n) ≤ f(n) ≤ c2.g(n)对于所有 n≥no
        g(n)≤(1/C1)。f(n)和 g(n) ≥ (1/c2)。f(n)
        (1/C2)。f(n) ≤ g(n) ≤ (1/c1)。f(n)
        由于 c1 和 c2 是正常数，1/c1 和 1/c2 定义得很好。因此，根据θ的定义，g(n)=θ(f(n))
    *   ***充分性部分:***
        g(n)=θ(f(n))【f(n)=θ(g(n))
        根据θ的定义，存在正常数 c1、c2，不存在 c1.f(n) ≤ g(n) ≤ c2.f(n)对于所有 n≥no
        f(n)≤(1/C1)。g(n)和 f(n) ≥ (1/c2)。g(n)
        (1/C2)。g(n) ≤ f(n) ≤ (1/c1)。g(n)
        根据θ(θ)的定义，f(n)=θ(g(n))
3.  **Transistivity:**

    ```
    f(n) = O(g(n)) and g(n) = O(h(n)) ⇒ f(n) = O(h(n))
    ```

    *例:*
    如果 f(n) = n，g(n) = n <sup>2</sup> 和 h(n)= n<sup>3</sup>
    n 是 O(n <sup>2</sup> )而 n <sup>2</sup> 是 O(n <sup>3</sup> )那么 n 就是 O(n <sup>3</sup> )
    ***证明:***
    否使得所有 n ≥ no 的 f(n)≤c . g(n)
    f(n)≤C1 . g(n)
    g(n)≤C2 . h(n)
    f(n)≤C1 . c2h(n)
    f(n)≤c . h(n)，其中，c = c1.c2 根据定义，f(n) = O(h(n))
    同样，

    ```
    f(n) = Θ(g(n)) and g(n) = Θ(h(n)) ⇒ f(n) = Θ(h(n))
    f(n) = Ω(g(n)) and g(n) = Ω(h(n)) ⇒ f(n) = Ω(h(n))
    f(n) = o(g(n)) and g(n) = o(h(n)) ⇒ f(n) = o(h(n))
    f(n) = ω(g(n)) and g(n) = ω(h(n)) ⇒ f(n) = ω(h(n))
    ```

4.  **Transpose Symmetry:**

    ```
    f(n) = O(g(n)) if and only if g(n) = Ω(f(n))
    ```

    *例:*
    若 f(n) = n 且 g(n) = n <sup>2</sup> 则 n 为 O(n <sup>2</sup> )且 n <sup>2</sup> 为ω(n)
    ***证明:***

    *   ***必要部分:***
        f(n)= O(g(n))
        g(n)=ω(f(n)】根据 Big-Oh (O)的定义 f(n) ≤ c.g(n)对于某些正常数 c g(n)≥(1/c)。f(n)
        根据ω(ω)的定义，g(n)=ω(f(n))
    *   ***充分部分:***
        g(n)=ω(f(n))= O(g(n))
        根据ω(ω)的定义，对于某些正常数 c g(n)≥c . f(n)f(n)≤(1/c)。g(n)
        根据大-Oh(O)的定义，f(n) = O(g(n))

    同样的，

    ```
    f(n) = o(g(n)) if and only if g(n) = ω(f(n)) 
    ```

5.  因为这些性质适用于渐近表示法，所以可以在函数 f(n)和 g(n)与两个实数 a 和 b 之间进行类比。
    *   *g(n) = O(f(n))类似于 a ≤ b*
    *   *g(n)=ω(f(n))类似于 a ≥ b*
    *   *g(n)=θ(f(n))类似于 a = b*
    *   *g(n) = o(f(n))类似于 a < b*
    *   *g(n) = ω(f(n))类似于 a > b*
6.  **Observations:**

    ```
    *max(f(n), g(n)) = Θ(f(n) + g(n))* 
    ```

    ***证明:***
    不失一般性，假设 f(n) ≤ g(n)，max(f(n)，g(n)) = g(n)
    考虑，g(n) ≤ max(f(n)，g(n))≤g(n)
    g(n)≤max(f(n)，g(n))≤f(n)+g(n)
    g(n)/2+g(n)/2≤max(f(n)

7.  ```
    *O(f(n)) + O(g(n)) = O(max(f(n), g(n)))*
    ```

    ***证明:***
    不失一般性，假设 f(n)≤g(n)
    O(f(n))+O(g(n))= C1 . f(n)+C2 . g(n)
    从我们所假设的可以写出
    O(f(n))+O(g(n))≤C1 . g(n)+C2 . g(n)
    ≤(C1+C2)g(n)
    ≤c。

**注:**

1.  如果***lim<sub>n→∞</sub>f(n)/g(n)= c***，c ∈ R+则***f(n)=θ(g(n)】***
2.  如果***lim<sub>n→∞</sub>f(n)/g(n)≤c***，c ∈ R (c 可以为 0)那么 ***f(n) = O(g(n))***
3.  如果***lim<sub>n→∞</sub>f(n)/g(n)= 0***，那么 ***f(n) = O(g(n))*** 和 ***g(n) = O(f(n))***
4.  如果***lim<sub>n→∞</sub>f(n)/g(n)≥c***，c ∈ R (c 可以是∨)那么***f(n)=ω(g(n)】***
5.  如果***lim<sub>n→∞</sub>f(n)/g(n)=∑***，那么***f(n)=ω(g(n))***和***g(n)=ω(f(n))***