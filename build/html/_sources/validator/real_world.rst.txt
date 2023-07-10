Real world usage
==================

.. _valkey:

Generating validator keys
-----------------------------

Generating a new validator key in Secure-Signer is easy. Run the following:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c "./client --bls-keygen --mrenclave 0xdd4678fdcaac0c2b823c1b46438ba15a8995edc95819f35bb2c2486ab29abe01"

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c  "cat ss_out/keygen_response"

.. code-block:: json

    {
    "pk_hex": "0xa1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745",
    "evidence": {
        "raw_report": "{\"id\":\"162751886891308410237998812549463066896\",\"timestamp\":\"2023-04-17T19:42:46.045624\",\"version\":4,\"epidPseudonym\":\"EbrM6X6YCH3brjPXT23gVh/I2EG5sVfHYh+S54fb0rrAqVRTiRTOSfLsWSVTZc8wrazGG7oooGoMU7Gj5TEhsvAcefuLUIgX9D/eSfKyPJrznAaJ6ASxrfof9j48uVWfvoqKn6oT+UnqCyE4eVpzR96KC/Sik9BzMXCii8uJ5u0=\",\"advisoryURL\":\"https://security-center.intel.com\",\"advisoryIDs\":[\"INTEL-SA-00334\",\"INTEL-SA-00615\"],\"isvEnclaveQuoteStatus\":\"SW_HARDENING_NEEDED\",\"isvEnclaveQuoteBody\":\"AgABAIAMAAANAA0AAAAAAEJhbJjVPJcSY5RHybDnAD8AAAAAAAAAAAAAAAAAAAAAFBQLB/+ADgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABQAAAAAAAAAfAAAAAAAAAN1GeP3KrAwrgjwbRkOLoVqJle3JWBnzW7LCSGqymr4BAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACD1xnnferKFHD2uvYqTXdDA8iZ22kCD5xw7h38CMfOngAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAChqb1xyRBvVGgThHECNMObku+PNIJ0CbU72YpmX1jcNvmsTVVIy+s23Azcckha10UAAAAAAAAAAAAAAAAAAAAA\"}",
        "signed_report": "ZTWyi+jGxyCOGuV2Cvg0DLwW5/xAyqxAFlpLe0YFOodg7A1sq81iANzYGbcPlXnUJ1lteX9uPc2zFDXd0aYIPSNR2r0opq7f0OkOEvMdfYBEdA0zaGFa1Kayg0HsSNkgPpiOd4jlLCxpwNw5veKDwiy6H8VmRWWVUdAC2J21bY4456F/l/3DThsuoP/b1UdhI1HH/CmOGG6HlYZVGhA2cfSD1ZHIPvpNx0rw3/+1VMuPeisvBxMuZLf9rpsrRLPuiDxPK90qUGeBD/s/iyt7HI7/ir1wQeGsVlyC/CtNm4of6uvWvW5B4vVzypfXtMk1v3Uffk1u2/8ypWiyVJ5UFw==",
        "signing_cert": "-----BEGIN CERTIFICATE-----\nMIIEoTCCAwmgAwIBAgIJANEHdl0yo7CWMA0GCSqGSIb3DQEBCwUAMH4xCzAJBgNV\nBAYTAlVTMQswCQYDVQQIDAJDQTEUMBIGA1UEBwwLU2FudGEgQ2xhcmExGjAYBgNV\nBAoMEUludGVsIENvcnBvcmF0aW9uMTAwLgYDVQQDDCdJbnRlbCBTR1ggQXR0ZXN0\nYXRpb24gUmVwb3J0IFNpZ25pbmcgQ0EwHhcNMTYxMTIyMDkzNjU4WhcNMjYxMTIw\nMDkzNjU4WjB7MQswCQYDVQQGEwJVUzELMAkGA1UECAwCQ0ExFDASBgNVBAcMC1Nh\nbnRhIENsYXJhMRowGAYDVQQKDBFJbnRlbCBDb3Jwb3JhdGlvbjEtMCsGA1UEAwwk\nSW50ZWwgU0dYIEF0dGVzdGF0aW9uIFJlcG9ydCBTaWduaW5nMIIBIjANBgkqhkiG\n9w0BAQEFAAOCAQ8AMIIBCgKCAQEAqXot4OZuphR8nudFrAFiaGxxkgma/Es/BA+t\nbeCTUR106AL1ENcWA4FX3K+E9BBL0/7X5rj5nIgX/R/1ubhkKWw9gfqPG3KeAtId\ncv/uTO1yXv50vqaPvE1CRChvzdS/ZEBqQ5oVvLTPZ3VEicQjlytKgN9cLnxbwtuv\nLUK7eyRPfJW/ksddOzP8VBBniolYnRCD2jrMRZ8nBM2ZWYwnXnwYeOAHV+W9tOhA\nImwRwKF/95yAsVwd21ryHMJBcGH70qLagZ7Ttyt++qO/6+KAXJuKwZqjRlEtSEz8\ngZQeFfVYgcwSfo96oSMAzVr7V0L6HSDLRnpb6xxmbPdqNol4tQIDAQABo4GkMIGh\nMB8GA1UdIwQYMBaAFHhDe3amfrzQr35CN+s1fDuHAVE8MA4GA1UdDwEB/wQEAwIG\nwDAMBgNVHRMBAf8EAjAAMGAGA1UdHwRZMFcwVaBToFGGT2h0dHA6Ly90cnVzdGVk\nc2VydmljZXMuaW50ZWwuY29tL2NvbnRlbnQvQ1JML1NHWC9BdHRlc3RhdGlvblJl\ncG9ydFNpZ25pbmdDQS5jcmwwDQYJKoZIhvcNAQELBQADggGBAGcIthtcK9IVRz4r\nRq+ZKE+7k50/OxUsmW8aavOzKb0iCx07YQ9rzi5nU73tME2yGRLzhSViFs/LpFa9\nlpQL6JL1aQwmDR74TxYGBAIi5f4I5TJoCCEqRHz91kpG6Uvyn2tLmnIdJbPE4vYv\nWLrtXXfFBSSPD4Afn7+3/XUggAlc7oCTizOfbbtOFlYA4g5KcYgS1J2ZAeMQqbUd\nZseZCcaZZZn65tdqee8UXZlDvx0+NdO0LR+5pFy+juM0wWbu59MvzcmTXbjsi7HY\n6zd53Yq5K244fwFHRQ8eOB0IWB+4PfM7FeAApZvlfqlKOlLcZL2uyVmzRkyR5yW7\n2uo9mehX44CiPJ2fse9Y6eQtcfEhMPkmHXI01sN+KwPbpA39+xOsStjhP9N1Y1a2\ntQAVo+yVgLgV2Hws73Fc0o3wC78qPEA+v2aRs/Be3ZFDgDyghc/1fgU+7C+P6kbq\nd4poyb6IW8KCJbxfMJvkordNOgOUUxndPHEi/tb/U7uLjLOgPA==\n-----END CERTIFICATE-----\n-----BEGIN CERTIFICATE-----\nMIIFSzCCA7OgAwIBAgIJANEHdl0yo7CUMA0GCSqGSIb3DQEBCwUAMH4xCzAJBgNV\nBAYTAlVTMQswCQYDVQQIDAJDQTEUMBIGA1UEBwwLU2FudGEgQ2xhcmExGjAYBgNV\nBAoMEUludGVsIENvcnBvcmF0aW9uMTAwLgYDVQQDDCdJbnRlbCBTR1ggQXR0ZXN0\nYXRpb24gUmVwb3J0IFNpZ25pbmcgQ0EwIBcNMTYxMTE0MTUzNzMxWhgPMjA0OTEy\nMzEyMzU5NTlaMH4xCzAJBgNVBAYTAlVTMQswCQYDVQQIDAJDQTEUMBIGA1UEBwwL\nU2FudGEgQ2xhcmExGjAYBgNVBAoMEUludGVsIENvcnBvcmF0aW9uMTAwLgYDVQQD\nDCdJbnRlbCBTR1ggQXR0ZXN0YXRpb24gUmVwb3J0IFNpZ25pbmcgQ0EwggGiMA0G\nCSqGSIb3DQEBAQUAA4IBjwAwggGKAoIBgQCfPGR+tXc8u1EtJzLA10Feu1Wg+p7e\nLmSRmeaCHbkQ1TF3Nwl3RmpqXkeGzNLd69QUnWovYyVSndEMyYc3sHecGgfinEeh\nrgBJSEdsSJ9FpaFdesjsxqzGRa20PYdnnfWcCTvFoulpbFR4VBuXnnVLVzkUvlXT\nL/TAnd8nIZk0zZkFJ7P5LtePvykkar7LcSQO85wtcQe0R1Raf/sQ6wYKaKmFgCGe\nNpEJUmg4ktal4qgIAxk+QHUxQE42sxViN5mqglB0QJdUot/o9a/V/mMeH8KvOAiQ\nbyinkNndn+Bgk5sSV5DFgF0DffVqmVMblt5p3jPtImzBIH0QQrXJq39AT8cRwP5H\nafuVeLHcDsRp6hol4P+ZFIhu8mmbI1u0hH3W/0C2BuYXB5PC+5izFFh/nP0lc2Lf\n6rELO9LZdnOhpL1ExFOq9H/B8tPQ84T3Sgb4nAifDabNt/zu6MmCGo5U8lwEFtGM\nRoOaX4AS+909x00lYnmtwsDVWv9vBiJCXRsCAwEAAaOByTCBxjBgBgNVHR8EWTBX\nMFWgU6BRhk9odHRwOi8vdHJ1c3RlZHNlcnZpY2VzLmludGVsLmNvbS9jb250ZW50\nL0NSTC9TR1gvQXR0ZXN0YXRpb25SZXBvcnRTaWduaW5nQ0EuY3JsMB0GA1UdDgQW\nBBR4Q3t2pn680K9+QjfrNXw7hwFRPDAfBgNVHSMEGDAWgBR4Q3t2pn680K9+Qjfr\nNXw7hwFRPDAOBgNVHQ8BAf8EBAMCAQYwEgYDVR0TAQH/BAgwBgEB/wIBADANBgkq\nhkiG9w0BAQsFAAOCAYEAeF8tYMXICvQqeXYQITkV2oLJsp6J4JAqJabHWxYJHGir\nIEqucRiJSSx+HjIJEUVaj8E0QjEud6Y5lNmXlcjqRXaCPOqK0eGRz6hi+ripMtPZ\nsFNaBwLQVV905SDjAzDzNIDnrcnXyB4gcDFCvwDFKKgLRjOB/WAqgscDUoGq5ZVi\nzLUzTqiQPmULAQaB9c6Oti6snEFJiCQ67JLyW/E83/frzCmO5Ru6WjU4tmsmy8Ra\nUd4APK0wZTGtfPXU7w+IBdG5Ez0kE1qzxGQaL4gINJ1zMyleDnbuS8UicjJijvqA\n152Sq049ESDz+1rRGc2NVEqh1KaGXmtXvqxXcTB+Ljy5Bw2ke0v8iGngFBPqCTVB\n3op5KBG3RjbF6RRSzwzuWfL7QErNC8WEy5yDVARzTA5+xmBc388v9Dm21HGfcC8O\nDD+gT9sSpssq0ascmvH49MOgjt1yoysLtdCtJW/9FZpoOypaHx0R+mJTLwPXVMrv\nDaVzWh5aiEx+idkSGMnX\n-----END CERTIFICATE-----\n"
    }
    }

Breaking down what happened
----------------------------

- We supplied the ``--mrenclave`` flag with the value obtained :ref:`here<mrenclave>`.
- The Client requested Secure-Signer to generate a new BLS keypair then perform remote attestation. The attestation evidence was written to ``ss_out/keygen_response``.
- The Client verified the remote attestation evidence, gaining trust that this SGX instance is indeed running Secure-Signer. The verification process required that the reports ``MRENCLAVE`` value matched the expected, the evidence was signed by Intel, and the 48-Byte compressed BLS public key was committed to in the report.

Secure-Signer now safeguards the private key corresponding to the public key ``0xa1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745`` with a slash protection database initialized to ``slot=0``, ``source_epoch=0``, and ``target_epoch=0``. The remote attestation evidence serves as proof that the BLS public key was generated by a Secure-Signer enclave.

Listing Keys
--------------

We can verify that Secure-Signer has custody of the imported and generated
BLS keys by running the following:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c "./client -h"
    docker exec -w /home secure_signer_container /bin/bash -c  "cat ss_out/list_bls_keys"

.. code-block:: json

    {
    "data": [
        {
        "pubkey": "0x9612d7a727c9d0a22e185a1c768478dfe919cada9266988cb32359c11f2b7b27f4ae4040902382ae2910c15e2b420d07"
        },
        {
        "pubkey": "0xa1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745"
        }
    ]
    }

Network Config:
Before we generate our DepositData to register our validator keys, there are some parameters that change depending on the target Testnet. By default the Client uses the ``conf/network_config.json`` file which is configured to work with the `Goerli launchpad <https://goerli.launchpad.ethereum.org/en/upload-deposit-data>`_. To work with a different Testnet, either modify this file or supply a new file using the flag ``--config <path_to_your_network_config>``.

Registering your validator
---------------------------

To register your validator, you must use your validator key to sign off on a DepositData. The following command will make the Client request Secure-Signer to generate a ``deposit_data.json`` file to the default directory ``ss_out`` using the public key ``0xa1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745``.

The Client generates withdrawal credentials using the ``ETH1_ADDRESS_WITHDRAWAL_PREFIX`` (0x01) described in the `Capella specs <https://github.com/ethereum/consensus-specs/blob/dev/specs/capella/beacon-chain>`_.md#new-process_bls_to_execution_change , which requires a 20-Byte hex-encoded ETH address. In this example, we’re setting partial withdrawals to send ETH to ``0x4D68568B8D4E6244233c685B48fEa619621B78D2``.

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c "./client --deposit --validator-pk-hex 0xa1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745 --execution-addr 0x4D68568B8D4E6244233c685B48fEa619621B78D2"

You can extract this ``deposit_data.json`` file by running the following:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c  "cat ss_out/deposit_data.json" > ~/deposit_data.json
    cat ~/deposit_data.json 

.. code-block:: json

    [
    {
        "amount": 32000000000,
        "deposit_cli_version": "2.3.0",
        "deposit_data_root": "853e1ba19b31d630aa3686d75f4750c436a4782d9b73a651c31f91247bb31592",
        "deposit_message_root": "3c0974bd6b5e82ad0db9f0e35a0f420122aebfc0aa72a1e339a0d7e7947254b0",
        "fork_version": "00001020",
        "network_name": "goerli",
        "pubkey": "a1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745",
        "signature": "a79ed4118518270271f72f01b89d933b1fb8992b74103ce93e24901d467dcca876a8c3b7a7d5c6f60787195d66c5874b0ca79b1bca1d5d18f5b311cccbfdcce70c6262e5c9c5df4dddf24cfcfe118b53561d7313ec2374bd71430a26bdc8d926",
        "withdrawal_credentials": "0100000000000000000000004d68568b8d4e6244233c685b48fea619621b78d2"
    }
    ]

If Secure-Signer is running on a remote server, you can fetch the
file on your local machine by running the following with your username and IP:

.. code-block:: shell

    scp user@12.345.678.910:~/deposit_data.json .

Navigate to the `Goerli launchpad <https://goerli.launchpad.ethereum.org/en/upload-deposit-data>`_  and upload your ``deposit_data.json`` file:

Congrats! Continue to follow the launchpad’s instructions and your validator will make it onto the Testnet.

Exiting a validator
---------------------

Post-Shapella, we can exit validators by submitting signed ``VoluntaryExit`` messages. Assuming the public key ``0xa1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745`` corresponds to ``ValidatorIndex=999``, we can exit this validator on ``epoch=123456`` run the following:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c "./client --withdraw --validator-pk-hex 0xa1a9bd71c9106f54681384710234c39b92ef8f34827409b53bd98a665f58dc36f9ac4d5548cbeb36dc0cdc72485ad745 --epoch 123456 --validator-index 999"

You can extract this ``voluntary_exit_message.json`` file by running the following:

.. code-block:: shell

    docker exec -w /home secure_signer_container /bin/bash -c  "cat ss_out/voluntary_exit_message.json" > ~/voluntary_exit_message.json
    cat ~/voluntary_exit_message.json

.. code-block:: json

    {
    "message": {
        "epoch": "123456",
        "validator_index": "999"
    },
    "signature": "0x9842b502ff901fcd003e53306773f8b88f184a11541cb015f4e2ffeb4b42623c67d621e766e7edc736e8dbe9e81b799201bfe8dfdd58b459c8f8291054d0cdde6ab0cba5191f9b20108c0481d06ebde4d1f28a40aae8119d5478d443fed8df0e"
    }