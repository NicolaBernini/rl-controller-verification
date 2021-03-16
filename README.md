Learning a Control for Quadcopter with Reinforcement Learning
=============================================================

Code associated to the paper 

**A Few Lessons Learned in Reinforcement Learning for Quadcopter Attitude Control** 

- [Nicola Bernini](https://nicolabernini.github.io/), [Mikhail Bessa](https://www.linkedin.com/in/mikha%C3%AFl-bessa-847102139/), [Rémi Delmas](https://www.linkedin.com/in/r%C3%A9mi-delmas-6909352a/), [Arthur Gold](https://www.linkedin.com/in/arthur-gold/), [Eric Goubault](https://www.linkedin.com/in/eric-goubault-31a188103/), [Romain Pennec](https://www.linkedin.com/in/romain-pennec-a2346366/), [Sylvie Putot](https://www.linkedin.com/in/sylvie-putot-04b48917/) and [François Sillion](https://www.linkedin.com/in/sillion/)

- Published at [HSCC 2021](https://hscc.acm.org/2021/accepted-papers/)



Development environment
-----------------------

A docker image is provided for the code development: `brzl/quadcopter:devel`.
The definition of the image can be found inside the folder `docker`. As you
can see, it is based on the brezel research platform, with additional python
dependencies. The first thing you need to do is build the image, which can
takes a while (but you usually need to build it once for all):

    make build


The commands described in the rest of this README are supposed to be run
from the devel container. Enter `make run` to get a shell.

If you need X11 suport, use `make run-x11` instead.
Do `xrdb -merge Xresources` once in the container.


Getting started
---------------

#### 1. Build applications

    bazel build :all

Note that you will need to run `bazel sync --configure` in case you
modify the content of folder `gym-quadcopter`.

#### 2. Run the training

    bazel run :training

It will read params from `config_training.yaml` file.
Results will be available in `results/experiment_DATETIME`.

#### 3. Inspect results with Tensorboard

You need to enter the Tensorboard Container (from your host) with

    make tensorboard

and then run Tensorboard making it point to the experiment directory

    tensorboard --logdir /results/experiment_DATETIME/runs --bind_all

#### 4. Export Weights for Sherlock

    bazel run :export

It will read params from `config_export.yaml` file.

The input is the `model/quadcopter-{i}.pkl` selected
and the export is defined in the config file.

Notes
-----

- `config_training.yaml` has all hyperparameters
- in `models`: the pkl checkpoints
- in `figures`: all plots (rewards etc.)
- in `log`: log file
- in `tests`: all tests that are run with proper tags
- `config_tests` contains the corresponding parameters and figures and log inside each of them
