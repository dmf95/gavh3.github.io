---
title: Why you need a conda environment, like now.
date: 2021-09-13 18:25:00 -0700
categories: [Bloopers]
tags: [python, selfpost]     # TAG names should always be lowercase
image:
  src: /assets/img/matrixcode.jpg
  width: 640   # in pixels
  height: 427   # in pixels
  alt: it's all virtual.
---
Before we begin, I want to say that this is not a comprehensive guide to Python virtual environments. There are very good resources online already discerning between conda, pip, and virtualenv (see: [The Definitive Guide to Conda Environments](https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533))

Let me start off with a story of how I wasted an entire afternoon after corrupting my conda environment.

#### How I ended up here
Recently, a Python package - `vaex` was brought to my attention. This library was everything we ever wanted to overcome a technical challenge at work. It's actually pretty nifty and I would recommend checking out their [docs](https://vaex.io/docs/index.html). Long story short, it wasn't the easiest to install on top of my already-bloated list of installed packages.

After tracing back error after error and a slew of package downloads later.. nothing. I had tried running so many random commands at this point that the next step is one that anyone with a remotely IT-related background would default to - blow it all up.

Since I hadn't been disciplined to properly use environments, every project I've ever worked on was built on one aptly named "py3". On top of the mess that remains of my py3 environment, none of my other project code worked. How I would have done it differently:

#### Creating conda environments
Before diving into commands, let's take a step back and talk a little about Anaconda. By default, Anaconda creates an environment called "base". You'll see this in brackets `()` whenever you open Anaconda Prompt. `base` contains the version of Python that was installed with Anaconda. I like to treat `base` as if it were sacred, and just avoid installing additional libraries directly to it.

If you navigate to `/your/anaconda/path/` on a new Anaconda install, you find a empty folder called `envs`. Running `conda create -n YOUR_ENV_NAME` tells Anaconda to create a fresh environment into `envs`. At this point, the environment is entirely **empty** (no interpreter, no packages). By the way, a good rule of thumb is to create a new environment for each new project. You can also specify the version of Python that you want for this new environment by slightly modifying the command to `conda create -n YOUR_ENV_NAME python=X.X`. This method comes with Pip installed automatically inside the environment. Note that you can also create a new environment [based off of an existing environment](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#cloning-an-environment). Now, go ahead and install the packages for your project! Yay, you can now avoid needless package dependency conflicts. Please clap.

If you encounter `command not found: pip` in your new environment, running `conda install pip` should take care of it.

#### Deleting existing environments
Should you decide to part ways with your conda environment, first **make sure it is deactivated** by running `conda deactivate`. Then, it's as simple as running `conda env remove -n YOUR_ENV_NAME`. This should automatically remove the folder inside `envs` for that environment, but if not, you can manually delete it if you want to reuse the name. Double check with `conda env list` that the environment you deleted is no longer listed.

So, recap thus far:
- Keep your **base environment clean**
- Use `conda create -n YOUR_ENV_NAME python=X.X` when possible. Install Pip immediately after if you'd rather leave out the `python=X.X` part
- For each new project, make a new conda environment. It's free to do!
- To delete an environment, call `conda deactivate` and `conda env remove -n YOUR_ENV_NAME`. Confirm with `conda env list`.