# CUDA 10.1 + CUDNN 7 based docker image with customization to start ML/DL project

## `cuda10-base` image include:
- CUDA 10.1 + CUDNN 7
- Miniconda
- GraphViz
- OpenCV
- Conda environment `work`, include:
  - Numpy
  - Pandas
  - H2O
  - Matplotlib
  - Seaborn
  - GraphViz Python
  - SciPy
  - SciKit-Learn
  - Jupyter
  - OpenCV python
  - Scrapy

## Any other variations?
I still working on this and I will realease another (such as Keras, Tensorflow, PyTorch, or non GPU image) soon

## How to Install

1. Clone this repository

2. From the root directory of this repo, build the image by command below:
```
docker build --network=host -t cuda10-base cuda10-base/
```

3. When image is built and attached, run a container by command below:
```
docker run -d --net=host --name=nvidia-dl-base -e DISPLAY -v <your-shared-dir>:/workspace --runtime=nvidia cuda10-base
```

4. Lastly, login into container by command below:
```
docker exec -it nvidia-dl-base bash
```
