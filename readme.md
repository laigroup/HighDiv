# HighDiv: SMT(LIA) Sampling with High Diversity

## 1. Project Structure
In HighDiv, three sampling modes have been implemented, namely *LS-MODE*, *CDCL-MODE*, and *HYBRID-MODE*.

### 1.1. Framework of HighDiv
![alt text](pics/framework.png)

Here's an overview of the key components in the project structure:
```
.
├── HighDiv
│   ├── LIA_bench
│   ├── build
│   ├── make-z3.sh
│   ├── makefile
│   ├── my_scripts
│   ├── samples
│   ├── src
│   └── z3pp
├── pics
├── readme.md
└── z3
    ├── CMakeLists.txt
    ├── LICENSE.txt
    ├── README-CMake.md
    ├── README.md
    ├── RELEASE_NOTES.md
    ├── azure-pipelines.yml
    ├── build
    ├── cmake
    ├── configure
    ├── contrib
    ├── doc
    ├── docker
    ├── examples
    ├── genaisrc
    ├── noarch
    ├── resources
    ├── scripts
    ├── src
    │   ├── ackermannization
    │   ├── api
    │   ├── ast
    │   ├── cmd_context
    │   ├── math
    │   ├── model
    │   ├── muz
    │   ├── nlsat
    │   ├── opt
    │   ├── params
    │   ├── parsers
    │   ├── qe
    │   ├── sampler
    │   ├── sat
    │   ├── shell
    │   ├── smt
    │   ├── solver
    │   ├── tactic
    │   ├── test
    │   └── util
    ├── z3.pc.cmake.in
    └── z3guide.jpeg

```
The implementation of sampling based on local search is primarily located in the `./z3/src/sampler` folder.  

In the `./HighDiv/src` folder, we use z3's C++ API to encapsulate the sampling algorithm.  

Note that since this framework relies on certain tactics in z3 (e.g., `solve-eqs`), it requires the use of z3's model generation and model transformation mechanisms.

## 2. Installation

```bash
git clone git@github.com:laigroup/HighDiv.git
git submodule init && git submodule update
```

### 2.1. Compile z3

To ensure compatibility and performance, we recommend compiling Z3 within a controlled Python virtual environment:

First, activate the Python virtual environment.

```bash
# Activate the Python virtual environment
cd HighDiv
python3 -m venv venv
source venv/bin/activate

# Compile Z3 with Python bindings
cd z3
python3 scripts/mk_make.py --python
cd build
make -j 15
make install
```

### 2.2. Compile HighDiv

```bash
cd HighDiv
make
```

## 3. Usage

Run a test case to see how HighDiv works:
```bash
./HighDiv -i LIA_bench/LIA_convert_query-1164.smt2 -o samples -n 10 -t 900 -s 123 -m hybrid
```

## 4. Command Line Options
```
Usage: ./highdiv [options]
Options:
  -i <smt file>               Specify the path to the input file
  -o <output dir>             Specify the output directory path
  -n <num samples>            Specify the number of samples
  -t <time limit>             Set the time limit (in seconds)
  -s <seed>                   Set the random seed
  -m <sampling mode>          Set the sampling mode <ls, cdcl, hybrid>
  -e <cdcl epoch>             Set CDCL epochs for sampling (Only effective in hybrid mode)
  -p <fixed var percentage>   Set the percentage of fixed variables (Only effective in hybrid mode)
  -h                          Display this help message
```

## 5. Contributors
The following researchers have contributed to this project (sorted alphabetically by last name):
* Yong Lai (laiy@jlu.edu.cn)
* Junjie Li (jjli23@mails.jlu.edu.cn)
* Chuan Luo (chuanluo@buaa.edu.cn)

## 6. Getting Help
For support or questions, please contact the project maintainers at jjli23@mails.jlu.edu.cn or open an issue in our GitHub repository's issue tracker.