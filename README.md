stateline
=========
Stateline is a framework for distributed Markov Chain Monte Carlo (MCMC) sampling written in C++11. It focuses on [parallel tempering](http://en.wikipedia.org/wiki/Parallel_tempering) methods which are highly parallelisable.

System Support
--------------
Currently, Stateline runs on Linux-based operating systems only, though there
is also a Dockerfile. 

Compiler Support
----------------
Stateline has been compiled and tested under g++ 4.8.2.

Building
--------
To build Stateline, you will need:
* GCC 4.8.2/Clang 6.0 or newer
* CMake 3.0 or newer ([link](https://cmake.org/install/))

The simplest way to build Stateline running is to clone the repository and fetch the dependencies:

```bash
$ git clone https://github.com/NICTA/stateline.git
$ cd stateline && ./tools/fetch-deps
```

This will automatically download and build the necessary dependencies into `build/prereqs`. Then, to build Stateline in debug, run:

```bash
$ ./tools/configure debug
$ cd build/debug && make
```

You usually only need to configure once, so just run `make` next time you want to re-compile. Only when you make significant changes to the build procedures will you need to run `./tools/configure`. More information about building can be found [here](https://github.com/NICTA/stateline/wiki/Installation-Guide).

Communications
--------------
By default, Stateline workers communicate with the sever on port 5555. Keep
this port open or exposed on the Docker containers.

Running C++ Demo
----------------
To see Stateline in action, open two terminals and run the following commands in a build directory (either `build/debug` or `build/release`):

Run the Stateline server in Terminal 1:

```bash
$ ./stateline --config=demo-config.json
```

Run a Stateline worker in Terminal 2:

```bash
$ ./demo-worker
```

Running Python Demo
-------------------
There is also a demo in Python, which shows how workers written in other languages can interact with the Stateline server. This demo requires the [zmq] module (install via `pip  install zmq`). Again, open two terminals and run the following commands in a build directory (either `build/debug` or `build/release`):

Run the Stateline server in Terminal 1:

```bash
$ ./stateline --config=demo-config.json
```

Run a Stateline worker in Terminal 2:

```bash
$ python ./demo-worker.py
```

Output
-------------------

After running one of the above examples,  you should see a folder called `demo-output` in your build directory. This folder contains samples from the demo MCMC. Running

```bash
$ python vis.py demo-output/0.csv
```

will launch a Python script that visualises the samples of the first chain. You'll need NumPy and the excellent [corner-plot](https://github.com/dfm/corner.py) module (formerly triangle-plot).


Documentation
-------------
Documentation can be found in the
[wiki](http://github.com/NICTA/stateline/wiki), and there is automatic doxygen documentation generated by running

```bash
$ make doc
```

in a build directory. Please ensure Doxygen is installed. Finally, there are demos for python and C++ in the src/bin folder.

Licence
-------
Please see the LICENSE file, and COPYING and COPYING.LESSER.

Bug Reports
-----------
If you find a bug, please open an [issue](http://github.com/NICTA/stateline/issues).

Contributing 
------------
Contributions and comments are welcome. Please read our [style guide](docs/CodeGuidelines.md) before submitting a pull request.
