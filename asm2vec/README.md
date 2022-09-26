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

