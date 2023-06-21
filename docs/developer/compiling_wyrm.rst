Compiling Wyrm
##############

Prerequisites
*************

Like LLVM, we use CMake to generate our local build system and Sphinx to
generate documentation.

Downloading LLVM
================

Wyrm depends on LLVM libraries. As LLVM does not offer a stable API, we require
a specific version of LLVM, currently |wyrm_llvm_version_req|.

The release binaries for LLVM are available for download from the
`releases page <https://releases.llvm.org/>`_ on llvm.org. Download the
appropriate binaries for your operating system and extract them to a directory
outside the Wyrm repository.

Compiling LLVM From Source
==========================

It's also possible to build LLVM from sources, install the libraries somewhere,
and provide that path to Wyrm during configuration.

.. warning:
  LLVM builds are compute and storage intensive. Even on powerful computers,
  builds can take significant time.

See the `LLVM CMake Build Instructions <https://llvm.org/docs/CMake.html>`_ for
details about building LLVM with CMake. ``-DCMAKE_INSTALL_PREFIX=<path>``.


Building The Documentation
**************************

Prerequisites
=============

``pip install sphinx-better-theme``

``cmake -DWYRM_DOCS=On ..``

Then the docs build with CMake automatically, appearing in ``build/doc/html``.