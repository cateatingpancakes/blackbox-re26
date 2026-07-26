This repository contains our work for the Blackbox reproducibility challenge. We reproduce the findings of a study by [Bolukbasi et al. (2021)](https://arxiv.org/abs/2104.07143) in which the authors find that the neurons of [a BERT model](https://huggingface.co/google-bert/bert-base-uncased) appear to have "learned" certain patterns, but that this appearance is illusory and vanishes upon a closer analysis.

## Repository structure

Below is a summary of the files and purpose of each directory and important subdirectory in our project.

|Directory|Files and purpose|
|-|-|
|`/datasets`|Contains 8 top-level files with the exact samples we used from each dataset. For each dataset, there is a human-readable `.csv` file and a `.parquet` file we use in code.|
|`/embeds`|This directory should be empty on the repository, as the files required within are too large for upload. This directory contains the sentence embeddings for each dataset in a subdirectory `/embeds/full`. Get the sentence embeddings we used in a release or regenerate them using the notebook in `/scripts/encode_samples.ipynb`.|
|`/tokenized`|Used mainly for `/scripts/experiments/exp_03`. Contains the BERT-tokenized datasets in a subdirectory `/tokenized/datasets`, alongside the 828-token vocabulary we considered and the monotonically increasing/decreasing tokens from this vocabulary.|
|`/panels`|Contains our 10-sentence panels given to annotators in `.csv` and `.parquet` format. The annotation data we received can also be found before and after manual grouping was performed on identical-meaning annotations.|
|`/scripts`|Contains the notebooks with the code we ran. Here we prepare the datasets, calculate the sentence embeddings and run our experiments. Naming should be generally descriptive, e.g. `save_samples.ipynb` saves our dataset samples to a location in `/datasets`.|

## Our experiments

Each directory in `/scripts/experiments` represents some task or experiment we performed to obtain our reproducibility results. Here is a listing of all of them:

|Directory|What it does|
|-|-|
|`exp_00`|Generates the UMAP diagram with all 4 datasets projected on it, which is used in Figure 1.|
|`exp_01`|Obtains and summarize statistics from our annotators' data, producing Tables 1 and 2.|
|`exp_02`|Trains a SVM classifier with [scikit-learn](https://scikit-learn.org) to prove the linear separability of the considered datasets. The confusion matrix is reported in the paper in Figure 2.|
|`exp_03`|Looks at how some neurons encode certain concepts, based on their (monotone or not) activations when a token that "proxies" for the concept is present in sentences. Used to make Figure 3 and Table 3.|
|`exp_04`|Calculates locality scores between a top-activating sentence and the other 9 top-activating sentences and compares it to the score for a draw of 10 random sentences, showing the presence of local concepts. This experiment produces Table 4.|
|`exp_05`|Summarizes statistics like `exp_01`, except the annotator here is a LLM, not a human.|

## Requirements

Quick refresher on how to set up the Python environment needed to run the scripts:

- Create a new virtual environment in a directory `/.venv` with `python -m venv .venv`.
- Activate it with `source /.venv/bin/activate` on Linux or `/.venv/Scripts/activate` on Windows.
- Install the requirements with `pip install -r requirements.txt`.
- Use this virtual environment as the kernel for the notebooks you want to run.

## Read our paper

We have also included [the paper](blackbox_nlp.pdf) here for convenience, exactly as we submitted on [OpenReview](https://openreview.net/). Authors remain anonymized.