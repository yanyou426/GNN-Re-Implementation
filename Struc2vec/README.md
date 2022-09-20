
## Model Environment
The model is written using Tensorflow 1.4 in Python 2.7. You can install the dependencies by running:
```bash
pip install -r requirements.txt
```

## Model Implementation
To train: run
```bash
python train.py
```

To evaluate, run
```bash
python eval.py
```

## Model explanation
### Basic structure2vec algorithm

structure2vec算法中，对每个节点的特征vector更新公式如下：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/point.png" style="zoom:30%;"/>

其中F为非线性映射。执行更新的迭代次数越多，顶点特征将传播到更远的顶点并在远处的顶点处非线性聚合。如果在T次迭代后终止更新过程，则每个嵌入的顶点$\mu _v^t$将包含有关其T跳邻域的信息，该邻域由图拓扑和所涉及的顶点特征确定。

在二进制相似性比较的背景下，$x_v$为basic block的特征vector，具体可以由Genius文章中的提取ACFG的工具生成，主要包含以下几个特征，均为手动提取的特征：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/features.png" style="zoom:30%;"/>

F公式具体如下所示：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/function.png" style="zoom:30%;"/>

$\sigma$具体为多层的Relu函数组成，用于非线性激活：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/relu.png" style="zoom:30%;"/>

作者将F中的参数与后续比较两个graph的Siamese架构的参数一起训练，使用随机梯度下降，一旦AUC达到较好值训练终止：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/lossfunc.png" style="zoom:30%;"/>

整体算法如下，算法最终输出为每个graph的embedding：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/algorithm.png" style="zoom:30%;"/>

### Dataset
使用GCCv5.4编译OpenSSL(version 1.0.1f和1.0.1u)，分别有三种架构x86, MIPS, ARM, 以及编译优化等级O0-O3。总共有18,269个二进制文件，包含129,365个ACFG

### Result

模型训练的结果为：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/train.png" style="zoom:30%;"/>

在验证集与测试集上的结果为：

<img src="https://github.com/yanyou426/GNN-Re-Implementation/blob/main/Struc2vec/img/eval.png" style="zoom:30%;"/>

可以看出，使用structure2vec算法+手动提取特征作为节点特征vector，在判断两个graph是否相似的任务上准确率还是比较高的。

