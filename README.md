# Panoptic Segmentation Framework

## Dataset - PASTIS

The dataset can be downloaded from [zendo](https://zenodo.org/record/5012942) 

PASTIS is a benchmark dataset for panoptic and semantic segmentation of agricultural parcels from satellite time series. 
It contains 2,433 patches within the French metropolitan territory with panoptic annotations (instance index + semantic labelfor each pixel). Each patch is a Sentinel-2 multispectral image time series of variable lentgh. 

We propose an official 5 fold split provided in the dataset's metadata, and evaluated several of the top-performing image time series networks. You are welcome to use our numbers and to submit your own entries to the leaderboard!

- **Dataset in numbers**

:arrow_forward: 2,433 time series             |  :arrow_forward: 124,422 individual parcels         | :arrow_forward: 18 crop types   
:-------------------------------------------- | :-------------------------------------------------- | :------------------------------
:arrow_forward: **128x128 pixels / images**   | :arrow_forward:  **38-61 acquisitions / series**    | :arrow_forward:  **10m / pixel** 
:arrow_forward:  **10 spectral bands**        | :arrow_forward: **covers ~4,000 km²**                       | :arrow_forward: **over 2B pixels**


## UTAE + PaPs

The original paper can be found [here](https://arxiv.org/abs/2107.07933).

The original implmentation of the UTAE-PaPs can be found [here](https://github.com/VSainteuf/utae-paps/) 

### Prepare the folder Structure

- Pretrained weights can be downloaded from [here](https://zenodo.org/record/5172301)
- If your folder structure is different, you may need to change the corresponding paths in config files in downloaded pre trained weights folders.
- create an output directory including five folders for each folds (Fold_1, Fold_2, etc.)
```
Panoptic_Segmentation
├── datasets
│   ├── PASTIS
│   │   ├── PASTIS
│   │   │    ├── ANNOTATIONS
│   │   │    ├── DATA_S2
│   │   │    ├── INSTANCE_ANNOTATIONS
│   │   │    ├── metadata.geojson
│   │   │    ├── NORM_s2_patch.json
├── pre_trained_weights
│   ├── UATE_zenodo
│   ├── UTAE_PaPs
├── exp_results
├── panoptic_segmentation_framework
│   ├── src
│   ├── train_panoptic.py
│   ├── teain_semantic.py
│   ├── test_panoptic.py
│   ├── test_semantic.py
│   ├── requirments.py
```
### Running the training scripts

- Install all the requirments from the requirments.txt file
- To avoid library dependancy issues make sure to install **torch 1.4** and **torch-scatter 1.4** versions
- To perfrom panoptic segmentation and semantic segmentation training run:
```
python train_panoptic.py --fold 3 --dataset_folder ../datasets/PASTIS/PASTIS --res_dir ../exp_results/ex1/panop --batch_size 2
```
```
python train_semantic.py --fold 3 --dataset_folder PATH_TO_DATASET --res_dir PATH_TO_OUT_DIR --batch_size 2
```
### Inference with pre-trained models

- To perform inference using pre-trained models on test set run:
```
python test_panoptic.py --dataset_folder PATH_TO_DATASET --weight_folder PATH_TO_WEIGHT_FOLDER
```
```
python test_semantic.py --dataset_folder PATH_TO_DATASET --weight_folder PATH_TO_WEIGHT_FOLDER
```

## References
If you use PASTIS please cite the [related paper](https://arxiv.org/abs/2107.07933):
```
@article{garnot2021panoptic,
  title={Panoptic Segmentation of Satellite Image Time Series
with Convolutional Temporal Attention Networks},
  author={Sainte Fare Garnot, Vivien  and Landrieu, Loic },
  journal={arxiv},
  year={2021}
}
```

## Credits

- The satellite imagery used in PASTIS was retrieved from [THEIA](www.theia.land.fr): 
"Value-added data processed by the CNES for the Theia www.theia.land.fr data cluster using Copernicus data.
The treatments use algorithms developed by Theia’s Scientific Expertise Centres. "

- The annotations used in PASTIS stem from the French [land parcel identification system](https://www.data.gouv.fr/en/datasets/registre-parcellaire-graphique-rpg-contours-des-parcelles-et-ilots-culturaux-et-leur-groupe-de-cultures-majoritaire/) produced
 by IGN, the French mapping agency.
 
- This work was partly supported by [ASP](https://www.asp-public.fr), the French Payment Agency. 


