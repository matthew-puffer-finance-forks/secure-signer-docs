Prerequisites
===============

Prepare a volume
------------------

By default, any data created within a Docker container is lost if the container is removed. Secure-Signer maintains our keys and slashing protection databases, so we want this data to persist should anything happen to the container. To do so, we will create a Docker volume called ``Secure-Signer-Backup``.

.. code-block:: shell

    docker volume create Secure-Signer-Backup

We can verify the volume exists and inspect it with the following:

.. code-block:: shell

    docker volume ls

.. code-block:: text

    DRIVER    VOLUME NAME
    local     Secure-Signer-Backup

.. code-block:: shell

    docker volume inspect Secure-Signer-Backup 

.. code-block:: text

    [                                                                                                                                       
        {                                                                                                                                   
            "CreatedAt": "2023-02-01T00:17:30Z",                                                                                            
            "Driver": "local",                                                                                                              
            "Labels": {},
            "Mountpoint": "/var/lib/docker/volumes/Secure-Signer-Backup/_data",
            "Name": "Secure-Signer-Backup",
            "Options": {},
            "Scope": "local"
        }
    ]

Setup the Docker container
----------------------------

The ``pufferfinance/secure_signer:latest`` container image can be found `here <https://hub.docker.com/r/pufferfinance/secure_signer>`_. The following command will start running a ``secure_signer`` container with the name ``secure_signer_validator``.
Notice we are mounting the volume ``Secure-Signer-Backup`` to the ``/Secure-Signer`` enclave
directory so any changes to Secure-Signer persist if the container is removed:

.. code-block:: shell

    docker run -itd --network host --mount type=volume,source=Secure-Signer-Backup,destination=/Secure-Signer -v /var/run/aesmd:/var/run/aesmd --device /dev/sgx/enclave --device /dev/sgx/provision --name secure_signer_validator pufferfinance/secure_signer:latest 

.. _mrenclave:

Getting Secure-Signer enclave measurements
--------------------------------------------

The Secure-Signer enclave’s ``MRENCLAVE`` value is necessary so that you know you
are interfacing only with the correct version of Secure-Signer running on SGX.
This is extremely important to verify before importing any of your keys!
Note that the ``MRENCLAVE`` value used in this guide may have changed
since the time of writing. To fetch this value run:

.. code-block:: shell

    docker exec secure_signer_container /bin/bash -c  "cat MRENCLAVE"

``dd4678fdcaac0c2b823c1b46438ba15a8995edc95819f35bb2c2486ab29abe01``

Thus the ``MRENCLAVE`` value for this version of Secure-Signer is
0xdd4678fdcaac0c2b823c1b46438ba15a8995edc95819f35bb2c2486ab29abe01.

Client CLI usage
------------------

The Client is a CLI app written in Rust to help interface with Secure-Signer
during the setup phase. For the rest of this guide, we will invoke the Client
from outside of the Docker container. Run the following to get its usage:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c "./client -h"

.. code-block:: text

    Secure-Signer Client Interface

    Usage: client [OPTIONS]

    Options:
    -p, --port <PORT>
            The port that Secure-Signer is exposing [default: 9001]
    -o, --outdir <OUTDIR>
            The path to the directory to save Secure-Signer outputs [default: ./ss_out]
    -b, --bls-keygen
            Requests Secure-Signer to generate BLS key perform remote attestation [requires --mrenclave]
    -l, --list
            Requests Secure-Signer to list all of its keys
    -i, --import
            Requests Secure-Signer to import a keystore [requires --mrenclave, --keystore-path, --password-path]
        --keystore-path <KEYSTORE_PATH>
            The path to the keystore.JSON
        --password-path <PASSWORD_PATH>
            The path to the password.txt
        --slash-protection-path <SLASH_PROTECTION_PATH>
            The path to EIP-3076 .JSON to import with the keystore
    -d, --deposit
            Request Secure-Signer to generate a DepositData [requires validator-pk-hex, --execution-addr]
        --debug
            Skips checking remote attestation, allowing the client to interface with a non-SGX-enabled Secure-Signer instance
    -v, --validator-pk-hex <VALIDATOR_PK_HEX>
            The validator public key in hex
    -e, --execution-addr <EXECUTION_ADDR>
            The ETH address for withdrawals
        --mrenclave <MRENCLAVE>
            The expected MRENCLAVE value
    -c, --config <CONFIG>
            The path to the JSON network config file [default: ./conf/network_config.json]
    -w, --withdraw
            Requests Secure-Signer to sign a VoluntaryExitMesssage [requires --validator-pk-hex, --epoch, --validator-index]
        --epoch <EPOCH>
            
        --validator-index <VALIDATOR_INDEX>
            
    -h, --help
            Print help
    -V, --version
            Print version