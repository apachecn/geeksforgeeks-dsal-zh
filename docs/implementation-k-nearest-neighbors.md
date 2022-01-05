# K 近邻的实现

> 原文:[https://www . geesforgeks . org/implementation-k-近邻/](https://www.geeksforgeeks.org/implementation-k-nearest-neighbors/)

**先决条件:**T2【K】最近的邻居

**简介**

假设给我们一组数据项，每个数据项都有数值特征(如身高、体重、年龄等)。如果特征的计数是 *n* ，我们可以将项目表示为一个 *n* 维网格中的点。给定一个新项目，我们可以计算从该项目到集合中每一个其他项目的距离。我们挑选最接近的 T4 邻居，看看这些邻居的分类。我们在那里分类新的项目。
那么问题就变成了**我们如何计算物品之间的距离。**这个问题的解决方案取决于数据集。如果值是真实的，我们通常使用欧几里得距离。如果值是分类的或二进制的，我们通常使用汉明距离。
**算法:**

```
Given a new item:
    1\. Find distances between new item and all other items
    2\. Pick k shorter distances
    3\. Pick the most common class in these k distances
    4\. That class is where we will classify the new item
```

**读取数据**

让我们的输入文件采用以下格式:

```
Height, Weight, Age, Class
1.70, 65, 20, Programmer
1.90, 85, 33, Builder
1.78, 76, 31, Builder
1.73, 74, 24, Programmer
1.81, 75, 35, Builder
1.73, 70, 75, Scientist
1.80, 71, 63, Scientist
1.75, 69, 25, Programmer
```

每个项目都是一行，在“类”下，我们可以看到项目的分类。要素名称下的值(“高度”等)。)是该项对该功能的价值。所有值和特征都用逗号分隔。
将这些数据文件放置在工作目录[数据 2](https://media.geeksforgeeks.org/wp-content/uploads/data2.txt) 和[数据](https://media.geeksforgeeks.org/wp-content/uploads/data.txt)中。选择一个，将内容原样粘贴到名为*数据*的文本文件中。
我们将从文件(名为“data.txt”)中读取，并将输入按行分割:

```
f = open('data.txt', 'r');
lines = f.read().splitlines();
f.close();
```

文件的第一行保存要素名称，最后是关键字“类”。我们希望将特征名称存储到一个列表中:

```
# Split the first line by commas,
# remove the first element and 
# save the rest into a list. The
# list now holds the feature 
# names of the data set.
features = lines[0].split(', ')[:-1];
```

然后我们继续看数据集本身。我们将项目保存到一个名为*项目*的列表中，其元素是字典(每个项目一个)。这些条目字典的关键是特征名，加上“类”来保存条目类。最后，我们想打乱列表中的项目(这是一种安全措施，以防项目顺序不正常)。

## 蟒蛇 3

```
items = [];

for i in range(1, len(lines)):

    line = lines[i].split(', ');

    itemFeatures = {"Class" : line[-1]};

    # Iterate through the features
    for j in range(len(features)):

        # Get the feature at index j
        f = features[j];

        # The first item in the line
        # is the class, skip it
        v = float(line[j]);

        # Add feature to dict
        itemFeatures[f] = v;

    # Append temp dict to items
    items.append(itemFeatures);

shuffle(items);
```

**数据分类**

随着数据存储到*项*中，我们现在开始构建我们的分类器。对于分类器，我们将创建一个新的功能，*分类*。它将把我们想要分类的项目、项目列表和最近邻居的数量 *k* 作为输入。
如果 *k* 大于数据集的长度，我们就不进行分类，因为我们不能有比数据集中项目总数更多的最近邻居。(或者，我们可以将 k 设置为*项*的长度，而不是返回错误消息)

```
if(k > len(Items)):

        # k is larger than list
        # length, abort
        return "k larger than list length";
```

我们要计算待分类项目与训练集中所有项目之间的距离，最终保持 *k* 最短距离。为了保持当前最近的邻居，我们使用了一个名为*邻居*的列表。最少的每个元素都有两个值，一个是距离要分类的项目的距离，另一个是邻居所在的类别。我们将通过广义欧几里德公式计算距离(对于 *n* 维)。然后，我们将选择在*邻居*中出现时间最多的类，这将是我们的选择。代码:

## 蟒蛇 3

```
def Classify(nItem, k, Items):
    if(k > len(Items)):

        # k is larger than list
        # length, abort
        return "k larger than list length";

    # Hold nearest neighbors.
    # First item is distance,
    # second class
    neighbors = [];

    for item in Items:

        # Find Euclidean Distance
        distance = EuclideanDistance(nItem, item);

        # Update neighbors, either adding
        # the current item in neighbors
        # or not.
        neighbors = UpdateNeighbors(neighbors, item, distance, k);

    # Count the number of each
    # class in neighbors
    count = CalculateNeighborsClass(neighbors, k);

    # Find the max in count, aka the
    # class with the most appearances.
    return FindMax(count);
```

我们需要实现的外部功能有 *EuclideanDistance* 、*updateneighborsclass*、*calculate eigruborsclass*、 *FindMax* 。

**求欧氏距离**

两个向量 x 和 y 的广义欧几里德公式是这样的:

```
distance = sqrt{(x_{1}-y_{1})^2 + (x_{2}-y_{2})^2 + ... + (x_{n}-y_{n})^2}
```

用代码:

## 蟒蛇 3

```
def EuclideanDistance(x, y):

    # The sum of the squared
    # differences of the elements
    S = 0;

    for key in x.keys():
        S += math.pow(x[key]-y[key], 2);

    # The square root of the sum
    return math.sqrt(S);
```

**更新邻居**

我们有我们的邻居列表(最多应该有 *k* 的长度)，我们想添加一个给定距离的项目到列表中。首先，我们将检查*邻居*的长度是否为 *k* 。如果它有更少的，我们就不考虑距离而添加项目(因为在我们开始拒绝项目之前，我们需要将列表填充到 *k* )。如果没有，我们将检查该项目的距离是否比列表中距离最大的项目短。如果是真的，我们将用新的物品替换最大距离的物品。
为了更快地找到最大距离项，我们将保持列表按升序排序。因此，列表中的最后一项将具有最大距离。我们将用一个新的项目替换它，然后我们将再次对它进行排序。
为了加快这个过程，我们可以实现一个插入排序，在列表中插入新的项目，而不必对整个列表进行排序。尽管代码很长，虽然很简单，但会使教程陷入困境。

## 蟒蛇 3

```
def UpdateNeighbors(neighbors, item, distance, k):

    if(len(neighbors) > distance):

            # If yes, replace the last
            # element with new item
            neighbors[-1] = [distance, item["Class"]];
            neighbors = sorted(neighbors);

    return neighbors;
```