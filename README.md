# Give context to solver errors in Solved Python Packages

## Aim
Use solver dataset provided by [Thoth Dependency Solver](https://github.com/thoth-station/solver), so that we can derive context on why dependencies cannot be solved in order to better advise users on why something cannot be used.

## Background on Thoth Dependency solver
The aim of Thoth solver is to answer a simple question - what packages will be installed (resolved by pip or any Python compliant dependency resolver) for the provided stack? 

**What is a solver?**
In Thoth language a solver example is solver-fedora-31-py37 which is named after:
- **operating system** used (e.g Fedora 31)
- **Python interpreter** installed (e.g. Python 3.7)\
on which the specific **Python package** is going to be installed.


## Thoth Solver Dataset 
[Thoth Solver Dataset](https://github.com/thoth-station/datasets) is part of a series of datasets related to observations regarding software stacks (e.g. dependency tree, installability, performance, security, health) as part of Project Thoth. \
Thoth Solver Dataset is made by solver reports in json format, where each solver report is created for a specific package (e.g Python package from a certain index in a certain version), solved using a certain solver and it is described in the notebook called [Thoth Solver Dataset](https://github.com/thoth-station/datasets/blob/master/notebooks/thoth-solver-dataset/ThothSolverDataset.ipynb).


### Thoth Solver Error Data
If the installation of a package was not succesfull there will be information stored for each package error;
#### Solver Error data from solver reports consists of following information:
- **command**,command used to install the package;
- **message**,error log;
- **return_code**,
- **stderr**,
- **stdout**,
- **timeout**,
- **index_url,** from where the package was download;
- **package_name;**
- **package_version;**
- **type,** error type;


## This repo contains two notebooks :
**These notebooks can be executed in a workflow using [papermill](https://github.com/nteract/papermill).**

**1. Template notebook to pre-process solver dataset and output clean dataset which is the input for clustering : [notebooks/PreprocessSolverErrorData.ipynb](notebooks/PreprocessSolverErrorData.ipynb)** \
The purpose of this notebook is to preprocess solver data, i.e, extract error data from solver data, prepare data for clustering, clean and tokenize the clustering data and save the clean dataset for ClusterError notebook.\
Excuecute via CLI: \
 `papermill PreprocessSolverErrorData.ipynb PreprocessSolverErrorData.ipynb -p get_fresh_data False`\
 where get_fresh_data is the parameter which decides if we need to get fresh data from Ceph or use the data from csv file.
 
**2. Template notebook to cluster errors to identify the type of errors that can appear in solver reports : [notebooks/ClusterErrors.ipynb](notebooks/ClusterErrors.ipynb)** \
The purpose of this notebook is to cluster solver errors in order to identify the type of errors that can appear in solver reports.\
 Excuecute via CLI: \
 `papermill ClusterErrors.ipynb ClusterErrors.ipynb -p preprocessed_filename  'error-clean-data.csv'`\
 where preprocessed_filename is the parameter which contains the filename of preprocessed clean data.

## Background/References
**1. Thoth:** https://thoth-station.ninja/ \
**2. Thoth GitHub:** https://github.com/thoth-station \
**3. Solver:** https://github.com/thoth-station/solver \
**4. Thoth Solver dataset on Kaggle:** https://www.kaggle.com/thothstation/thoth-solver-dataset-v10 \
**5. Thoth Solver dataset on GitHub:** https://github.com/thoth-station/datasets 
