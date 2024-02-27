# cc0-resnet-learning
Download CC0 datasets from museums and train a ResNet-50 on them! WIP, will serve as a backbone for my other ReIndentifiCATion project.

Currently work-in-progress, is suppossed to be updated more or less daily with new commits until it's done.

### Training

1. Use notebooks to download datasets from three museums. They can be done in parallel, this process may take about 30h, depending on set dataset size.
   1. CMA Collection Download
   2. MET Collection Download
   3. NGA Collection Download
   4. AIC Collection Download
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
|Museum CC0 ResNet|2024-02-14|1.5038|33.5%|Trained on 125k of images, 200 epochs, 25 classes, added a learning rate scheduler|
|Museum CC0 ResNet|2024-02-22|1.3672|55.3%|Trained on 189k of images, 27 epochs, 51 classes, added AIC dataset, downloaded much more data, changed optimizer to SGD. Training is now much more chaotic.|
|Museum CC0 ResNet|2024-02-22|1.2476|51.0%|Trained on 189k of images, 90 epochs, 51 classes.|

The trained ResNet, after adding much more data, is able to at last achieve a better score than a random network, showing it's possible to do learning transfer from it. 

Readme should be updated weekly with progress on the work.

Roadmap:
1. Adding Getty Museum data scraping and its incorporation into the pipeline
2. Scraping more MET Museum data
3. Training a neural network on the data
4. If the test taccuracy on the flower dataset is at least 60%, then publishing the model on HuggingFace
5. Working on more sources of CC0 data 

