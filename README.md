# __capp__ (C++ Aspect-Oriented Parallel Programming)
========
__capp__ uses aspects in c++ to simplify parallel programming with OpenCL. AspectC++ is used to perform most of the overhead of setting up the parallel programming context allowing users to focus on writing the kernels and performing the processing.

# Setup
---------
To use __capp__, clone the repository. See the __Prerequisits__ section below for installing AspecC++ and OpenCL.

The directory structure for any program using __capp__ should the same as that outline in the __Directory structure__ section. Examples can be seen in the Examples/exampleName/ folders. 

## Prerequisits
Currently there is only support for linux and OSX, but Windows support will be implemented soon.

### Linux
To install AspectC++ on Ubuntu simply type ```sudo apt-get install aspectc++```. Alternatively constult [AspecC++](http://www.aspectc.org/Download.php).

To install OpenCL you need to download the SDK relevant to the device you have. For any CPU and AMD GPU, the AMD SDK will work, for NVIDIA GPU's the NVIDIA OpenCL SDK and cuda development tools are required.

#### AMD 
First get the AMD SDK from [AMD](http://developer.amd.com/tools-and-sdks/opencl-zone/amd-accelerated-parallel-processing-app-sdk/). 

Extract the file and run ```sudo sh Install-AMD-APP.sh```. 

Then install the opencl headers. On Ubuntu this is done by ```sudo apt-get install opencl-headers```. Alternatively they can be downloaded from [OpenCL-Headers](https://www.khronos.org/registry/cl/). Whichever way you get the headers __make sure__ that they are version 1.1 or lower if you are going to be using an NVIDIA GPU at some point. Check the cl.hpp file (usually at /usr/local/CL/cl.hpp - linux, /usr/local/include/OpenCL/cl.hpp) and make sure that it is version 1.1.

#### NVIDIA
Download and install the latest CUDA development kit from [CUDA](https://developer.nvidia.com/cuda-downloads) and follow their instructions. Again make sure that cl.hpp is version 1.1 (__this is very important for NVIDIA__).

## Directory structure
The following is the directory structure which must be used:

```
-ProjectRoot
--aspects
---*.ah, *.cc (All aspects)
--kernels
--- *.cl (All kernels)
--src
---*.h, *.cpp (All cpp source)
--builds
--- All executables reside inside builds
--tests
--- tests.cpp (The test source file)
--temp
--- (Usually empty, but used by the aspect weaver and the compiler to build executables)
--Makefile
```
**Note** Please do not change the name, move or delete the ```temp``` directory
or else this wont compile. A fix for this will be implemented in the near
future.

## Makefile
The Makefile must be in the project root directory as specified above. The directory names can be changed appropriately in the Makefile by editing the *_DIR variables in the Makefile.

## Compiling
To compile any program make sure that the files are in correct directories as specified above. Also make sure that you have AspectC++ and OpenCL installed, see __Prerequisits__ section. Once in the __ProjectRoot__ directory type "__make__" and the executable will reside in the __ProjectRoot/builds/__ directory.
