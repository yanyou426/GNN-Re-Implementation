
## Requirements
torch >= 1.2.0  
networkx >= 2.3  
numpy >= 1.16.4  
six >= 1.12

## Usage
The code includes an example of graph edit distances by using graph matching networks.

To train: run
```bash
./run.sh
```

## References:
[Deepmind-research](https://github.com/deepmind/deepmind-research/tree/master/graph_matching_networks)

## Model explanation


给定两个图![](http://latex.codecogs.com/svg.latex?{G_1}=\\left({{V_1},{E_1}}\\right))和![](http://latex.codecogs.com/svg.latex?{G_2}=\\left({{V_2},{E_2}}\\right))，模型希望计算它们的相似度分数![](http://latex.codecogs.com/svg.latex?s\\left({{G_1},{G_2}}\\right))，论文提出2个用于图之间相似性计算的模型，一个是基于GNN的图嵌入学习(Graph Embedding Models)方法，另一个是GMN(Graph Matching Networks)。

### Graph Embedding Models

三部分组成：encoder + propagation layer + aggregator

encoder:

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/encoder.png" style="zoom:30%;"/>

propagation:

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/propagation.png" style="zoom:30%;"/>

aggregator：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/aggregator.png"  width="500" height="70"/>

### Graph Matching Networks

GMN把一对图作为输入，与嵌入模型相比，匹配模型在一对图上计算相似性分数，而不是独立地将每个图映射到一个向量。

网络结构也是encoder+propagation+aggregator，其中encoder和aggregator结构一样

propagation:

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/propagation2.png" style="zoom:30%;"/>

其中交互信息 ![](http://latex.codecogs.com/svg.latex?{\\mu}) 采用了注意力机制：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/attention.png" style="zoom:30%;"/>

### Model learning

本文提出的模型可以采用pairwise训练或者triplet训练的方式进行模型训练：


<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/2and3.png" style="zoom:30%;"/>

### Datasets and Results on graph edit distances

目前仅复现了GNN和GMN模型在图编辑距离上的实验，数据集为随机生成的图，positive数据集则在随机生成图的基础上随机修改一条边，negative数据集则随即修改两条边。

可以看出GMN（上）比GNN（下）在图编辑距离这个task上效果要好：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/GMNres.png" style="zoom:30%;"/>

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/GMNonGraphEditDistance/imgofGMN/GNNres.png" style="zoom:30%;"/>

### Future work

给Security22的作者发了邮件，说会在这几天push一下GMN在二进制代码相似分析task上的code 蹲一波:)

