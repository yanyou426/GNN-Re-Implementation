## Model Environment
### Prerequisites

Python 3.8 or above version is required. To install python dependencies, run
```bash
$ pip3 install pipenv
```

### Use pipenv shell

Install dependencies
```bash
$ pipenv install
```

Activate pipenv shell
```bash
$ pipenv shell
```

## Model Implementation

Training Instruction2vec (i2v) embeddings and Siamese-LSTM from data in `/revos/data/done/${programs}/innereye.csv` 
```bash
python train.py --targets={programs}
```

Test the trained model
```bash
python validation.py
```

Extract basic block embeddings using a model trained on {programs}
```bash
python extract.py --targets={programs}
```

## Model explanation

### Overview

### Instruction embedding

使用word2vec中的skip-gram模型学习每条指令的嵌入。每条指令会学习成一个数字，每个basic block会生成一个vector，由于一个函数由多个basic block组成，故经过word embedding这一过程后，每个函数最终由多个vector组成的矩阵来表示。

### Basic block embedding

生成basic block的embedding的最简单的方法就是将指令的embedding组合起来，但在有不同架构不同优化等级的编译条件下，这显然是不成立的。

NLP中：LSTM将一个句子看作是一段具有依赖关系的单词，以递增的方式对句子的语义向量进行编码。当到达句子末尾时，语义向量已经嵌入了所有单词的语义及之间的依赖关系，可以将其视为整个句子的有效特征表示。

作者类比：设计了一个Siamese结构，每个LSTM单元在每个时间步上依次接受一个输入，当到达最后一个指令嵌入时，最后一层的最后一个LSTM单元提供基本块的语义表示。最后，将两个基本块的相似度视为两个块嵌入的距离。

### Path similarity comparison

### Component similarity comparison

### Insight & Conclusion
