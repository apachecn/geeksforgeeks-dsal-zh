# 识别地图中每个节点的所有父节点

> 原文:[https://www . geesforgeks . org/identify-all-grand-parent-nodes-of-in-a-map 中的每个节点/](https://www.geeksforgeeks.org/identify-all-grand-parent-nodes-of-each-node-in-a-map/)

在输入中给出一个人和他们的孩子之间的关系，对于这个数据中的所有人，识别输入中所有人的祖父母。

```
Input: A map of all the people and their children
Map[String, Set[String]]

Output: A map of all people and their grandparents
Map[String, Set[String]]

Example:
Input 
Map(A -> Set(B,C), B -> Set(D, C), C -> Set(E))

Output:
Map(D -> Set(A), C -> Set(A), E -> Set(A, B)) 
```

**我们强烈建议您最小化浏览器，先自己尝试一下**

在这里，我们迭代地图中的每个节点，找出每个子节点的父节点。

想法是使用递归。但是，不用递归也可以解决。

让我们先看看无递归解决方案:

**解 1(无递归):**

这里我们必须使用可变标量映射。下面是 Scala 代码。

```
val input = Map("A" -> Set("B","C"), "B" -> Set("D", "C"), "C" -> Set("E"))
val output: scala.collection.mutable.Map[String, Set[String]]
  = scala.collection.mutable.Map()

  input.map(node => node._2.map(child =>
    input.get(child).map(grandchildren =>
      grandchildren.map{grandchild =>
        if(output.keys.exists(_ == grandchild)) {
          output.put(grandchild, output.get(grandchild).get ++ Set(node._1))
        } else {
          output.put(grandchild, Set(node._1))
        }
      }
    )
  ))

```

这里我们迭代地图的每个节点，找出每个子节点的孙子。这将有助于我们创建一个有祖父母和外祖父母关系的地图。

**解 2(带递归):**

这里我们可以像使用递归一样使用不可变的 Scala 映射。

```
val input = Map("A" -> Set("B","C"), "B" -> Set("D", "C"), "C" -> Set("E"))
val output = findGrandparents(input)

  def findGrandparents(family: Map[String, Set[String]]): Map[String, Set[String]] = {
    family.foldLeft(Map[String, Set[String]]()){
      case (grandParents, oneFamily) => {
        val grandChildren: Set[String] = oneFamily._2.flatMap(member => family.get(member)).flatten
        val res =  grandChildren.map(child => {
          grandParents.get(child) match {
            case None =>(child -> Set(oneFamily._1))
            case Some(x) => (child -> (x + oneFamily._1))
          }
        }).toMap
        grandParents ++ res
      }

```

本文由**希曼舒·古普塔**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论