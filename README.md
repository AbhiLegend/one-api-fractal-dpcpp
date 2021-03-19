# `Mandelbrot` Sample

Mandelbrot is an infinitely complex fractal patterning that is derived from a simple formula.  It demonstrates using DPC++ for offloading computations to a GPU (or other devices) and shows how processing time can be optimized and improved with parallelism.

For comprehensive instructions regarding DPC++ Programming, go to https://software.intel.com/en-us/oneapi-programming-guide and search based on relevant terms noted in the comments.

| Optimized for                       | Description
|:---                               |:---
| OS                                | Linux* Ubuntu* 18.04; Windows 10
| Hardware                          | Skylake with GEN9 or newer
| Software                          | Intel&reg; oneAPI DPC++/C++ Compiler
| What you will learn               | How to offload the computation to GPU using the Intel&reg; oneAPI DPC++/C++ Compiler
| Time to complete                  | 15 minutes

## Purpose
Mandelbrot is a DPC++ application that generates a fractal image by initializing a matrix of 512 x 512, where the computation at each point (pixel) is entirely independent of the computation at other points. The sample includes both parallel and serial calculation of the set, allowing for a direct comparison of results. The parallel implementation can demonstrate the use of Unified Shared Memory (USM) or buffers. You can modify parameters such as the number of rows, columns, and iterations to evaluate the difference in performance and load between USM and buffers. This is further described at the end of this document in the "Running the Sample" section.
## Update
Major fractal functions covered

The code will attempt first to execute on an available GPU and fallback to the system's CPU if a compatible GPU is not detected.  The device used for compilation is displayed in the output along with elapsed time to render the mandelbrot image. This is helpful for comparing different offload implementations based on complexity of the computation. 

## Key Implementation Details 
The basic DPC++ implementation explained in the code includes device selector, buffer, accessor, kernel, and command groups.
 
## License  
This code sample is licensed under MIT license. 

## Building the `Mandelbrot` Program for CPU and GPU

> Note: if you have not already done so, set up your CLI 
> environment by sourcing  the setvars script located in 
> the root of your oneAPI installation. 
>
> Linux Sudo: . /opt/intel/oneapi/setvars.sh  
> Linux User: . ~/intel/oneapi/setvars.sh  
> Windows: C:\Program Files(x86)\Intel\oneAPI\setvars.bat

### Include Files
The include folder is located at %ONEAPI_ROOT%\dev-utilities\latest\include on your development system.

### Running Samples In DevCloud
If running a sample in the Intel DevCloud, remember that you must specify the compute node (CPU, GPU, FPGA) as well whether to run in batch or interactive mode. For more information see the Intel® oneAPI Base Toolkit Get Started Guide (https://devcloud.intel.com/oneapi/get-started/base-toolkit/)

### On a Linux* System
Perform the following steps:
1. Build the program using the following `cmake` commands. 
``` 
$ mkdir build
$ cd build
$ cmake ..
$ make
```

> Note: by default, exectables are created for both USM and buffers. You can build individually with the following: 
>    Create buffers executable: make mandelbrot
>    Create USM executable: make mandelbrot_usm

2. Run the program (default uses buffers):
    ```
    make run
    ```
> Note: for USM use `make run_usm`

3. Clean the program using:
    ```
    make clean
    ```

### On a Windows* System Using Visual Studio* Version 2017 or Newer
* Build the program using VS2017 or VS2019
      Right click on the solution file and open using either VS2017 or VS2019 IDE.
      Right click on the project in Solution explorer and select Rebuild.
      From top menu select Debug -> Start without Debugging.


* Build the program using MSBuild
      Open "x64 Native Tools Command Prompt for VS2017" or "x64 Native Tools Command Prompt for VS2019"
      Run - MSBuild mandelbrot.sln /t:Rebuild /p:Configuration="Release"


## Running the Sample

### Example of Output
```
Platform Name: Intel(R) OpenCL HD Graphics
  Platform Version: OpenCL 2.1 
       Device Name: Intel(R) Gen9 HD Graphics NEO
    Max Work Group: 256
 Max Compute Units: 24

Parallel Mandelbrot set using buffers.
Rendered image output to file: mandelbrot.png (output too large to display in text)
       Serial time: 0.0430331s
     Parallel time: 0.00224131s
Successfully computed Mandelbrot set.
```

### How was the learning experience
## Good
Easy to get started,good amount of examples,Ready template availables
## Bad
Very hard to attain basics,too much time required  to adapt to DPC++


## Update new code
We use One API Devcloud to find different solutions to fractals
How to use it?
In the input.txt file change your paramater no.s
Its currently numbered from 1 to 10
The Ipython notebook is self explanatory run it and you will see a new fractal being created using the parameters
Just Change a number say 1 to 2... save it and run the ipython notebook

Major Fractals covered.

We have covered lots of variants of Fractal functions that are there utilizing lots of trignometric functions with different values to get the desired results in the DPC++ format.
## Ran the code with Iris Max option on Devcloud
nodes=1:iris_xe_max:ppn=2
## The following output was achieved.
813427.v-qsvr-1 ...ub-singleuser u58899 00:00:55 R jupyterhub 813470.v-qsvr-1 run-fractal.sh u58899 0 Q batch
Waiting for Output █████████████████████ Done⬇
########################################################################
Date: Thu 18 Mar 2021 03:21:37 PM PDT
Job ID: 813470.v-qsvr-1.aidevcloud
User: u58899
Resources: neednodes=1:iris_xe_max:ppn=2,nodes=1:iris_xe_max:ppn=2,walltime=06:00:00
########################################################################
u58899 is compiling Fractal DPCPP
Platform Version: 1.0 Device Name: Intel(R) Graphics [0x4905] Max Work Group: 512 Max Compute Units: 96
########################################################################
End of output for job 813470.v-qsvr-1.aidevcloud
Date: Thu 18 Mar 2021 03:21:55 PM PDT
########################################################################

## The functions that are used to form different Fractals
exp() function
complex_square(z) + z

exponential z (power cubed) + complex(squarez)
z(cubed) + complex(square z) + z

plus more....

## quad Intel® Iris® Xe MAX Graphics compute node
nodes=1:iris_xe_max:dual_gpu:ppn=2

813427.v-qsvr-1 ...ub-singleuser u58899 00:01:09 R jupyterhub 813488.v-qsvr-1 run-fractal.sh u58899 0 Q batch
Waiting for Output █████████████████████ Done⬇
########################################################################
Date: Thu 18 Mar 2021 03:47:01 PM PDT
Job ID: 813488.v-qsvr-1.aidevcloud
User: u58899
Resources: neednodes=1:iris_xe_max:dual_gpu:ppn=2,nodes=1:iris_xe_max:dual_gpu:ppn=2,walltime=06:00:00
########################################################################
u58899 is compiling Fractal DPCPP
Platform Version: 1.0 Device Name: Intel(R) Graphics [0x4905] Max Work Group: 512 Max Compute Units: 96
########################################################################
End of output for job 813488.v-qsvr-1.aidevcloud
Date: Thu 18 Mar 2021 03:47:19 PM PDT
########################################################################

