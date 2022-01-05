# 图基-克莱默后分析测试

> 原文:[https://www . geeksforgeeks . org/tukey-Kramer-事后分析测试/](https://www.geeksforgeeks.org/tukey-kramer-test-for-post-hoc-analysis/)

如果在方差分析检验中，我们得出结论，我们必须拒绝我们的零假设(H <sub>0</sub> )，然后我们知道一些治疗或因子水平的平均值是不同的，我们希望找到它们，然后我们用图基检验进行事后分析，以找到哪一对是不同的。这种方法是多重比较法。

**约:**

*   用来讲述人口意味着有显著的差异。
*   用方差分析方法剔除 H <sub>0</sub> 时完成。
*   在这种方法中，我们需要进行成对比较。
*   使用临界范围来比较绝对平均值差异。

**临界范围公式:**

<center>

![\text { Critical Range }=Q_{U} \sqrt{\frac{\mathrm{MSW}}{2}\left(\frac{1}{\mathrm{n}_{\mathrm{j}}}+\frac{1}{\mathrm{n}_{\mathrm{j}^{\prime}}}\right)}](img/0eb275b6870ab6ea297d99dd38e3df34.png "Rendered by QuickLaTeX.com")

**步骤:**

1.  计算所有可能对的绝对平均差异。
2.  从标准表中找到*Q<sub>u</sub>T3】值。*
3.  根据上面提到的公式计算临界范围。
4.  与步骤 1 中获得的结果进行比较。

**示例:**

一家水果公司想知道他们果汁的完美果肉量，为此他们进行了一项调查，并要求消费者根据味道从 0 到 25 进行评分。注意味道不取决于果肉的数量，它取决于人造果肉。

以下是推断的结果:

<center>

<figure class="table">

| 纸浆(%) | 观察 | 总数 | 平均的 |
| one | Two | three | four | five | six |
| five | seven | eight | Fifteen | Eleven | nine | Ten | Sixty | Ten |
| Ten | Twelve | Seventeen | Thirteen | Eighteen | Nineteen | Fifteen | Ninety-four | Fifteen point six seven |
| Fifteen | Fourteen | Eighteen | Nineteen | Seventeen | Sixteen | Eighteen | One hundred and two | Seventeen |
| Twenty | Nineteen | Twenty-five | Twenty-two | Twenty-three | Eighteen | Twenty | One hundred and twenty-seven | Twenty-one point one seven |
|   |   |   |   |   |   |   | Three hundred and eighty-three | Fifteen point nine six |

</figure>

</center>

**第 1 步:**计算绝对平均差异:

![\begin{aligned} &\left|\overline{\mathrm{x}}_{1}-\overline{\mathrm{x}}_{2}\right|=|10.00-15.67|=5.67 \\ &\left|\overline{\mathrm{x}}_{1}-\overline{\mathrm{x}}_{3}\right|=|10.00-17.00|=7 \\ &\left|\overline{\mathrm{x}}_{2}-\overline{\mathrm{x}}_{3}\right|=|15.67-17.00|=1.33 \\ &\left|\overline{\mathrm{x}}_{1}-\overline{\mathrm{x}}_{4}\right|=|10.00-21.17|=11.17 \\ &\left|\overline{\mathrm{x}}_{2}-\overline{\mathrm{x}}_{4}\right|=|15.67-21.17|=5.5 \\ &\left|\overline{\mathrm{x}}_{3}-\overline{\mathrm{x}}_{4}\right|=|17.00-21.17|=4.17 \end{aligned}](img/a8e59bca7a88ddaadc072bfbc5d27eec.png "Rendered by QuickLaTeX.com")

**第二步:**

这里，*C = 4*N-C = 24–4 = 20

设α = 0.05

来自标准 Q 表 Q <sub>u</sub> = 3.96

**第三步:**把上面得到的值放进去，我们得到临界范围= 4.124

**步骤 4:** 将其与步骤 1 中的每个结果进行比较，我们得到所有的绝对平均值差都大于临界范围。除了(*X<sub>2</sub>T5、*X<sub>3</sub>T9)。因此，除了在 5%显著性水平上的 10%浓度和 15%浓度之外，我们看到每对平均值之间有显著差异。**

</center>