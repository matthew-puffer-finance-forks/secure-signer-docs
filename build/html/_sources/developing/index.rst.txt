Developing secure-signer
=========================

When you enter into a shell for the secure-signer docker file you're going to
want to clone your own branch there. You can fork the `secure-signer branch <https://github.com/PufferFinance/secure-signer>`_ and
setup git to work from your shell. To edit your code directly in the VM checkout
the VS Code plugin `Dev Containers <https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers>`_.

Building secure-signer
-----------------------

The build_secure_signer.sh is a convenience script for building Secure-Signer.
If you set the LOCAL_DEV environment variable, the script will build locally
without the Occlum runtime, which is convenient for developing without an SGX-enabled CPU:

.. code-block:: shell

    export LOCAL_DEV=true

The following command will compile the codebase and create an Occlum image.

.. code-block:: shell

    ./build_secure_signer.sh -b

Use -h for help:

.. code-block:: shell

    ./build_secure_signer.sh -h

.. code-block:: text

    Build and containerize Secure-Signer.
    Run "LOCAL_DEV=true ./build_secure_signer.sh <args>" for local dev compilation without SGX dependencies.
    usage: build_secure_signer.sh [OPTION]...
        -p <Secure-Signer Server port> default 9001.
        -c clean Cargo then build all
        -b build from cached dependencies
        -x Run Secure-Signer on port set by -p (default 9001)
        -d Build and package the Docker Container Image (assumes "occlum package" has been run)
        -m Measure Secure-Signer's MRENCLAVE and MRSIGNER (assumes this is run in SGX env)
        -t Run all unit tests
        -h <usage> usage help

Running secure-signer
----------------------

After you've built secure-signer you may wish to run it. Either inside an
enclave or as a regular program:

.. code-block:: shell

    ./build_secure_signer.sh -x

Running tests
---------------

Before all the tests for secure-signer can pass additional test vectors need to
be downloaded (Ethereum consensus test vectors:)

.. code-block:: shell

    cd tests
    make

To run the tests:

.. code-block:: shell

    export SECURE_SIGNER_PORT=9001
    ./build_secure_signer.sh -t

Docker releases
------------------

.. toctree::
    docker

