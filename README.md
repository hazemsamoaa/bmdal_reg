# Deep Batch Active Learning for Regression

This repository contains code accompanying our paper ["A Framework and Benchmark for Deep Batch Active Learning for Regression"](https://arxiv.org/abs/2203.09410). It can be used to apply various pool-based Batch Mode Deep Active Learning (BMDAL) algorithms for regression to custom networks or to compare BMDAL algorithms using our benchmark. An initial version of the code and the data generated by it will be archived at [DaRUS](https://doi.org/10.18419/darus-2615).

## License

This source code is licensed under the Apache 2.0 license. However, the implementation of the acs-rf-hyper kernel transformation in `bmdal/features.py` is adapted from the source code at [https://github.com/rpinsler/active-bayesian-coresets](https://github.com/rpinsler/active-bayesian-coresets), which comes with its own (non-commercial) license. Please respect this license when using the acs-rf-hyper transformation directly from `bmdal/features.py` or indirectly through the interface provided at `bmdal/algorithms.py`.

## Installation

The following packages (available through `pip`) need to be installed:
- General: `torch`, `numpy`, `dill`
- For running experiments with `run_experiments.py`: `psutil`
- For plotting the experiment results: `matplotlib`, `seaborn`
- For downloading the data sets with `download_data.py`: `pandas`, `openml`, `mat4py`

If you want to install PyTorch with GPU support, please follow the instructions [on the PyTorch website](https://pytorch.org/get-started/locally/). The following command installs the versions of the libraries we used for running the benchmark:
```
pip3 install -r requirements.txt
```
Alternatively, the following command installs current versions of the packages:
```
pip3 install torch numpy dill psutil matplotlib seaborn pandas openml mat4py
```

Clone the repository (or download the files from the repository) and change to its folder:
```
git clone git@github.com:dholzmueller/bmdal_reg.git
cd bmdal_reg
```
Then, copy the file `custom_paths.py.default` to `custom_paths.py` via
```
cp custom_paths.py.default custom_paths.py
```
and, if you want to, adjust the paths in `custom_paths.py` to specify the folders in which you want to save data and results.

## Downloading data

If you want to use the benchmark data sets, you need to download and preprocess them. We do not provide preprocessed versions of the data sets to avoid copyright issues, but you can download and preprocess the data sets using
```
python3 download_data.py
```
Note that this may take a while. This depends of course on your download speed. The preprocessing is mostly fast, but for the (large) methane data set, it took around five minutes and 25 GB of RAM for us. If you cannot download/process the data due to limited RAM, please contact the main developer (see below).

## Usage

Depending on your use case, some of the following introductory Jupyter notebooks may be helpful:
- [examples/benchmark.ipynb](https://github.com/dholzmueller/bmdal_reg/blob/main/examples/benchmark.ipynb) shows how to download or reproduce our experimental results, how to benchmark other methods, and how to evaluate the results.
- [examples/using_bmdal.ipynb](https://github.com/dholzmueller/bmdal_reg/blob/main/examples/using_bmdal.ipynb) shows how to apply our BMDAL framework to your use-case.
- [examples/framework_details.ipynb](https://github.com/dholzmueller/bmdal_reg/blob/main/examples/framework_details.ipynb) explains how our BMDAL framework is implemented, which may be relevant for advanced usage.

Besides these notebooks, you can also take a look at the code directly. The more important parts of our code are documented with docstrings.

## Code structure

The code is structured as follows:
- The `bmdal` folder contains the implementation of all BMDAL methods, with its main interface in `bmdal/algorithms.py`.
- The `evaluation` folder contains code for analyzing and plotting generated data, which is called from `run_evaluation.py`
- The `examples` folder contains Jupyter Notebooks for instructive purposes as mentioned above.
- The file `download_data.py` allows for downloading the data, `run_experiments.py` allows for starting the experiments, `test_single_task.py` allows for testing a configuration on a data set, and `rename_algs.py` contains some functionality for adjusting experiment data in case of mistakes. 
- The file `check_task_learnability.py` has been used to check the reduction in RMSE on different data sets when going from 256 to 4352 random samples. We used this to sort out the data sets where the reduction in RMSE was too small, since these data sets are unlikely to make a substantial difference in the benchmark results.
- The files `data.py`, `layers.py`, `models.py`, `task_execution.py`, `train.py` and `utils.py` implement parts of data loading, training, parallel execution.

## Contributors

- [David Holzmüller](https://www.isa.uni-stuttgart.de/institut/team/Holzmueller/) (main developer)
- [Viktor Zaverkin](https://www.itheoc.uni-stuttgart.de/institute/team/Zaverkin/) (contributed to the evaluation code)

If you would like to contribute to the code, please contact David Holzmüller.








