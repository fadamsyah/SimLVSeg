# UniLVSeg: Unified Left Ventricular Segmentation with Sparsely Annotated Echocardiogram Videos through Self-Supervised Temporal Masking and Weakly Supervised Training

[![paper](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)](https://arxiv.org/abs/2310.00454)

Official implementation of the paper "UniLVSeg".

## Highlights
### Abstract
> *Echocardiography has become an indispensable clinical imaging modality for general heart health assessment. From calculating biomarkers such as ejection fraction to the probability of a patient’s heart failure, accurate segmentation of the heart and its structures allows doctors to plan and execute treatments with greater precision and accuracy. However, achieving accurate and robust left ventricle segmentation is time-consuming and challenging due to different reasons. Hence, clinicians often rely on segmenting the left ventricular (LV) in two specific echocardiogram frames to make a diagnosis. This limited coverage in manual LV segmentation makes it challenging to develop automatic LV segmentation with high temporal consistency since the resulting datasets are annotated sparsely. This work introduces a novel approach for consistent left ventricular (LV) segmentation from sparsely annotated echocardiogram videos. We achieve this through (1) self-supervised learning (SSL) using temporal masking followed by (2) weakly supervised training. We investigate two different segmentation approaches: 3D segmentation and a novel 2D superimage (SI). We demonstrate how our proposed method outperforms the state-of-the-art solutions by achieving a 93.32% (95%CI 93.21-93.43%) dice score on a large-scale dataset (EchoNet-Dynamic) while being more efficient. To show the effectiveness of our approach, we provide extensive ablation studies, including pre-training settings and various deep learning backbones. Additionally, we discuss how our proposed methodology achieves high data utility by incorporating unlabeled frames in the training process.*
>

### Methodology
![methodology](https://github.com/fadamsyah/UniLVSeg/blob/main/assets/img_General_Architecture.pdf)

### Main Result
![SOTA-comparison](https://github.com/fadamsyah/UniLVSeg/blob/main/assets/img_SOTA_comparisons.pdf)
![main-table](https://github.com/fadamsyah/UniLVSeg/blob/main/assets/main_table.png)

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