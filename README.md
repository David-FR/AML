# AML Project

The code in this repository is associated with the paper _[DARTS: Deceiving Autonomous Cars with Toxic Signs](https://arxiv.org/abs/1802.06430)_  and its earlier extended abstract _[Rogue Signs: Deceiving Traffic Sign Recognition with Malicious Ads and Logos](https://arxiv.org/pdf/1801.02780.pdf)_ , a research project under the INSPIRE group in the Electrical Engineering Department at Princeton University. It is the same code that we used to run the experiments, but excludes some of the run scripts as well as the datasets used. Please download the dataset in pickle format [here](https://disq.us/url?url=https%3A%2F%2Fd17h27t6h515a5.cloudfront.net%2Ftopher%2F2017%2FFebruary%2F5898cd6f_traffic-signs-data%2Ftraffic-signs-data.zip%3AWO3Nq9Ds8s63rCvcn6CrIqXkNk0&cuid=4444009), or visit the original [website](http://benchmark.ini.rub.de/?section=home&subsection=news) for GTSRB and GTSDB datasets.  

Website: http://adversarial-learning.princeton.edu/darts/

## Setup 
### Versions
- Tensorflow: 1.15
- Cuda version: 10.0
- CUdnn version: 7.6
- I used conda to facilitate the environment management
- [myevn3.yml](./myenv3.yml): lists the full set of dependencies required to run
### Setup
- Create a conda environent: *conda env create -f myenv3.yml*
- Install all dependencies in [myevn3.yml](./myenv3.yml)
- This will generate an error because the version of *scipy* required to run the code is incompatible
- With *pip* you need to install *scipy version 0.19.1* (This took A LOT) of time to figure out


## Files Organization
### Files with experiments
- [AML.ipynb](./AML.ipynb): demonstrates creation of different models based on miss detection of attacks
- [Tensorflow_GPU.ipynb](./Tensorflow_GPU.ipynb): to check that the GPUs are being used by Tensorflow 1.x correctly


### Files implemented by papers: _[DARTS: Deceiving Autonomous Cars with Toxic Signs](https://arxiv.org/abs/1802.06430)_  and its earlier extended abstract _[Rogue Signs: Deceiving Traffic Sign Recognition with Malicious Ads and Logos](https://arxiv.org/pdf/1801.02780.pdf)_ 
The main implementation is in [./lib](./lib) containing:
- [parameters.py](./parameters.py): Relevant parameters are set in a separate configure file called 
- [utils.py](./lib/utils.py): utility functions
- [attacks.py](./lib/attacks.py): previously proposed adversarial examples generation methods
- [keras_utils.py](./lib/keras_utils.py): define models in [Keras](https://keras.io/)
- [OptProjTran.py](./lib/OptProjTran.py):  optimization code for generating physicall robust adversarial examples
- [Run_Robust_Attack.ipynb](./Run_Robust_Attack.ipynb): demonstrates our procedures and usage of the functions in the library (includes code that we to run most of the experiments from generating the attacks). **Even with the usage of a V100 GPU, this file takes 10+ hours to run (5+ hours per attack)**

- [OptCarlini.py](./lib/OptCarlini.py): implementation of [Carlini-Wagner's attack](https://arxiv.org/abs/1608.04644)
- [RandomTransform.py](./lib/RandomTransform.py): implementation of random perspective transformation

For specific data/setup we used in our experiments:
- [images](./images): contains original images to generate the attacks 
  - [Original_Traffic_Sign_samples](./images/Original_Traffic_Sign_samples): original traffic signs for Adversarial Traffic Signs
  - [Logo_samples](./images/Logo_samples): original logos for Logo Attack
  - [Custom_Sign_samples](./images/Custom_Sign_samples): blank signs to be used as background for Custom Sign Attack
- [adv_signs](./adv_signs): contains some of the adversarial signs we produced, saved in pickle. Organized by types of the attacks: [Adversarial_Traffic_Signs](./adv_signs/Adversarial_Traffic_Signs), [Logo_Attacks](./adv_signs/Logo_Attacks), [Custom_Sign_Attacks](./adv_signs/Custom_Sign_Attacks), and [Lenticular](./adv_signs/Lenticular). Code to read the data is in [Run_Robust_Attack.ipynb](./Run_Robust_Attack.ipynb).
- [keras_weights](./keras_weights): contains the weight of multiple Keras models we used in the experiment
  - `weights_mltscl_dataaug.hdf5`: multi-scale CNN with data augmentation ("CNN A" in the paper)
  - `weights_cnn_dataaug.hdf5`: normal CNN with data augmentation ("CNN B" in the paper)


