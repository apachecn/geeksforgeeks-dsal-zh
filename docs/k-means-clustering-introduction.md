# K 表示聚类–简介

> 原文:[https://www . geesforgeks . org/k-means-clustering-introduction/](https://www.geeksforgeeks.org/k-means-clustering-introduction/)

给我们一组数据项，带有特定的特征，以及这些特征的值(比如向量)。任务是将这些项目分类。为此，我们将使用 kMeans 算法；一种无监督学习算法。

**概述**

(如果你把项目看作 n 维空间中的点，会有帮助)。该算法将把这些项目分成 k 个相似性组。为了计算相似度，我们将使用欧几里得距离作为度量。
算法工作原理如下:

1.  首先，我们随机初始化 k 个点，称为平均值。
2.  我们将每个项目分类到其最接近的平均值，并更新平均值的坐标，这是迄今为止在该平均值中分类的项目的平均值。
3.  我们对给定的迭代次数重复这个过程，最后，我们得到了我们的集群。

上面提到的“点”之所以被称为平均值，是因为它们包含了分类项目的平均值。要初始化这些手段，我们有很多选择。一个直观的方法是初始化数据集中随机项目的平均值。另一种方法是在数据集边界之间的随机值处初始化平均值(如果对于一个特征 *x* 项的值在[0，3]中，我们将在[0，3]处用 *x* 的值初始化平均值)。
以上算法用伪代码:

```
Initialize k means with random values

For a given number of iterations:
    Iterate through items:
        Find the mean closest to the item
        Assign item to mean
        Update mean
```

**读取数据**

我们以文本文件(' data.txt ')的形式接收输入。每行代表一个项目，它包含用逗号分隔的数值(每个特征一个)。你可以在这里找到一个样本数据集[。](https://github.com/MrDupin/Machine-Learning/blob/master/Clustering/kMeans%20-%20Standard/data.txt)
我们将从文件中读取数据，将其保存到列表中。列表中的每个元素都是另一个包含要素项值的列表。我们通过以下功能做到这一点:

## 蟒蛇 3

```
def ReadData(fileName):

    # Read the file, splitting by lines
    f = open(fileName, 'r');
    lines = f.read().splitlines();
    f.close();

    items = [];

    for i in range(1, len(lines)):
        line = lines[i].split(',');
        itemFeatures = [];

        for j in range(len(line)-1):

            # Convert feature value to float
            v = float(line[j]);

            # Add feature value to dict
            itemFeatures.append(v);

        items.append(itemFeatures);

    shuffle(items);

    return items;
```

**初始化意味着**

我们希望在项目的特征值范围内初始化每个平均值。为此，我们需要找到每个特征的最小值和最大值。我们通过以下功能来实现:

## 计算机编程语言

```
def FindColMinMax(items):
    n = len(items[0]);
    minima = [sys.maxint for i in range(n)];
    maxima = [-sys.maxint -1 for i in range(n)];

    for item in items:
        for f in range(len(item)):
            if (item[f] < minima[f]):
                minima[f] = item[f];

            if (item[f] > maxima[f]):
                maxima[f] = item[f];

return minima,maxima;
```

变量*最小值、最大值*分别是包含项目最小值和最大值的列表。我们在上述两个列表中的相应最小值和最大值之间随机初始化每个平均值的特征值:

## 计算机编程语言

```
def InitializeMeans(items, k, cMin, cMax):

    # Initialize means to random numbers between
    # the min and max of each column/feature   
    f = len(items[0]); # number of features
    means = [[0 for i in range(f)] for j in range(k)];

    for mean in means:
        for i in range(len(mean)):

            # Set value to a random float
            # (adding +-1 to avoid a wide placement of a mean)
            mean[i] = uniform(cMin[i]+1, cMax[i]-1);

    return means;
```

**欧氏距离**

我们将使用欧几里德距离作为数据集的相似性度量(注意:根据您的项目，您可以使用另一个相似性度量)。

## 蟒蛇 3

```
def EuclideanDistance(x, y):
    S = 0; # The sum of the squared differences of the elements
    for i in range(len(x)):
        S += math.pow(x[i]-y[i], 2)

    #The square root of the sum
    return math.sqrt(S)
```

**更新方式**

为了更新平均值，我们需要为平均值/聚类中的所有项目找到其特征的平均值。我们可以通过将所有值相加，然后除以项目数来实现这一点，或者我们可以使用更优雅的解决方案。我们将通过执行以下操作来计算新平均值，而无需重新添加所有值:

```
m = (m*(n-1)+x)/n
```

其中 *m* 为特征的平均值， *n* 为聚类中的项目数， *x* 为添加项目的特征值。我们对每个特征进行上述操作，以获得新的平均值。

## 计算机编程语言

```
def UpdateMean(n,mean,item):
    for i in range(len(mean)):
        m = mean[i];
        m = (m*(n-1)+item[i])/float(n);
        mean[i] = round(m, 3);

    return mean;
```

**物品分类**

现在我们需要编写一个函数，将一个项目分类到一个组/集群中。对于给定的项目，我们将找到它与每个平均值的相似性，并将项目分类到最接近的一个。

## 计算机编程语言

```
def Classify(means,item):

    # Classify item to the mean with minimum distance   
    minimum = sys.maxint;
    index = -1;

    for i in range(len(means)):

        # Find distance from item to mean
        dis = EuclideanDistance(item, means[i]);

        if (dis < minimum):
            minimum = dis;
            index = i;

    return index;
```

**查找方式**

为了真正找到平均值，我们将遍历所有项目，将它们分类到最近的聚类中，并更新聚类的平均值。我们将重复固定次数的迭代过程。如果在两次迭代之间没有项目改变分类，我们就停止这个过程，因为算法已经找到了最优解。
下面的函数将 *k* (期望聚类的数量)、项目和最大迭代次数作为输入，并返回平均值和聚类。项目的分类存储在位于下方的数组*中，一个集群中的项目数量存储在*集群大小*中。* 

## 计算机编程语言

```
def CalculateMeans(k,items,maxIterations=100000):

    # Find the minima and maxima for columns
    cMin, cMax = FindColMinMax(items);

    # Initialize means at random points
    means = InitializeMeans(items,k,cMin,cMax);

    # Initialize clusters, the array to hold
    # the number of items in a class
    clusterSizes= [0 for i in range(len(means))];

    # An array to hold the cluster an item is in
    belongsTo = [0 for i in range(len(items))];

    # Calculate means
    for e in range(maxIterations):

        # If no change of cluster occurs, halt
        noChange = True;
        for i in range(len(items)):

            item = items[i];

            # Classify item into a cluster and update the
            # corresponding means.       
            index = Classify(means,item);

            clusterSizes[index] += 1;
            cSize = clusterSizes[index];
            means[index] = UpdateMean(cSize,means[index],item);

            # Item changed cluster
            if(index != belongsTo[i]):
                noChange = False;

            belongsTo[i] = index;

        # Nothing changed, return
        if (noChange):
            break;

    return means;
```

**查找集群**

最后，我们想找到集群，给定的手段。我们将遍历所有项目，并将每个项目分类到它最接近的集群。

## 计算机编程语言

```
def FindClusters(means,items):
    clusters = [[] for i in range(len(means))]; # Init clusters

    for item in items:

        # Classify item into a cluster
        index = Classify(means,item);

        # Add item to cluster
        clusters[index].append(item);

    return clusters;
```

其他常用的相似性度量是:-
1。**余弦距离:**它决定了 n 维空间
![d = \frac{X.Y}{||X||*||Y||}\ ](img/bed8fcdfdcd350d398900313fb11854c.png "Rendered by QuickLaTeX.com")
2 中两个点的点向量之间夹角的余弦。**曼哈顿距离:**计算两个数据点坐标的绝对差之和。
![d = \sum_{n} X{_{i}}-Y{_{i}} ](img/bd65e39079a7fcd327bf039ffce0bea0.png "Rendered by QuickLaTeX.com")
3。**闵可夫斯基距离:**也称为广义距离度量。它可以用于序数和数量变量
![d = (\sum _{n}|X_{i}-Y_{i}|^{\frac{1}{p}})^{p} ](img/2b8bd436b9856f9b18606e274162d267.png "Rendered by QuickLaTeX.com")
你可以在我的 [GitHub](https://github.com/MrDupin/Machine-Learning/tree/master/Clustering/kMeans%20-%20Standard) 上找到整个代码，还有一个样本数据集和一个绘图函数。感谢阅读。
本文由**安东妮斯·马罗尼科拉基斯**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。