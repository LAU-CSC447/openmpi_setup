# Lab 0: OpenMPI Setup
### Due: January 27, 11:59 PM

The purpose of this lab is to prepare your environment for C development using OpenMPI and to get yourself familiar with Git and GitHub.

## Installation
The recommended operating system is Linux. However, Windows and macOS are also supported. This section will guide you through the installation of the tools and libraries required to complete the lab work. Specifically, you will need to install:

- A C compiler (e.g., GNU gcc)
- The OpenMPI library
- The `git` command line tool

Follow the instructions appropriate to your operating system.

### Linux
The example below is for Debian-based distributions (e.g., Ubuntu).
```
sudo apt-get update
sudo apt-get install -y git build-essential
sudo apt-get install -y libopenmpi-dev
```

### macOS
OpenMPI can be installed using [brew](https://brew.sh). First, start by installing the XCode development tools which include Git and the C compiler:

```
xcode-select --install 
```

Next, install brew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Finally, install OpenMPI
```
brew update
brew install open-mpi
```

### Windows
OpenMPI can be installed using [Cygwin](https://cygwin.com):
- Download and install Git: https://git-scm.com
- Download and run the Cygwin installer: https://cygwin.com/setup-x86_64.exe
- During the installation process, search for and choose the following packages:
  - `gcc-core`
  - `libopenmpi-devel`
  - `zlib-devel`
  - `openssh`
  - `libevent-devel`
  - `libhwloc-devel`
- You may need to add the Cygwin bin directory to the PATH enviromental variable. Here's a video that demonstrates this process: https://www.youtube.com/watch?v=x8x02BjKvpU
  
## Testing
Clone this repository. Make sure to modify the URL accordingly (i.e., replace `<username>` with your Github username).

```
git clone https://github.com/LAU-CSC447/lab0-<username> lab0
cd lab0
```

Compile `hello_mpi.c` using `mpicc`

```
mpicc -o hello hello_mpi.c
```

Use the `mpirun` command to run the compiled binary `hello` using 4 processes
```
mpirun -np 4 hello
```

The output should look like
```
Hello world from processor Karims-MacBook-Air.local, rank 0 out of 4 processors
Hello world from processor Karims-MacBook-Air.local, rank 1 out of 4 processors
Hello world from processor Karims-MacBook-Air.local, rank 2 out of 4 processors
Hello world from processor Karims-MacBook-Air.local, rank 3 out of 4 processors
```

## Troubleshooting
If you get a 'not enough slots' error when running `mpirun` then you probably have less than 4 cores available on your system. You can either reduce the number of processes (i.e., the `-np` argument) or simply add the `--oversubscribe` flag. e.g.,
```
mpirun --oversubscribe -np 4 hello
```

`--oversubscribe` forces mpirun to create the number of processes specified using `-np` regardless of the number of processing units available. The processes will end up sharing whatever cores you have available on your system. Obviously, this will hurt performance (you shouldn't see a meaningful speedup), but it's fine for our purposes.

## Tasks
Complete the tasks below

### Task 1
Modify `hello_mpi.c` to print 'Hello CSC447 from...' instead of 'Hello world from...'
Compile and test your program. Example output:
```
Hello CSC447 from processor Karims-MacBook-Air.local, rank 0 out of 4 processors
Hello CSC447 from processor Karims-MacBook-Air.local, rank 1 out of 4 processors
Hello CSC447 from processor Karims-MacBook-Air.local, rank 2 out of 4 processors
Hello CSC447 from processor Karims-MacBook-Air.local, rank 3 out of 4 processors
```
### Task 2
Commit and push your changes to your Github repository.
```
git add hello_mpi.c
git commit -m 'completed task 1'
git push -u origin master
```
Go to your repository on Github and make sure all changes were commited succesfully. 
