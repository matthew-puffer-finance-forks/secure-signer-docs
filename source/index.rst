.. Secure Signer documentation master file, created by
   sphinx-quickstart on Mon Jul 10 10:43:13 2023.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Protect yourself from slashable offenses
=========================================

Secure-signer is a Rust binary that runs inside special CPU-cages called 'enclaves.' Secure-signer is designed to interface with Ethereum consensus clients to help prevent slashable offenses.

Overview
----------

Secure-signer can either run in simulated mode or directly on real hardware. When its running on real hardware it will use the 'SGX' feature of Intel CPUs for its enclave support. Running this software requires some complex dependencies. We've therefore made a `docker <https://www.docker.com/>`_ file which is the recommended way to run secure-signer.

The Docker file automatically maps ports and still allows for secure-signer to use real hardware features of the CPU without prohibitive overhead. The work flow for developers using the Docker file involves opening their Docker VM in the VS Code plugin `Dev Containers <https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers>`_. From there they can edit code in the VM directly and run their changes using our shell scripts.

The rest of the docs are dedicated towards exploring that process.

Contents
---------

.. toctree::
   hardware/index
   install
   running
   developing/index
   validator/index





