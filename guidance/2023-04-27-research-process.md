# Overview
Here, I will talk about the research process: [setup](#step-1-setup), [data collection](#step-2-data-collection), [model training](#step-3-model-training), [inference](#step-4-inference), and [possible extensions](#step-5-extensions) 
* note: you can click these links to jump to that section in the markdown. 

There are a couple different repositories we are using to facilitate the data collection and inference process. The diagram below demonstrates how they are connected:

<p align="center">
  <img src="https://user-images.githubusercontent.com/70297740/235019833-8a17623d-fc64-4971-a63e-68229e95897d.jpg" width="500" height="400">
</p>

UE5 is Unreal Engine 5, a videogame-making platform we are using to make hyper-realistic simulations. [UnrealCV](https://github.com/unrealcv/unrealcv) is what we use as a bridge between UE5 and our python scripts, it allows us to communicate with UE5 projects over a port and send in commands to our project to do things like make the agent move, take screenshots, etc. [UE5env](https://github.com/arcslaboratory/ue5env) is a python package developed by the lab that acts as a wrapper around UnrealCV, giving us functions that enable us to easily connect the client, move, etc. via Python scripts. [boxnav](https://github.com/arcslaboratory/boxnav) is a Python script that facilitates movement in UE5.

One more repository, we will use is called [OldenborgTraining](https://github.com/arcslaboratory/OldenborgTraining). This repo contains scripts to train models and conduct inference in the Oldenborg Training environment.

If something is confusing, please email/slack me or refer to my reports (and search for key words via the github search bar) for more information.

## Step 1: Setup
You will first need to setup UE5 and unrealcv. Follow this [tutorial](https://compusciencing.github.io/unrealcv-ue5-windows.html) to do this. Refer to Professor Clark to get an idea of which software you need to setup (it may or may not be everything in the tutorial).
* note: when opening projects that contain the plugins for unrealcv, you will be notified that the project includes plugins made for UE5.0. Just press continue.
* I recommend taking some time to get oriented with UE5, a basic tutorial on the mechanics + orientation with some of its capabilities should be fine for now

With UE5 and unrealcv now installed, you should be able to clone the lab repositories that you need in order to have an agent move through a UE5 project. Clone the [UE5env](https://github.com/arcslaboratory/ue5env) repository and the [boxnav](https://github.com/arcslaboratory/boxnav) repository. Refer to the boxnav ReadMe for information on how to run boxnav and more information about it. Make sure to test that boxnav is working by just trying to run it.
* note: REMEMBER your UE5 project must be in playmode in order for a connection to be made between your python script and UE5.

Now we will setup the Oldenborg project that Liz made in Unreal Engine. The project is [here](https://github.com/arcslaboratory/OldenborgUE). Clone this repository, put it in your UE5 project folder, make sure to copy the UnrealCV plugin into the project (like you've done with other projects), and open the project in UE5. The project may or may not load in.
* if the project is not loading in -> [Untick the "is Spacially Loaded" box](https://forums.unrealengine.com/t/map-check-error-level-script-blueprint-refrences-streamed-actor/534202/7) on the elements that come up as causing errors. See link for more info.

## Step 2: Data Collection
boxnav, but forward issue

## Step 3: Model Training
Model training is to be done on the lab server. To train models, the [FastAI](https://www.fast.ai/) framework will be used; make sure this is installed in your conda environment.

At this point, it may help to also have [JupyterNotebook](https://jupyter.org/install) in your conda environment, feel free to also install this.

The script to train models is in the [OldenborgTraining](https://github.com/arcslaboratory/OldenborgTraining) repo. I have written a [training script](https://github.com/christymarc/OldenborgTraining/blob/inference_training/run_training.py) to streamline this process, but you will need to edit this according to your needs. Specifically, you need to edit what dataset you are using and what models you want to change; you may also want to add to this script if you want to train a certain number of iterations of a model. Refer to the repo's ReadMe for info on how to run the script.

## Step 4: Inference
## Step 5: Extensions
novel data collection, changing lighting with image collection
development of adversarial examples in order to introduce effective noise into training
