# 测试

> 原文:[https://www.geeksforgeeks.org/t-test/](https://www.geeksforgeeks.org/t-test/)

**先决条件–**[假设检验](https://www.geeksforgeeks.org/understanding-hypothesis-testing/)、 [p 值](https://www.geeksforgeeks.org/p-value-in-machine-learning/)

t 检验是一种推理统计，用于确定两组平均值之间是否存在显著差异，这可能与某些特征有关。

<center>

![t=\frac{\text { variance between groups }}{\text { variance within groups }}](img/468671c1d4d4dd02d87658ed85e3ec24.png "Rendered by QuickLaTeX.com")

</center>

If t-value is large => the two groups belong to different groups. 
If t-value is small => the two groups belong to same group.

**涉及的术语**

*   **自由度(df)–**它告诉我们用于计算 2 个样本组之间估计值的自变量数量。**【等式-2】**

<center>

![d f=\sum n_{s}-1](img/90bc2da1577faa65d03832e4425abec3.png "Rendered by QuickLaTeX.com")

</center>

```
where, 
df = degree of freedom
n<sub>S =</sub> size of the sample S
```

> 假设我们有两个样本 A 和 b。df 的计算公式如下
> 
> **df =(n<sub>A</sub>-1)+(n<sub>B</sub>-1)**

*   **显著性水平(α)–**是当零假设为真时，拒绝零假设的概率。简单来说，它告诉我们说两组人之间存在差异所涉及的风险百分比，而实际上并不存在。

有三种类型的 t 检验，它们被分为依赖型和独立型 t 检验。

1.  **独立样本 t 检验:**比较两组的平均值。
2.  **配对样本 t 检验:**比较同一组在不同时间(比如相隔一年)的平均值。
3.  **一个样本 t 检验测试:**单个组相对于已知平均值的平均值。

**1。独立样本 t 检验**

独立样本 t 检验，通常称为不成对样本 t 检验，用于找出两组之间发现的差异实际上是显著的还是只是随机出现的。

**我们可以用这个当:**

*   总体平均值或标准偏差未知。(人口信息未知)
*   这两个样本是分开的/独立的。男孩和女孩(两者相互独立)

**使用的公式:**

<center>![t=\frac{\mu_{A}-\mu_{B}}{\sqrt{\left[\frac{1}{n_{A}}+\frac{1}{n_{B}}\right] *\left[\left(\sum A^{2}-\frac{\left(\sum A\right)^{2}}{n_{A}}\right)+\left(\sum B^{2}-\frac{\left(\sum B\right)^{2}}{n_{B}}\right)\right] *\left[\frac{1}{d f}\right]}}](img/f4fd38c75cb189802148812fdb57864f.png "Rendered by QuickLaTeX.com")</center>

```
where,
t = t-value 
A = Sample of A
B = Sample of B
μ<sub>A =</sub> Mean of sample A
μ<sub>B =</sub> Mean of sample B
n<sub>A =</sub> samele size of A  
n<sub>B =</sub> sample size of B 
df = degree of freedom
```

**涉及的步骤**

```
Step 1 - Find the sum of all values in each sample. 
Step 2 - Square the sum values found in step 1.
Step 3 - Find the sum of square of individual values in each sample.
Step 4 - Calculate the mean of each sample.
Step 5 - Find the degree of freedom (df) using Eq-2.
Step 6 - Insert all the values found in Steps 1-4 into Eq-3 and find the calculated t-value.
Step 7 - Use the values of df and α (take α = 0.05 if not given) in the two-tails t-table **(Click here)** to 
      find the table value of t.
Step 8 - Compare values of t found in Step-6 and Step-7.
```

**解释结果**

```
If t<sub>cal > ttable</sub>=> p < (α=0.05) => significant difference between two groups found.
If t<sub>cal < ttable</sub> => p > (α=0.05) => no significant difference between two groups.
```

**例题(循序渐进)**

假设给出了两个独立的样本数据 A 和 B，取值如下。我们必须对这些数据进行独立样本 t 检验。

<figure class="table">

| 

样品甲

 | 

样本 B

 |
| --- | --- |
| one | one |
| Two | Two |
| four | Two |
| four | three |
| five | three |
| five | four |
| six | five |
| seven | six |
| eight | seven |
| eight | seven |

```
Step 1 - 
∑A = 1 + 2 + 4 + 4 + 5 + 5 + 6 + 7 + 8 + 8 = 50
∑B = 1 + 2 + 2 + 3 + 3 + 4 + 5 + 6 + 7 + 7 = 40
```

```
Step 2 -
(∑A)<sup>2 =</sup> (50)2 = 2500
(∑B)<sup>2 =</sup>    (40)2 = 1600
```

```
Step 3 -
∑A<sup>2 =</sup> 12 + 22 + 42 + 42 + 52 + 52 + 62 + 72 + 82 + 82 = 300
∑B<sup>2 =</sup> 12 + 22 + 22 + 32 + 32 + 42 + 52 + 62 + 72 + 72 = 202
```

```
Step 4 -
n = 10
μ<sub>A = (∑A / n) =</sub> 50/10 = 5
μ<sub>B = (∑B / n) =</sub> 40/10 = 4
```

```
Step 5 - 
df = (nA - 1) + (nB - 1) = (10-1) + (10-1) = 18 [using Eq-2]
```

```
Step 6 - Putting values found in Eq-3 to find the calculated value of t.
     we get, t<sub>cal = 0.99</sub>
```

```
Step 7 - Let value of α = 0.05 and df = 18\. Looking up the two-tailed t-table. 
     (See table below or refer link above)
     we get, t<sub>table = 2.10</sub>
```

<figure class="table">

| (df)/(α) | Zero point two | Zero point one | Zero point zero five | 。。 |
| --- | --- | --- | --- | --- |
| 

∞

 | One point two eight two | One point six four five | One point nine six | 。。 |
| 

one

 | Three point zero seven eight | Six point three one four | Twelve point seven zero six | 。。 |
| 

Two

 | One point eight eight six | Two point nine two | Four point three zero three | 。。 |
| 

：

 | ： | ： | ： | 。。 |
| 

eight

 | One point three nine seven | One point eight six | Two point three zero six | 。。 |
| 

nine

 | One point three eight three | One point eight three three | Two point two six two | 。。 |
| 

：

 | ： | ： | ：

 | 。。 |
| 

Eighteen

 |  1.330 | One point seven three four | Two point one zero one | 。。 |
| 

Nineteen

 |  1.328 |  1.729 |  2.093 | 。。 |
| 

Twenty

 |  1.325  | 1.725  | Two point zero eight six | 。。 |
| 

：

 | ： | ： | ： | 。。 |

</figure>

```
Step 8 - 
0.99 < 2.10 (t<sub>cal < ttable</sub> by 1.11)
=> no significant difference found between two groups.
```

**2。配对样本 t 检验**

配对样本 t 检验，通常称为相依样本 t 检验，用于找出两个样本的平均值之差是否为 0。测试是在相关样本上进行的，通常集中在特定的人群或事物上。在这种情况下，每个实体被测量两次，产生一对观测值。

**我们可以用这个当:**

*   给出了两个相似的(孪生的)样品。[例如，英语和数学(两科)成绩]
*   因变量(数据)是连续的。
*   这些观察是相互独立的。
*   因变量近似正态分布。

**使用的配方**

<center>![t=\frac{\left(\sum D\right) / N}{\sqrt{\frac{\sum D^{2}-\left(\frac{(\Sigma D)^{2}}{N}\right)}{(N)(N-1)}}}](img/2d14c6cff64a81154d3fc76626402a2f.png "Rendered by QuickLaTeX.com")</center>

```
where, 
t = t-value
D = difference between the two samples (A-B)
N = sample size (same as n)
```

**涉及的步骤**

```
Step 1 - Find the sum of difference of each two samples in data. [∑D = ∑(A-B)]
Step 2 - Find the sum of square of each D found in Step 1\. [(∑D<sup>2)</sup>]
Step 3 - Find the square of summation of D. [(∑D)<sup>2</sup>]
Step 4 - Put the values found from Steps 1-3 in Eq-4 and find the t-value.
Step 5 - Find the degree of freedom (df) using Eq-2.
```

> **注:**这里，df 是对数据的整体计算，而不是对每个单独的样本集。这是因为两个样品 A 和 B 是孪生像。(类似)
> 
> **所以，df =∑(N<sub>S</sub>–1)= N-1**

```
Step 6 - Use the values of df and α (take α = 0.05 if not given) in the two-tails t-table (Click here) to 
      find the table value of t. 
Step 7 - Compare values of t found in Step-4 and Step-6.
```

**结果解读**

与独立样本 t 检验相同。

**例题(循序渐进)**

考虑下面的例子。数学和科学技术科目的分数(共 25 分)是从 10 名学生中抽取的。我们必须对这些数据进行配对样本 t 检验。

<figure class="table">

| 

学生号。

 | 

数学

 | 

超音速运输机

 | 

第一步
(四)

 | 

步骤 2(【D1】2

 |
| --- | --- | --- | --- | --- |
| one | four | Fifteen | -11 | One hundred and twenty-one |
| Two | four | Sixteen | -12 | One hundred and forty-four |
| three | seven | Fourteen | -7 | forty-nine |
| four | Sixteen | Fourteen | Two | four |
| five | Twenty | Twenty-two | -2 | four |
| six | Eleven | Twenty-two | -11 | One hundred and twenty-one |
| seven | Thirteen | Twenty-three | -10 | One hundred |
| eight | nine | Eighteen | -9 | Eighty-one |
| nine | Eleven | Eighteen | -7 | forty-nine |
| Ten | Fifteen | Nineteen | -4 | Sixteen |
| 总和– |   |   | **(∑d)= = 71** | **d<sup>2</sup>= 689** |

```
Step 1 and Step 2 - as shown in table above.
```

```
Step 3 - (∑D)<sup>2</sup> = (71)2 = 5041
```

```
Step 4 - Putting values in Eq-4, we get
     t<sub>cal = -4.96</sub>
```

```
Step 5 - df = n -1 = 10 - 1 = 9
```

```
Step 6 - Using df = 9 and α = 0.05 in table. We get,
     t<sub>table = 2.26</sub>
```

```
Step 7 - -4.96 < 2.26 (tcal < ttable by 7.22)
=> no significant difference found between two groups.
```

**3。一个样本 t 检验**

一个样本 t 检验是一种广泛使用的 t 检验，用于将数据的样本平均值与特定的给定值进行比较。用于比较样本平均值与真实/总体平均值。

**我们可以用这个当:**

样本量很小。(30 岁以下)数据是随机收集的。数据近似正态分布。

**使用的公式:**

<center>![t=\frac{\bar{x}-\mu}{\frac{\sigma}{\sqrt{n}}}](img/125be6598a5744f3a629c4cc4890783c.png "Rendered by QuickLaTeX.com")</center>

```
where,
t = t-value
x_bar = sample mean
μ = true/population mean
σ = standard deviation
n = sample size
```

**涉及的步骤**

```
Step 1 - Define the null (h<sub>0)</sub> and alternative (h<sub>1)</sub> hypothesis.
Step 2 - Calculate sample mean. (if not given) 
     [population mean, standard deviation, n is given]
Step 3 - Put the values found in Step 1 into Eq-5 and calculate t-value. (t<sub>cal)</sub>
Step 4 - Calculate degree of freedom (df). (same as done in paired sample t-test)
Step 5 - Take α = 0.05 if not given. Use the value of df and α and find t<sub>table</sub>from one tailed t-table. (Click here)
Step 6 - Compare values of t found in Step-3 and Step-5.
```

**结果解读**

与独立样本 t 检验相同。

**例题(循序渐进)**

考虑下面的例子。在将 25 名肥胖者纳入营养营之前，对他们的体重进行了测量。在开始营地之前，发现人口平均体重为 45 公斤。完成营地后，对于同样的 25 人，样本平均值为 75，标准偏差为 25。健身营成功了吗？

```
Step 1 - h0 -> μ = 45 (sample mean is true mean)
      h1 -> μ ≠ 45 (sample mean is not true mean)
```

```
Step 2 - Given,
      x_bar = 75
      μ = 45
      σ = 25
      n = 25
```

```
Step 3 - Putting the values from Step 2 in Eq-5. we get,
     t<sub>cal = 6</sub>
```

```
Step 4 - df = n - 1 = 24
```

```
Step 5 - Using df = 24 and α = 0.05 in table. We get,
     t<sub>table = 1.711</sub>
```

```
Step 6 - 6 > 1.711 (tcal > ttable)
=> significant difference found between two groups.
=> the nutrition camp significantly impacted the weights and it was a success. 
```

专家们在医院的研究领域中广泛使用上述类型的 t 检验，以获得关于给予他们的关于各种药物和药物对人群的影响的医疗数据的重要信息，并帮助他们得出关于这些信息的重要推论。然而，这个人有责任确保哪一个 t 检验会产生最好的结果，并且那个 t 检验的所有假设都得到遵守。如有任何疑问/疑问，请在下面评论。

</figure>

</figure>