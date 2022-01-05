# 计算 N 维数组中元素的地址

> 原文:[https://www . geesforgeks . org/计算 n 维数组中元素的地址/](https://www.geeksforgeeks.org/calculating-the-address-of-an-element-in-an-n-dimensional-array/)

**N 维数组:**[N 维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)基本上是数组的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)。由于 **1-D** 阵列被识别为单个索引，因此 **2-D** 阵列使用两个索引来识别，类似地， **N 维**阵列使用 **N** 索引来识别。一个[多维](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)数组声明如下:

> NDA 国际机场 1<sub>2</sub><sub>3</sub>……..【S<sub>N</sub>；

**<u>解说</u> :**

*   这里，NDA 是 N 维数组的名字。它可以是任何有效的[标识符](https://www.geeksforgeeks.org/difference-between-keyword-and-identifier/)名称。
*   在上面的语法中， **S <sub>1</sub> ，S <sub>2</sub> ，S<sub>3</sub>……S<sub>N</sub>T9】表示 **N** 尺寸的最大尺寸。**
*   假设所有维度的下限都为零。
*   以上[数组](https://www.geeksforgeeks.org/how-to-initialize-array-of-objects-with-parameterized-constructors-in-c/)声明为整数数组。它也可以是整数以外的任何有效的[数据类型](https://www.geeksforgeeks.org/c-data-types/)。

**<u>N 维数组的地址计算</u> :**

**<u>假设:</u>**

*   N 维最大尺寸为**S<sub>1</sub>S<sub>2</sub>S<sub>3</sub>……，S<sub>N</sub>T9】的 N 维阵 NDA。**
*   需要计算其地址的元素具有索引**1<sub>1</sub>，1<sub>2</sub>，1<sub>3</sub>，……..l <sub>N</sub> 分别为**。
*   数组索引的下限可能不为零。例如，考虑以下数组 T:**T[-5…5][2…9][14…54][-9…-2]。**

**<u>解说</u> :**

*   在上面的数组 **T** 中，索引的下限不是零。
*   所以现在数组的索引的大小是不同的，可以用下面的公式计算:

> **upper round–lower round+1**

*   所以，这里 S<sub>1</sub>= 5 –(-5)+1 = 11。同样，S <sub>2</sub> = 8，S <sub>3</sub> = 41，S <sub>4</sub> = 8。

地址计算的下限为 **t <sub>1</sub> ，t <sub>2</sub> ，t <sub>3</sub> ……。t <sub>N</sub>** 。存储数组元素有两种方法:

*   主要行
*   列专业

**柱主公式:**

> NDA【我 <sub>1</sub> 【我 <sub>2</sub> 】地址。。。[I<sub>N</sub>= BaD+W *[(…E<sub>N</sub>S<sub>N-1</sub>+E<sub>N-1</sub>)S<sub>N-2</sub>+…E<sub>3</sub>)S<sub>2</sub>+E<sub>2</sub>)S<sub>1</sub>+E<sub>1</sub>
> 
> *   BAd 表示数组的**基地址**。
> *   w 代表数组的**宽度**，即数组中的维数。
> *   另外，E <sub>i</sub> 由 **E <sub>i</sub> 给出= l<sub>I</sub>–t<sub>I</sub>**，其中 l <sub>i</sub> 和 t <sub>i</sub> 分别是计算出的指标(需要确定的数组元素的指标)和下限。

**行主公式:**

> NDA【我 <sub>1</sub> 【我 <sub>2</sub> 】地址。。。。【l<sub>N</sub>= BaD+W *[((E<sub>1</sub>S<sub>2</sub>+E<sub>2</sub>)S<sub>3</sub>+E<sub>3</sub>)S<sub>4</sub>…..+E<sub>N-1</sub>S<sub>N</sub>+E<sub>N</sub>

**学习公式最简单的方法:**

**对于行-专业:**如果宽度= 5，内部顺序为*T3】E<sub>1</sub>S<sub>2</sub>+E<sub>2</sub>S<sub>3</sub>+E<sub>3</sub>S<sub>4</sub>+E<sub>4</sub>S<sub>5</sub>+E<sub>5</sub>T23】如果宽度= 3，按照顺序找出图案，并按照四个基本步骤计算任意宽度的公式:*

*   写出内部序列。
*   除第一项外，在每个 **E** 后放上右括号。所以对于宽度= 5，它变成

> E<sub>1</sub>S<sub>2</sub>+E<sub>2</sub>S<sub>3</sub>+E<sub>3</sub>)S<sub>4</sub>+E<sub>4</sub>S<sub>5</sub>+E<sub>5</sub>)。

*   首先放好所有的左括号。

> (((E<sub>1</sub>S<sub>2</sub>+E<sub>2</sub>)S<sub>3</sub>+E<sub>3</sub>)S<sub>4</sub>+E<sub>4</sub>)S<sub>5</sub>+E<sub>5</sub>)。

*   在公式中加入基址和宽度。

对于**主列**来说，方法是相似的，但是内部序列的模式与主行模式相反。

**对于柱专业:**如果宽度=5，内部顺序为**E<sub>5</sub>S<sub>4</sub>+E<sub>4</sub>S<sub>3</sub>+E<sub>3</sub>S<sub>2</sub>+E<sub>2</sub>S<sub>1</sub>+E<sub>1</sub>**。

**例:**我们取一个多维数组 **A[10][20][30][40]** ，基地址 **1200** 。任务是找到元素**A【1】【3】【5】【6】**的地址。

这里，BAd = 1200，宽度= 4。
S1 = 10，S2 = 20，S3 = 30，S4 = 40

因为没有给出下限，所以下限假设为零。
E1 = 1–0 = 1；
E2 = 3–0 = 3；
E3 = 5–0 = 5；
E4 = 6–0 = 6。

任何技术(行专业或列专业)都可以用于计算答案(除非特别说明)。
应用行主公式，直接将公式写成:

a[1][3][5][6]= 1200+4((1×20+3)30+5)40+6)

 =1200 +4((23 × 30 +5)40 +6) 

=1200 + 4(695 × 40 + 6) 

=1200 + (4 × 27806) 

=112424.