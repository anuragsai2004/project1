<div align="center">
	
## OpenEarthMap Land Cover Mapping Few-Shot Challenge </br> Generalized Few-shot Semantic Segmentation
## Challenge proposed by the [Geoinformatics Team of RIKEN-AIP](https://geoinformatics2018.com/) and co-organized with the [3rd L3D-IVU Workshop](https://sites.google.com/view/l3divu2024/overview) @ CVPR 2024 Conference

<p><img src="docs/assets/img/img2.jpg"></p>
</div>

<div align="center">
	
[![GitHub license](https://badgen.net/github/license/Naereen/Strapdown.js)](https://github.com/Naereen/StrapDown.js/blob/master/LICENSE)
<a href="https://pytorch.org/get-started/locally/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-ee4c2c?logo=pytorch&logoColor=white"></a>
![Python](https://img.shields.io/badge/python-3.7+-blue.svg)
</div>

<div align="justify">
Participate in obtaining more accurate maps for a more comprehensive description and a better understanding of our environment! 
Come push the limits of state-of-the-art semantic segmentation approaches on a large and challenging dataset. Get in touch at ai-challenge@ign.fr

</div>

## Data & Context

<!--
<div style="border-width:1px; border-style:solid; border-color:#d2db8c; padding-left: 1em; padding-right: 1em; ">
  
<h2 style="margin-top:5px;">Links</h2>


- **Datapaper :** https://arxiv.org/pdf/2211.12979.pdf

- **Dataset links :** https://ignf.github.io/FLAIR/ or https://huggingface.co/datasets/IGNF/FLAIR

- **Challenge page :**  https://codalab.lisn.upsaclay.fr/competitions/8769 [🛑 closed!]

</div>


<div align="center">


<h2>
   </br>
   <small>Co-organized with the <a href="https://sites.google.com/view/l3divu2024/overview">L3D-IVU CVPR 2024</a> Workshop</small>
</h2>
</div>

<div align="justify">
<p>
This repository contains the baseline model code for the OpenEarthMap land cover mapping generalized few-shot semantic segmentation challenge, 
co-organized with the <b>Learning with Limited Labelled Data for Image and Video Understanding</b> Workshop at the <b>CVPR 2024</b> Conference.
</p>
</div>

### Baseline Code adopted from ...
Run from a terminal, use the `test.sh` script, which its general syntax is:
```bash
bash test.sh 
```
-->

<!-- 
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cliffbb/OEM-Fewshot-Challenge/blob/master/test.ipynb)
[pre-trained mode]('https://drive.google.com/file/d/1eLjfUJ2ajAMkJKCsoJr-MGSSzZ-LqDbR/view?usp=drive_link')


# DIaM for Generalized Few-Shot Semantic Segmentation

This repository contains the code for our **CVPR 2023** paper, [A Strong Baseline for Generalized Few-Shot Semantic Segmentation](https://arxiv.org/abs/2211.14126).

> **Abstract:** *This paper introduces a generalized few-shot segmentation framework with a straightforward training process and an easy-to-optimize inference phase. In particular, we propose a simple yet effective model based on the well-known InfoMax principle, where the Mutual Information (MI) between the learned feature representations and their corresponding predictions is maximized. In addition, the terms derived from our MI-based formulation are coupled with a knowledge distillation term to retain the knowledge on base classes. With a simple training process, our inference model can be applied on top of any segmentation network trained on base classes. The proposed inference yields substantial improvements on the popular few-shot segmentation benchmarks PASCAL-5<sup>i</sup> and COCO-20<sup>i</sup>. Particularly, for novel classes, the improvement gains range from 7% to 26% (PASCAL-5<sup>i</sup>) and from 3% to 12% (COCO-20<sup>i</sup>) in the 1-shot and 5-shot scenarios, respectively. Furthermore, we propose a more challenging setting, where performance gaps are further exacerbated.*

## &#x1F3AC; Getting Started

### :one: Requirements
We used `Python 3.9` in our experiments and the list of packages is available in the `requirements.txt` file. You can install them using `pip install -r requirements.txt`.

### :two: Download data

#### Pre-processed data from drive

We provide the versions of PASCAL VOC 2012 and MS-COCO 2017 used in this work [here](https://etsmtl365-my.sharepoint.com/:u:/g/personal/seyed-mohammadsina_hajimiri_1_ens_etsmtl_ca/Earq9o6KqvJDleNRKqfFZ_cB1AzQCtaZ5g2noh4yjZoecg?e=g1g9t4). You can download the full .zip and directly extract it in the `data/` folder.

#### From scratch

Alternatively, you can prepare the datasets yourself. Here is the structure of the data folder for you to reproduce:

```
data
├── coco
│   ├── annotations
│   ├── train
│   ├── train2014
│   ├── val
│   └── val2014
└── pascal
|   ├── JPEGImages
|   └── SegmentationClassAug
```
**PASCAL**: The JPEG images can be found in the PASCAL-VOC 2012 toolkit to be downloaded at [PASCAL VOC 2012](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar) and [SegmentationClassAug](https://etsmtl365-my.sharepoint.com/:u:/g/personal/seyed-mohammadsina_hajimiri_1_ens_etsmtl_ca/Ef70aWKWEidJoR_NZb131SwB3t7WIHMjJK316qxIu_SPyw?e=CVtNKY) (pre-processed ground-truth masks).

**COCO**: COCO 2014 train images, validation images and annotations can be downloaded at [COCO](https://cocodataset.org/#download). Once this is done, you will have to generate the subfolders `coco/train` and `coco/val` (ground truth masks). Both folders can be generated by executing the python script `data/coco/create_masks.py` (note that this script uses the [pycocotools](https://github.com/cocodataset/cocoapi/tree/master/PythonAPI/pycocotools) package):

```
cd data/coco
python create_masks.py
 ```

#### About the train/val splits

The train/val splits are directly provided in `lists/`. How they were obtained is explained at https://github.com/Jia-Research-Lab/PFENet.

### :three: Download pre-trained models

#### Pre-trained backbone and models
We provide the pre-trained backbone and models at https://drive.google.com/file/d/1WuKaJbj3Y3QMq4yw_Tyec-KyTchjSVUG/view?usp=share_link. You can download them and directly extract them at the root of this repo. This will create two folders: `initmodel/` and `model_ckpt/`.

## &#x1F5FA; Overview of the repo

Default configuration files can be found in `config/`. Data are located in `data/`. `lists/` contains the train/val splits for each dataset. All the codes are provided in `src/`. Testing script is located at the root of the repo.

## &#x2699; Training (optional)

If you want to use the pre-trained models, this step is optional. Our contribution lies in the inference phase and our approach is modular, i.e., it can be applied on top of any segmentation model that is trained on the base classes. 
We use a simple training scheme by minimizing a standard cross-entropy over base classes. To this end, we have used the [`train_base.py`](https://github.com/chunbolang/BAM/blob/main/train_base.py) script and base learner models of [BAM](https://github.com/chunbolang/BAM) (see [this issue](https://github.com/sinahmr/DIaM/issues/3) for more info).

## &#x1F9EA; Testing

To test the model, use the `test.sh` script, which its general syntax is:
```bash
bash test.sh {benchmark} {shot} {pi_estimation_strategy} {[gpu_ids]} {log_path}
```
This script tests successively on all folds of the benchmark and reports the results individually. The overall performance is the average over all the folds. Some example commands are presented below, with their description in the comments.

```bash
bash test.sh pascal5i 1 self [0] out.log  # PASCAL-5i benchmark, 1-shot, estimate pi by model's output
bash test.sh pascal10i 5 self [0] out.log  # PASCAL-10i benchmark, 5-shot, estimate pi by model's output
bash test.sh coco20i 5 upperbound [0] out.log  # COCO-20i benchmark, 5-shot, the upperbound model mentioned in the paper
```

If you run out of memory, reduce `batch_size_val` in the config files.

### &#x1F4CA; Results
To reproduce the results, please first download the pre-trained models from [here](https://drive.google.com/file/d/1WuKaJbj3Y3QMq4yw_Tyec-KyTchjSVUG/view?usp=share_link) (also mentioned in the "download pre-trained models" section) and then run the `test.sh` script with different inputs, as explained above.
<table>
    <tr>
        <th colspan="2"></th>
        <th colspan="3">1-Shot</th>
        <th colspan="3">5-Shot</th>
    </tr>
    <tr>
        <th>Benchmark</th>
        <th>Fold</th>
        <th>Base</th> <th>Novel</th> <th>Mean</th>
        <th>Base</th> <th>Novel</th> <th>Mean</th>
    </tr>
    <tr>
        <td rowspan="5"><b>PASCAL-5<sup>i</sup></b></td>
        <td>0</td>
        <td>71.33</td> <td>29.36</td> <td>50.35</td>
        <td>71.06</td> <td>53.72</td> <td>62.39</td>
    </tr>
    <tr>
        <td>1</td>
		<td>69.54</td> <td>46.72</td> <td>58.13</td>
		<td>69.63</td> <td>63.33</td> <td>66.48</td>
    </tr>
    <tr>
        <td>2</td>
		<td>69.10</td> <td>27.07</td> <td>48.09</td>
		<td>69.12</td> <td>54.01</td> <td>61.57</td>
    </tr>
    <tr>
        <td>3</td>
		<td>73.60</td> <td>37.30</td> <td>55.45</td>
		<td>73.60</td> <td>50.19</td> <td>61.90</td>
    </tr>
    <tr>
        <td>mean</td>
		<td>70.89</td> <td>35.11</td> <td>53.00</td>
		<td>70.85</td> <td>55.31</td> <td>63.08</td>
    </tr>
    <tr>
        <td rowspan="5"><b>COCO-20<sup>i</sup></b></td>
        <td>0</td>
		<td>49.01</td> <td>15.89</td> <td>32.45</td>
		<td>48.90</td> <td>24.86</td> <td>36.88</td>
    </tr>
    <tr>
        <td>1</td>
		<td>46.83</td> <td>19.50</td> <td>33.17</td>
		<td>47.10</td> <td>33.94</td> <td>40.52</td>
    </tr>
    <tr>
        <td>2</td>
		<td>48.82</td> <td>16.93</td> <td>32.88</td>
		<td>49.12</td> <td>27.15</td> <td>38.14</td>
    </tr>
    <tr>
        <td>3</td>
		<td>48.45</td> <td>16.57</td> <td>32.51</td>
		<td>48.37</td> <td>28.95</td> <td>38.66</td>
    </tr>
    <tr>
        <td>mean</td>
		<td>48.28</td> <td>17.22</td> <td>32.75</td>
		<td>48.37</td> <td>28.73</td> <td>38.55</td>
    </tr>
    <tr>
        <td rowspan="5"><b>PASCAL-10<sup>i</sup></b></td>
        <td>0</td>
		<td>68.69</td> <td>34.40</td> <td>51.55</td>
		<td>68.49</td> <td>55.94</td> <td>62.22</td>
    </tr>
    <tr>
        <td>1</td>
		<td>71.83</td> <td>28.17</td> <td>50.00</td>
		<td>72.00</td> <td>47.84</td> <td>59.92</td>
    </tr>
    <tr>
        <td>mean</td>
		<td>70.26</td> <td>31.29</td> <td>50.77</td>
		<td>70.25</td> <td>51.89</td> <td>61.07</td>    </tr>
</table>

## &#x1F64F; Acknowledgments

We gratefully thank the authors of [RePRI](https://github.com/mboudiaf/RePRI-for-Few-Shot-Segmentation), [BAM](https://github.com/chunbolang/BAM), [PFENet](https://github.com/Jia-Research-Lab/PFENet), and [PyTorch Semantic Segmentation](https://github.com/hszhao/semseg) from which some parts of our code are inspired.

## &#x1F4DA; Citation

If you find this project useful, please consider citing:

```bibtex
@inproceedings{hajimiri2023diam,
  title={A Strong Baseline for Generalized Few-Shot Semantic Segmentation},
  author={Hajimiri, Sina and Boudiaf, Malik and Ben Ayed, Ismail and Dolz, Jose},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={11269--11278},
  year={2023}
}
``` 
#######################################################
<div align="center">
<p><img src="demo_data/oem_logo.png"></p>
<p>
    <a href="https://github.com/cliffbb/OEM-Lightweight/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-<p>.svg?style=for-the-badge"></a>
    <a href="https://pytorch.org/get-started/previous-versions/"><img src="https://img.shields.io/badge/PYTORCH-1.12+-red?style=for-the-badge&logo=pytorch"></a>
    <a href="https://www.python.org/downloads/"><img src="https://img.shields.io/badge/PYTHON-3.7+-red?style=for-the-badge&logo=python&logoColor=white"></a>
</p>
</div>

# Lightweight Mapping Model
### Overview
___
This is a demo of OpenEarthMap lightweight models searched with
[SparseMask](https://arxiv.org/abs/1904.07642) and
[FasterSeg](https://arxiv.org/abs/1912.10917) neural architecture search methods. 
The models were automatically searched and pretrained on the OpenEarthMap 
[dataset](https://zenodo.org/record/7223446#.Y2Jj1OzP2Ak) 
(using only the training and validation sets).

### OpenEarthMap dataset
___
OpenEarthMap is a benchmark dataset for global high-resolution land cover mapping. 
OpenEarthMap consists of 5000 aerial and satellite images with manually annotated 
8-class land cover labels and 2.2 million segments at a 0.25-0.5m ground 
sampling distance, covering 97 regions from 44 countries across 6 continents. 
OpenEarthMap fosters research, including but not limited to semantic segmentation
and domain adaptation. The project website is https://open-earth-map.org/
```
@inproceedings{xia_2023_openearthmap,
    title = {OpenEarthMap: A Benchmark Dataset for Global High-Resolution Land Cover Mapping},
    author = {Junshi Xia and Naoto Yokoya and Bruno Adriano and Clifford Broni-Bediako},
    booktitle = {Proceedings of the IEEE/CVF Winter Conference on Applications of Computer Vision (WACV)},
    month = {January},
    year = {2023}
}
```

### Lightweight model
___
The lightweight models searched and pretrained on the OpenEarthMap dataset 
can be downloaded as following:

| Method    | Searched architecture   | Pretrained weights           | #Params |  FLOP   |
|:----------|:------------------------|:-----------------------------|:-------:|:-------:|
| SpareMask | [mask_thres_0.001.npy](https://drive.google.com/file/d/1WwE2pIHTb7xGql7xQ9TxeZ1pZmk2JhCl/view?usp=sharing)| [checkpoint_63750.pth.tar](https://drive.google.com/file/d/170o8NNBrrIBJqFdoeYCJoyKHvuub0v2k/view?usp=sharing) | 2.96MB  | 10.45GB |
| FasterSeg | [arch_1.pt](https://drive.google.com/file/d/12oDzi-sDnD_Y4CBONei_g2SZBMZ6cx-2/view?usp=sharing)           | [weights1.pt](https://drive.google.com/file/d/1BgCu1Rz2PvTPJzI_J97hNkr4HvlvI-pE/view?usp=sharing)              | 3.47MB  | 15.43GB |

### Usage
___
* **SparseMask model:** download the [architecture mask](https://drive.google.com/file/d/1WwE2pIHTb7xGql7xQ9TxeZ1pZmk2JhCl/view?usp=sharing) and the [pretrained weights](https://drive.google.com/file/d/170o8NNBrrIBJqFdoeYCJoyKHvuub0v2k/view?usp=sharing)
and put them into folder `models/SparseMask/`.   
Start the evaluation demo as:
```
python eval_oem_lightweight.py \
    --model "sparsemask" \
    --arch "models/SparseMask/mask_thres_0.001.npy" \
    --pretrained_weights "models/SparseMask/checkpoint_63750.pth.tar" \
    --save_image --save_dir "results" 
```   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Or use the Jupyter notebook: `sparsemask_demo.ipynb`.

* **FasterSeg model:** download the [architecture structure](https://drive.google.com/file/d/12oDzi-sDnD_Y4CBONei_g2SZBMZ6cx-2/view?usp=sharing) and the [pretrained weights](https://drive.google.com/file/d/1BgCu1Rz2PvTPJzI_J97hNkr4HvlvI-pE/view?usp=sharing)
and put them into folder `models/FasterSeg/`.   
Start the evaluation demo as:
```
python eval_oem_lightweight.py \
    --model "fasterseg" \
    --arch "models/FasterSeg/arch_1.pt" \
    --pretrained_weights "models/FasterSeg/weights1.pt" \
    --save_image --save_dir "results" 
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Or use the Jupyter notebook `fasterseg_demo.ipynb`.

### Example of predictions
___
* **SparseMask model**   
![](demo_data/sparsemask1.png)    
![](demo_data/sparsemask2.png)
* **FasterSeg model**    
![](demo_data/fasterseg1.png)    
![](demo_data/fasterseg2.png)

### Acknowledgement
___
Automated neural architecture search method code from
* [SparseMask](https://github.com/wuhuikai/SparseMask)
* [FasterSeg](https://github.com/VITA-Group/FasterSeg)

-->




