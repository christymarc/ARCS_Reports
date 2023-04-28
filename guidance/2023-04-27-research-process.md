# Overview
Here, I will talk about the research process: [setup](#step-1-setup), [data collection](#step-2-data-collection), [model training](#step-3-model-training), [inference](#step-4-inference), and [possible extensions](#step-5-extensions). 

There are a couple different repositories we are using to facilitate the data collection and inference process. The diagram below demonstrates how they are connected:

![research_diagram](https://user-images.githubusercontent.com/70297740/235019833-8a17623d-fc64-4971-a63e-68229e95897d.jpg = 250x300)

UE5 is Unreal Engine 5, a videogame-making platform we are using to make hyper-realistic simulations. [UnrealCV](https://github.com/unrealcv/unrealcv) is what we use as a bridge between UE5 and our python scripts, it allows us to communicate with UE5 projects over a port and send in commands to our project to do things like make the agent move, take screenshots, etc. [UE5env](https://github.com/arcslaboratory/ue5env) is a python package developed by the lab that acts as a wrapper around UnrealCV, giving us functions that enable us to easily connect the client, move, etc. via Python scripts. 

If something is confusing, please email/slack me or refer to my reports (and search for key words via the github search bar) for more information.

## Step 1: Setup
You will first need to setup UE5 and unrealcv. Follow this [tutorial](https://compusciencing.github.io/unrealcv-ue5-windows.html) to do this. Refer to Professor Clark to get an idea of which software you need to setup (it may or may not be everything in the tutorial).
* note: when opening projects that contain the plugins for unrealcv, you will be notified that the project includes plugins made for UE5.0. Just press continue.
* I recommend taking some time to get oriented with UE5, a basic tutorial on the mechanics + orientation with some of its capabilities should be fine for now

With UE5 and unrealcv now installed, you should be able to clone the lab repositories that you need in order to have an agent move through a UE5 project. Clone the [UE5env](https://github.com/arcslaboratory/ue5env) repository and the [boxnav](https://github.com/arcslaboratory/boxnav) repository. Refer to the boxnav ReadMe for information on how to run boxnav and more information about it.
* note: REMEMBER your UE5 project must be in playmode in order for a connection to be made between your python script and UE5.

## Step 2: Data Collection
## Step 3: Model Training
## Step 4: Inference
## Step 5: Extensions
