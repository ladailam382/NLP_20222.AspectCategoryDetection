# Unsupervised Attention Based Aspect Extraction (ABAE)
Codes and Dataset for ACL2017 paper ‘‘An unsupervised neural attention model for aspect extraction’’. [(pdf)](http://aclweb.org/anthology/P/P17/P17-1036.pdf)

## Data
You can find the pre-processed datasets and the pre-trained word embeddings in [[Download]](https://drive.google.com/open?id=1L4LRi3BWoCqJt5h45J2GIAW9eP_zjiNc). The zip file should be decompressed and put in the main folder.

You can also download the original datasets of Restaurant domain and Beer domain in [[Download]](https://drive.google.com/open?id=1qzbTiJ2IL5ATZYNMp2DRkHvbFYsnOVAQ). For preprocessing, put the decompressed zip file in the main folder and run 
```
python preprocess.py
python word2vec.py
```
respectively in code/ . The preprocessed files and trained word embeddings for each domain will be saved in a folder preprocessed_data/.

## Train
Under code/ and type the following command for training:

Go to the `utils` folder adn run
```
python train.py \
--emb ../cache/w2v_embedding.vec \
--domain $domain \
-o output_dir \
```
where *$domain* is the corresponding domain, *--emb* is the path to the pre-trained word embeddings, *-o* is the path of the output directory. You can find more arguments/hyper-parameters defined in train.py with default values used in our experiments.

After training, two output files will be saved in code/output_dir/$domain/: 1) *aspect.log* contains extracted aspects with top 100 words for each of them. 2) *model_param* contains the saved model weights

## Evaluation
Under code/ and type the following command:
```
python evaluation.py \
--domain $domain \
-o output_dir \
```
Note that you should keep the values of arguments for evaluation the same as those for training (except *--emb*, you don't need to specify it), as we need to first rebuild the network architecture and then load the saved model weights.

This will output a file *att_weights* that contains the attention weights on all test sentences in code/output_dir/$domain.


## Requirements


You can install prerequirements, using the following command.

```
pip install -r requirements.txt
```

## Cite
If you use the code, please cite the following paper:
```
@InProceedings{he-EtAl:2017:Long2,
  author    = {He, Ruidan  and  Lee, Wee Sun  and  Ng, Hwee Tou  and  Dahlmeier, Daniel},
  title     = {An Unsupervised Neural Attention Model for Aspect Extraction},
  booktitle = {Proceedings of the 55th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)},
  month     = {July},
  year      = {2017},
  address   = {Vancouver, Canada},
  publisher = {Association for Computational Linguistics}
}
```





