# PEAN
code implementation for paper: [A Novel Multimodal Deep Learning Framework for Encrypted Traffic Classification](https://ieeexplore.ieee.org/abstract/document/9931999)

**If you find this method helpful for your research, please cite this paper:**

```
@article{lin2022novel,
  title={A Novel Multimodal Deep Learning Framework for Encrypted Traffic Classification},
  author={Lin, Peng and Ye, Kejiang and Hu, Yishen and Lin, Yanying and Xu, Cheng-Zhong},
  journal={IEEE/ACM Transactions on Networking},
  year={2022},
  publisher={IEEE},
  volume={},
  number={},
  pages={1-16},
  doi={10.1109/TNET.2022.3215507}
}
```

## Requirements
- Pytorch=1.2.0
- torchvision=0.2.0
- cudatoolkit=10.0
- python 3.6
- transformers=3.0.2 (refer to: [huggingface/transformers](https://github.com/huggingface/transformers))

## Project Structure
After you run PEAN model, your directory structure should be like this:
```
../PEAN
|-- Config
|   |-- pretrain_config.json
|   `-- vocab.txt
|-- DataCache (Generated)
|   `-- sni_whs_10_400_10.txt  (data cache, for easily rerun model at next time)
|-- Model (Generated)
|   |-- log 
|   |-- loss
|   |-- pretrain (where the pretrained model is saved)
|   |-- record
|   `-- save (where the model is saved)
|-- TrafficData
|   |-- class.txt
|   |-- pretrain_test.txt
|   |-- pretrain_train.txt
|   `-- sni_whs_train.txt
|-- PEAN_model.py (core code for PEAN model)
|-- TRF.py        (an implementation of transformer)
|-- config.py     (config for PEAN)
|-- main.py       (main file to run the model)
|-- pretrain.py   (pretrian code)
|-- train_eval.py (implementation of training and eval)
`-- utils.py      (utils)
```

**Some of the above files are missing, the complete codes will be released after the paper is accepted**

## Quick Start
- The quickest way to use PEAN is (raw bytes + length sequence + improved loss): 
```shell
cd ./PEAN
python main.py --imploss True
```
- Only use bytes
```shell
cd ./PEAN
python main.py --feature raw
```
- Only use length sequence
```shell
cd ./PEAN
python main.py --feature length
```
- Change the packet number (default: 10)
```shell
cd ./PEAN
python main.py --pad_num 12 --pad_len_seq 12
```
- Change the byte number (default: 400)
```shell
cd ./PEAN
python main.py --pad_len 500
```
- if you want to pretrain, you must first:;
```shell
cd ./PEAN
python pretrain.py
```
and then: 
```shell
python main.py --embway pretrain --imploss True
```

## Data format
- We provide a small number of training samples (`sni_whs_train.txt`) to help you run our model quickly. However, to fully evaluate PEAN, you may need to build your own training and pretraining dataset. The data format for them are described as follows:
- The training dataset is in `sni_whs_train.txt`, each row is a flow sample, which is composed of byte of each packet, length sequence and the label, each content is separated by `\t`. Like this: (**The space and `\t` may not be clearly distinguished in the following content**)
```
b0 b5 01 bb 22 b3 c6 0f 39 62 aa 12 50 18 fd 20 a4 c0 00 00 16 03 01 02 00 01 00 01 fc 03 03 e6 21 91 26 74 2d ba c8 18 41 cd bb 0e 38 eb c3 0a 7a 9b 3a 26 42 77 e6 4f cc 61 4a bf 0c f6 c9 20 68 55 34 f7 0d da 19 9d 50 fa 43 57 9d f5 de a2 70 c4 64 e5 aa 0e 4b bc 57 3c 7e 98 82 16 f0 64 00 22 c0 2b c0 2f c0 2c c0 30 cc a9 cc a8 cc 14 cc 13 c0 09 c0 13 c0 0a c0 14 00 9c 00 9d 00 2f 00 35 00 0a 01 00 01 91 ff 01 00 01 00 00 00 00 11 00 0f 00 00 0c 68 6d 2e 62 61 69 64 75 2e 63 6f 6d 00 17 00 00 00 23 00 68 68 be b2 14 2e 77 00 e5 f6 08 b7 5c d3 67 1c 77 c0 26 67 ce d0 b6 11 72 40 f7 d1 e7 88 64 64 d6 30 50 f7 e3 99 7b 98 2b 7f 27 43 ca b3 60 13 3e c9 f0 18 cf 54 c0 46 57 d3 2b dc 57 23 b2 d1 4c af 47 58 a7 83 c5 fc 9e 92 23 6c c0 6d c6 c6 e5 46 62 cb 3f 12 e7 e8 45 07 f5 25 1c 27 ae 9e 78 ff 33 f7 68 2a db 1f f5 00 0d 00 12 00 10 06 01 06 03 05 01 05 03 04 01 04 03 02 01 02 03 00 05 00 05 01 00 00 00 00 00 12 00 00 00 10 00 0e 00 0c 02 68 32 08 68 74 74 70 2f 31 2e 31 75 50 00 00 00 0b 00 02 01 00 00 0a 00 08 00 06 00 1d 00 17 00 18 00 18 00 04 00 06 01 02 00 15 00 b0 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00	01 bb b0 b5 39 62 aa 12 22 b3 c8 14 50 18 3c b8 67 80 00 00 16 03 03 00 5b 02 00 00 57 03 03 5b 23 1c 8a 41 b5 94 bc 2e 1a 72 a3 20 5d f3 c2 95 bd 1c 7d be 74 9f 1e 7a 6b 1e 75 67 76 df fe 20 68 55 34 f7 0d da 19 9d 50 fa 43 57 9d f5 de a2 70 c4 64 e5 aa 0e 4b bc 57 3c 7e 98 82 16 f0 64 c0 2f 00 00 0f 00 10 00 0b 00 09 08 68 74 74 70 2f 31 2e 31	01 bb b0 b5 39 62 aa 72 22 b3 c8 14 50 18 3c b8 55 84 00 00 14 03 03 00 01 01	01 bb b0 b5 39 62 aa 78 22 b3 c8 14 50 18 3c b8 cd 35 00 00 16 03 03 00 28 00 00 00 00 00 00 00 00 8e 86 8e e0 3a fa ed 0b 4e c7 30 b4 a7 63 36 26 c0 b2 d7 8c 78 04 93 3b 8d 0d a2 1c 0f 8d 9d b5	b0 b5 01 bb 22 b3 c8 14 39 62 aa a5 50 18 fc 8d 83 25 00 00 14 03 03 00 01 01 16 03 03 00 28 00 00 00 00 00 00 00 00 c1 c7 59 02 64 19 f8 d2 38 2b 80 6d e1 db 5a 00 22 01 73 15 a9 09 7d 3f ac 0a d3 ef 66 78 17 d3	01 bb b0 b5 39 62 aa a5 22 b3 c8 48 50 18 3c b8 91 b9 00 00 15 03 03 00 1a 00 00 00 00 00 00 00 01 7d 19 25 c0 17 3e 6d 33 b9 04 d3 98 21 b6 3c d5 39 34	537 116 26 65 71 51	5
``` 
For example, the above sample has 6 packets, 'b0 b5 ... 39 34' is the bytes of this 6 packets (separated by `\t`). '537 116 26 65 71 51' is the length sequence of the flow. '5' is the label of the flow.
- The data for pretrian are in `pretrain_train.txt` and `pretrain_test.txt`, which are composed of byte of some packet (e.g. 10 packets). The pretrianing donot need label and length sequence, so a sample of pretrain is like this:
```
de 8d 01 bb cc 99 aa 9a 71 5e cf 8f 50 18 ff ff f0 95 00 00 16 03 01 00 f3 01 00 00 ef 03 03 cf 3e 77 7d 18 38 97 85 59 45 f5 1b 4f ab 5f fb 80 45 d8 f1 b6 2e 14 81 57 5a f7 66 4e fe 62 0f 20 c0 df 79 77 f4 c0 34 37 56 55 e6 54 3f f3 e9 31 aa da 13 0d b7 96 42 1c 7c 14 11 c2 ea 78 ac 0c 00 28 c0 2c c0 2b c0 24 c0 23 c0 0a c0 09 cc a9 c0 30 c0 2f c0 28 c0 27 c0 14 c0 13 cc a8 00 9d 00 9c 00 3d 00 3c 00 35 00 2f 01 00 00 7e ff 01 00 01 00 00 00 00 15 00 13 00 00 10 61 63 73 2e 6d 2e 74 61 6f 62 61 6f 2e 63 6f 6d 00 17 00 00 00 0d 00 14 00 12 04 03 08 04 04 01 05 03 08 05 05 01 08 06 06 01 02 01 00 05 00 05 01 00 00 00 00 33 74 00 00 00 12 00 00 00 10 00 1b 00 19 08 73 70 64 79 2f 33 2e 31 06 73 70 64 79 2f 33 08 68 74 74 70 2f 31 2e 31 00 0b 00 02 01 00 00 0a 00 0a 00 08 00 1d 00 17 00 18 00 19	01 bb de 8d 71 5e cf 8f cc 99 ab 92 50 10 1c 84 c9 df 00 00 16 03 03 00 6c 02 00 00 68 03 03 f9 91 bf 2f 1d 16 b5 ae a7 ed 34 c6 53 f6 9c 60 45 ac e6 5a 61 2b ff 29 a8 9a c4 7e 22 73 a7 21 20 cb 37 16 b8 3d ef 3a f4 2d 97 7f 23 e7 84 2b ac 3a 52 55 9f 65 1c e1 c3 ff 98 2c d4 b9 4a 17 74 c0 2b 00 00 20 00 00 00 00 ff 01 00 01 00 00 0b 00 04 03 00 01 02 00 10 00 0b 00 09 08 73 70 64 79 2f 33 2e 31 16 03 03 12 c5 0b 00 12 c1 00 12 be 00 0e 4b 30 82 0e 47 30 82 0d 2f a0 03 02 01 02 02 0c 33 57 36 62 d7 f2 a4 6b d2 d1 d8 f9 30 0d 06 09 2a 86 48 86 f7 0d 01 01 0b 05 00 30 66 31 0b 30 09 06 03 55 04 06 13 02 42 45 31 19 30 17 06 03 55 04 0a 13 10 47 6c 6f 62 61 6c 53 69 67 6e 20 6e 76 2d 73 61 31 3c 30 3a 06 03 55 04 03 13 33 47 6c 6f 62 61 6c 53 69 67 6e 20 4f 72 67 61 6e 69 7a 61 74 69 6f 6e 20 56 61 6c 69 64 61 74 69 6f 6e 20 43 41 20 2d 20 53 48 41 32 35 36 20 2d 20 47 32 30 1e 17 0d 31 38 30 36 31 34 30 32 32 37 30 39 5a 17 0d 31 38 31 31 30 34 31 33 30 36 30 34 5a 30 79 31 0b 30 09 06 03 55 04 06 13 02 43 4e 31 11 30 0f 06 03 55 04 08 13 08 5a 68 65 4a 69 61 6e 67 31 11 30 0f 06 03 55 04 07 13 08 48 61 6e 67 5a 68 6f 75 31 2d 30 2b 06 03 55 04 0a 13 24 41 6c 69 62 61 62 61 20 28 43 68 69 6e 61 29 20 54 65 63 68 6e 6f 6c 6f 67 79 20 43 6f 2e 2c 20 4c 74 64 2e 31 15 30 13 06 03 55 04 03 0c 0c 2a 2e 74 61 6f 62 61 6f 2e 63 6f 6d 30 59 30 13 06 07 2a 86 48 ce 3d 02 01 06 08 2a 86 48 ce 3d 03 01 07 03 42 00 04 df d9 d5 da 22 06 67 51 a4 37 e4 7f ed db da cb 7e a0 0c 37 05 92 fa ab f8 ff e4 57 73 b6 00 18 c8 0a 30 55 58 51 06 34 f5 a8 ef 3d a1 ec db e3 b5 9d 4c 3f 5a 35 9a c1 ee 4f 59 1d 31 86 46 48 a3 82 0b ab 30 82 0b a7 30 0e 06 03 55 1d 0f 01 01 ff 04 04 03 02 03 88 30 81 a0 06 08 2b 06 01 05 05 07 01 01 04 81 93 30 81 90 30 4d 06 08 2b 06 01 05 05 07 30 02 86 41 68 74 74 70 3a 2f 2f 73 65 63 75 72 65 2e 67 6c 6f 62 61 6c 73 69 67 6e 2e 63 6f 6d 2f 63 61 63 65 72 74 2f 67 73 6f 72 67 61 6e 69 7a 61 74 69 6f 6e 76 61 6c 73 68 61 32 67 32 72 31 2e 63 72 74 30 3f 06 08 2b 06 01 05 05 07 30 01 86 33 68 74 74 70 3a 2f 2f 6f 63 73 70 32 2e 67 6c 6f 62 61 6c 73 69 67 6e 2e 63 6f 6d 2f 67 73 6f 72 67 61 6e 69 7a 61 74 69 6f 6e 76 61 6c 73 68 61 32 67 32 30 56 06 03 55 1d 20 04 4f 30 4d 30 41 06 09 2b 06 01 04 01 a0 32 01 14 30 34 30 32 06 08 2b 06 01 05 05 07 02 01 16 26 68 74 74 70 73 3a 2f 2f 77 77 77 2e 67 6c 6f 62 61 6c 73 69 67 6e 2e 63 6f 6d 2f 72 65 70 6f 73 69 74 6f 72 79 2f 30 08 06 06 67 81 0c 01 02 02 30 09 06 03 55 1d 13 04 02 30 00 30 49 06 03 55 1d 1f 04 42 30 40 30 3e a0 3c a0 3a 86 38 68 74 74 70 3a 2f 2f 63 72 6c 2e 67 6c 6f 62 61 6c 73 69 67 6e 2e 63 6f 6d 2f 67 73 2f 67 73 6f 72 67 61 6e 69 7a 61 74 69 6f 6e 76 61 6c 73 68 61 32 67 32 2e 63 72 6c 30 82 08 da 06 03 55 1d 11 04 82 08 d1 30 82 08 cd 82 0c 2a 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 12 61 70 69 2e 65 6e 74 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 19 63 6c 69 63 6b 2e 6d 7a 2e 73 69 6d 62 61 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 19 63 6c 69 63 6b 2e 74 7a 2e 73 69 6d 62 61 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 14 6d 2e 73 65 72 76 69 63 65 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 13 6f 70 65 6e 2e 61 6d 70 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 16 70 61 63 2e 70 61 72 74 6e 65 72 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 1b 70 72 65 2d 74 65 73 74 31 2e 6e 65 78 74 62 69 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 1e 70 72 65 2d 74 65 73 74 31 2e 77 73 2d 6e 65 78 74 62 69 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 19 73 2e 69 6a 69 70 69 61 6f 2e 74 72 69 70 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 18 73 2e 6a 69 70 69 61 6f 2e 74 72 69 70 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 1b 73 68 6f 77 63 61 73 65 2e 64 69 73 70 6c 61 79 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 18 74 6d 61 74 63 68 2e 73 69 6d 62 61 32 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 14 74 72 61 63 65 2e 63 70 73 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 0e 2a 2e 32 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 0f 2a 2e 61 69 2e 74 61 6f 62 61 6f 2e 63 6f 6d 82 16 2a	01 bb de 8d 71 5e df 8f cc 99 ab 92 50 18 1c 84 39 eb 00 00 cc 70 a5 9d 20 c3 0e 53 3f 7e c0 4e c2 98 49 ca 47 d5 23 ef 03 34 85 74 c8 a3 02 2e 46 5c 0b 7d c9 88 9d 4f 8b f0 f8 9c 6c 8c 55 35 db bf f2 b3 ea fb e3 56 e7 4a 46 d9 13 22 ca 36 d5 9b c1 a8 e3 96 43 93 f2 0c bc e6 f9 e6 e8 99 c8 63 48 78 7f 57 36 69 1a 19 1d 5a d1 d4 7d c2 9c d4 7f e1 80 12 ae 7a ea 88 ea 57 d8 ca 0a 0a 3a 12 49 a2 62 19 7a 0d 24 f7 37 eb b4 73 92 7b 05 23 9b 12 b5 ce eb 29 df a4 14 02 b9 01 a5 d4 a6 9c 43 64 88 de f8 7e fe e3 f5 1e e5 fe dc a3 a8 e4 66 31 d9 4c 25 e9 18 b9 89 59 09 ae e9 9d 1c 6d 37 0f 4a 1e 35 20 28 e2 af d4 21 8b 01 c4 45 ad 6e 2b 63 ab 92 6b 61 0a 4d 20 ed 73 ba 7c ce fe 16 b5 db 9f 80 f0 d6 8b 6c d9 08 79 4a 4f 78 65 da 92 bc be 35 f9 b3 c4 f9 27 80 4e ff 96 52 e6 02 20 e1 07 73 e9 5d 2b bd b2 f1 02 03 01 00 01 a3 82 01 25 30 82 01 21 30 0e 06 03 55 1d 0f 01 01 ff 04 04 03 02 01 06 30 12 06 03 55 1d 13 01 01 ff 04 08 30 06 01 01 ff 02 01 00 30 1d 06 03 55 1d 0e 04 16 04 14 96 de 61 f1 bd 1c 16 29 53 1c c0 cc 7d 3b 83 00 40 e6 1a 7c 30 47 06 03 55 1d 20 04 40 30 3e 30 3c 06 04 55 1d 20 00 30 34 30 32 06 08 2b 06 01 05 05 07 02 01 16 26 68 74 74 70 73 3a 2f 2f 77 77 77 2e 67 6c 6f 62 61 6c 73 69 67 6e 2e 63 6f 6d 2f 72 65 70 6f 73 69 74 6f 72 79 2f 30 33 06 03 55 1d 1f 04 2c 30 2a 30 28 a0 26 a0 24 86 22 68 74 74 70 3a 2f 2f 63 72 6c 2e 67 6c 6f 62 61 6c 73 69 67 6e 2e 6e 65 74 2f 72 6f 6f 74 2e 63 72 6c 30 3d 06 08 2b 06 01 05 05 07 01 01 04 31 30 2f 30 2d 06 08 2b 06 01 05 05 07 30 01 86 21 68 74 74 70 3a 2f 2f 6f 63 73 70 2e 67 6c 6f 62 61 6c 73 69 67 6e 2e 63 6f 6d 2f 72 6f 6f 74 72 31 30 1f 06 03 55 1d 23 04 18 30 16 80 14 60 7b 66 1a 45 0d 97 ca 89 50 2f 7d 04 cd 34 a8 ff fc fd 4b 30 0d 06 09 2a 86 48 86 f7 0d 01 01 0b 05 00 03 82 01 01 00 46 2a ee 5e bd ae 01 60 37 31 11 86 71 74 b6 46 49 c8 10 16 fe 2f 62 23 17 ab 1f 87 f8 82 ed ca df 0e 2c df 64 75 8e e5 18 72 a7 8c 3a 8b c9 ac a5 77 50 f7 ef 9e a4 e0 a0 8f 14 57 a3 2a 5f ec 7e 6d 10 e6 ba 8d b0 08 87 76 0e 4c b2 d9 51 bb 11 02 f2 5c dd 1c bd f3 55 96 0f d4 06 c0 fc e2 23 8a 24 70 d3 bb f0 79 1a a7 61 70 83 8a af 06 c5 20 d8 a1 63 d0 6c ae 4f 32 d7 ae 7c 18 45 75 05 29 77 df 42 40 64 64 86 be 2a 76 09 31 6f 1d 24 f4 99 d0 85 fe f2 21 08 f9 c6 f6 f1 d0 59 ed d6 56 3c 08 28 03 67 ba f0 f9 f1 90 16 47 ae 67 e6 bc 80 48 e9 42 76 34 97 55 69 24 0e 83 d6 a0 2d b4 f5 f3 79 8a 49 28 74 1a 41 a1 c2 d3 24 88 35 30 60 94 17 b4 e1 04 22 31 3d 3b 2f 17 06 b2 b8 9d 86 2b 5a 69 ef 83 f5 4b c4 aa b4 2a f8 7c a1 b1 85 94 8c f4 0c 87 0c f4 ac 40 f8 59 49 98 16 03 03 00 93 0c 00 00 8f 03 00 17 41 04 3d d5 76 39 49 0c 54 11 bc f7 b9 f8 95 f0 0d 8e a0 e3 ec 74 f7 cf e9 d0 35 2a a9 aa 3a ed 40 78 5c 63 2d 7c f1 7a 8c 16 af fd db ae 6d 58 f0 5c e8 51 8a b2 18 b3 93 d9 25 7a 0c e7 69 22 a5 70 05 03 00 46 30 44 02 20 3b f5 fd 39 90 77 bd 59 15 5c 16 df e3 2f 0d 58 e8 15 55 5b 26 2d 86 bb 8e 86 a1 30 bd 0b 9d 5b 02 20 1a ee f9 8b 7b 7d 84 a3 15 78 b7 2c 03 cd 7d 84 f2 ad 72 ab da 46 b9 64 76 98 b5 db a7 f1 5e bd 16 03 03 00 04 0e 00 00 00	de 8d 01 bb cc 99 ab 92 71 5e e3 6b 50 18 ff ff 65 bd 00 00 16 03 03 00 46 10 00 00 42 41 04 d8 e8 ad 21 b1 4b e9 e1 75 39 f4 99 69 af b5 6c 5d ab 97 f5 3f eb bb ec 2b d1 81 0e 04 1a 21 69 13 60 6b e4 f2 43 29 8a 9e f0 54 a9 c1 1a 53 d3 bd 2f 8e 41 13 be 4b 99 2a 36 41 8f 62 aa 88 9c 14 03 03 00 01 01 16 03 03 00 28 00 00 00 00 00 00 00 00 0a ea 53 52 b4 b0 3d 38 51 93 c0 70 b4 f4 f9 78 9e 6f 1d d6 f5 fe a4 ca 01 bc 6a c7 f8 ed df 4c	01 bb de 8d 71 5e e3 6b cc 99 ac 10 50 18 1c 84 c8 eb 00 00 14 03 03 00 01 01 16 03 03 00 28 b1 d7 c1 56 26 f4 e0 53 20 ad ec 6c 9c 1e a7 03 a0 40 1c ff 22 04 08 7b 51 bc a5 04 22 78 09 53 e9 e8 56 68 20 6e 03 36	01 bb de 8d 71 5e e3 9e cc 99 ac 10 50 18 1c 84 ef 4c 00 00 17 03 03 00 44 b1 d7 c1 56 26 f4 e0 54 bb dd 66 12 29 46 30 70 ad 7f 65 ae f9 8f de 98 68 3c 8d 62 c0 e4 db 4f 27 ee c3 70 0b 7b 1c 2a 75 0a df be d4 60 74 2c 7e 0e 6f d3 8d 67 17 8d dc fb 92 15 97 ac 8b 7a 70 40 d9 d4	de 8d 01 bb cc 99 ac 10 71 5e e3 e7 50 18 ff ff 11 9e 00 00 17 03 03 05 08 00 00 00 00 00 00 00 01 51 29 48 f1 0f 41 b5 9b 2e b5 25 1e 0d 1b 19 86 58 4d 65 af 2c 86 f5 20 90 b5 dd af c0 7f ea 64 4a 19 60 e8 59 d9 ce 5f 32 14 eb 18 f7 b5 dd b2 61 78 e6 41 9e 7e a3 e1 36 85 26 9f c7 f7 a5 76 5d 20 50 de 27 0c 23 11 90 e4 98 56 6f e8 69 8e 7f f4 46 0a 19 3b 71 4b b9 1e 61 81 22 58 e8 88 88 31 fb 9e ea 0b ad 32 5b c8 b8 2a b3 91 cb 2d 85 1b 43 62 18 8f cd 16 d6 ce aa 9a f8 78 00 49 cc 8a b7 f8 4c 85 25 7b f6 aa a7 86 9d f8 98 86 f8 0d 87 a5 cb c1 fc c3 62 4d 8e fb 7d cd 79 3b 79 ca 78 91 82 2d 8a 47 10 41 ce 89 74 b6 c4 44 25 07 8b 4c 04 38 1c b2 2b 8b 76 e1 a3 58 ca b6 d4 2f 81 a3 a4 53 dd 3e db a2 84 35 8b 67 22 ae f7 ed ae 8c 16 08 61 9e 04 57 ff bb 69 d4 50 a0 db 37 a5 2b 2d ca b0 b5 a1 25 f8 23 0e de 8f 76 6e 96 80 84 9d c1 cd 55 f5 0d 8f 24 94 02 11 e3 e0 f7 bd 29 ef 4a a3 8e c6 0e 8b 9e 32 c7 23 b3 5c eb e9 47 87 7d fd ee cb 6a 1a e9 55 89 d0 7c ab 02 7d 60 2f 4e 50 21 d2 6a 11 e3 87 a4 e9 60 0d 5a 57 b2 b0 ad e5 be 4f 66 1c 8f 7c 1f 8f f3 f2 d5 60 d8 59 ab 7b b4 a2 b1 24 b0 91 67 25 6b 6f 2b ca f0 50 79 c5 10 8f 8e a3 58 08 bd c0 00 9d 87 2d 13 b6 ed e7 52 a7 df dd a7 1e 83 0a b3 f1 0d 80 54 36 c1 ef 72 6a f8 32 81 28 f0 95 ff 1e eb 6d 99 b4 60 64 a5 dc 23 fa 72 99 8e 7d 61 14 48 2b bb 6d 70 ce a2 10 1d e4 4a 23 b5 cb c0 75 76 44 a3 f5 fc 69 b1 78 49 36 a1 a8 a7 82 e5 fe 6e f8 fa b3 1e 6c 71 fc 6f ff 0d 1c 62 38 59 a9 ef 48 8c b8 7b 70 ac 4f 95 35 35 f1 0e 7e 03 c8 f8 de b3 1d 62 f7 ac 4b e3 5f 89 64 60 5e 7d 6a 8e 72 a5 07 ca 4b 0a 25 7b 64 18 3f 23 d5 ef 6c f0 30 fa 11 40 2f cb 9b 36 5f 44 77 75 fd 5a 11 93 6d 38 e5 88 3d 96 7a e8 9d f0 4f 31 3c d3 04 79 d5 63 39 ea 4d db 36 93 45 3a de e2 cd 39 0f 58 78 17 3a 01 da 31 3f ea 7f 6c 11 36 01 aa 85 db 76 dd b0 78 d9 39 ef b3 b8 fa d7 78 bf bb a7 56 13 f7 ed a1 a2 d1 c1 0a 11 84 76 d0 32 ae 44 27 c2 16 15 42 33 b4 c9 a5 63 c7 30 cb d7 f3 c2 5f 87 33 f1 b3 a0 6b 9a 47 dd 38 f0 da 99 87 5f c0 8e 03 63 84 b6 74 54 70 ab 48 7d af bd 17 5a 89 ed 40 a0 6a d1 70 27 f5 98 e1 82 d5 f7 ca 43 30 06 a1 74 12 84 06 00 f0 f7 31 4f 81 18 5a cc 4e 52 78 0b e7 ef ac f0 56 f8 30 17 05 cd a8 14 f2 4e 5d e6 19 5c a7 80 c8 67 d8 56 39 a8 92 69 38 4e c9 ff a6 10 c4 e3 8e 39 94 27 ff cd 0f 66 37 00 49 57 7a 00 a9 4a 93 25 e9 97 33 3b 15 11 9b b6 7d d5 4c 98 9c 20 ad 0c aa bc 15 0a b9 8f 13 53 23 6a 82 ab 6f 90 f8 67 64 67 d8 02 ef f2 1d c2 7f 5d 24 f4 fd 8b a5 1d 92 f1 9d d8 f9 6e 26 77 05 c5 71 dc b7 37 14 98 22 07 c0 2f 14 ae 70 1c f2 d7 b2 53 84 78 65 47 c6 07 09 93 e9 cc 4d 46 9a 0f 8f 60 ea 10 f5 24 b3 0e b6 18 71 ab c8 5d 0f 25 ec 13 ea d3 53 c8 62 9f 96 2f a4 1c 83 34 0a 7f 62 2c a5 be 7a ce c8 44 7d b0 3a c3 b3 c3 2e 7d cf a0 4b cd b5 0c a2 97 9e 5c cd 78 2e 45 5f bd d8 26 13 9e 1f 29 77 65 e4 38 95 fe 54 1f af 40 56 97 95 8c 33 58 bf 20 36 e1 8c d3 c3 ac fb 86 a6 29 87 db 7d 95 ba 23 7f 5f e4 d3 10 e8 40 7c 48 34 47 a6 ae 49 00 94 d0 4d de 70 9f a1 48 e5 7e d2 1e a8 a6 75 3d 48 d3 74 ec d5 84 cb 4c c5 45 cc 03 31 e2 59 9e 44 56 2a 58 3f 84 8f 23 7f d4 00 1b a0 4a 84 e0 6b 88 f8 48 b2 a7 23 4b 10 65 4f 27 20 f9 0a a5 b9 4f e0 de b0 1c d4 e6 ab d9 28 d8 eb 00 19 98 96 74 f3 57 67 f8 ba b2 40 a7 de 38 6d 64 5a 3e bb 34 a6 e5 0c 43 c6 ff 9c c6 d0 f3 86 80 f0 cf e5 6a 14 06 1d f0 6b 8e 84 4e 2b 04 97 7f 18 8a c1 b6 e1 9d a4 c7 31 3f 85 7f 4b 2c eb c0 61 fb 21 7b 3b eb 00 e7 57 95 f9 36 3c cd 88 78 28 46 4d 25 fe e7 26 18 fd e9 d9 e6 c2 a3 ce 42 69 3a ad 2d 06 13 22 f5 54 99 d3 72 b1 75 70 6e 57 af 95 ef 6f 2f f9 0a ec 96 e2 22 23 74 3e b4 7e 5c 33 ac 33 d3 f0 1b ca 70 ea 24 06 9c ab 2d 8f db 9f 5d 5b 67 a7 97 a1 1e 40 8a ee 2e 2b 90 bf d0 d7 92 36 c4 40 20 8c 18 de af 5d c0 bd e2 3f 9d 41 e8 06 e7 1c 1f 28 5d 59 fb 49 7b 73 61 07 8b 44 b6 33 e9 f1 2e 01 3f 5e e8 77 3a 98 b2 c9 9c 96 5e 38 1d 3a a9 0f 9f 25 f1 df c3 f1 51 f9 29 dd a9 d6 8e 75 27 e7 58 1b c9 4e 6a f8 08 3d f3 0e 7a 2d 6f c5 c4 9b 31 13 ce 59 7b ec 00 0d 78 32 83 b9 85	01 bb de 8d 71 5e e3 e7 cc 99 b1 1d 50 18 23 5b 91 30 00 00 17 03 03 01 d0 b1 d7 c1 56 26 f4 e0 55 44 8a a7 f0 f3 ea 1c 78 1e b3 05 69 f0 ac 8d ef 6f 51 2f 37 7f 93 c9 95 b4 f0 ab 5c 4f 2f 84 23 f9 0e 35 41 dd b4 7d c7 57 5e c2 88 64 df 5f 29 d0 8f 82 c6 1e bf 5b 07 a5 0d 8e 00 d7 f5 d8 e7 85 59 95 7e f4 9d f4 6f 5f 89 48 3a c8 7b 20 e9 cb 3a d2 bd 57 af d9 78 c1 7f 03 b8 1d cc 6e 4f dd cb e2 fe c3 e6 4e bf a7 c4 ee 45 3c 7d 07 f7 32 de 0b 3a 1a ca 1b e5 4c a2 c8 01 69 92 52 b7 cd c1 13 06 f3 52 e7 1f 0e 0e 0d 61 b2 00 bb a9 28 10 3c 33 a2 00 4f 41 ff 0b 89 cd e5 3a 3c e2 eb d7 b5 f6 b0 1a 6f 5d 77 08 8a 15 21 86 97 9a d7 e6 ed e1 26 6f 07 64 a0 4c cb 7a f0 26 45 a1 a5 35 1d 61 8b f5 8a 0e d2 2d 1b 1b 2d 4f 94 7e 89 9c d9 9e 05 35 3d 8b 19 36 fd 89 60 87 b2 0a 29 00 68 a2 17 aa 3d 85 a7 7b b8 0f b7 c8 b8 fc 64 5a 4d 5a 70 b7 08 d0 d0 1a b3 b1 0c fa 5f 2e 9f 04 a7 56 c0 d8 d1 b6 7b 77 c2 bb a8 0a 19 86 40 17 14 e6 0c ba 3e 55 d4 56 77 cc f3 23 6e 20 a2 f6 66 fc 27 3b b1 22 1f c9 f5 82 ba 5e db a1 bd d6 9c 49 f8 35 d9 4e 99 de 77 89 4a ff ad 5a 69 02 51 bb cd e4 a4 22 61 a8 26 ac fa 12 1b fe ed 6e 1e 91 75 3c 7d f9 d9 59 d1 83 cb 6a 8c 21 f0 60 f3 61 77 55 37 32 ae c4 12 87 33 31 f1 8c de 6b 62 69 88 70 39 fe 0a 88 1c b5 66 ab a1 bd dd bf e0 fe 97 6a 56 c1 8f e8 75 27 0f 34 0a a8 7e 33 a2 8c ad 4f 6b e8 07 b5 e1 9f 96 08 5f 65 e9 07 a7 16 14 a9 0b e0 d8 50 e3 a2 b5 32 a7 7e 82 d1 73 78 a1 66 e0 87 e6 2a 3c 8c 05 1f 06 17 78 46 1c 9e 34 e6 ff 68	01 bb de 8d 71 5e e5 bc cc 99 b1 1d 50 18 23 5b 4f 81 00 00 17 03 03 00 20 b1 d7 c1 56 26 f4 e0 56 d9 13 78 d3 a7 ba a1 61 61 4d 32 27 24 4b d1 b1 b4 d4 28 b9 27 5f dc a1	de 8d 01 bb cc 99 b1 1d 71 5e e5 e1 50 18 ff ff 58 54 00 00 17 03 03 00 28 00 00 00 00 00 00 00 02 7d 35 d1 6a e1 02 fd 80 54 7f dd 10 61 4c ff 8c b5 18 43 23 8a 90 59 f4 3c 6b f9 0a 71 9d 98 2b	01 bb de 8d 71 5e e5 bc cc 99 b1 1d 50 18 23 5b 4f 81 00 00 17 03 03 00 20 b1 d7 c1 56 26 f4 e0 56 d9 13 78 d3 a7 ba a1 61 61 4d 32 27 24 4b d1 b1 b4 d4 28 b9 27 5f dc a1
```
