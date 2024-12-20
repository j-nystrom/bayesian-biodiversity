# Bayesian Biodiversity
Large-scale bayesian estimation of biodiversity intactness.

## Getting started

### 1. Clone the repository

To get started, create a project folder on your local machine and clone the repository:

```bash
mkdir <folder_name>
cd <folder_name>
git clone https://github.com/j-nystrom/bayesian-biodiversity.git
```

### 2. Set up a virtual environment

To manage the dependencies of the project, it's recommended that you use a virtual environment. To create a ``conda`` environment with a ``Python`` installation:

```bash
conda create --name <env_name> python=3.11
conda activate <env_name>
```

The project currently requires ``Python`` versions >=3.11 and <3.12, to be compatible with all dependencies.

To install all dependencies, run this from the root of the project:

```bash
conda config --add channels conda-forge
conda install --file requirements.txt
```

### 3. Configure the PYTHONPATH

To enable imports of project modules into other parts of the project like this,

```python
from core.data.data_processing import create_site_coord_geometries
```

 we need to set the ``PYTHONPATH`` to recognize the project folder structure. Create a file named ``set_path.sh`` (for Linux / macOS) or ``set_path.bat`` (for Windows) in the following directory within your Conda environment:

```bash
<conda_env_path>/etc/conda/activate.d/
```

Replace ``<conda_env_path>`` with the actual path to your Conda environment, which you can find by running ``conda info --envs``.

In the file you created, add the content below.

Linux / macOS:
```bash
#!/bin/sh
export PYTHONPATH="<path_to_your_project>:$PYTHONPATH"
```

Windows:
```bash
@echo off
set PYTHONPATH=<path_to_your_project>;%PYTHONPATH%
```

Replace ``<path_to_your_project>`` with the actual path to the project's root directory.

Finally, we need to unset the path when deactivating the environment. Create an ``unset_path.sh`` (Linux / macOS) or ``unset_path.bat`` (Windows) in the equivalent deactivation folder

```bash
<conda_env_path>/etc/conda/deactivate.d/
```

with the content below.

Linux / macOS:
```bash
#!/bin/sh
unset PYTHONPATH
```

Windows:
```bash
@echo off
set PYTHONPATH=
```

## Local data storage structure

The project is currently set up to use local file storage on disk. For the code to run out of the box, it's important that the input and output data follow the structure shown below:

```
└── bayesian-biodiversity (*this is where the code is located*)
└── data (*main data directory at the same level as the code*)
    ├── PREDICTS
    │   ├── PREDICTS_2016
    │   │   ├── data.csv
    │   ├── PREDICTS_2022
    │   │   ├── data.csv
    ├── EarthEnv
    │   └── topography
    │       ├── elevation_1KMmn_GMTEDmd.tif
    │       ├── roughness_1KMmn_GMTEDmd.tif
    │       ├── sdata201840.pdf
    │       ├── slope_1KMmn_GMTEDmd.tif
    │       └── tri_1KMmn_GMTEDmd.tif
    ├── WorldClim
    │   ├── Bioclimatic
    │   │   ├── wc2.1_30s_bio_1.tif
    │   │   ├── wc2.1_30s_bio_10.tif
    │   │   ├── wc2.1_30s_bio_11.tif
    │   │   ├── wc2.1_30s_bio_12.tif
    │   │   ├── wc2.1_30s_bio_13.tif
    │   │   ├── wc2.1_30s_bio_14.tif
    │   │   ├── wc2.1_30s_bio_15.tif
    │   │   ├── wc2.1_30s_bio_16.tif
    │   │   ├── wc2.1_30s_bio_17.tif
    │   │   ├── wc2.1_30s_bio_18.tif
    │   │   ├── wc2.1_30s_bio_19.tif
    │   │   ├── wc2.1_30s_bio_2.tif
    │   │   ├── wc2.1_30s_bio_3.tif
    │   │   ├── wc2.1_30s_bio_4.tif
    │   │   ├── wc2.1_30s_bio_5.tif
    │   │   ├── wc2.1_30s_bio_6.tif
    │   │   ├── wc2.1_30s_bio_7.tif
    │   │   ├── wc2.1_30s_bio_8.tif
    │   │   └── wc2.1_30s_bio_9.tif
    │   └── Elevation
    │       └── wc2.1_30s_elev.tif
    ├── GPW
    │   ├── gpw_v4_2000_30_sec.tif
    │   ├── gpw_v4_2005_30_sec.tif
    │   ├── gpw_v4_2010_30_sec.tif
    │   ├── gpw_v4_2015_30_sec.tif
    │   ├── gpw_v4_2020_30_sec.tif
    ├── gROADS
    │   ├── africa
    │   │   ├── gROADS-v1-africa.shp
    │   ├── americas
    │   │   ├── gROADS-v1-americas.shp
    │   ├── asia
    │   │   ├── gROADS-v1-asia.shp
    │   ├── europe
    │   │   ├── gROADS-v1-europe.shp
    │   ├── oceania
    │   │   ├── groads-v1-oceania.shp (note: merged outside of main code)
    │   ├── oceania-east
    │   │   ├── gROADS-v1-oceania-east.shp
    │   ├── oceania-west
    │   │   ├── gROADS-v1-oceania-west.shp
    ├── output
    ├── runs

´´´


### Data sources

*To be added*

## Running the code

### 1. Organization of pipelines
The code is organized into ``DAGs``, ``Tasks`` and ``Modules``:

``DAG``: This is the entry points to running the code. Each DAG consists of one or several Tasks that are run in sequence. For example, to run the first step of preprocessing of the PREDICTS data, just navigate to the ``core/dags`` folder and run:
```bash
python dags.py predicts
```
``Task``:

``Module``:

To validate that everything has been set up correctly, try running the ``predicts`` DAG shown above, after downloading the data and putting it in the right folder.

### 2. Overview of DAGs and Tasks

This list contains all the steps required to run the whole pipeline end-to-end, starting with raw data and ending with model predictions and validation.

*To be filled out*
