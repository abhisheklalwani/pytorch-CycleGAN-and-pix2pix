## Introductions
This repository highlights my research over the Summer of 2021 at the Computer Vision Lab, University of Massachusetts Amherst, under the supervison of Professor Subhransu Maji.

My research majorly revolves around the generation of realistic textures from basic sketches.

We have majorly explored the conditional GAN architecture for this task, with a specific focus on Pix2Pix, given the easily expandable nature of the Pix2Pix architecture.

We have also explored various inputs in this task, such as global color palettes as well as local color scribbles, which supplement our basic input of human-drawn sketches.
We modify the basic pre-processing pipeline of the Pix2Pix to support these inputs.

We have also focused on StyleGAN architecture, which we will document in a separate repository.

## Prerequisites
- Linux or macOS
- Python 3
- CPU or NVIDIA GPU + CUDA CuDNN

## Getting Started
### Installation

- Clone this repo:
```bash
git clone https://github.com/abhisheklalwani/pytorch-CycleGAN-and-pix2pix.git
cd pytorch-CycleGAN-and-pix2pix
```

- Install [PyTorch](http://pytorch.org) and 0.4+ and other dependencies (e.g., torchvision, [visdom](https://github.com/facebookresearch/visdom) and [dominate](https://github.com/Knio/dominate)).
  - For pip users, please type the command `pip install -r requirements.txt`.
  - For Conda users, you can create a new Conda environment using `conda env create -f environment.yml`.
  - For Docker users, we provide the pre-built Docker image and Dockerfile. Please refer to our [Docker](docs/docker.md) page.
  - For Repl users, please click [![Run on Repl.it](https://repl.it/badge/github/junyanz/pytorch-CycleGAN-and-pix2pix)](https://repl.it/github/junyanz/pytorch-CycleGAN-and-pix2pix).

### pix2pix test
1. Download the zipped checkpoints folder from the [link](https://drive.google.com/file/d/1CTyLfVdBEUra1d4pt3spc-813fK3Vk4b/view?usp=sharing) here and extract it in the main folder. It contains 3 models for the 3 supported use-cases.
    - Edges-to-Textures (dtd_pix2pix_150)
    - Edges-plus-Color-to-Texture (Global) (dtd_pix2pix_150_single_color)
    - Edges-plus-Color-to-Texture (Local) (dtd_pix2pix_100_local_color)
2. Put your data in the datasets folder. There is a specific format for setting up the testing data for each model. You can find some example in the current dataset folder. Make sure that the input size is 256x256 or 512x256 (For the single color use-case).
3. Test the model by running the command given below - 
```
python test.py --dataroot ./datasets/dtd_binary_test --name dtd_pix2pix_binary --model test --netG unet_256 --norm batch
```
- Fr testing the dtd_pix2pix_150_single_color model, please specify one more parameter ```--input_nc 4```. This is done to specify that the model should take 4 channels as input. 1 for the edge map and 3 for the dominant color.
- The dataroot parameter will contain the folder which will contain the images which you want to test.
- The name parameter will take the model name which you want to test. You can find the model names given in the brackets above. Rest of the parameters should be used as is.
- The test results will be saved to a html file here: `./results/facades_pix2pix/test_latest/index.html`. You can find more scripts at `scripts` directory.
