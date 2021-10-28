Example for using dcmtk with pkg-config patch
=============================================
This repository provides an example based on dcmdata-test from dcmtk showing
how the suggest pkg-config patch is usable when wanting to use dcmtk in a 
system having pkg-config

If you want to test this - setup an ubuntu with build tools and *libssl-dev*
*libtiff-dev*

Getting Started
---------------
**1.  Build dcmtk with shared libs and pkg-config.**

Use the branch https://github.com/frosteyes/dcmtk/tree/pkg-config
Build and install dcmtk as presented below from inside your dcmtk folder
after creation of build folder

    $ cd build
    $ cmake -DBUILD_SHARED_LIBS:BOOL=ON -DUSE_COMPILER_HIDDEN_VISIBILITY:BOOL=ON -DDCMTK_WITH_TIFF:BOOL=ON -DDCMTK_WITH_OPENSSL:BOOL=ON  ..  
    $ make -j24
    $ sudo make install

**2.  Verify your dcmtk.pc file.**

    $ $ cat /usr/local/lib/pkgconfig/dcmtk.pc 
    prefix="/usr/local"
    exec_prefix="${prefix}"
    libdir="${prefix}/lib"
    includedir="${prefix}/include/"

     Name: DCMTK
    Description: DICOM ToolKit (DCMTK)
    URL: http://dcmtk.org
    Version: 3.6.6
    Requires: 
    Requires.private:  libssl zlib
    Cflags: -I"${includedir}"
    Libs: -L"${libdir}"  -lofstd -loflog -ldcmdata -li2d -ldcmimgle -ldcmimage -ldcmjpeg -lijg8 -lijg12 -lijg16 -ldcmjpls -ldcmtkcharls -ldcmtls -ldcmnet -ldcmsr -lcmr -ldcmdsig -ldcmwlm -ldcmqrdb -ldcmpstat -ldcmrt -ldcmiod -ldcmfg -ldcmseg -ldcmtract -ldcmpmap -ldcmect
    Libs.private: -L"${libdir}"

**3.  Clone this repo and test build.**

    $ git clone https://github.com/frosteyes/dcmtk-pkg-config-test.git
    $ cd dcmtk-pkg-config-test
    $ mkdir build && cd build
    $ cmake ..
    $ make -j24

**4.  Run the resulting app.**

    $ ./dcmdata-test/local_dcmdata_tests 
    Test results for module 'dcmdata': 95 succeeded, 0 failed.
