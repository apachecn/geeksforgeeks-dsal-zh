# 因子分析简介

> 原文:[https://www . geesforgeks . org/factor-analytics 简介/](https://www.geeksforgeeks.org/introduction-to-factor-analytics/)

因子分析是一种特殊的技术，将大量的变量减少到几个因子中，称为数据的因子分解，管理哪些数据将出现在表中属于因子分析。这完全是一种统计方法，也用于根据称为*因子*的潜在较低数量的未观察变量来描述观察变量和相关变量之间的波动。

因子分析技术从所有变量中提取最大公共方差，并将它们放入一个公共得分中。这是一种用于训练机器学习模型的理论，因此它与数据挖掘密切相关。因子分析技术背后的信念是，获得的关于观察变量之间相互依赖关系的信息可以在以后用于减少数据集中的变量集。

对于复杂的概念，如社会地位、经济地位、饮食模式、心理量表、生物学、心理测量学、人格理论、市场营销、产品管理、运筹学、金融学等，因子分析是检验可变关系的非常有效的工具。它可以帮助研究人员调查那些不容易用简单快捷得多的方式直接测量的概念，将大量的变量转化为几个容易解释的基本因素。

**因子分析类型:**

1.  **Exploratory factor analysis (EFA) :**
    It is used to identify composite inter-relationships among items and group items that are the part of uniting concepts. The Analyst can’t make any prior assumptions about the relationships among factors. It is also used to find the fundamental structure of a huge set of variables. It lessens the large data to a much smaller set of summary variables. It is almost similar to the Confirmatory Factor Analysis(CFA).

    相似之处在于:

    *   评估金额的内部可靠性。
    *   检查由项目集表示的因素。他们认为这些因素并不相关。
    *   调查每个项目的等级。

    不过，一些常见的差异，大部分都是关注因子是如何使用的。基本上，EFA 是一种数据驱动的方法，它允许所有项目加载所有因子，而在 CFA 中，您需要指定需要加载哪些因子。如果你不知道可能存在哪些共同因素，全民教育确实是一个不错的选择。全民教育能够为你的数据生成大量可能的模型，如果研究者必须指定因素，这是不可能的。如果你对模型的实际外观有一点概念，然后你想测试你对数据结构的假设，在这种情况下，CFA 是一个更好的方法。

2.  **Confirmatory factor analysis (CFA) :**
    It is a more complex(composite) approach that tests the theory that the items are associated with specific factors. Confirmatory Factor Analysis uses a properly structured equation model to test a measurement model whereby loading on the factors allows for the evaluation of relationships between observed variables and unobserved variables.
    As we know, the Structural equation modelling approaches can board measurement error easily, and these are much less restrictive than least-squares estimation thus provide more exposure to accommodate errors. Hypothesized models are tested against actual data, and the analysis would demonstrate loadings of observed variables on the latent variables (factors), as well as the correlation between the latent variables.
    Confirmatory Factor Analysis allows an analyst and researcher to figure out if a relationship between a set of observed variables (also known as manifest variables) and their underlying constructs exists. It is similar to the Exploratory Factor Analysis.

    两者的主要区别是:

    *   简单用探索性因子分析来探索模式。
    *   使用验证性因素分析进行假设检验。

    验证性因素分析提供了表示数据集所需的因素数量的标准质量信息。使用验证性因素分析，您可以定义所需因素的总数。例如，验证性因素分析能够回答像*这样的问题，我的千问调查是否能够准确测量一个特定的因素*。尽管它在技术上适用于任何一种学科，但它通常用于社会科学。

3.  **Multiple Factor Analysis :**
    This type of Factor Analysis is used when your variables are structured in changeable groups. For example, you may have a teenager’s health questionnaire with several points like sleeping patterns, wrong addictions, psychological health, mobile phone addiction, or learning disabilities.

    多因素分析分两步进行，即

    *   首先，主成分分析将对数据的每个部分进行分析。此外，这可以给出有用的特征值，其实际上用于标准化数据集以供进一步使用。
    *   新形成的数据集将合并成一个独特的矩阵，然后进行全局主成分分析。
4.  **Generalized Procrustes Analysis (GPA) :**
    The Procrustes analysis is actually a suggested way to compare then the two approximate sets of configurations and shapes, which were originally developed to equivalent to the two solutions from Factor Analysis, this technique was actually used to extend the GP Analysis so that more than two shapes could be compared in many ways. The shapes are properly aligned to achieve the target shape. Mainly GPA (Generalized Procrustes Analysis) uses geometric transformations.

    几何进展是:

    *   各向同性重新缩放，
    *   反思，
    *   旋转，
    *   转换矩阵来比较数据集。

    **特征值**
    当因子分析要生成因子时，每个因子都有一个相关的特征值，该特征值将给出每个因子解释的总方差。
    通常，特征值大于 1 的因子是有用的:

    ```
    Percentage of variation explained by F1   =   Eigenvalue of Factor 1/No. of Variables

    Percentage of variation explained by F2   =   Eigenvalue of Factor 2/No. of Variables

    ```

    # X？向量=？？向量
    X 和以前一样是一般矩阵，乘以某个向量，然后？是一个特征值。看一下方程，注意到当你用矩阵乘以向量时，效果是复制了刚才乘以值的同一个向量？。这是不寻常的行为，赚取矢量和数量？特殊名称:特征向量和特征值。

    **因子负荷**
    此外，因子是平等创造的；有些因素权重较大，有些权重较低。举个简单的例子，想象一下你的汽车公司说马鲁蒂·铃木正在进行一项调查，包括电话调查、身体调查、谷歌表格等。对于客户满意度，结果显示以下因素负载:

    ```
    VARIABLE         |      F1         |      F2         |     F3
                     |                 |                 |
    Problem 1        |    0.985        |    0.111        |    -0.032
    Problem 2        |    0.724        |    0.008        |    0.167
    Problem 3        |    0.798        |    0.180        |    0.345

    ```

    此处–
    F1–因子 1
    F2–因子 2
    F3–因子 3
    对问题影响最大的因子(因此具有最高的因子负荷)以粗体显示。因子负荷类似于相关系数，因为它们可以从-1 变化到 1。因子越接近-1 或 1，它们对变量的影响就越大。
    **注:**加载因子为 0 表示无影响。