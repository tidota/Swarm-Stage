# Swarming of Multiple Robots on Stage
*The Argos version can be found [here](https://github.com/tidota/swarm-argos).

This contains code to simulate swarming of multiple robots, which runs on [Stage simulator](https://github.com/rtv/Stage). A swarm of robots forms a path from the starting point to the destination in an unknown environment. The program is based on the algorithm proposed by Nouyan et al. ([Path formation in a robot swarm](https://link.springer.com/article/10.1007/s11721-007-0009-6)).

To simulate a large group of robots, the whole system was made lighter by directly running the program on Stage without Player or any other middleware.
I modeled a (very) simple robot for swarming simulation with specific world files. It follows a set of rules to interact with the environment locally, and a group of robots engenders emergence of more compilated behaviors as a whole system.

<img src="./img/footbot_stage.png" width="150"> <img src="./img/footbots_stage.png" width="300"> <img src="./img/demo_stage_large2.png" width="300">


## Dependencies
The same as the original Stage does.
On my PC (Ubuntu 16.04), I installed the following.
```
sudo apt-get install git cmake g++ fltk1.1-dev libjpeg8-dev libpng12-dev libglu1-mesa-dev libltdl-dev
```

## Installation
```
mkdir stage
cd stage
git clone git@github.com:tidota/swarm-stage.git
export STG=$HOME/stg
cmake -DCMAKE_INSTALL_PREFIX=$STG swarm-stage
make
make install
```
## Environment Settings
add these lines at the end in .bashrc
```
export STG=$HOME/stg
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$STG/lib
export PATH=$PATH:$STG/bin

```
Then, on the terminal
```
. ~/.bashrc
```

## To Run It
On the terminal,
```
stage swarm-stage/worlds/<world file>
```
For example,
```
stage swarm-stage/worlds/pathformdemo_05.world
```
This will run a simulation with 5 walking robots (with the start and goal robots).

<img src="./img/demo_stage_ideal.png" width="250"> <img src="./img/demo_stage_ideal2.png" width="250"> <img src="./img/demo_stage_ideal3.png" width="250">

## System Diagram
The core code is designed to be used by other simulators such as ARGoS.
<img src="./img/prog_diagram.png" width="600">

________________________________________________________________
________________________________________________________________
The following below is the original README.md of Stage
________________________________________________________________
________________________________________________________________
# The Stage Simulator
This is the Stage README file, containing an introduction, license and citation information. Stage is a 2(.5)D robotics standalone simulator and can also be used as a C++ library to build your own simulation environment. Up-to-date **documentation can be found [here](https://codedocs.xyz/CodeFinder2/Stage/)**.

For release notes see RELEASE.txt
For installation notes see INSTALL.txt

Copyright Richard Vaughan and contributors 1998-2011
Part of the Player Project (http://playerstage.org)

[![Build Status](https://travis-ci.org/CodeFinder2/Stage.svg?branch=master)](https://travis-ci.org/CodeFinder2/Stage)

# License
This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License version 2 as
published by the Free Software Foundation.

This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
General Public License for more details.

A copy of the license is included with the sourcecode in the file
'COPYING". Copying and redistribution is permitted only under the
terms of the license.


# Introduction
Stage is a robot simulator. It provides a virtual world populated by
mobile robots and sensors, along with various objects for the robots
to sense and manipulate.

There are three ways to use Stage:
  1. The "stage" program: a standalone robot simulation program
that loads your robot control program from a library that you provide.
  2. The Stage plugin for Player (libstageplugin) - provides a
population of virtual robots for the popular Player networked robot
interface system.
  3. Write your own simulator: the "libstage" C++ library makes it
easy to create, run and customize a Stage simulation from inside your
own programs.


# Models
Stage provides several sensor and actuator models, including sonar
or infrared rangers, scanning laser rangefinder, color-blob tracking,
fiducial tracking, bumpers, grippers and mobile robot bases with
odometric or global localization.


# Design
Stage was designed with multi-agent systems in mind, so it provides
fairly simple, computationally cheap models of lots of devices rather
than attempting to emulate any device with great fidelity. This design
is intended to be useful compromise between conventional high-fidelity
robot simulations, the minimal simulations described by Jakobi [4], and
the grid-world simulations common in artificial life research [5]. We
intend Stage to be just realistic enough to enable users to move
controllers between Stage robots and real robots, while still being
fast enough to simulate large populations. We also intend Stage to be
comprehensible to undergraduate students, yet sophisticated enough for
professional reseachers.

Player also contains several useful 'virtual devices'; including
some sensor pre-processing or sensor-integration algorithms that help
you to rapidly build powerful robot controllers. These are easy to use
with Stage.


# Citations
If you use Stage in your work, we'd appreciate a citation. At the time of writing, the most suitable reference is either:
- Richard Vaughan. "Massively Multiple Robot Simulations in Stage", Swarm Intelligence 2(2-4):189-208, 2008. Springer, [download PDF](http://autonomylab.org/doc/vaughan_si08.pdf)

Or, if you are using Player/Stage:
- Brian Gerkey, Richard T. Vaughan and Andrew Howard. "The Player/Stage Project: Tools for Multi-Robot and Distributed Sensor Systems" Proceedings of the 11th International Conference on Advanced Robotics, pages 317-323, Coimbra, Portugal, June 2003 (ICAR'03), [download PDF](http://robotics.stanford.edu/~gerkey/research/final_papers/icar03-player.pdf)

Please help us keep track of what's being used out there by correctly
naming the Player/Stage components you use. Player used on its own is
called "Player". Player and Stage used together are referred to as
"the Player/Stage system" or just "Player/Stage". When Stage is used
without Player, it's just called "Stage". When the Stage library is
used to create your own custom simulator, it's called "libstage" or
"the Stage library". When Player is used with its 3D ODE-based
simulation backend, Gazebo, it's called Player/Gazebo. Gazebo without Player is just "Gazebo". All this software is part of the "Player Project".

# Support
Funding for Stage has been provided in part by:

- DARPA (USA)
- NASA (USA)
- NSERC (Canada)
- DRDC Suffield (Canada)
- NSF (USA)
- Simon Fraser University (Canada)

Names
-----
The names "Player" and "Stage" were inspired by the lines:

  > All the world's a stage,  
  > And all the men and women merely players

from "As You Like It" by William Shakespeare.


References
----------
[4] Nick Jakobi (1997) "Evolutionary Robotics and the Radical Envelope
of Noise Hypothesis", Adaptive Behavior Volume 6, Issue 2. pp.325 -
368.

[5] Stuart Wilson (1985) "Knowledge Growth in an Artificial Animal",
Proceedings of the First International Conference on Genetic Agorithms
and Their Applications.  Hillsdale, New Jersey. pp.16-23.
