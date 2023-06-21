Wyrm Requirements and Specifications
####################################

Summary
*******

Wyrm:
  * is :ref:`statically typed <static-typing>`
  * has automatic garbage collection
  * supports both Ahead-of-Time (AoT) and Just-In-Time (JIT) compilation

    * can generate standalone and redistributable binaries

  * has multi-threaded and asynchronous execution models
  * has robust support for object-oriented programming, including:

    * compile-time enforcement of encapsulation (public and private members)
    * multiple inheritance
    * reflection
    * namespaces

  * supports Digital Signal Processing (DSP) with:

    * a generic programming system to allow expressive type programming with
      functional units
    * LLVM-backed optimization of DSP code supporting vectorization,
      inlining, loop unrolling, and others
    * generation of both CPU and GPU instructions from the same source code

  * prioritizes interoperability by:

    * allowing any C ABI compiled code to call and be called by Wyrm code
    * loading static and dynamic shared objects at runtime
    * providing limited parsing of C and C++ header files

  * supports robust diagnostics, including profiling and debugging
  * runs on any platform supported by LLVM, including:

    * Linux and other Unixes
    * macOS
    * Windows
    * Bare-metal embedded platforms

Detailed Discussion
*******************

.. _static-typing:

Static Typing
=============


