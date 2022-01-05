# 肖尔因子分解算法

> 原文:[https://www . geeksforgeeks . org/shors-因式分解-算法/](https://www.geeksforgeeks.org/shors-factorization-algorithm/)

**<u>肖尔因子分解算法</u> :**

*   肖尔因式分解[算法](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)由彼得·肖尔提出。
*   这表明量子力学允许因子分解在[多项式时间](https://www.geeksforgeeks.org/polynomial-time-approximation-scheme/)内进行，而不是使用经典算法后达到的指数时间。
*   这可能会对[数据安全](https://www.geeksforgeeks.org/data-security/)领域产生巨大影响，这是一个基于[大数质因数分解](https://www.geeksforgeeks.org/prime-factors-big-number/)的概念。
*   许多整数乘法的多项式时间算法(例如[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/))确实存在，但是不存在因式分解的多项式时间算法。
*   于是，绍尔想出了一个算法，即绍尔因式分解算法，一个分解 **L** 位的非质数 **N** 的算法。
*   **量子算法**比经典算法好得多，因为它们基于量子傅里叶变换。
*   经典计算机上的运行时间是**O【exp(L<sup>1/3</sup>(log L)<sup>2/3</sup>)】**，而量子计算机上的运行时间是 **O(L <sup>3</sup> )** 。
*   所以，肖尔算法在原理上表明，量子计算机能够在多项式时间内分解非常大的数字。

**<u>肖尔的算法依赖于</u> :**

*   [模运算](https://www.geeksforgeeks.org/modular-arithmetic/)
*   [量子平行度](https://www.geeksforgeeks.org/introduction-to-parallel-computing/)
*   [量子傅里叶变换](https://www.geeksforgeeks.org/fast-fourier-transformation-poynomial-multiplication/)

**<u>算法代表</u> :**

给定一个奇数[合成数](https://www.geeksforgeeks.org/composite-number/) **N** ，求一个整数 **d** ，严格在 **1** 和 **N** 之间，除以 **N** 。

绍尔算法由以下两部分组成:

*   分解问题转化为求周期问题。这部分可以用经典的手段来实现。
*   利用**量子傅里叶变换**求周期或量子周期，负责量子加速，利用量子并行性。

在绍尔算法中，**输入**为非质数 **N** ，**输出**为 **N** 的非平凡因子

> *INPUT(N)*—>***SHOR 算法***—>*OUTPUT(N 的非平凡因子)*

**算法:**它包含几个步骤，仅在第 2 步需要使用量子计算机。

1.  选择任意一个随机数，比如说 **r** ，这样 **r < N** 这样它们就是彼此的素数。
2.  用量子计算机确定函数 **f <sub>r，N</sub>(x)= r<sup>x</sup>**[**mod**](https://www.geeksforgeeks.org/modular-arithmetic/)**N**的未知周期 **p** 。
3.  如果 **p** 是奇数，则返回**步骤 1** 。否则进入下一步。
4.  由于 **p** 是偶数，因此**(r<sup>p/2</sup>–1)(r<sup>p/2</sup>+1)= r<sup>p</sup>–1 = 0 mod N**。
5.  现在，如果 **r <sup>p/2</sup> + 1 = 0 mod N** 的值，回到**步骤 1** 。
6.  如果 **r <sup>p/2</sup> 的值+ 1！= 0 mod N** ，否则进入下一步。
7.  计算 **d = gcd(r <sup>p/2</sup> -1，N)** 。
8.  需要的答案是“ **d** ”。

**<u>经典部分(</u>寻序题):**
这是寻序题的经典部分。假设 **x** 和 **N** ，使得 **x < N** 和 **gcd(x，N) = 1** 。 **x** 的顺序是最小正整数 y，这样 **x <sup>y</sup> = 1(mod N)** 。

1.  随机选择一个数字 **n** ，使得 **n < N** 。计算 **gcd(n，N)** 。
2.  这可以使用欧几里德算法来完成。
3.  如果 **gcd(n，N)！= 1** ，那么有一个非平凡的 N 因子，如果**(x+p)= N<sup>x+p</sup>mod N = N<sup>x</sup>mod N = f(x)**。
4.  如果 r 为奇数，则返回**步骤 1** 。
5.  如果 **n <sup>p/2</sup> = -1(mod N)** ，则返回**步骤 1** 。
6.  **gcd(n <sup>p/2</sup> +/- 1，N)** 是 **N** 的一个不可忽视的因素。

**<u>量子部分:</u>**

> 这是量子顺序寻找部分。选择 2 的幂，然后
> **Q = 2L，这样 N<sup>2</sup>T7 = Q<= 2N<sup>2</sup>T6】**

并考虑 f = {0，1，2，…，Q-1}

其中，**f(y)= 1/(Q)<sup>1/2</sup>∑<sub>x = 0</sub><sup>Q-1</sup>I f(x)I w<sup>xy</sup>T9】和 **w = exp(2π i/Q)** ，即 Q <sup>th</sup> 的单位根。**

*   让我们用一个例子来执行 **Shor 算法**:对一个奇数 N 进行因子化(让 N = 17)。
*   选择一个整数 Q，使得**N<sup>2</sup>T6 = Q≤2N<sup>2</sup>T5(让 Q = 324)。**
*   然后，随机选择任意整数 N，使得 [gcd](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) (n，N)=1，(让我们选择整数 n=7)。
*   然后创建两个量子寄存器(这些寄存器应该纠缠在一起，以便输入寄存器的崩溃对应于输出寄存器的崩溃)
    *   **输入寄存器:**必须包含足够多的量子位来表示 Q-1 这样大的数。(即最多 323 个，因此我们需要 9 个量子位)。
    *   **输出寄存器:**必须包含足够多的量子位来表示与**(N–1)**一样大的数字。(即最多 16 个，因此我们需要 4 个量子位)。

**代码:**

## 计算机编程语言

```
from qiskit import IBMQ
from qiskit.aqua import QuantumInstance
from qiskit.aqua.algorithms import Shor

# Enter your API token here
IBMQ.enable_account('ENTER API TOKEN HERE') 
provider = IBMQ.get_provider(hub='ibm-q')

# Specifies the quantum device
backend = provider.get_backend('ibmq_qasm_simulator')

print('\n Shors Algorithm')
print('--------------------')
print('\nExecuting...\n')

# Function to run Shor's algorithm
# where 21 is the integer to be factored
factors = Shor(35)

result_dict = factors.run(QuantumInstance(
    backend, shots=1, skip_qobj_validation=False))

 # Get factors from results
result = result_dict['factors']

print(result)
print('\nPress any key to close')
input()
```

**输出:**

```
Shors Algorithm
- - - - - - - - - - - - -
Executing...
[[5,7]]
Press any key to close
```

上面代码的输出显示了 N=35 时的系数 5 和 7。