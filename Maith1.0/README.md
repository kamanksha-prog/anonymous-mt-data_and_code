# Maithili-Hindi Translation Models

## IndicTrans2 Model

### 1. Create Project Structure
```bash
mkdir it2_maihin
mkdir MaitH 1.0
cd MaitH 1.0/it2_maihin
```

### 2. Create Experiment Folder
```bash
mkdir indic-indic-exp
cd indic-indic-exp
mkdir train devtest vocab final_bin
```

#### Folder Structure
```
indic-indic-exp
├── train
│   ├── mai_Deva-hin_Deva
│       ├── train.mai_Deva
│       └── train.hin_Deva
│
├── devtest
│   ├── all
│   ├── mai_Deva-hin_Deva
│       ├── dev.mai_Deva
│       ├── dev.hin_Deva
│       ├── test.mai_Deva
│       └── test.hin_Deva
│
├── vocab
│   ├── model.SRC
│   ├── model.TGT
│   ├── vocab.SRC
│   └── vocab.TGT
└── final_bin
    ├── dict.SRC.txt
    └── dict.TGT.txt
```

### 3. Install Dependencies
```bash
source install.sh
```

### 4. Clone IndicTrans2 Repository
```bash
git clone https://github.com/AI4Bharat/IndicTrans2
```

### 5. Data Preparation & Binarization
```bash
cd IndicTrans2
bash prepare_data_joint_finetuning.sh <exp_dir>
```

### 6. Finetuning
```bash
bash finetune.sh <exp_dir> <model_arch> <pretrained_ckpt>
```

### 7. Inference
```bash
bash joint_translate.sh <infname> <outfname> <src_lang> <tgt_lang> <ckpt_dir>
```

### 8. Evaluation: Compute BLEU4, chrF2, TER, COMET, METEOR, BERTScore Scores
```bash
cd ..
cd output
python BLEU4_chrF_TER_new.py
python COMET_METEOR.py
python BERTscore.py
```



## mT5 Model

### 1. Create Conda Environment
```bash
conda create --name hgftransformer
conda activate hgftransformer
mkdir hgftransformer
```

### 2. Install Requirements
```bash
pip install -r requirement.txt
```

### 3. Training
```bash
python3 S2T2/examples/pytorch/translation/run_translation.py \
    --model_name_or_path /home/hgftransformer/mt5 \
    --do_train --do_eval \
    --source_lang ma --target_lang hi --source_prefix "<2hi> " \
    --train_file /home/hgftransformer/data/train/train_mai_hin.json \
    --validation_file /home/hgftransformer/data/test/test_mai_hin.json \
    --test_file /home/hgftransformer/data/test/test_mai_hin.json \
    --output_dir checkpoints/mT5_mahi/ \
    --per_device_train_batch_size=2 \
    --per_device_eval_batch_size=4 \
    --num_train_epochs 7 \
    --predict_with_generate --save_strategy no \
    --metric_for_best_model bleu --overwrite_output_dir
```

### 4. Inference & BLEU Score Calculation
```bash
python3 S2T2/examples/pytorch/translation/run_translation.py \
    --model_name_or_path checkpoints_new/mT5_mahi \
    --do_predict \
    --source_lang ma --target_lang hi --source_prefix "<2hi> " \
    --validation_file /home/hgftransformer/data/test/test_mai_hin.json \
    --test_file /home/hgftransformer/data/test/test_mai_hin.json \
    --output_dir checkpoints_new/mT5_mahi/output \
    --per_device_eval_batch_size=4 \
    --predict_with_generate --overwrite_output_dir
```

### 5. ### 5. Compute BLEU4, chrF2, TER, COMET, METEOR, BERTScore Scores
```bash
python BLEU4_chrF_TER_new.py
python COMET_METEOR.py
python BERTscore.py
```

---

## mBART50 Model

### 1. Create Project Structure
```bash
mkdir mBART50_mai_hin
```

### 2. Download mBART50 Model from HuggingFace
Ensure that all dataset files are in `.json` format (e.g., `train.json`, `valid.json`, `test.json`).

### 3. Training
```bash
python3 S2T2/examples/pytorch/translation/run_translation.py \
    --model_name_or_path /media/mBART50_mai_hin/mbart \
    --do_train --do_eval \
    --source_lang ma_XX --target_lang hi_IN \
    --train_file /mBART50_mai_hin/data/train/train.json \
    --validation_file /mBART50_mai_hin/data/dev/dev.json \
    --test_file /mBART50_mai_hin/data/test/test.json \
    --output_dir checkpoint/mBART50_mai_hin/ \
    --per_device_train_batch_size=6 \
    --per_device_eval_batch_size=8 \
    --num_train_epochs 7 \
    --predict_with_generate --save_strategy no \
    --metric_for_best_model bleu --overwrite_output_dir \
    --logging_dir /mBART50_mai_hin/log --report_to tensorboard
```

### 4. Inference
```bash
python3 S2T2/examples/pytorch/translation/run_translation.py \
    --model_name_or_path checkpoint/mBART50_mai_hin/ \
    --do_predict \
    --source_lang ma_XX --target_lang hi_IN \
    --validation_file /media/mBART50_mai_hin/data/dev/dev.json \
    --test_file /media/mBART50_mai_hin/data/test/test.json \
    --output_dir /media/output \
    --per_device_eval_batch_size=4 \
    --predict_with_generate --overwrite_output_dir
```

### 5. Compute BLEU4, chrF2, TER, COMET, METEOR, BERTScore Scores
```bash
python BLEU4_chrF_TER_new.py
python COMET_METEOR.py
python BERTscore.py
```

## NLLB-200 Model

### 1. Create Project Structure
```bash
mkdir NLLB-200_mai_hin
cd NLLB-200_mai_hin
```

### 2. Download nllb-200-distilled-600M Model from HuggingFace, Ensure that all dataset files are in huggingface dataset format (e.g., `train`, `valid`, `test`).

```bash
python download.py
python convert_dataset.py
```
### 3. Training
```bash
python train.py

### 4. Inference

```bash
python inference.py

### 5. Compute BLEU4, chrF2, TER, COMET, METEOR, BERTScore Scores
```bash
python BLEU4_chrF_TER_new.py
python COMET_METEOR.py
python BERTscore.py
```
## License

The dataset in this repository is licensed under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).  
You are free to share and adapt the material for any purpose, even commercially, with proper attribution.
