## Handwriting generation
Implementation of handwriting generation with use of recurrent neural networks in tensorflow. Based on Alex Graves paper (https://arxiv.org/abs/1308.0850).

## How to train a model

#### 1. Download dataset
First you need to download this dataset ([data/original-xml-part.tar.gz](http://www.fki.inf.unibe.ch/databases/iam-on-line-handwriting-database/download-the-iam-on-line-handwriting-database)) and unpack it in repository directory.

#### 2. Preprocess dataset
```
python preprocess.py
```

This scipt searches local directory for `xml` files with handwriting data and does some preprocessing like normalizing data and spliting strokes in lines. As a result it should create `data` directory with preprocessed dataset.

#### 3. Train model
```
python train.py
```

This will launch training with default settings (for experimentation look at `argparse` options). By default it creates `summary` directory with separate `experiment` directories for each run. If you want to restore training provide a path to the experiment you want to continue. Like:
```
python train.py --restore=summary\experiment-0
```
You can lookup losses in command line or with tensorboard. Example loss plot:

![Loss plot](https://github.com/Grzego/handwriting-generation/blob/master/imgs/loss-plot.PNG)

With default settings training took about 5h (using tensorflow 1.2, with GTX 1080).


#### 4. Generate handwriting!
```
python generate.py --model=path_to_model
```

When model is trained you can use `generate.py` scipt to test how it works. Without providing `--text` argument this script will ask you what to generate in loop.

Additional options for generation:
* `--bias` (`float`) - with higher bias generated handwriting is more _clear_ so to speak (read paper for more info)
* `--noinfo` - plots only generated handwriting (without attention window)
* `--animation` - animation of writing

![example-1](https://github.com/Grzego/handwriting-generation/blob/master/imgs/example-1.PNG)

![example-2](https://github.com/Grzego/handwriting-generation/blob/master/imgs/example-2.gif)

_Samples were generated with bias set to 1._

Any feedback is welcome :smile: