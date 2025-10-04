SerialEMLibs is a repository for libraries used by SerialEM and SerialEMCCD.
It should be located in a folder adjacent to the folders for those projects.

See the Copyright.txt in SerialEM and ReadMe.txt in SerialEMCCD for
descriptions of various license terms.

See the file libimod/README-VIS.STUDIO.txt in the IMOD source package for
descriptions of how the IMOD libraries here are built in Visual Studio and
required environment variable settings.  See the file ReadMe.txt in the
SerialEM source for instructions on modifying the configurations there to use
some of the alternative libraries here.

The libctffind files here are a bit different from other variations:
libctffind.lib is from a regular build of IMOD with Intel compilers.
Specifically, they are built with the 2019 Intel C++ compiler used with the
VS2015 toolset.  A SerialEM built with this will depend on the libctffind.dll
built in IMOD and Intel libraries libiomp5md.dll and libmmd.dll, all
distributed with SerialEM.  The libctffind-VCOMP.dll and libctffind-VCOMP.lib
are built with Visual Studio against vcomp.lib instead of libiomp5md.lib;
SerialEM built with libctffind-VCOMP.lib will depend only on the
libctffind-VCOMP.dll included here.

Below is a table of what libraries are used in what builds.  v90 and v140 refer
to the toolsets installed by VS2008 and VS2015, respectively.  Higher versions
of Visual Studio offer a selection of toolsets if earlier versions are
installed.

The current building procedure when a library needs updating in either
SerialEM or SerialEMCCD is as follows.  If libcfshr or libiimod needs updating
in SerialEMCCD, open libimod/libimod.sln in VS2008, build Release x64 for
whichever needs updating, and copy the resulting lib's to here.  Then open
libimod/libimod14.sln in VS2015, and build Intel-OMP Win32 and x64 for
libcfshr, libiimod, and/or libimod, and copy the libcfshr-I*.lib,
libiimod-I*.lib, and/or libimod-I*.lib to here.  (These builds require
environment variables IOMP_LIB32_DIR and IOMP_LIB64_DIR with the paths to
32-bit and 64-bit libiomp5md.lib, respectively.)  Then build Release Win32
and Win64 for libcfshr, libiimod and/or libimod, and DLL-Release x64 and
IOMP-noHDF for the noHDF versions of libiimod if that needs updating for
SerialEMCCD. Copy libcfshr-[^I]*.lib, libiimod-[^I]*.lib, and/or
libimod-[^I]*.lib to here.

Currently, to retain the ability to run on Windows XP, the 32-bit 
libiomp5md.lib and dll from the Intel 2015 compilers is used.  This seems to
work, but to avoid problems, libraries from Intel 2019 are used for the 64-bit
builds.

libifft-MKL is built in VS2015 against static MKL libraries in the Intel 2019
compilers, using the Intel-OMP Win32 and x64 configurations.  These
configurations rely on the environment variable ICPP_COMPILER19, which is
defined by the Intel install.  This is used in the C/C++ - General section and
the Linker - Input section.  The 32-bit configuration relies on IOMP_LIB32_DIR
so that the older libiomp5md.lib can be used.

                        SerialEM with MKL  Intel-free SerialEM  SerialEMCCD
                          32-bit 64-bit       32-bit 64-bit      v90  v140
hdf5-14.lib                  X                   X 
hdf5-14-64.lib                     X                   X

libcfshr-64.lib                                                   X
libcfshr-14.lib                                  X
libcfshr-14-64.lib                                     X                X
libcfshr-IOMP.lib            X
libcfshr-IOMP-64.lib               X                                    X

libctffind.lib               X
libctffind-VCOMP.dll                             X
libctffind-VCOMP-14.lib                          X
x64/libctffind.lib                 X
x64/libctffind-VCOMP.dll                               X
x64/libctffind-VCOMP-14.lib                            X

libifft-64.lib                                                    X  
libifft-14.lib                                   X
libifft-14-64.lib                                      X                X 
libifft-MKL.lib              X
libifft-MKL-64.lib                 X

libiimod-64.lib                                                   X
libiimod-14.lib                                  X
libiimod-14-64.lib                                     X         
libiimod-noHDF-14-64.lib                                                X
libiimod-IOMP-noHDF-64.lib                                              X
libiimod-IOMP.lib            X
libiimod-IOMP-64.lib               X

libimod.lib                                      X
libimod-64.lib                                         X
libimod-IOMP.lib             X
libimod-IOMP-64.lib                X

libimxml-64.lib                                                   X
libimxml-14.lib              X                   X
libimxml-14-64.lib                 X                   X                X

libiwarp.lib                 X                   X
libiwarp-64.lib                    X                   X

libiomp5md.lib               X
x64/libiomp5md.lib                 X

libjpeg-64.lib                                                    X
libjpeg-14.lib               X                   X
libjpeg-14-64.lib                  X                   X                X

libtiff-64.lib                                                    X
libtiff-14.lib               X                   X
libtiff-14-64.lib                  X                   X                X

zlib.lib                     X                   X                X
zlib-64.lib                        X                   X                X  
