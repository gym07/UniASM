# UniASM

This is the official repository for UniASM, which is a pre-train Language model for Binary Code Similarity Detection (BCSD) tasks. Currently supported platforms: x86_64.

You can find the pre-trained model at [kaggle](https://www.kaggle.com/datasets/littledj/uniasm-pretrained-model/download?datasetVersionNumber=1): 



## Acknowledgement:

This implementation is based on [bert4keras](https://github.com/bojone/bert4keras), [SimBERT](https://github.com/ZhuiyiTechnology/simbert) and [Asm2Vec-pytorch](https://github.com/oalieno/asm2vec-pytorch).



## Requirements:

- Tensorflow >= 2.4
- Radare2 (optional, for ASM files generation)



## 1. Generate ASM files

```
python bin2asm.py -i testdata\bin\elfedit-gcc-o0 -o testdata\out-elfedit-gcc-o0
```



## 2. Generate embedding for ASM function

```
python embedding.py testdata\bfd_coff_gc_keep
```

outputs:

```
100%|███████████████████████████████████| 1/1 [00:00<?, ?it/s]
[ 0.10191602  0.9945721   0.99785066  0.9999895  -0.9999946   0.585041
  0.16400526  0.39048684 -0.982188   -0.9025699   0.9975684  -0.99533683
  ...
 -0.26505318  0.9999827   0.999393   -0.99974316  0.33585668 -0.96132857
  0.97931385 -0.96559024  0.04376203 -0.9998853  -0.9984222   0.7902496 ]
```



## 3. Calculate similarity for two ASM functions

```
python similarity.py testdata\out-elfedit-gcc-o0\dbg.adjust_relative_path testdata\out-elfedit-gcc-o1\dbg.adjust_relative_path
```

outputs:

```
100%|███████████████████████████████████| 1/1 [00:00<00:00, 977.01it/s]
100%|███████████████████████████████████| 1/1 [00:00<00:00, 972.25it/s]
0.95588565
```



