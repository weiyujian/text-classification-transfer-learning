## README
- 迁移学习思想用于文本分类
- domain网络现在一个大的数据集上训练出一个基模型，然后在目标数据集上训练的时候，
- 将基模型的参数restore给目标模型，从而加快收敛且提高准确率。
- domain网络 text_cnn_domain和目标网络text_cnn可以相同也可以不同，如果不同的话，
- 则共享参数部分的网络必须相同。比如，基模型是一个1000分类，但是目标模型仅是10分类
- 那么最后一层全连接层的参数就不能restore，这部分的变量需重新训练

## Training

```
#领域模型训练
CUDA_VISIBLE_DEVICES=0 python train_domain.py --model_version=domain

#训练好之后选择在验证集上表现最好的模型,训练目标模型
CUDA_VISIBLE_DEVICES=0 python train.py --model_version=***
```

## Evaluating

```
CUDA_VISIBLE_DEVICES=0 python eval.py --checkpoint_dir=./runs/***/checkpoints/
```
