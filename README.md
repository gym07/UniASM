# UniASM

This is the official repository for UniASM, which is a pre-train Language model for Binary Code Similarity Detection (BCSD) tasks. Currently supported platforms: x86_64.

You can find the pre-trained model [here](https://github.com/gym07/UniASM/releases/download/v1.0/uniasm_base.h5). 



## Acknowledgement:

This implementation is based on [bert4keras](https://github.com/bojone/bert4keras), [SimBERT](https://github.com/ZhuiyiTechnology/simbert) and [Asm2Vec-pytorch](https://github.com/oalieno/asm2vec-pytorch).



## Requirements:

- Tensorflow >= 2.4
- python3
- Radare2 (optional, for ASM files generation)



We use the following commands to initialize the conda environment:

```
conda create -n uniasm python=3.8
conda activate uniasm
pip install numpy==1.19.5 tensorflow==2.5.0 bert_pytorch scikit-learn==1.2.0 pandas==1.4.4 transformers==4.25.1 matplotlib==3.6.2 tqdm
```



## 1. Generate ASM files

```
python bin2asm.py -i testdata\bin\elfedit-gcc-o0 -o testdata\out-elfedit-gcc-o0
```



## 2. Generate embedding for ASM function

```
python embedding.py testdata\out-elfedit-gcc-o0\dbg.adjust_relative_path
```

outputs:

```
100%|███████████████████████████████████| 1/1 [00:00<?, ?it/s]
[ 0.71376026  0.9913202  -0.8564607   0.928958    0.674275    0.2007347
  0.9964851  -0.9999651  -0.99792427 -0.9964269   0.6482425  -0.99827206
  ...
 -0.38122872 -0.99985945  0.9994267   0.8081971   0.97346854  0.9234201
 -0.58380216  0.90942395  0.99129915 -0.99984354 -0.05967106  0.9671064 ]
```



## 3. Calculate the similarity of two ASM functions

```
python similarity.py testdata\out-elfedit-gcc-o0\dbg.adjust_relative_path testdata\out-elfedit-gcc-o1\dbg.adjust_relative_path
```

outputs:

```
100%|███████████████████████████████████| 1/1 [00:00<00:00, 977.01it/s]
100%|███████████████████████████████████| 1/1 [00:00<00:00, 972.25it/s]
0.91649896
```



## 4. Re-train UniASM

**Step 1**, create the training dataset.

```
python train_dataset.py
```



**Step 2**, train the model.

```
python train.py
```

