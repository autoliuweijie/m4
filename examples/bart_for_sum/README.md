# Summarization

## Finetune

```python3
CUDA_VISIBLE_DEVICES='0,1,2,3,4,5,6,7' nohup python3 -u finetune_summarization_model_with_ddp.py \
    --model_name bart-base \
    --init_model_path ./models/bart-base/ \
    --output_model_path ./models/bart-base-cnndm/ \
    --batch_size 8 --max_length 512 --num_train_epochs 3 --learning_rate 1e-4 \
    --train_dataset ./data/CNNDM/train.tsv \
    --valid_dataset ./data/CNNDM/valid.tsv \
    --test_dataset ./data/CNNDM/test.tsv \
    > train.log &
```

## Evaluation

```python3
python3 -u evaluate_summarization_model.py \
    --model_name bart-base \
    --model_path ./models/bart-base-cnndm/ \
    --batch_size 8 --max_length 512 --gen_kwargs bart-cnndm --num_workers 2 \
    --test_dataset ./data/CNNDM/test.tsv \
    --output ./data/CNNDM/result.tsv
```