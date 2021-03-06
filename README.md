# openMHA

H�rTech Open Master Hearing Aid (openMHA) 

1. Content of the openMHA release 4.5.1 (2017-07-17) 

The software contains the source code of the openMHA Toolbox library, of the 
openMHA framework and command line application, and of a selection of algorithm 
plugins forming a basic hearing aid processing chain featuring
- calibration
- bilateral adaptive differential microphones for noise suppression
- binaural coherence filter for feedback reduction and dereverberation
- multi-band dynamic range compressor for hearing loss compensation
- beamformer algorithm (delay-and-sum, and also MVDR)
- single-channel noise reduction
- simple upsampling and downsampling plugins
- STFT cyclic aliasing prevention
- simpler dynamic compressor

2. Citation in publications

In publications using openMHA, please cite

Herzke, T., Kayser, H., Loshaj, F., Grimm, G., Hohmann, V., Open signal
processing software platform for hearing aid research (openMHA).
Proceedings of the Linux Audio Conference. Universit� Jean Monnet,
Saint-�tienne, pp. 35-42, 2017.

As we are working on an updated paper, please check back this section
of the README for updates.

3. Source Code Overview 

Together with the MHA source code, we deliver the source code for the FFTW 
library, version 2.1.5, below the directory external_libs.
All openMHA source code lives under the directory mha: The MHA Toolbox
Library can be found in the sub-directory mha/libmha. It contains the
implementation of the MHA configuration language, of signal processing
primitives and also many signal processing algorithms to by used in MHA
plugins. The MHA command line application and its support framework 
can be found in the sub-directory mha/frameworks. The plugins contained in this 
release can be found in the sub-directory mha/plugins. The IO libraries, 
that connect the MHA e.g. to the sound card for live processing, or to sound 
files for offline processing, are also found here. 

4. Build Instructions 

The MHA source code has to be compiled before the MHA can be used. While MHA in 
general can be compiled for many operating systems and hardware platforms, in 
this release we concentrate on compilation on Ubuntu 16.04 for 64-bit PC
processors (x86_64) and on Debian 8 (jessie) for the Beaglebone Black
single-board ARM computer. 

Prerequisites: 
64-bit version of Ubuntu 16.04 or later,
or a Beaglebone Black with Debian jessie installed.

with the following software packages installed: 
- g++-5 for Ubuntu, g++-4.9 for Debian
- make 
- libsndfile1-dev, 
- libjack-jackd2-dev
- jackd2 
- optional: octave and default-jre

octave and default-jre are not essential for building or running the
openMHA.  The build process uses octave + java to run some tests after
building openMHA.  If octave is not available, this will fail.  But
the produced openMHA will still work.

The optional GUI (cf. openMHA_gui_manual.pdf) requires java-enabled
octave in version >= 4.2.1.

5. Compilation instructions: 

After downloading and unpacking the openMHA package, or cloning from github,
compile the MHA with ./configure && make

5.1 Installation instructions: 

No installation routine is provided together with the source code. The binaries 
will be generated in the source tree. To collect the relevant binaries in one 
place, you may e.g. create a bin directory and copy all the binaries there with 

mkdir bin; cp $(find . -name *.so) mha/frameworks/x86_64-linux-gcc-5/mha bin 

Then, you should set the environment variable LD_LIBRARY_PATH to point to your 
bin directory, like this: 

export LD_LIBRARY_PATH=$PWD/bin 

You can also add the bin directory to the PATH environment variable: 

export PATH=$PATH:$PWD/bin 

After this, you can invoke the MHA command line. Perform a quick test with 

mha ? cmd=quit 

Which should print the default configuration of the MHA without any plugins 
loaded. 


6. Usage instructions: 

We provide with this release several examples of configuration files
and sound examples. These are contained in the directory
./mha/configurations

For example, we can start an example featuring multiple algorithms
together with the following command:

mha ?read:mha/configurations/prerelease_combination.cfg cmd=start cmd=quit 

7. Documentation:

User manuals for different levels of usability in pdf format is provided 
with this release. These files can also be generated by typing 'make doc' in 
the terminal and the manuals will be created in the ./mha/doc/ directory. In 
addition, html documentation is generated in ./mha/doc/mhadoc/html/ and 
./mha/doc/mhaplugins/html/

Prerequisites:
Extra packages are needed for generating documentation:

- doxygen
- xfig
- graphviz
- texlive
- texlive-latex-extra
