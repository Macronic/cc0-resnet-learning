# cc0-resnet-learning
Download CC0 datasets from museums and train a ResNet-50 on them! WIP, will serve as a backbone for my other ReIndentifiCATion project.

Currently work-in-progress, is suppossed to be updated more or less daily with new commits until it's done.

### Training

1. Use notebooks to download datasets from three museums. They can be done in parallel, this process may take about 30h, depending on set dataset size.
   1. CMA Collection Download
   2. MET Collection Download
   3. NGA Collection Download
2. Use Common Data Format Conversion to create a combined metadata file
3. Use Data Preparation file to create dataset for the network to train on.
   You can look at Data Exploration for the work that was being done on creating the Data Preparation file.
   You can also, optionally, use Image Preprocessing notebook to resize the images to make the process of teaching faster. On my setup (3070TI + HDD), it made it about 15-20x faster.
4. Use ResNet-50 Learning to train a ResNet on the dataset

With ResNet-50 Transfer Learning Testing notebook, I've tested the networks with the original ResNet, basing on [this notebook](https://github.com/ovh/ai-training-examples/blob/main/notebooks/computer-vision/image-classification/tensorflow/resnet50/notebook-resnet-transfer-learning-image-classification.ipynb). 

Results are presented in the table below.

|Name|Date|Loss|Accuracy|Comment|
|---|---|---|---|---|
|ImageNet ResNet|----|0.3605|88.71%|Based on the article|
|Random Initialized ResNet|2024-02-07|1.5288|33.5%||
|Museum CC0 ResNet|2024-02-07|1.5987|29.5%|Trained on 61k of images, 10 epochs|
|Museum CC0 ResNet|2024-02-12|1.5557|28.8%|Trained on 125k of images, 13 epochs, changed RandomCropResize to resize, 25 classes, min. 500 images per class|

For now, the trained ResNet has the same efficiency as an untrained ResNet.

Readme should be updated weekly with progress on the work.

