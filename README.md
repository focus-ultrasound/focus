FOCUS
=====
Fast Object-Oriented C++ Ultrasound Simulator
-----

Building FOCUS
-----
FOCUS has been successfully built using GCC, Microsoft Visual Studio, and the Intel C++ Compiler on Windows and Linux.

### Requirements
#### All Platforms
FOCUS requires MATLAB R2008b or newer and the FFTW 3 library.

#### Windows Requirements
* Microsoft Visual C++ 2008 SP1 Redistributable Package (x86 or x64)

#### Linux Requirements
* g++ 4.3 or newer (4.2 or newer if not using OpenMP)

### Compiling
The MATLAB_Build function can be called from within MATLAB to compile the FOCUS code. See its documentation for details on the available compilation options.


Adding Calculation Methods to FOCUS
-----

### Structure
All of the calculation functions in FOCUS are methods of the abstract Transducer class. The various transducer shapes implement their own calculations in these methods. For example, fnm_cw is defined differently for each transducer shape, but the function itself is defined in the Transducer class.

The code that allows FOCUS to interact with MATLAB exists in the MEX directory. These files are responsible for checking the input arguments and returning the output of the calculations in a form MATLAB can understand.

#### Adding a New Method
There are a few steps required to add a calculation method to FOCUS.

1. Add a virtual function to the transducer class, e.g. fnm_cw(). This method should return an unsigned int and should take no arguments. Any parameters used in the calculation should already be stored in the Transducer object or in an object it points to.
2. Define the behavior of this function for each transducer shape. If the calcualtion can not be performed for certain shapes, these classes should have `return RETURN_NOT_IMPLEMENTED;` as the body of the calculation function.
3. Place the argument-checking and output processing code in /MEX.
4. Add this file to the MATLAB_Build script so that it is compiled along with the rest of FOCUS.

#### Encouraged Additional Steps
The following steps *should* be followed, but are not strictly required for any new code to work

1. Write some documentation accordint to the template in /Docs/Functions
2. Write a MATLAB script containing a typical use case for your code in the style of the existing examples
