# Official implementation of SegViz: A federated-learning based framework for multi-organ segmentation on heterogeneous data sets with partial annotations

![Depiction of the SegViz framework](assets/Segviz_fig.png)

To replicate our work, you will need the following datasets:

- We use datasets for the Liver, Spleen, Pancreas, and Kidneys from the [Medical Segmentation Decathalon challenge](http://medicaldecathlon.com/)

- We use all the 30 training samples from the [Beyond the Cranial Vault datasets](https://www.synapse.org/#!Synapse:syn3193805/wiki/89480\n)


We have the following notebooks for your reference -

- W&B_SegViz_3d_LSPK_combined_anon.ipynb - You will need to consolidate all the samples from the training set of all the four datasets and store it in the MSD format. Then you can pass your path to the `root_dir` variable in the notebook. 

- W&B_SegViz_3d_liver_only_128_rescrop_anon.ipynb - This is the notebook to train the liver baseline model i.e the model trained specifically for the liver dataset. To run this notebook, simply change the path in the notebook to your local path.

- W&B_SegViz_3d_liver_spleen_pan_kid_multi_FT_anon.ipynb - This notebook demonstrates training a distributed FL setup using the FedAvg algorithm for the four datasets - Each client node is trained for one of the four datasets. The global model is initialized and aggregates certain weights of each model and returns it back to nodes after every 10 epoch iterations. This process is continued for 50 rounds of communication (500 epochs). This script later shows how to fine-tune the models to the local datasets. 

- W&B_SegViz_3d_liver_spleen_pan_kid_multi_FT_FedBN_anon.ipynb - This notebook demonstrates the FedBN algorithm for the four datasets and is similar to the above notebook.

- generate_metrics_Segviz_anon.ipynb - This notebook can be used to generate the dice metrics during model evaluation. 


To reproduce all the experiments successfully, please clone this repository locally and initiate a conda virtual environment using the given `environment.yml` file using 

```
conda env create -f environment.yml
```

Simply run the notebooks using this conda environment.


## Other specific parameters

- Set the MONAI seed '0' for reproducibilty - Changing this value can cause variations in your results. 
