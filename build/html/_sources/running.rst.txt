Running secure-signer
======================

Start the Docker container
----------------------------

The ``pufferfinance/secure_signer:latest`` container image can be found `here <https://hub.docker.com/r/pufferfinance/secure_signer>`_. The following command will start running a ``secure_signer`` container with the name ``secure_signer_container``. 

.. code-block:: shell

    docker run -itd --network host -v /var/run/aesmd:/var/run/aesmd --device /dev/sgx/enclave --device /dev/sgx/provision --name secure_signer_container pufferfinance/secure_signer:latest 


Verify that the container is running
--------------------------------------

.. code-block:: shell

    docker container ls    
                                                                                            
.. code-block:: text

    CONTAINER ID   IMAGE                                COMMAND   CREATED         STATUS         PORTS     NAMES
    3ce85f5a1d33   pufferfinance/secure_signer:latest   "bash"    4 seconds ago   Up 3 seconds             secure_signer_container


Attach to the container
-------------------------

Attach to the container using its name ``secure_signer_container``. Notice the username is now `root`, indicating we are now inside the container.

.. code-block:: shell

    exec -it secure_signer_container bash
    whoami

``root``


Run Secure-signer
------------------

The Secure-Signer enclave is built using the `Occlum LibOS <https://github.com/occlum/occlum>`_. To start Secure-Signer we will use the ``occlum run`` command and point to the ``secure-signer`` binary stored within the Occlum enclave image and specify port ``9003``.

.. code-block:: shell

    occlum run /bin/secure-signer 9003

``Starting SGX Secure-Signer: localhost:9003``

The Secure-Signer HTTP server is now running! 

Run using Docker exec
---------------------------

Alternatively, you can start Secure-Signer without attaching to the container by running the following:

.. code-block:: shell

    docker exec secure_signer_container /bin/bash -c "occlum run /bin/secure-signer 9003"

``Starting SGX Secure-Signer: localhost:9003``