# chaii
Chaii - Hindi and Tamil Question Answering Kaggle Competition Solution

## Reproduction instructions

I trained all my models via jupyter notebooks. The notebooks used to train the models from my final ensemble are saved in the `training_notebooks` folder.

The notebooks refer to the following csv files:

- `tydiqa_train.csv.zip` - this file can be recreated by executing this notebook: https://www.kaggle.com/thedrcat/tydi-qa-download
- `nq_small.csv.zip` - I published this dataset here: https://www.kaggle.com/thedrcat/nqsmall
- `chaii_mlqa_xquad_5folds.csv` - this comes from the following dataset: https://www.kaggle.com/zacchaeus/chaiimlqaxquad

In some instances I used an interim checkpoint when both local CV and public LB indicated it's better than final checkpoint. The following table illustrates that. Note that due to some potential randomness I'd recommend to watch validation when reproducing the results. 

| Experiment | data | backbone | schedule | wmup | ep | lr (e-5) | wd | bs/ga | seqlen | LB  | Checkpoint |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 52 | XLMR pretraining 2/2 epochs squad+tydi beteen, neg sampling 0.1, 384/192, eval on chaii | xlm-roberta-large | linear | 0.2 | 2 | 1 | 0.01 | 8/4 | 384/192 | 786 | final |
| 68 | tydi beteen + squad, tydi beteen + nqsmall, chaii all data, fold 1/3 | xlm-roberta-large | linear | 0.2 | 1 | 1 | 0.01 | 8/4 | 384/192 | 788 | final |
| 71 | tydi beteen + squad, tydi beteen + nqsmall, chaii all data, fold 1/3 | muril-large | linear | 0.1 | 1 | 3 | 0.01 | 8/4 | 384/192 | 802 | checkpoint 7000 |
| 73 | tydi beteen + squad, tydi beteen + nqsmall, chaii all data, fold 2/3 | muril-large | linear | 0.1 | 1 | 3 | 0.01 | 8/4 | 384/192 | 798 | checkpoint 7000 |
| 77-final | tydi beteen + squad, tydi beteen + nqsmall, chaii all data, fold 1/3 | rembert | linear | 0.1 | 1 | 1 | 0.01 | 8/16 | 384/192 | 786 | final |
| 78-final | tydi beteen + squad, tydi beteen + nqsmall, chaii all data, fold 0/3 | rembert | linear | 0.1 | 1 | 1 | 0.01 | 8/16 | 384/192 | 782 | final |
| 79-1000 | tydi beteen + squad, tydi beteen + nqsmall, chaii all data, fold 2/3 | rembert | linear | 0.1 | 1 | 1 | 0.01 | 8/16 | 384/192 | 790 | checkpoint 1000 |
| 79-final | tydi beteen + squad, tydi beteen + nqsmall, chaii all data, fold 2/3 | rembert | linear | 0.1 | 1 | 1 | 0.01 | 8/16 | 384/192 | 783 | final |
| 116 | progressive resizing, data recipes, fold 0 | xlm-roberta-large | linear | 0.2 | 1 | 1 | 0.01 | 8/4 | 256-448 | 786 | final |
| 119f1 | progressive resizing, cutout 0.1, data recipes, fold 1 | xlm-roberta-large | linear | 0.2 | 1 | 1 | 0.01 | 8/4 | 256-384 | 791 | final |
| 119f2 | progressive resizing, cutout 0.1, data recipes, fold 2 | xlm-roberta-large | linear | 0.2 | 1 | 1 | 0.01 | 8/4 | 256-384 | 785 | final |
| 122f0 | progressive resizing, cutout 0.03, longer seqlen, smaller LR | muril-large | linear | 0.1 | 1 | 2.5 | 0.01 | 8/4 | 384-448 | 801 | checkpoint 4000 |
| 126-s1 | 1 epoch all data, no cutout | rembert | linear | 0.1 | 1 | 1 | 0.01 | 8/16 | 384 | 793 | final |

