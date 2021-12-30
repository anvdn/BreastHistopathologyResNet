# Breast Histopathology

I went back to my Breast Histopathology project with more computational resources (NVIDIA A100) and performed classification with ResNet18, ResNet34 and ResNet50 [1]. I built the architectures in PyTorch to have more flexibility at training time (images are only 50x50x3 and not 224x224x3 as in ImageNet [2]).

[1] Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun. Deep Residual Learning for Image Recognition. arXiv:1512.03385

[2] Deng, J. et al., 2009. Imagenet: A large-scale hierarchical image database. In 2009 IEEE conference on computer vision and pattern recognition. pp. 248–255.


## Presentation

Early-stage breast cancer detection - the most diagnosed in women – increases the 5-year relative survival rate up to 99%. This crucial process is improved by introducing a computer-aided
diagnosis system to automate cancerous tissue identification from whole slide images. This work proposes a replicable approach for the detection of Invasive Ductal Carcinoma (IDC)- accounting for 80% of all breast cancers - and aims at outperforming diagnostic accuracy of an experienced human eye (~79%).

## Data

277,524 patches scanned at x40 in resolution 50 x 50. Metadata contains patient ID (279 patients in total), coordinates of the patch in tissue slice and target (cancerous or not).
You can find the original dataset here: https://www.kaggle.com/paultimothymooney/breast-histopathology-images/download

```
# Install kaggle API with pip
pip install kaggle

# set up kaggle environment variables with the API credentials (obtained by generating a key from kaggle.com)
export KAGGLE_USERNAME=datadinosaur
export KAGGLE_KEY=xxxxxxxxxxxxxx

# install dataset into /input
mkdir input
cd ./input
kaggle datasets download paultimothymooney/breast-histopathology-images
unzip breast-histopathology-images.zip
rm breast-histopathology-images.zip
rm -rf IDC_regular_ps50_idx5
mkdir breast-histopathology-images
mv * breast-histopathology-images
```

## Accuracy

| Model             | Acc.        |
| ----------------- | ----------- |
| [Baseline](https://github.com/AntoninVidon/BreastHistopathology) (XGBoost after PCA)                             | 81.38%      |
| [ResNet18](https://arxiv.org/abs/1512.03385)                                                                     | 85.76%      |
| [ResNet34](https://arxiv.org/abs/1512.03385)                                                                     | 85.73%      |
| [ResNet50](https://arxiv.org/abs/1512.03385)                                                                     | 85.78%      |



## Organization of this directory


```./
├── models
│   └── resnet.py
├── input
│   └── DATA
├── data
│   └── DATA
├── figures
│   |── ResNet18.png
│   |── ResNet34.png 
│   └── ResNet50.png
├── checkpoint
│   |── ResNet18.pth
│   |── ResNet34.pth
│   └── ResNet50.pth
├── viz.ipynb
├── train.ipynb
├── prep.ipynb
└── README.md
