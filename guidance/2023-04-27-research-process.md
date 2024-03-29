# Overview
Here, I will talk about the research process: 
1. [setup](#step-1-setup)
2. [data collection](#step-2-data-collection)
3. [model training](#step-3-model-training)
4. [inference](#step-4-inference)
5. [possible extensions](#step-5-extensions). 

There are a couple different repositories we are using to facilitate the data collection and inference process. The diagram below demonstrates how they are connected:

<p align="center">
  <img src="https://user-images.githubusercontent.com/70297740/235019833-8a17623d-fc64-4971-a63e-68229e95897d.jpg" width="500" height="400">
</p>

UE5 is Unreal Engine 5, a videogame-making platform we are using to make hyper-realistic simulations. [UnrealCV](https://github.com/unrealcv/unrealcv) is what we use as a bridge between UE5 and our python scripts, it allows us to communicate with UE5 projects over a port and send in commands to our project to do things like make the agent move, take screenshots, etc. [UE5env](https://github.com/arcslaboratory/ue5env) is a python package developed by the lab that acts as a wrapper around UnrealCV, giving us functions that enable us to easily connect the client, move, etc. via Python scripts. [boxnav](https://github.com/arcslaboratory/boxnav) is a Python script that facilitates movement in UE5 and is what we will use for data collection.

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
For data collection, all work should be done on the lab computer. Clone [boxnav](https://github.com/arcslaboratory/boxnav) onto the computer. Create folders for image collection and your dataset. Then run and specify the script to '--collect' images via the desired navigator type.
* Navigator types are just different methods of data collection.

### TODO: 
Currently, there is currently an issue with the [forward/backward](https://github.com/arcslaboratory/ue5env/blob/main/ue5env/__init__.py#L60) command in the ue5env wrapper. Even when given small incremements, the agent will move much farther forward than intended. There are a couple of ways that we may go about fixing this:
* Maybe use a physical agent like an RC car. This could make it so that we could move the agent to a new spot in the map and/or create a blueprint for greater control of movement in the map. 
  * Note: Make sure your able to disable passive movement (aka make sure the agent won't move down a slope automatically, it will only move with the forward() command).
* We could also try scaling the Oldenborg environments size up so larger movements are relatively more small.
This process may require editing the ue5env repo as well as some of the repos that depend on ue5env like boxnav and OldenborgTraining. I have written TODOs to try and point to areas that may need editing but this may not cover all edits that need to be made.

## Step 3: Model Training
Model training is to be done on the lab server, so you should copy your training images from the lab computer to the server. 

To train models, the [FastAI](https://www.fast.ai/) framework will be used; make sure this is installed in your conda environment.

At this point, it may help to also have [JupyterNotebook](https://jupyter.org/install) in your conda environment, feel free to also install this.

The script to train models is in the [OldenborgTraining](https://github.com/arcslaboratory/OldenborgTraining) repo. In the repo, I have written run_training.py to streamline this process, but you will need to edit this according to your needs. Specifically, you need to edit what dataset you are using and what models you want to change; you may also want to add to this script if you want to train a certain number of iterations of a model. Refer to the repo's ReadMe for info on how to run the script.

## Step 4: Inference
Inference will be done on the lab machine, so you will need to export your trained models onto the lab machine. Inference will also use the [OldenborgTraining](https://github.com/arcslaboratory/OldenborgTraining) repo. Also in the repo, I have written run_inference.py to streamline this process, but you will have to edit this according to your needs. The images collected via inference will be in your UE5 project folder, in the Oldenborg project's ScreenShots<timestamp> folder (the timestamp is the time the folder was created).

## Step 5: Extensions
This project will likely have a couple of extensions beyond training and assessing basic models. Possible Extensions/Next Steps:
* Implement training and inference for cmd+image models
  * Cmd+image models are hybrid CNNs that takes as input the last move the model made as well as the current image frame and output the next move (these were shown to have the best performance in our 2021 experimentations).
  * Old code can be referenced as the original architecture design is in Pytorch, but things like the custom dataset creation as well as training process may differ as new versions of Fastai have come out since 2021.
    * code for training this architecture: [raycasting-simulation](https://github.com/anthonyjclark/raycasting-simulation/blob/master/Experiments/TrainCmdClassification.py)
* Novel data collection
  * Changing lighting with image collection so that everytime you snap a photo of the image, the lighting setting changes multiple times before the agent makes its next move.
  * Maybe could also just have boxnav run through multiple times with differing lighting configurations.
* Development of adversarial examples in order to introduce effective noise into training.
  * This idea came from this [paper](https://aclanthology.org/P19-1103.pdf) on adversarial example generation for textual examples through synonym replacement and a novel scoring/replacement-ordering method.
  * Adversarial examples are examples that have slight changes to examples that the model runs well on, but they make the model act in unexpected, and usually undesired, ways. For example, you want a model to turn left, but you change the lighting and now it goes right.
  * Basically we would edit images with slight distortions until an adversarial example is created. Maybe change things like lighting, texture, color variations, item positioning, etc. until an adversarial example is created then we use those examples to finetune the models.
  * This may be a way of efficiently streamlining the training process, finding the real weaknesses of our models--rather than guessing what they are--and then finetuning our model accordingly.
* Put the model on a robot and have it navigate through Oldenborg!

