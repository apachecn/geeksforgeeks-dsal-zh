# 谜题|天启

> 原文:[https://www.geeksforgeeks.org/puzzle-the-apocalypse/](https://www.geeksforgeeks.org/puzzle-the-apocalypse/)

**谜题:**
在新的后启示录世界，世界女王极度关注出生率。因此，她下令所有家庭应确保他们有一个女孩，否则他们将面临巨额罚款。如果所有家庭都遵守这一政策——也就是说，他们一直继续生孩子，直到生下一个女孩，到了这个时候他们就立即停止——新一代的性别比例会是多少？(假设某人在任何特定的怀孕期间生男孩或女孩的几率相等。)从逻辑上解决这个问题，然后写一个它的计算机模拟。

**提示:**

1.  注意每个家庭都会有一个女孩。
2.  想想把每个家庭写成一系列的 Bs 和 Gs。

**解决方案**:

*   如果每个家庭都遵守这一政策，那么每个家庭将有一个零个或多个男孩后跟一个单身女孩的序列。
*   也就是说，如果“G”表示女孩，“B”表示男孩，那么孩子的顺序会看起来像 G 中的一个；BG；BBG；BBBGBBBBG 等等。

**数学上**:

*   它可以计算出每个性别序列的[概率](https://www.geeksforgeeks.org/mathematics-probability/)。
    1.  **P(G) = 1/2-**
        也就是 50%的家庭会先有一个女孩。其他人会生更多的孩子。
    2.  **P(BG) = 1/4-**
        生二胎的人中(也就是 50%)，50%的人下次会生女孩。
    3.  **P(BBG) = 1/8-**
        有第三个孩子的人(占 25%)，50%的人下次会生女孩。等等。
*   据说每个家庭只有一个女孩。
*   平均每个家庭有几个男孩？为了计算这个，让我们看看男孩数量的期望值。
*   男孩数量的期望值是每个序列的概率乘以该序列中的男孩数量。

下表说明了男孩数量的期望值:

<figure class="table">

| **序列** | **男孩数量** | **概率** | **男生人数*概率** |
| G |        0 |     1/2 |                  0 |
| 保加利亚 | one |     1/4 |                1/4 |
| BBG |        2 |     1/8 |                2/8 |
| BBBG | three |     1/16 |               3/16 |
| BBBBG | four |     1/32 |               4/32 |
| BBBBBG | five |     1/64 |               5/64 |
| BBBBBBG | six |     1/128 |              6/128 |

*   或者换句话说，这是 I 到 I 无穷之和除以 2 <sup>i</sup> 。

**逻辑上**:

*   思考这个问题的一种方法是，想象我们把每个家庭的所有性别序列放在一个巨大的字符串中。所以如果家庭 1 有 BG，家庭 2 有 BBG，家庭 3 有 G，那就是 BGBBGG。
*   孩子一出生，其性别(B 或 G)就可以追加到字符串中。
*   下一个角色成为 G 的几率有多大？嗯，如果生男孩和女孩的几率相同，那么下一个角色是 G 的几率是 50%。
*   因此，大约一半的字符串应该是 Gs，一半应该是 Bs，给出一个均匀的性别比例。
*   这其实很有道理。生物学没有改变。
*   新生婴儿一半是女孩，一半是男孩。
*   遵守一些关于什么时候停止生孩子的规则并不能改变这个事实。
*   因此，性别比例为 50%的女孩和 50%的男孩。

下面是计算家里有女孩概率的伪代码-

```
double r unNFamilies (int n) 
{
    int boys = 0;
    int girls = 0;
    for (int i = 0; i < n; i++) 
    {
        int [] genders = runOneFamilY();
        girls += genders[0];
        boys += genders[1];
    }
    return girls / (double) (boys + girls);
}

int[] runOneFamily() 
{
    Random random = new Random();
    int boys = 0;
    int girls = 0;
    while (girls == 6) 
    {    
        // until we have a girl
        if (random.nextBoolean ()) 
        {    
            // girl
            girls += 1;
        } 
        else
        {  
            // boy
            boys += 1;
        }
    }
    int[] genders = {girls, boys};
    return genders;
}
```

如果这个伪代码在大的 n 值上执行，那么结果将非常接近 0.5。

</figure>