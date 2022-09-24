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

Working...