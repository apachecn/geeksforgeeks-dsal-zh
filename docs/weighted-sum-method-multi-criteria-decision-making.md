# 加权求和法-多准则决策

> 原文:[https://www . geesforgeks . org/加权求和-方法-多准则-决策/](https://www.geeksforgeeks.org/weighted-sum-method-multi-criteria-decision-making/)

加权求和法是一种多准则决策方法，其中会有多个方案，我们必须根据多个准则来确定最佳方案。还有其他可用的方法，包括加权乘积法(WPM)、按理想解相似性排序的偏好技术(TOPSIS)、VIKOR、MOORA、GTMA 等。让我们通过一个例子来理解加权求和法的工作原理。

考虑一个案例，我们必须从 5 个参加面试的候选人中选出最好的候选人。表 1 包括 5 名学生的详细情况，其中包括他们的工资总额、他们每月期望的工资、他们在技术考试中的分数以及他们在能力倾向测试中取得的成绩。

**表 1:样本数据集**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| 学生 1 | nine | Twelve thousand | seventy-two | B1 |
| 学生 2 | Seven point six | Eight thousand five hundred | sixty-eight | B1 |
| 学生 3 | Eight point two | Nine thousand five hundred | Sixty-three | B2 |
| 学生 4 | Eight point five | ten thousand | Seventy | 主动脉第二声 |
| 学生 5 | Nine point three | Fourteen thousand | seventy-two | 主动脉第二声 |

考虑面试小组假设的权重如下:
CGPA = 30%，期望津贴= 20%，技术考试分数= 25%，能力倾向测试等级= 25%

**表 2:各属性的权重**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |
| 学生 1 | nine | Twelve thousand | seventy-two | B1 |
| 学生 2 | Seven point six | Eight thousand five hundred | sixty-eight | B1 |
| 学生 3 | Eight point two | Nine thousand five hundred | Sixty-three | B2 |
| 学生 4 | Eight point five | ten thousand | Seventy | 主动脉第二声 |
| 学生 5 | Nine point three | Fourteen thousand | seventy-two | 主动脉第二声 |

有益属性是一个人渴望最大价值的属性。在这里，CGPA、技术考试分数和能力倾向测试分数是有益的属性，因为公司希望学生拥有更多这些属性。
非有益属性是需要最小值的属性。在这种情况下，期望的津贴是一个非有益的属性。公司提高了那些愿意以低工资多工作的人的工资。

现在我们用加权求和法看看公司要选哪个学生。
为此，我们必须对表 2 中的值进行归一化。

1.  对于有益属性，![X=x/xmax](img/c09cb5a0403f4991d7e3d8fb9c53a44b.png "Rendered by QuickLaTeX.com")
2.  对于非有益属性，![X=xmin/x](img/2f6bba2045a8cbe488510f14333af928.png "Rendered by QuickLaTeX.com")

**表 3:确定有益属性的最大值和非有益属性的最小值**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |
| 学生 1 | nine | Twelve thousand | **72(最大值)** | B1 |
| 学生 2 | Seven point six | **8500(分钟)** | sixty-eight | B1 |
| 学生 3 | Eight point two | Nine thousand five hundred | Sixty-three | B2 |
| 学生 4 | Eight point five | ten thousand | Seventy | **A2(最大值)** |
| 学生 5 | **9.3(最大值)** | Fourteen thousand | seventy-two | 主动脉第二声 |

等级体系
A1–5
A2–4
B1–3
B2–2
C1–1
**我们将考虑以下几点表 4:更新能力倾向测验等级**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |
| 学生 1 | nine | Twelve thousand | **72(最大值)** | three |
| 学生 2 | Seven point six | **8500(分钟)** | sixty-eight | three |
| 学生 3 | Eight point two | Nine thousand five hundred | Sixty-three | Two |
| 学生 4 | Eight point five | ten thousand | Seventy | **4(最大值)** |
| 学生 5 | **9.3(最大值)** | Fourteen thousand | seventy-two | four |

根据有益属性和非有益属性，规范化相应属性的值。
**表 5:正常化**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |
| 学生 1 | 9/9.3 | 8500/12000 | 72/72 | 3/4 |
| 学生 2 | 7.6/9.3 | 8500/8500 | 68/72 | 3/4 |
| 学生 3 | 8.2/9.3 | 8500/9500 | 63/72 | 2/4 |
| 学生 4 | 8.5/9.3 | 8500/10000 | 70/72 | 4/4 |
| 学生 5 | 9.3/9.3 | 8500/14000 | 72/72 | 4/4 |

**表 6:权重归一化决策矩阵**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |
| 学生 1 | 0.9677 | 0.7083 | one | Zero point seven five |
| 学生 2 | 0.8172 | one | 0.9444 | Zero point seven five |
| 学生 3 | 0.8817 | 0.8947 | Zero point eight seven five | Zero point five |
| 学生 4 | 0.9134 | Zero point eight five | 0.9722 | one |
| 学生 5 | one | 0.6071 | one | one |

**表 7:将每个参数乘以各自的权重**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |
| 学生 1 | 0.9677 × 0.3 | 0.7083 × 0.2 | 1 × 0.25 | 0.75 × 0.25 |
| 学生 2 | 0.8172 × 0.3 | 1 × 0.2 | 0.9444 × 0.25 | 0.75 × 0.25 |
| 学生 3 | 0.8817 × 0.3 | 0.8947 × 0.2 | 0.875 × 0.25 | 0.5 × 0.25 |
| 学生 4 | 0.9134 × 0.3 | 0.85 × 0.2 | 0.9722 × 0.25 | 1 × 0.25 |
| 学生 5 | 1 × 0.3 | 0.6071 × 0.2 | 1 × 0.25 | 1 × 0.25 |

上表简化如下
**表 8:表 7** 的简化版

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 |
| --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |
| 学生 1 | 0.29031 | 0.14166 | Zero point two five | 0.1875 |
| 学生 2 | 0.24516 | Zero point two | 0.2361 | 0.1875 |
| 学生 3 | 0.26451 | 0.17894 | 0.21875 | Zero point one two five |
| 学生 4 | 0.27402 | Zero point one seven | 0.24305 | Zero point two five |
| 学生 5 | Zero point three | 0.12142 | Zero point two five | Zero point two five |

我们必须将每一行中的成分相加，计算出加权和，即为成绩分数，并给学生赋予优先级
**表 9:按成绩分数计算的学生等级排名**

<figure class="table">

| 属性 | 断续器 | 预期津贴 | 技术考试分数 | 能力倾向测验等级 | 绩效评分 | 军阶 |
| --- | --- | --- | --- | --- | --- | --- |
| **重量** | **0.3** | **0.2** | **0.25** | **0.25** |   |   |
| 学生 1 | 0.29031 | 0.14166 | Zero point two five | 0.1875 | 0.86947 | three |
| 学生 2 | 0.24516 | Zero point two | 0.2361 | 0.1875 | 0.86876 | four |
| 学生 3 | 0.26451 | 0.17894 | 0.21875 | Zero point one two five | 0.7872 | five |
| 学生 4 | 0.27402 | Zero point one seven | 0.24305 | Zero point two five | **0.93707** | **1** |
| 学生 5 | Zero point three | 0.12142 | Zero point two five | Zero point two five | 0.92142 | Two |

**结论:**从加权求和法来看，确定学生 4 是其中的最佳选择。

</figure>

</figure>

</figure>

</figure>

</figure>

</figure>

</figure>

</figure>

</figure>