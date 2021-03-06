---
title: "`conda` quickref"
author: "Christopher Johnson"
date: "2021-03-23"
output: 
  html_document:
    keep_md: true
    toc: true
    toc_float:
      smooth_scroll: true
---

## Anaconda

To get `conda` and Anaconda Prompt, [download and install Anaconda](https://www.anaconda.com/download/). It is very easy to [install](https://docs.anaconda.com/anaconda/install/) and [verify](https://docs.anaconda.com/anaconda/install/verify-install/).

`conda` is

* the command line alternative to Anaconda Navigator
* a package manager
* a virtual environment manager
* is similar to `virtualenv` and `pyenv`
* language agnostic
  * yes, this includes R!

## Conda workflows

One workflow is based on *accomplishing a task*:

1. create an environment (`conda create`)
2. activate it (`conda activate`)
3. explore it (`conda list`)
3. search for and install needed packages (`conda search`, `conda install`)
4. update or remove those packages (`conda update`, `conda remove`)
5. do some work (`ninja.exe`)
6. deactivate (`conda deactivate`)

Another workflow is based on *managing your tasks*:

1. list environments (`conda info --envs`, `conda env list`)
2. list contents of a specific environment (`conda list`)
2. delete environments (`conda remove`)

## Environments

An environment includes

* a Python interpreter
* a Python packages
* utility scripts
  * `conda`
  * `pip`

The default virtual environment is `base(root)`, where root is `C:/Users/user/AppData/Local/Continuum/anaconda3/`. <!-- verify this is correct -->

Matthew Sarmiento provides a nice [guide to Conda environments](https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533).

## Choose your environment

To list all environments, use one of `conda env list` or `conda info --envs`.

The active environment can be determined with

    conda activate env_name
    echo %CONDA_PREFIX%

## Create your environment

To create an environment with a specific version `M.m` of Python and packages, use `conda create -n env_name [python=M.m] [list_of_packages]`.

## Explore your environment

To list everything in the active environment, use `conda list`.

`env list` to show all environments (alternatively `conda info --envs`)

To list everything in a specific environment, use `conda list -n env_name`. Likewise, a query for a specific package in a specific environment is possible with `conda list -n env_name package_name`.

To get the instance of Python being used by an environment

    conda activate env_name
    where python

## Change your environment

### Install packages

To install a single package, submit `conda install package_name` to the Anaconda Prompt. Multiple packages can be installed by providing a list, e.g. `conda install package_1 package_2`. To install a specific version `M.m` (major and minor) of a package, use `conda install package_1=M.m`.

Search for a package: `conda search *search_term*` (or `conda search '*search_term*'` if shell expands `*`). For Geeks: MatchSpec is the query language for conda; this is what is used.

### Upgrade packages

Update all the packages:

    conda upgrade conda
    conda upgrade --all

`conda upgrade --all` should encompass `conda upgrade conda`, but it doesn't hurt

### Update packages

Packages should be updated in the default environment.

`conda update package_name`

`conda update --all` <!-- how does this differ from `conda upgrade --all`? -->

### Remove packages

Packages can be removed from an environment with `conda remove package_name`.

Remove (delete) an environment: `conda env remove -n env_name`

To remove environments

    conda remove --name name_of_project --all

## Change environments

Activate an environment: `conda activate my_env`

Activated projects will have the prompt `(my_env) ~ $`

Deactivate current environment: `conda deactivate`

## Share your environment

`conda` makes it possible to create a file that specifies the dependencies for a project so that it can be used by collaborators to recreate the environment. 

`conda env export` prints the dependencies to the console (useful for previewing). To write those dependencies to file to share with collaborators, submit `conda env export > environment.yaml`. Anyone with the `environment.yaml` file can recreate the environment with `conda env create -f environment.yaml`.

### `pip` and `virtualenv`

If collaborating with someone who doesn't use Anaconda, no worries: Anaconda includes `pip`. Verify `pip` is installed by submitting `pip --version` to the Anaconda Prompt. If for some reason `pip` is not installed, install it with `conda install pip`.

The `pip` analog to 

* `environment.yaml` is `requirements.txt`
* `conda env export` is `pip freeze`
* `conda env create` is `pip install`

Usage is shown below:

    pip freeze > requirements.txt
    pip install -r requirements.txt

## Best practices

It is a good idea to create some sandbox environments that are for general hacking. The following creates Python 2 and Python 3 "sandboxes":

    conda create -n py2_env python=2
    conda create -n py3_env python=3

## Get help

To view all `conda` commands, submit `conda --help` in Anaconda Prompt. To view help for a specific command, simply append `--help` to the command.

Check out the following from Anaconda: 

* [Starter guide](https://docs.anaconda.com/_downloads/9ee215ff15fde24bf01791d719084950/Anaconda-Starter-Guide.pdf)
* [Cheat sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf)
* [Conda glossary](https://docs.conda.io/projects/conda/en/latest/glossary.html).
* [Command reference](https://conda.io/projects/conda/en/latest/commands.html)
* [Managing environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#managing-environments)

## Interesting reads

Jake VanderPlas published a list of [myths and misconceptions about `conda`](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/).
