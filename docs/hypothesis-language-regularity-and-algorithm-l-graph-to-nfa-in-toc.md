# TOC

中的假设(语言规律性)和算法(L 图到 NFA)

> 原文:[https://www . geesforgeks . org/假说-语言-规律性-和-算法-l-graph-to-nfa-in-toc/](https://www.geeksforgeeks.org/hypothesis-language-regularity-and-algorithm-l-graph-to-nfa-in-toc/)

先决条件–[有限自动机](https://www.geeksforgeeks.org/toc-finite-automata-introduction/)、[L-图以及它们所代表的](https://www.geeksforgeeks.org/theory-of-computation-l-graphs-and-what-they-represent/)、
L-图可以生成上下文相关的语言，但是编写上下文相关的语言比编写常规语言要困难得多。这就是为什么我提出了一个假设，关于什么样的 L 图可以生成一种规则的语言。但是首先，我需要向大家介绍我所说的迭代嵌套。

正如你所记得的，一个巢是一条中立的路径![T_1T_2T_3](img/cf141fcc7d26ff4f599942385f23c9ad.png "Rendered by QuickLaTeX.com")，其中![T_1](img/96a6733fdaf50c52e52e85cd454070bb.png "Rendered by QuickLaTeX.com")和![T_3](img/391c6f9ba720008bcd1c0ef22a3a11d2.png "Rendered by QuickLaTeX.com")是周期，![T_2](img/c42f122bb69494abc4b51a381f5db39b.png "Rendered by QuickLaTeX.com")路径是中立的。我们将![T_1T_2T_3](img/cf141fcc7d26ff4f599942385f23c9ad.png "Rendered by QuickLaTeX.com")称为迭代嵌套，如果![T_1](img/96a6733fdaf50c52e52e85cd454070bb.png "Rendered by QuickLaTeX.com")、![T_2](img/c42f122bb69494abc4b51a381f5db39b.png "Rendered by QuickLaTeX.com")和![T_3](img/391c6f9ba720008bcd1c0ef22a3a11d2.png "Rendered by QuickLaTeX.com")路径多次打印同一个符号串，更准确的说![T_1](img/96a6733fdaf50c52e52e85cd454070bb.png "Rendered by QuickLaTeX.com")打印![\alpha^k](img/a697c3510613ba237845647f8abe6e8b.png "Rendered by QuickLaTeX.com")、![T_2](img/c42f122bb69494abc4b51a381f5db39b.png "Rendered by QuickLaTeX.com")打印![\alpha^l](img/58a0e25508d7a2f817ed6a964563c083.png "Rendered by QuickLaTeX.com")、![T_3](img/391c6f9ba720008bcd1c0ef22a3a11d2.png "Rendered by QuickLaTeX.com")打印![\alpha^m](img/4e7198982f11424d8d1de290e94a7515.png "Rendered by QuickLaTeX.com")、![k, \: l, \: m \geqslant 0](img/a83932d76bcd4a1ad7d3605a31f90fca.png "Rendered by QuickLaTeX.com")和![\alpha](img/da2f298cb7c1dd3024c0cfda151c6997.png "Rendered by QuickLaTeX.com")是一串输入符号(最好是![k, \: l\: and\: m\: is \geqslant 1](img/37f4fb6baf8c42b3fd8698419b3cbff1.png "Rendered by QuickLaTeX.com")中至少有一个)。
从这个定义中引出了下一个假设。

**假设–**如果在一个上下文无关的 L-图 G 中所有的嵌套都在迭代，那么这个 L-图 G 定义的语言 L(G)是正则的。
如果这个假设将在不久的将来被证明，它可以改变编程的许多方面，这将使创建新的简单的编程语言比现在容易得多。上面的假设引出了下一个算法，即将迭代嵌套的上下文无关 L 图转换为 NFA 图。

**算法–**将带有迭代补码的上下文无关 L 图转换为相应的 NFA
**输入–**带有迭代补码的上下文无关 L 图![G=(\Sigma, V, P, \lambda, P_0, F)](img/4260e20f6184d863c3451e647becc206.png "Rendered by QuickLaTeX.com")
**输出–**![G'=(\Sigma', V', \lambda', P'_0, F')\\*](img/383183cd5dd6d87ce8a1f12463f8743a.png "Rendered by QuickLaTeX.com")

*   **第一步:**L 图和 NFA 的语言必须相同，因此，我们不需要新的字母表![\Rightarrow \Sigma'' = \Sigma, \: P'' = P](img/7f484acb82a370118844d0562ed87c67.png "Rendered by QuickLaTeX.com")。(注释:我们构建上下文无关的 L 图 G ' '，它等于起始图 G ' '，没有冲突的嵌套)
*   **Step-2:** Build Core(1, 1) for the graph G.
    V’’ := {(v, ![\varepsilon](img/77f4fbcd49baff036c135afef166de95.png "Rendered by QuickLaTeX.com")) | v ![\in](img/b543f5d0e78b7be8c9e6e2ec6a682bef.png "Rendered by QuickLaTeX.com") V of ![\forall](img/9dea966ef2ec64199005c6b655762165.png "Rendered by QuickLaTeX.com") canon k ![\in](img/b543f5d0e78b7be8c9e6e2ec6a682bef.png "Rendered by QuickLaTeX.com") Core(1, 1), v ![\notin](img/3024d7fbe2a878f8fe52b6dceb092b8f.png "Rendered by QuickLaTeX.com") k}
    ![\lambda''](img/c0fa4838dd143d31113faa363fe9dc3c.png "Rendered by QuickLaTeX.com") := { arcs ![o \in \lambda](img/191f509662ed8296ed6eb48464a80001.png "Rendered by QuickLaTeX.com") | start and final states ![o', o'' \in](img/2f5cc58c33dc2d9eb7bdb2b8a63a0820.png "Rendered by QuickLaTeX.com") V’’}

    对于所有 k ![\in](img/b543f5d0e78b7be8c9e6e2ec6a682bef.png "Rendered by QuickLaTeX.com")核心(1，1):
    步骤 1’。v :=佳能第一州![\eta := \varepsilon](img/08ceb0cdb7a383b1485afe98ca4c37a0.png "Rendered by QuickLaTeX.com")。
    V ' '![\cup= (v, \eta)](img/e3f59c158d2df1efe1c5a6d9eeeeb9f9.png "Rendered by QuickLaTeX.com")T5【第二步】。![\lambda'' \cup=](img/0af80db2ed1682552789e212aa10fb21.png "Rendered by QuickLaTeX.com")弧从状态![(v, \eta)](img/3dde5846dc985dd45cbfe57ab7a27996.png "Rendered by QuickLaTeX.com")跟随该弧进入新状态，新状态用以下规则定义:
    ![\eta := \eta](img/f2a6da328605005c5ef8cc503c04a438.png "Rendered by QuickLaTeX.com")，如果输入括号在该弧上![= \varepsilon](img/1ae8a7c83277455c7eb59b4e8451f762.png "Rendered by QuickLaTeX.com")；![\eta'the\: input\: bracket'](img/596fbf2eeb634cc001ce7a611faec31b.png "Rendered by QuickLaTeX.com")，如果输入括号是开括号；![\eta 'without\: the\: last\: bracket'](img/cc7dbcb3fa36893b484fca2b1a5fa4bd.png "Rendered by QuickLaTeX.com")，如果输入括号是闭合括号
    v :=佳能 k 的第二状态
    V'' ![\cup= (v, \eta)](img/e3f59c158d2df1efe1c5a6d9eeeeb9f9.png "Rendered by QuickLaTeX.com")
    步骤 3’。重复步骤 2’，同时佳能中仍有弧线。

*   **第三步:**构建核心(1，2)。
    如果佳能连续有 2 个相等的弧:开始状态和最终状态匹配；我们把给定状态的弧线加入到自身中，利用这个弧线，达到![\lambda''](img/c0fa4838dd143d31113faa363fe9dc3c.png "Rendered by QuickLaTeX.com")。
    以![(v, \varepsilon) - (u, \varepsilon) (\alpha)](img/115afc9c8259197421de0594cd6a6720.png "Rendered by QuickLaTeX.com")的形式将![\lambda](img/73aa9bb7ff52ad1f2fda1ba95744b076.png "Rendered by QuickLaTeX.com")弧 v–u![(\alpha)](img/24000ccac2b3b8a19fc1b256e47be24f.png "Rendered by QuickLaTeX.com")中的剩余部分添加到![\lambda''](img/c0fa4838dd143d31113faa363fe9dc3c.png "Rendered by QuickLaTeX.com")中
*   **Step-4:** ![P''_0 = (P_0, \varepsilon).\: F'' = \{(f, \varepsilon) | f \in F\}](img/e235c0b348e4dd83894450be0e357a24.png "Rendered by QuickLaTeX.com")
    (备注:以下是将上下文无关的 L-graph G ' '转换为 NFA G ' '的算法)
*   **第 5 步:**对 G“”中的每一个迭代补码![T = T_1T_2T_3](img/51905668375aeedd721fc9ca50c4e0ca.png "Rendered by QuickLaTeX.com")
    做如下操作:添加一个新的状态 v .创建一个从状态![beg(T_3)](img/5c6731b6a51d8ad1bd5dd45c58e613c2.png "Rendered by QuickLaTeX.com")开始的路径，等于![T_3](img/391c6f9ba720008bcd1c0ef22a3a11d2.png "Rendered by QuickLaTeX.com")。从 v 进入![T_3](img/391c6f9ba720008bcd1c0ef22a3a11d2.png "Rendered by QuickLaTeX.com")创建路径，等于![T_1](img/96a6733fdaf50c52e52e85cd454070bb.png "Rendered by QuickLaTeX.com")。删除循环![T_1](img/96a6733fdaf50c52e52e85cd454070bb.png "Rendered by QuickLaTeX.com")和![T_3](img/391c6f9ba720008bcd1c0ef22a3a11d2.png "Rendered by QuickLaTeX.com")。
*   **第 6 步:** G' = G ' '，其中弧没有加载括号。

所以上面的每一步都很清楚，我给你们看下一个例子。
![\textbf{Example:}\\ \textbf{Input:}](img/faf5933d25e70dac1106ea1fb506d058.png "Rendered by QuickLaTeX.com")上下文无关的 L 图，具有迭代补语
![G = ( \{a, b, c\}, \\*\{1, 2, 3\} \\*\{( (, ) ), ( [, ] )\}, \\*\\*\{ (: \{ 1 - a - 1 \}, \\*): \{ 2 - a - 2 \}, \\*\big[: \{ 1 - b - 2 \}, \\*\big]: \{ 2 - c - 3 \}, \\*\varepsilon: \{ 1 - a - 2 \} \}, \\*\\*1, \\*\{2, 3\} \}](img/6fe2d3327004bf838949431f97960e69.png "Rendered by QuickLaTeX.com")、
，确定了![language = \{a^(^2^n^+^1^) | n \geqslant 0\} \cup \{bc\}](img/7f20454503471758f0710ded78819615.png "Rendered by QuickLaTeX.com")
![](img/cc9c94bced8f3fd4a9f5339ef4f54477.png)开始图 G
![\Sigma'' = \{a, b, c\}\\ V'' = \varnothing\\ \lambda'' = \varnothing](img/b60266add83e53341b32b2a10239d030.png "Rendered by QuickLaTeX.com")
核心(1，1)= { 1–a–2；1–a，(1–1–a–2–a)，1–2；1–b，(2–2–c，)2–3 }
核心(1，2) =核心(1，1)![\cup](img/020f5f94e46bf134a64da62cef374608.png "Rendered by QuickLaTeX.com"){ 1–a，(1–1–a)，(1–1–a–2–a，)1–2–a，)1–2 }
步骤 2:步骤 1’–步骤 3’
![\Rightarrow\\ V'' = \{(1, \varepsilon), (2, (_2), (3, \varepsilon), (1, (_1), (2, )_1), (2, \varepsilon)\}\\* \lambda'' = \{ \\*(: \{ (1, \varepsilon) - a - (1, (); (1, () - a - (1, () \}, \\*): \{ (2, )) - a - (2, )); (2, )) - a - (2, \varepsilon) \}, \\*\big[: \{ (1, \varepsilon) - b - (2, [) \}, \\*\big]: \{ (2, [) - c - (3, \varepsilon) \}, \\*\varepsilon: \{ (1, \varepsilon) - a - (2, \varepsilon); (1, () - a - (2, )) \} \}\\ P''_0 = (1, \varepsilon)\\ F'' = \{(2, \varepsilon), (3, \varepsilon)\}\\ G'' = (\Sigma'', V'', P'', \lambda'', P''_0, F'')](img/d1613b59e5c8c112a14e286b38941357.png "Rendered by QuickLaTeX.com")
![](img/dc6411f0a4117f94f3c0c72f439501d8.png)中间图 G ' '
![\Sigma' = \{a, b, c\}\\ V' = V'' \cup \{4\}\\ P'_0 = P''_0\\ F' = F''\\ \lambda' = \{ \\*(1, \varepsilon) - a - (1, (); \\*(2, )) - a - 4; \\*4 - a - (2, )); \\*(2, )) - a - (2, \varepsilon); \\*(1, \varepsilon) - b - (2, [); \\*(2, [) - c - (3, \varepsilon); \\*(1, \varepsilon) - a - (2, \varepsilon); \\*(1, () - a - (2, )) \}\\  G' = (\Sigma', V', \lambda', P'_0, F')](img/c4a2cec08cddf80bad3f7702967319f0.png "Rendered by QuickLaTeX.com")
T21】NFA G’