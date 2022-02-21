# VQGAN-CLIP Implementation for Process Architecture Testing

A repo for running VQGAN+CLIP locally. This started out as a Katherine Crowson VQGAN+CLIP derived Google colab notebook, and further derived from a project to run the notebook locally using Anaconda for Python found [in this repository](https://github.com/nerdyrodent/VQGAN-CLIP)

This project aims to provide compatibility for arm64-based systems and allow for testing of maching learning workloads across processor architectures.

---
## Hardware and OS Requirements

This project is only tested on an AMD-based x86-64 system (should not differ for Intel processors) and a Raspberry Pi 3B+. With more interest, it may be tested for Apple Silicon-based systems.

64-bit installations of your distro of choice (only tested on Ubuntu 20.04 LTS) are required for this project to run smoothly. Due to lack of development of certain dependancies namely conda and pytorch for armhf and other 32-bit OS's, the project is limited to 64-bit systems (or not, if you are willing and able to get the problematic dependancies installed)

## For x86-64 Processors

The project can be installed and run normally, and for testing purposes Ubuntu 20.04 LTS will be used to provide consistancy. Installation instructions can be found in the [original project repository](https://github.com/nerdyrodent/VQGAN-CLIP)

## For arm64 Processors

Note: This project still remains untested on arm64 architectures, and testing is in progress to provide full compatibility.

Ubuntu 20.04 for arm64 is recommended to provide maximum compatibility, and testing for arm64 compatibility will only be done with the Raspberry Pi model 3B+. Future revisions may include tests done on Apple Silicon-based processors.

### Anaconda for arm64

Anaconda is only developed for x86-64 systems, so miniconda3 must be used, installation instructions can be found [in this thread](https://stackoverflow.com/questions/39371772/how-to-install-anaconda-on-raspberry-pi-3-model-b)

VQGAN is built for Python 3.9, to install in the miniconda3 environment run 
```
conda install python=3.9
```

### Pytorch for arm64

Pytorch is also required, and installation instructions for arm systems can be found [on this page](http://mathinf.com/pytorch/arm64/)

Note: Pytorch now includes arm64 support in their nightly builds, and can be installed with 
```
pip install numpy
pip install --pre torch torchvision torchaudio -f https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html
```
## VQGAN Models
To use with a pretrained image generation model, configure and run the `download_models.sh` script to download your model of choice. A word of caution, these models are massive and take huge amounts of disk space, bandwith, and time to download, so choose your model(s) and download location carefully.

Models can be chosen by editing this section of the `download_models.sh` script. If unchanged, the `Imagenet_16384` model will be downloaded by default.
```
# Which models to download?
IMAGENET_1024=false
IMAGENET_16384=true
GUMBEL=false
#WIKIART_1024=false
WIKIART_16384=false
COCO=false
FACESHQ=false
SFLCKR=false
```

### VQGAN Model Training from Custom Datasets
To train a custom VQGAN model off of custom datasets, use the code and follow the steps in [this project](https://github.com/CompVis/taming-transformers#training-on-custom-data)

As of now, custom model generation is only compatible with the CUDA version of Pytorch, so Nvidia GPU(s) are required. 
## Notes for Testing

The original version of this project is intended to run on GPU CUDA cores and is more efficient in such configuration. To force CPU use, add tag `-cd cpu` in the execution of `generate.py`

For our benchmark testing, the following generate line was used
```
python generate.py -cd cpu -i 500 -s 400 400 -p "A painting of a wizard riding a white horse into the sunset"
```

Image size is heavily dependant on avaliable VRAM, adjust the `-s 400 400` tag accordingly to accomodate avaliable hardware. Furthermore the tag `-ii /path_to/starting_image` can be used to set a starting image for VQGAN.