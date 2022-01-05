# 4 SAT 是 NP 完全的证明

> 原文:[https://www . geesforgeks . org/proof-4-sat-is-NP-complete/](https://www.geeksforgeeks.org/proof-that-4-sat-is-np-complete/)

**<u>4-SAT 问题</u> :** 4-SAT 是 3-SAT 的推广(k-SAT 是 SAT，其中每个子句都有 k 个或更少的文字)。

**<u>问题陈述</u> :** 给定一个由子句组成的合取范式(CNF)中的公式 ***f*** ，问题是识别公式 ***f*** 是否有令人满意的赋值。

**<u>解释</u> :** 问题的一个实例是指定给问题的输入。4-SAT 问题的一个例子是 CNF 公式，任务是检查公式是否有令人满意的赋值。由于一个 [NP-Complete](https://www.geeksforgeeks.org/np-completeness-set-1/) 是一个同时存在于 **NP** 和 **NP-hard** 中的问题，因此证明一个问题是 NP-Complete 的陈述由两部分组成:

> 1.  The problem itself lies in NP class.
> 2.  All other problems in NP class can be reduced to that by polynomial time.
>     (b can be reduced to c by polynomial time and expressed as b ≤ p <sup>c</sup> )

如果仅满足第二个条件，则问题称为 **[NP-Hard](https://www.geeksforgeeks.org/tag/nphard/)** 。

但是不可能把每一个 NP 问题都化为另一个 NP 问题来一直展示它的 NP 完全性。这就是为什么如果我们想证明一个问题是 NP-Complete，我们只需要证明这个问题是 NP 中的问题，并且任何 NP-Complete 问题都可以简化为 NP-Complete，那么我们就完成了，也就是说，如果 B 是 NP-Complete，B ≤ <sup>C</sup> 。对于 NP 中的 C，那么 C 就是 NP-Complete。因此，使用以下两个命题可以验证 **4-SAT 问题**是 NP-完全的:

1.  **<u>4-SAT 问题在 NP 中</u> :**
    如果有任何问题在 NP 中，那么，给定一个‘证书’，它是问题的一个解决方案和问题的一个实例(一个公式 ***f*** ，在这种情况下)，可以验证(检查给定的解决方案是否正确)该证书在多项式时间内。这可以通过以下方式来完成:
    给定属于公式 ***f*** 的变量赋值，该赋值可以在线性时间内验证，如果它满足公式或不满足公式。
2.  **<u>4-SAT 问题是 NP-Hard</u> :**
    为了证明 4-SAT 问题是 NP-Hard，从一个已知的 NP-Hard 问题推导出这个问题的一个约简。推导出一个归约，由此 3-SAT 问题可以归约为 4-SAT 问题。例如，对于 **3-SAT** 公式 ***f*** 中的每一个子句，都应该在公式中添加一个字面 **a** 及其对应的补语 **a'** 。设一个子句 **c** ，这样 **c = u V v' V w**
    要在 4-SAT 中转换它，我们将 **c** 转换为 **c'** ，这样，
    **c ' =(u V V ' V w V a)AND(u V V ' V w V a ')**。
    模拟此转换后，有两个属性保持不变:
    1.  如果 3-SAT 有一个可满足的赋值，也就是说，对于一组特定的文字值，每个子句的计算结果都为真，那么 4-SAT 也将成立，因为每个子句集都是由一个文字和它的补码组成的，它们的值不会有任何区别。
    2.  如果 4-SAT 对于任何一个 **(u V v V w V a)** 和**(u V V V w V a)**都是可满足的，那么 3-SAT 也是可满足的，因为 **a** 和**a‘**是补码，这表明该公式也是可满足的，除了 a。

因此，遵循上述命题，4-SAT 问题为 **NP-Complete** 。