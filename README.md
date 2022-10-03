# WASP Summer School 2022

![Project Pipeline](/docs/project-pipeline.gif)

- [Welcome](#welcome)
- [Installation](#installation)
  * [Prerequisites](#prerequisites)
  * [Cloning the repository](#cloning-the-repository)
  * [Setting up Docker](#setting-up-docker)
  * [Setting up Blender Keemap](#setting-up-blender-keemap)
  * [Remarks](#remarks)
- [Next steps](#next-steps)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## Welcome

This repository hosts the full pipeline code for the WASP summer school 2022 project on visualizing 3D avatars with speech driven gestures. The system contains four major components, with corresponding resources broken down into the following folders:

- Generating text with a text prompt : `./subsystem1_text-generation/`
- Synthesizing speech from text : `./subsystem2_text-to-speech/`
- Generating gesture animations from audio : `./subsystem3_gesture-generation/`
- Visualizing the generated gestures : `./subsystem4_visualization/`
 
 <!--In addition, there are two folders in the repository root which are used for storing data files for the pipeline, as well as scripts for running different components of the system. These folders are `./data/` and `./scripts/`, with demo files showing the intended output of the pipeline residing in `./data/demo/`.-->

## Installation

### Prerequisites

Install the following on your machine before continuing with the rest of the setup:

- [git](https://git-scm.com/downloads)
- [Python 3.9.7](https://www.python.org/downloads/release/python-397/)
- [Docker Desktop v4.7.0](https://docs.docker.com/get-docker/) or later
- [NVIDIA Docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)
- [Blender 2.83 LTS](https://www.blender.org/download/releases/2-83/) (also on Steam > Blender > Properties > Betas > 2.83 - Stable - LTS)
- [Unreal Engine 4.25.4](https://www.unrealengine.com/en-US/download) (Windows only)

### Cloning the repository

Run the following commands in shell:

- `git clone https://github.com/WARA-ML/wasp-summer-school-2022.git`
- `cd wasp-2022-summer-school`

The repository makes use of [submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to include code from other repositories without copying files. Run the following to setup the submodules:

- `git submodule update --init --recursive`

### Setting up Docker

Subsystem 3 has code that uses Docker. This allows you to easily set up a working environment with all necessary dependencies, minimizing the risk of running into issues during the process. The script `./scripts/deploy.sh` is provided to automate the setup process. Run the script like this:

- First, make sure Docker Desktop is running!
- `cd ./scripts/`
- `bash ./deploy.sh` on Linux, or `./deploy.ps1` on Windows (PowerShell)

The script will build and deploy one Docker container, as well as mount relevant folders so that they can be accessed from within the container. This process could take a while, so why not check this cool [fluid simulator](https://paveldogreat.github.io/WebGL-Fluid-Simulation/) out in the meantime?

When ready,  verify that the container is deployed by running `docker ps` and looking for the following `IMAGE` string:

- `wasp-gg` (Audio2Gestures from subsystem 3)

Also take note of the `CONTAINER ID`, as it will be needed to run some of the scripts in `./scripts/` from within the Docker container.


### Setting up NVIDIA Docker 

For implementing Subsystem 2, a system with GPU access is required. To setup the environment, run `sudo bash ./subsystem2_text-to-speech/Neural-HMM/start.sh`. The command sets up nvidia docker container with project files in the directory `workspace`. Use the command `exit` to quit the container. 

### Setting up Blender Keemap

The animations exported by the gesture generation models are produced for a particular skeleton (source), defined inside `.bvh` files exported during gesture generation. However, the 3D avatars you will use do not necessarily have the same skeletal hierarchy or proportions (target). The process of transferring animation from one character to another is called "retargeting', and for this we can use the [Keemap plugin](https://github.com/nkeeline/Keemap-Blender-Rig-ReTargeting-Addon)  for Blender. You do not need to go to the repository as we have the necessary files included in the summer school project.

To install Keemap, do the following:

- Open `Blender`
- Select `Edit > Preferences > Add-ons`
- Select `Install`
- Navigate to the repository folder and then go to `/subsystem4_visualization/Blender/KeeMapAnimRetarget.zip`
- Enable `Transfer Animation: KeeMap Animation Transfer Tool` plugin
- Exit `Blender`


### Known issues/warnings

- It is possible that some commands fail due to lack of privilege. If this happens, write `sudo` at the beginning of your commands (on Linux) or launch your terminal with admin privilege (on Windows).
- Generally, all file system paths in this document (and subsystem documents) are relative to the repository root.

## Support

If you have any questions or comments, please open an issue on our GitHub repository.


You should now have all relevant software installed, and Docker set up and running. You are now ready to begin working on your assignments, which you will know more about from the tutorials presented to you during the summer school.

**Good luck and have fun!**

[Back to top](#wasp-summer-school-2022)
