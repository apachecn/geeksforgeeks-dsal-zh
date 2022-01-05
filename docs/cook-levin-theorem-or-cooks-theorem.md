# 库克-莱文定理或库克定理

> 原文:[https://www . geesforgeks . org/cook-Levin-定理-or-cooks-定理/](https://www.geeksforgeeks.org/cook-levin-theorem-or-cooks-theorem/)

在计算复杂性理论中，库克-莱文定理，也称为库克定理，指出布尔可满足性问题是 NP 完全的。也就是说，它在 NP 中，NP 中的任何问题都可以通过确定性图灵机在多项式时间内简化为布尔可满足性问题。

*斯蒂芬·阿瑟·库克和 L.A .莱文在 1973 年独立证明了**可满足性问题(SAT)** 是 NP 完全的。斯蒂芬·库克(Stephen Cook)在 1971 年发表了一篇题为《定理证明程序的复杂性》的重要论文，他在论文中概述了通过将 NP 完全问题简化为 **SAT** 来获得其证明的方法。他证明了**电路-SAT****3nf-SAT**的问题和 **SAT** 一样难。同样，列昂尼德·列文在当时的苏联独立研究这个问题。 **SAT** 是 NP-complete 的证明，就是在这两位科学家的努力下获得的。后来，卡普把哈密顿圈、顶点覆盖*、*和团等 21 个优化问题简化到 **SAT** 上，证明了这些问题是 NP 完全的。*

*<u>因此，</u>*an*<u>**<u>SAT</u>**<u>是一个重大问题，可以表述如下:</u></u>*

<u>给定一个布尔表达式 **F** 具有 **n** 变量 **x <sub>1</sub> ，x <sub>2</sub> ，…。，x <sub>n</sub> ，**和布尔运算符，有没有可能对变量赋值为真或假，使得二进制表达式 **F** 为真？</u>

<u>这个问题也被称为**公式——SAT**。 **SAT(公式-SAT 或简称 SAT)** 取一个布尔表达式 F，并检查给定的表达式(或公式)是否可满足。如果求值结果为真，则布尔表达式对于某些有效的变量赋值是令人满意的。在讨论 SAT 的细节之前，现在让我们讨论布尔表达式的一些重要术语。</u>

<u>*   **<u>Boolean variable:</u>** A variable, such as **x** , can only have two values, true or false, which is called a Boolean variable.*   **<u>Literally:</u>** A literal can be a logical variable, such as **x** , or a negation of it, that is, **x** or **x** ; **X** is called positive literal, **X** is called negative literal.*   **<u>Clause:</u>** A series of variables **(x <sub>1</sub> , x <sub>2</sub> , ... , x <sub>n</sub> )** can be separated by a logical **or** operator, which is called clause. For example, **(x <sub>1</sub> V x <sub>2</sub> V x <sub>3</sub> )** is a clause of three characters.*   **<u>Expression:</u>** You can use Boolean operators to combine all the preceding clauses into one expression.*   **<u>CNF form:</u>** If the clause set is separated by **and ()** operators, and the words are connected by **or (v)** operators, the expression is CNF form (conjunctive normal form). The following is an example of CNF expression: t88
    *   ***f =(x<sub>【1】</sub>【VX】<sub>【2】</sub>【v】<sub>【3】</sub>【x<sub>【1】</sub>【VX】<sub>3】</sub>***t88</u>

<u>因此， **SAT** 是最棘手的问题之一，因为除了暴力方法之外，没有其他已知的算法。强力算法将是指数时间算法，因为需要尝试可能的赋值来检查给定的布尔表达式是否为真。斯蒂芬·库克和列昂尼德·莱文证明了 **SAT** 是 NP 完全的。</u>

<u>库克向 sat 证明了其他难题的减少。卡普通过使用卡普约简将其简化为 SAT，提供了 21 个重要问题的证明，如哈密顿圈、顶点覆盖和团。</u>

<u>让我们简单介绍一下三种 sat。它们如下:</u>

1.  <u>**<u>Circuit-SAT:</u>** A circuit-SAT can be expressed as follows: Given a Boolean circuit, it is **and** , **or** , **Not** , **N** input, etc. Similarly, the difficulty of these problems lies in the **n** input of the circuit. **2 <sup>n</sup>** Possible outputs should be checked. Therefore, this brute force algorithm is an exponential algorithm, so it is a difficult problem.</u>
2.  <u>**<u>CNF-SAT:</u>** This question is a restrictive question of **SAT** , and the expression here should be conjunctive normal form. If all clauses are connected by Boolean **and** operators, the expression is called conjunction form. As in the case of **SAT** , this is about assigning true values to n variables so that the output of the expression is true **<u>.</u>**</u>
3.  <u>**<u>3-CNF-SAT (3-SAT):</u>** This question is another variant, in which the additional restriction is that the expression is conjunctive normal form, and each clause should contain exactly three words. This problem is also about assigning **n** of true value to **n** variable of Boolean expression, so that the output of the expression is true. Simply put, given an expression in 3-CNF, the 3-SAT problem is to check whether the given expression can be satisfied.</u>

<u>*这些问题可以用来证明一些重要问题的 NP 完全性。*</u>