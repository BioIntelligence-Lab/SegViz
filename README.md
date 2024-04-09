

# Privacy-Preserving Collaboration for Multi-Organ Segmentation via Federated Learning from Sites with Partial Labels

![SegViz figure](https://user-images.githubusercontent.com/22454450/224231573-83a70f40-8269-47bc-8e0f-e2d39aaf70af.png)

## Data Requirements
To replicate our work, you will need the following datasets:

- We use datasets for the Task03Liver, Task09_Spleen, and Task07_Pancreas from the [Medical Segmentation Decathalon challenge](http://medicaldecathlon.com/) (MSD) and KiTs19 [2019 Kidney Tumor Segmentation Challenge](https://kits19.grand-challenge.org/data/) for training and internal validation as part of in-federation data. 

- We use all the 30 training samples from the [Beyond the Cranial Vault datasets](https://www.synapse.org/#!Synapse:syn3193805/wiki/89480\n) as the external out-of-federation dataset.

## Dependencies
To reproduce all the experiments successfully, please clone this repository locally and initiate a conda virtual environment using the given `environment.yml` file using 

```
conda env create -f environment.yml
```

We have shared the following notebooks -
All notebooks are inspired by MONAI implementations

- [W&B_SegViz_3d_LSPK_combined_anon.ipynb](/notebooks/W&B_SegViz_3d_LSPK_combined_anon.ipynb) - This notebook demonstrates training a single model in a centrally aggregated model setup for multi-task segmentation. You will need to consolidate all the data from the training sets of all four datasets and ensure that it is in compliance with the [MSD data format](https://github.com/MIC-DKFZ/nnUNet/blob/nnunetv1/documentation/dataset_conversion.md). Then you can pass your path to the `root_dir` variable in the notebook. 

- [W&B_SegViz_3d_liver_only_128_rescrop_anon.ipynb](/notebooks/W&B_SegViz_3d_liver_only_128_rescrop_anon.ipynb) - This is the notebook to train the liver baseline model i.e the model trained specifically for the liver dataset but can be extrapolated to other organs. To run this notebook, simply change the `root_dir` in the notebook to your local path. 

- [W&B_SegViz_3d_liver_spleen_pan_kid_multi_FT_anon.ipynb](/notebooks/W&B_SegViz_3d_liver_spleen_pan_kid_multi_FT_anon.ipynb) - This notebook demonstrates training a distributed FL setup using the FedAvg algorithm for the four datasets - Each client node is trained for one of the four datasets. The global model is initialized and aggregates certain weights of each model and returns it back to nodes after every 10 iterations. This process is continued for 50 rounds of communication (for a total of 500 epochs). This script also shows how to fine-tune the models on the local datasets after running the entire FL setup. 

- [W&B_SegViz_3d_liver_spleen_pan_kid_multi_FT_FedBN_anon.ipynb](/notebooks/W&B_SegViz_3d_liver_spleen_pan_kid_multi_FT_FedBN_anon.ipynb) - This notebook demonstrates running the same setup as above but with the FedBN strategy.

- [generate_metrics_Segviz_anon.ipynb](/notebooks/generate_metrics_Segviz_anon.ipynb) - This notebook can be used to generate the dice metrics for model evaluation. You must have all four models from the FL setup already trained.  

## Results

### On the Internal Validation dataset
![int_metrics](https://user-images.githubusercontent.com/22454450/232371897-3e202711-9e61-469b-9d04-687e7b5f951b.png)

### On the external BTCV dataset
![btcv_metrics](https://user-images.githubusercontent.com/22454450/232371944-3bd5ee1c-e631-478c-a4f9-3d82767f41df.png)

## Other specific parameters

- Set the MONAI seed '0' for reproducibilty - Changing this value can cause variations in your overall results. 

## Trained models

All the trained models will be available to download from the `models` folder soon
