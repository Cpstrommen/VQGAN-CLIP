# VQGAN-CLIP Implementation for Process Architecture Testing

A repo for running VQGAN+CLIP locally. This started out as a Katherine Crowson VQGAN+CLIP derived Google colab notebook, and further derived from a project to run the notebook locally using Anaconda for Python found [in this repository](https://github.com/nerdyrodent/VQGAN-CLIP)

## For x86-64 Processors

The project can be installed and run normally, and for testing purposes Ubuntu 20.04 LTS will be used to provide consistancy.

## For arm64 Processors

Ubuntu 20.04 for arm64 is recommended to provide maximum compatibility, and testing for arm64 compatibility will only be done with the Raspberry Pi model 3B+.

This project still remains untested on arm64 architectures, and testing is in progress to provide compatibility.

## Notes for Testing

The original version of this project is intended to run on GPU CUDA cores and is more efficient in such configuration. To force CPU use, add tag `-cd cpu` in the execution of `generate.py`