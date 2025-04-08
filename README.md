# Practical Work in AI - Embedding Propagation for Molecular Target Activity Prediction

## Abstract
The aim of this report is to find out if embedding propagation is a useful technique that improves the performance of an MLP in molecular target activity prediction. Molecule data is often sparse and extremely skewed, as positive samples are rare. Therefore, it is necessary to verify if methods that work on other, more traditional datasets translate well to this special scenario. I compared results of a baseline random forest, an MLP and an MLP with embedding propagation. ROC-AUC and Delta-AUC-PR were compared for all three models for five runs, with a Wilcoxon rank-sum test calculated as a last step for these results. On the one hand, the average ROC-AUC was not significantly impacted. On the other hand, Delta-AUC-PR was not increased with embedding propagation. Additionally, for Delta-AUC-PR variation between runs was increased with EP. However, almost none of the relationships turned out to be statistically significant, but they offer first insights. These results highlight the need to adapt methods from different fields to make them more suitable for a molecular context. This repository contains the code for all results, figures and statistical tests described in the report.


## 1. Installation and Dependencies
Clone the repository and install all necessary dependencies:
```bash
pip install -r requirements.txt
```

## 2. General
All experiments outlined in the report can be reproduced with the provided code without any modifications. Most of the files are jupyter notebooks, all of them are self-contained. Every file can be run from start to finish to obtain all necesary results for further steps.

**a. Preprocessing**
All features for training the models are extraced from the provided molecule data in compute-features-checkpoint.ipynb. The final data is saved in data_scaled.npz in the data folder, which is then imported at the beginning of every model file.

**b. Model Results**
For each of the three models, metrics are computed and saved in a separate jupyter notebook. In each file, the corresponding model is trained and evaluated. At the end, ROC-AUC and Delta AUC-PR are saved in json files in the metrics subfolder for further processing. Each metric is saved once per run, as an average over tasks, once per task, as an average over runs, and once as averaged over both tasks and runs.

**c. Figures**
All figures that are used in the report were created in the figures notebook. The metrics for each model are loaded from the metrics subfolder and processed into figures.

**d. Statistical Tests**
A Wilcoxon rank-sum test was applied to every combination of two models and for both metrics.

## 3. Code Structure
```bash
├── README.md           
├── data/                       # MUV dataset, computed features for model training
├── metrics/                    # json output, three files per model
├── baseline.ipynb              # model file for baseline Random Forest
├── pretraining.ipynb           # model file for MLP without embedding propagation
├── pretraining_ep.ipynb        # model file for MLP with embedding propagation
├── compute_features_checkpoint.ipynb       # MUV data preprocessing, feature extraction
├── figures.ipynb                           # create figures for report based on metrics
├── stat_test.ipynb             # perform Wilcoxon rank-sum test
└── requirements.txt            # Python dependencies
```