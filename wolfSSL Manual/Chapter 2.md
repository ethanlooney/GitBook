# Chapter 2: Building wolfSSL
wolfSSL was written with portability in mind and should generally be easy to build on most systems. If you have difficulty building wolfSSL, please don’t hesitate to seek support through our support forums (http://www.wolfssl.com/forums) or contact us directly at support@wolfssl.com.

This chapter explains how to build wolfSSL on Unix and Windows, and provides guidance for building wolfSSL in a non-standard environment.  You will find the “getting started” guide in  **Chapter 3** and an SSL tutorial in **Chapter 11**.

When using the autoconf / automake system to build wolfSSL, wolfSSL uses a single Makefile to build all parts and examples of the library, which is both simpler and faster than using Makefiles recursively.

#### 2.1 Getting wolfSSL Source Code

The most recent version of wolfSSL can be downloaded from the wolfSSL website as a ZIP file:
http://wolfssl.com/wolfSSL/download/downloadForm.php

After downloading the ZIP file, unzip the file using the `unzip` “unzip” command.  To use native line endings, enable the “-a” modifier when using unzip.  From the unzip man page, the “-a” modifier functionality is described:

[...]  The -a option causes files identified by zip as text files (those with the ‘t’  label in  zipinfo  listings,  rather  than  ‘b’)  to  be automatically extracted  as  such,  converting   line   endings,   end-of-file characters  and  the  character  set  itself as necessary.  [...]

**NOTE**:  Beginning with the release of wolfSSL 2.0.0rc3, the directory structure of wolfSSL was changed as well as the standard install location.  These changes were made to make it easier for open source projects to integrate wolfSSL.  For more information on header and structure changes, please see **Sections 9.1** and **9.3**.

#### Building on *nix

When building wolfSSL on Linux, *BSD, OS X, Solaris, or other *nix-like systems, use the autoconf system. To build wolfSSL you only need to run two commands from the wolfSSL root directory:

``./configure``
``make``

You can append any number of build options to ./configure.  For a list of available build options, please see **Section 2.5** or run:

``./configure --help``

from the command line to see a list of possible options to pass to the ./configure script.  To build wolfSSL, run:

``make``

To install wolfSSL run:

``make install``

You may need superuser privileges to install, in which case precede the command with sudo:

``sudo make install``

To test the build, run the testsuite program from the root wolfSSL directory:

``./testsuite/testsuite.test``

or use autoconf to run the testsuite as well as the standard wolfSSL API and crypto tests:

``make test``

Further details about expected output of the testsuite program can be found in Section 3.2.  If you want to build only the wolfSSL library and not the additional items (examples, testsuite, benchmark app, etc.), you can run the following command from the wolfSSL root directory:

``make src/libwolfssl.la``

#### 2.3 Building on Windows

n addition to the instructions below, you can find instructions and tips for building wolfSSL with Visual Studio [here](https://www.google.com/url?q=https://wolfssl.com/wolfSSL/Docs-wolfssl-visual-studio.html&sa=D&ust=1568828990762000]).

**VS 2008**:  Solutions are included for Visual Studio 2008 in the root directory of the install.  For use with Visual Studio 2010 and later, the existing project files should be able to be converted during the import process.

**Note**:

If importing to a newer version of VS you will be asked:  “Do you want to overwrite the project and its imported property sheets?”  You can avoid the following by selecting “No”.  Otherwise if you select “Yes”, you will see warnings about EDITANDCONTINUE being ignored due to SAFESEH specification. You will need to right click on the testsuite, sslSniffer, server, echoserver, echoclient, and client individually and modify their Properties->Configuration Properties->Linker->Advanced (scroll all the way to the bottom in Advanced window).  Locate “Image Has Safe Exception Handlers” and click the drop down arrow on the far right. Change this to No (/SAFESEH:NO) for each of the aforementioned. The other option is to disable EDITANDCONTINUE which, we have found to be useful for debugging purposes and is therefore not recommended.

****VS 2010****: You will need to download Service Pack 1 to build wolfSSL solution once it has been updated. If VS reports a linker error, clean and rebuild the project; the linker error should be taken care of.

****VS 2013 (64 bit solution)****: You will need to download Service Pack 4 to build wolfSSL solution once it has been updated. If VS reports a linker error, clean the project then Rebuild the project and the linker error should be taken care of.

To test each build, choose “Build All” from the Visual Studio menu and then run the testsuite program.  To edit build options in the Visual Studio project, select your desired project (wolfssl, echoclient, echoserver, etc.) and browse to the “Properties” panel.

**Note**: 
After the wolfSSL v3.8.0 release the build preprocessor macros were moved to a centralized file located at ‘IDE/WIN/user_settings.h’. This file can also be found in the project. To add features such as ECC or ChaCha20/Poly1305 add #defines here such as HAVE_ECC or HAVE_CHACHA / HAVE_POLY1305.

**Cygwin**: If using Cygwin, or other toolsets for Windows that provides *nix-like commands and functionality, please follow the instructions in section 2.2, above, for “Building on *nix”.  If building wolfSSL for Windows on a Windows development machine, we recommend using the included Visual Studio project files to build wolfSSL.

#### 2.5 Build Options (./configure Options)

The following are options which may be appended to the ```./configure``` script to customize how the wolfSSL library is built.

By default, wolfSSL only builds in shared mode, with static mode being disabled. This speeds up build times by a factor of two. Either mode can be explicitly disabled or enabled if desired.

| Option        | Default Value           | Description  |
| ------------- |:-------------:| -----:|
| **--enable-debug**      | Disabled | Enable wolfSSL debugging support |
| **--enable-distro**      | Disabled      | Enable wolfSSL distro build |
| **--enable-singlethreaded** | Disabled neat |    Enable single threaded mode, no multi thread protections |
