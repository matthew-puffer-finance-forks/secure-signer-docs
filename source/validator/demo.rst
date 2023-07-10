Demo usage
============

Importing a validator key
---------------------------

Secure-Signer allows users to import validator keystore JSON files conforming
to version 4 of the `EIP-2355 <https://eips.ethlibrary.io/eip-2335.html>`_ specs. While importing the keystore, you may
optionally include a slash protection database JSON file conforming to `EIP-3076 <https://eips.ethereum.org/EIPS/eip-3076>`_
so Secure-Signer knows your previously signed material
(see the `API docs <https://pufferfinance.github.io/secure-signer-api-docs/redoc-static.html#tag/Keymanager/operation/KEYMANAGER_IMPORT>`_ for more information).

With the recent Shapella fork allowing withdrawals, we highly recommend
withdrawing existing validators and generating fresh BLS keys within Secure-Signer,
described :ref:`in this section<valkey>`. This will maximally protect against slashable
offenses as there will only be one copy of the BLS private key.

For the purpose of this demo we have generated three files:
dummy-v4-keystore.json, dummy-password.txt dummy-slash-protection-db.json.

First we can verify this is a V4 keystore:

.. code-block:: shell

    cat dummy-v4-keystore.json

.. code-block:: json

    {
        "crypto": {
            "kdf": {
                "function": "scrypt",
                "params": {
                    "dklen": 32,
                    "n": 262144,
                    "p": 1,
                    "r": 8,
                    "salt": "d4e56740f876aef8c010b86a40d5f56745a118d0906a34e69aec8c0db1cb8fa3"
                },
                "message": ""
            },
            "checksum": {
                "function": "sha256",
                "params": {},
                "message": "d2217fe5f3e9a1e34581ef8a78f7c9928e436d36dacc5e846690a5581e8ea484"
            },
            "cipher": {
                "function": "aes-128-ctr",
                "params": {
                    "iv": "264daa3f303d7259501c93d997d84fe6"
                },
                "message": "06ae90d55fe0a6e9c5c3bc5b170827b2e5cce3929ed3f116c2811e6366dfe20f"
            }
        },
        "description": "This is a test keystore that uses scrypt to secure the secret.",
        "pubkey": "9612d7a727c9d0a22e185a1c768478dfe919cada9266988cb32359c11f2b7b27f4ae4040902382ae2910c15e2b420d07",
        "path": "m/12381/60/3141592653/589793238",
        "uuid": "1d85ae20-35c5-4611-98e8-aa14a633906f",
        "version": 4
    }

This key has previously signed a block with slot number 1559 and an
attestation with source and target epochs of 1234 and 1238.

.. code-block:: shell

    cat dummy-slash-protection-db.json

.. code-block:: json

    {
        "metadata": {
        "interchange_format_version": "5",
        "genesis_validators_root": "0x04700007fabc8282644aed6d1c7c9e21d38a03a0c4ba193f3afe428824b3a673"
        },
        "data": [
        {
            "pubkey": "0x9612d7a727c9d0a22e185a1c768478dfe919cada9266988cb32359c11f2b7b27f4ae4040902382ae2910c15e2b420d07",
            "signed_blocks": [
            {
                "slot": "1559",
                "signing_root": "0x4ff6f743a43f3b4f95350831aeaf0a122a1a392922c45d804280284a69eb850b"
            }
            ],
            "signed_attestations": [
            {
                "source_epoch": "1234",
                "target_epoch": "1238",
                "signing_root": "0x587d6a4f59a58fe24f406e0502413e77fe1babddee641fda30034ed37ecc884d"
            }
            ]
        }
        ]
    }

Copy files into Docker
------------------------

.. code-block:: shell

    docker cp dummy-v4-keystore.json secure_signer_container:/home
    docker cp dummy-slash-protection-db.json secure_signer_container:/home
    docker cp dummy-password.txt secure_signer_container:/home

Verify the files were copied:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c  "ls"

.. code-block:: text

    client
    conf
    dummy-password.txt
    dummy-slash-protection-db.json
    dummy-v4-keystore.json

Import keystore and slash db
------------------------------

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c "./client --import --keystore-path dummy-v4-keystore.json --password-path dummy-password.txt --slash-protection-path dummy-slash-protection-db.json --mrenclave dd4678fdcaac0c2b823c1b46438ba15a8995edc95819f35bb2c2486ab29abe01"

.. code-block:: text

    - Connected to Secure-Signer on port 9001

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c  "cat ss_out/import_response"

.. code-block:: json

    {
    "data": [
        {
        "status": "imported",
        "message": "0x9612d7a727c9d0a22e185a1c768478dfe919cada9266988cb32359c11f2b7b27f4ae4040902382ae2910c15e2b420d07"
        }
    ]
    }

Breaking down what happened
---------------------------------

- We specified the paths to our keystore, slash protection, and password files (paths are relative to ``/home/client`` inside the container).
- We supplied the ``--mrenclave`` flag with the value obtained :ref:`here<mrenclave>`.
- The Client requested Secure-Signer to generate a fresh ephemeral ETH (SECP256K1) keypair and commit to it while performing remote attestation.
- The Client verified the remote attestation evidence, gaining trust that this SGX instance is indeed running Secure-Signer. The verification process required that the report's ``MRENCLAVE`` value matched the expected, the evidence was signed by Intel, and the ETH public key was committed to in the report.
- The Client encrypted the contents of ``dummy-password.txt`` with the ETH public key using `ECIES <https://en.wikipedia.org/wiki/Integrated_Encryption_Scheme>`_.
- The Client then imported the keystore, encrypted password, and slash protection into Secure-Signer via the `/eth/v1/keystores <https://pufferfinance.github.io/secure-signer-api-docs/redoc-static.html#tag/Keymanager/operation/KEYMANAGER_IMPORT>`_ API.
- Secure-Signer decrypted the keystore password and saved the validator key to the enclave's encrypted memory.

Attempt to sign a slashable block
------------------------------------

At this point, Secure-Signer is loaded with our validator key and slash protection database. We can verify that Secure-Signer prevents slashing by sending a block proposal with a non-increasing slot of ``1337``. Note, the following should not be attempted on real keys and is solely for demonstration purposes. In practice, all signing material (minus deposits and withdrawals) passed to Secure-Signer should originate from your consensus client.

.. code-block:: shell

    curl -X POST localhost:9001/api/v1/eth2/sign/0x9612d7a727c9d0a22e185a1c768478dfe919cada9266988cb32359c11f2b7b27f4ae4040902382ae2910c15e2b420d07 -H "Content-Type: application/json" -d '{
    "type": "BLOCK_V2",
    "fork_info":{
        "fork":{
            "previous_version":"0x80000070",
            "current_version":"0x80000071",
            "epoch":"750"
        },
        "genesis_validators_root":"0x2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a2a"
    },
    "signingRoot": "0x2ebfc2d70944cc2fbff6d67c6d9cbb043d7fbe0a660d248b6e666ce110af418a",
    "beacon_block": {
        "version": "CAPELLA",
        "block_header": {
            "slot": "1337",
            "proposer_index": "0",
            "parent_root":"0x0000000000000000000000000000000000000000000000000000000000000000",
            "state_root":"0x0000000000000000000000000000000000000000000000000000000000000000",
            "body_root":"0xcd7c49966ebe72b1214e6d4733adf6bf06935c5fbc3b3ad08e84e3085428b82f"
        }
    }
    }'

Secure-Signer prevents signing with the response: 

``{"error":"Signing operation failed due to slashing protection rules"}``

Cleanup
---------

We can now delete the files we copied into the container:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c  "rm dummy-password.txt dummy-v4-keystore.json dummy-slash-protection-db.json"

Note that if Secure-Signer is running remotely (e.g., on the cloud),
we could have alternatively run the Client locally.
This way we are not required to copy keystores or
passwords onto a potentially untrusted server.

This concludes the guide on how to import keys into Secure-Signer.
The next section will document the simpler and more
secure method of generating validator keys inside Secure-Signer.