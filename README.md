# UniLVSeg: Unified Left Ventricular Segmentation with Sparsely Annotated Echocardiogram Videos through Self-Supervised Temporal Masking and Weakly Supervised Training

[Fadillah Adamsyah Maani](https://scholar.google.com/citations?user=W-4975wAAAAJ&hl=en), [Asim Ukaye](https://www.linkedin.com/in/asim-ukaye-2070a73a/), [Nada Saadi](https://www.linkedin.com/in/nada-saadi-440632179/), [Numan Saeed](https://scholar.google.ae/citations?user=VMPEU20AAAAJ&hl=en), [Mohammad Yaqub](https://scholar.google.co.uk/citations?user=9dfn5GkAAAAJ&hl=en)

[![paper](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)](https://arxiv.org/abs/2310.00454)

Official implementation of the paper "UniLVSeg".

## Highlights
### Abstract
> *Echocardiography has become an indispensable clinical imaging modality for general heart health assessment. From calculating biomarkers such as ejection fraction to the probability of a patient’s heart failure, accurate segmentation of the heart and its structures allows doctors to plan and execute treatments with greater precision and accuracy. However, achieving accurate and robust left ventricle segmentation is time-consuming and challenging due to different reasons. Hence, clinicians often rely on segmenting the left ventricular (LV) in two specific echocardiogram frames to make a diagnosis. This limited coverage in manual LV segmentation makes it challenging to develop automatic LV segmentation with high temporal consistency since the resulting datasets are annotated sparsely. This work introduces a novel approach for consistent left ventricular (LV) segmentation from sparsely annotated echocardiogram videos. We achieve this through (1) self-supervised learning (SSL) using temporal masking followed by (2) weakly supervised training. We investigate two different segmentation approaches: 3D segmentation and a novel 2D superimage (SI). We demonstrate how our proposed method outperforms the state-of-the-art solutions by achieving a 93.32% (95%CI 93.21-93.43%) dice score on a large-scale dataset (EchoNet-Dynamic) while being more efficient. To show the effectiveness of our approach, we provide extensive ablation studies, including pre-training settings and various deep learning backbones. Additionally, we discuss how our proposed methodology achieves high data utility by incorporating unlabeled frames in the training process.*
>

### Methodology
![methodology](https://github.com/fadamsyah/UniLVSeg/blob/main/assets/img_General_Architecture.png)

### Main Result
![SOTA-comparison](https://github.com/fadamsyah/UniLVSeg/blob/main/assets/img_SOTA_comparisons.png)
![main-table](https://github.com/fadamsyah/UniLVSeg/blob/main/assets/main_table.png)

## Run UniLVSeg

To run this repository, you have to download the EchoNet-Dynamic original dataset.

### Installation
```bash
# Create a conda environment
conda env create -n hc701_fp python=3.8.13 -f environment.yml
```

### Training

The following is the bash script for the self-supervised pretraining with temporal asking. To use a pretrained weight, you have to include an additional argument `--checkpoint`.
```bash
python seg_3d_masking_train.py \
    --data_path $echonet_dynamic_data_dir \
    --mean 0.12741163 0.1279413 0.12912785 \
    --std 0.19557191 0.19562256 0.1965878 \
    --encoder "3d_unet" \
    --frames 32 \
    --period 1 \
    --mask_ratio 0.6 \
    --num_workers 8 \
    --batch_size 2 \
    --epochs 100  \
    --val_check_interval 0.5 \
    --seed 42
```

The following is the bash script for the weakly-supervised LV segmentation training pipeline. To use a pretrained weight, you have to include an additional argument `--checkpoint`.
```bash
python seg_3d_train.py \
    --data_path $echonet_dynamic_data_dir \
    --mean 0.12741163 0.1279413 0.12912785 \
    --std 0.19557191 0.19562256 0.1965878 \
    --encoder "3d_unet" \
    --frames 32 \
    --period 1 \
    --num_workers 8 \
    --batch_size 16 \
    --epochs 60  \
    --val_check_interval 0.25 \
    --seed 42
```

### Testing

To do the testing and get the CI of your models, you have to first generate the prediction using the following:
```bash
python seg_3d_test_get_predictions.py \
    --data_path $echonet_dynamic_data_dir \
    --checkpoint $path_to_your_model_weights \
    --save_dir $prediction_outputs_dir \
    --mean 0.12741163 0.1279413 0.12912785 \
    --std 0.19557191 0.19562256 0.1965878 \
    --encoder "3d_unet" \
    --frames 32 \
    --period 1 \
    --num_workers 4 \
    --batch_size 16 \
    --seed 42
```

Then, run the following code to get the CI for overall, ED, and ES DSC.
```bash
python evaluate_bootstrap.py \
    --data_dir $echonet_dynamic_data_dir \
    --prediction_dir $prediction_outputs_dir \
    --output_dir $evaluation_result_dir \
```

## Pretrained Weights

We provide training log, best model checkpoint (according to Val DSC), and model checkpoint at the last epoch.

| Model      | SSL      | #Frame | Period | Checkpoint       |
|------------|----------|----------|--------|---------------|
| 3D | ❌ | 32       | 1     | [link](https://drive.google.com/drive/folders/1-NXFFJEX4ieIm8TxPPz5YiFEmglb599N?usp=sharing) |
| 3D | ✔️ | 32       | 1     | [link](https://drive.google.com/drive/folders/1yLD1iqFk0qLb1YWtqVrnYw_23RpYxV0W?usp=sharing) |

## Citation
If you find this repository useful, please consider citing this work:
```latex
@misc{maani2024unilvseg,
      title={UniLVSeg: Unified Left Ventricular Segmentation with Sparsely Annotated Echocardiogram Videos through Self-Supervised Temporal Masking and Weakly Supervised Training}, 
      author={Fadillah Maani and Asim Ukaye and Nada Saadi and Numan Saeed and Mohammad Yaqub},
      year={2024},
      eprint={2310.00454},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```