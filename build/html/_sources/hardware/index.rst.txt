Hardware setup
===============

**If you only plan to use secure-signer in simulated mode you can skip this page.**
But if you mean to test out secure-signer on real hardware you will need a CPU
that supports some version of SGX.

You can check for what features your CPU supports with:

.. code-block:: shell

    cpuid | grep SGX1; cpuid | grep SGX2

.. code-block:: text
    
    SGX1 supported                         = true
    ...
    SGX2 supported                         = false
    ...

And verify your CPU supports Flexible Launch Control (FLC):

.. code-block:: shell

    cpuid | grep SGX_LC

.. code-block:: text

    SGX_LC: SGX launch config supported      = true
    SGX_LC: SGX launch config supported      = true

For those interested in using a remote server to run secure-signer Azure
offers a type of compute instance called 'confidential compute' that supports SGX.
We use this environment internally for our enclave development. To get yourself
started we've written a page on that here: 

.. toctree::
    azure
