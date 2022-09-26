## Model environment

```
python setup.py install
```


## Model Implementation

```bash
python scripts/bin2asm.py -i /bin/ -o asm/
```

First generate asm files from binarys under `/bin/`.  

```bash
python scripts/train.py -i asm/ -l 100 -o model.pt --epochs 100
```

Try to train the model using only 100 functions and 100 epochs for a taste.  
Then you can use more data if you want.

```bash
python scripts/test.py -i asm/123456 -m model.pt
```

After you train your model, try to grab an assembly function and see the result.  
This script will show you how the model perform.  

```bash
python compare.py -i1 asm/123456 -i2 asm/654321 -m model.pt -e 30
```

```
cosine similarity : 0.873684
```
Get the similarity score of two binaries.

## Model explanation

* Training：构造网络模型，将一系列汇编函数作为训练数据进行训练
* Produce：经过训练，为每个函数生成一个vector
* Estimate：使用模型生成目标函数的vector
* Compare：与数据库中的vector表示进行cosine计算，获取已知数据集种排名前k的相似函数

## Discussion & Future
* 应该是因为19年，还算是比较早的提出将NLP知识应用到asm，所以可以上SP。现在看，结合别的survey文章，asm2vec的原理是可以借鉴的，但是这篇文章的模型从结果上看并不是很好。
* asm2vec受编译变量改变的数量的影响，也就是鲁棒性并不是很好。同时，训练效率也是同等几个ml模型中比较低的。在非官方的数据集中，结果显示模型准确度也很低。
* 未来几天打算用Security22上提供的数据集以及code复现一下，并与同等的其他几个ml模型在同一数据集上实验。

