Learning State Representations with Robotic Priors
==================================================

Author and Contact
------------------

Rico Jonschkowski (rico.jonschkowski@tu-berlin.de)


Introduction
------------

This folder contains a simple implementation of the method for state representation learning described our the paper "Learning State Representations with Robotic Priors" (Jonschkowski and Brock, 2015). This implementation complements the paper to provide sufficient detail for reproducing our results and for reusing the method in other research while minimizing code overhead (extensive explanations and descriptions are omitted here and can be found in the paper: http://tinyurl.com/gly9sma).

If you are using this implementation in your research, please consider giving credit by citing our paper:

    @article{jonschkowski2015learning,
      title={Learning state representations with robotic priors},
      author={Jonschkowski, Rico and Brock, Oliver},
      journal={Autonomous Robots},
      volume={39},
      number={3},
      pages={407--428},
      year={2015},
      publisher={Springer}
    }


Files
-----

main.py -- python3 script that includes our method, plotting functions, and batch learning experiments for two different tasks
Tensorflow.py -- python3 script with the same functionality as main.py using Tensorflow and Sonnet instead of Theano.
*.npz -- training and test data for two different tasks (described in detail below, see DATA)


Dependencies
------------

Our code builds on the following python3 libraries:

numpy

    sudo apt-get install python3-numpy

matplotlib 

    sudo apt-get install python3-matplotlib

lasagne (and theano) --> http://lasagne.readthedocs.io/en/latest/user/installation.html

or alternative

sonnet --> https://github.com/deepmind/sonnet
Tensorflow --> https://www.tensorflow.org/install/

Usage
-----

If all dependencies are met, simply run

    python3 main.py

which should first learn state representations for the simple navigation task, followed by the slot car task. After the representation is learned from one batch of data (*train.npz) it is then applied to a new batch of data (*test.npz) for each task. The command line output will walk you through the process.


Data
----

Each of the four .npz files include data from 5000 consecutive steps that were generated by random exploration. Each .npz file contains four numpy arrays: observations, actions, rewards, episode_starts. Observations are flattened 16x16 RGB images, actions are integers, rewards are floats, and episode_starts are flags that denote whether the current step is the beginning of a new episode. (Note that the action at time step t is taken at time t but only influences observations and rewards at time step t+1.)

The following excerpt from main.py shows how to load the data in python.

    import numpy as np
    training_data = np.load('simple_navigation_task_train.npz')
