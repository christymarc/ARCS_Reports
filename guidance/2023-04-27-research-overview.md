# Overarching Goal of the Lab
The ARCS Lab is approaching the challenge of bridging the reality gap between simulated learning and real-life performance of robots

## Overarching Goal of Unreal Engine 5 (UE5) Research Project
The goal of this project is to create a hyper-realistic simulation in which a robot can memorize a path from start to finish in training then perform real-world navigation through the same non-simulate environment.
* with this goal, we are looking to isolate and observe the robot's ability to cross the reality gap rather than its ability to semantically navigate through environments
* the simulated environment is modeled after Oldenborg dorm in UE5
* this work is an extention of the work described in this paper: [Investigating Neural Network Architectures, Techniques, and Datasets for Autonomous Navigation in Simulation](https://cs.pomona.edu/~ajc/pdf/Chang.2021.SSCI.Architectures.pdf)

## Research Questions to Answer
From basic to complex (with reference to each step of the research process we look at):
* can we train an accurate model? -: (training)
* can we train a robot and have it perform well in the same environment with the same conditions? (inference/testing)
* can we have it perform well in simulated environments with different conditions? (generalization)
* can we train a model using simulation and have a real-world robot operate in Oldenborg dorm? (crossing the reality gap)
