
## Alpaca-LoRA

- 源码: https://github.com/tloen/alpaca-lora
- commit id : 9de612e582ab86013b5d1c3be6b0ed9f5ab2065a





## LoRA


### 7B

```
torchrun --nproc_per_node=8 --master_port=29005 finetune_metrics_epoch.py \
--base_model '/data/nfs/guodong.li/pretrain/hf-llama-model/llama-7b' \
--data_path '/home/guodong.li/llama-mp/GPT-4-LLM/data/alpaca_gpt4_data_zh.json' \
--output_dir '/home/guodong.li/output/alpaca-lora-7b-dp-zh' \
--batch_size 80 \
--micro_batch_size 10 \
--num_epochs 10 \
--cutoff_len=512 \
--group_by_length \
--lora_target_modules='[q_proj,k_proj,v_proj,o_proj]' \
--lora_r=16
```



| 模型 | 显存 | 耗时 | 数据量  |
| --- | --- | --- |  --- |
| 7B | 8 * 74G |  2小时5分钟 | 46818 |

![image](https://github.com/liguodongiot/llm-action/assets/13220186/238d86da-bbda-4944-94e4-49a87284e026)


### 13B




```
torchrun --nproc_per_node=8 --master_port=29005 finetune_metrics_epoch.py \
--base_model '/data/nfs/guodong.li/pretrain/hf-llama-model/llama-13b' \
--data_path '/home/guodong.li/llama-mp/GPT-4-LLM/data/alpaca_gpt4_data_zh.json' \
--output_dir '/home/guodong.li/output/alpaca-lora-13b-dp-zh' \
--batch_size 48 \
--micro_batch_size 6 \
--num_epochs 10 \
--cutoff_len=512 \
--group_by_length \
--lora_target_modules='[q_proj,k_proj,v_proj,o_proj]' \
--lora_r=16
```

| 模型 | 显存 | 耗时 | 数据量  |
| --- | --- | --- | --- |
| 13B | 8 * 76G |  2小时10分钟 | 46818 |

![image](https://github.com/liguodongiot/llm-action/assets/13220186/a66ea4a1-79fb-40d9-8a10-7a9132fde882)


### 30B

```
torchrun --nproc_per_node=8 --master_port=29005 finetune_metrics_epoch.py \
--base_model '/data/nfs/guodong.li/pretrain/hf-llama-model/llama-30b' \
--data_path '/home/guodong.li/llama-mp/GPT-4-LLM/data/alpaca_gpt4_data_zh.json' \
--output_dir '/home/guodong.li/output/alpaca-lora-30b-dp-zh-1' \
--batch_size 16 \
--micro_batch_size 2 \
--num_epochs 10 \
--cutoff_len=512 \
--group_by_length \
--lora_target_modules='[q_proj,k_proj,v_proj,o_proj]' \
--lora_r=16
```

训练过程：
```
trainable params: 51118080 || all params: 32580061696 || trainable%: 0.15689988704433913

{'train_runtime': 55949.6417, 'train_samples_per_second': 8.368, 'train_steps_per_second': 0.523, 'train_loss': 0.4879480355503537, 'epoch': 10.0}

100%|████████████████████████████████████████████████████████████████████████████████████████████| 29270/29270 [15:32:27<00:00,  1.91s/it]
```



| 模型 | 显存 | 耗时 | 数据量  |
| --- | --- | --- | --- |
| 30B | 8 * 75G |  15小时30分钟 | 46818 |

![image](https://github.com/liguodongiot/llm-action/assets/13220186/303b850c-3332-45aa-968d-bb0f52fa44a6)



```
torchrun --nproc_per_node=8 --master_port=29005 finetune.py \
--base_model '/data/nfs/guodong.li/pretrain/hf-llama-model/llama-30b' \
--data_path '/data/nfs/guodong.li/data/alpaca_data_cleaned.json' \
--output_dir '/home/guodong.li/output/alpaca-lora-30b-dp' \
--batch_size 96 \
--micro_batch_size 6 \
--num_epochs 3 
```



### 65B


```
torchrun --nproc_per_node=8 --master_port=29005 finetune.py \
--base_model '/data/nfs/guodong.li/pretrain/hf-llama-model/llama-65b' \
--data_path '/home/guodong.li/llama-mp/GPT-4-LLM/data/alpaca_gpt4_data_zh.json' \
--output_dir '/home/guodong.li/output/alpaca-lora-65b-dp-zh' \
--batch_size 8 \
--micro_batch_size 1 \
--num_epochs 3 
```

## 测试用例

```
请给我讲一个温馨的睡前故事
如何快速提升自己的写作能力？
计算以下表达式：(6+2)*(2-2)。
What are the five characteristics of a good argument?
```


## tensorboard

```
source /home/guodong.li/virtual-venv/alpara-lora-venv-py310-cu117/bin/activate

tensorboard --logdir /home/guodong.li/output/alpaca-lora-7b-dp-zh --port=16007 --host=0.0.0.0
tensorboard --logdir /home/guodong.li/output/alpaca-lora-13b-dp-zh --port=16008 --host=0.0.0.0
tensorboard --logdir /home/guodong.li/output/alpaca-lora-30b-dp-zh-1 --port=16009 --host=0.0.0.0
```




