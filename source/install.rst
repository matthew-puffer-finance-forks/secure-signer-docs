Installation
==============

Verify your Linux Kernel version is at least 5.10:

.. code-block:: shell

    uname -r

``5.15.0-1031-azure``

Installing Docker
------------------

Run this command to install Docker:

.. code-block:: shell

    sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
    apt-cache policy docker-ce
    sudo apt install -y docker-ce

Verify Docker was correctly installed:

.. code-block:: shell

    sudo systemctl status docker

Let Docker run without requiring sudo:

.. code-block:: shell

    sudo groupadd docker
    sudo usermod -aG docker $USER

Installing SGX drivers
------------------------

Secure-Signer requires Intel SGX drivers. The following will add Intel's packages
to APT. These packages are used when performing remote attestation.

.. code-block:: shell

    echo 'deb [arch=amd64] https://download.01.org/intel-sgx/sgx_repo/ubuntu focal main' | sudo tee /etc/apt/sources.list.d/intel-sgx.list
    wget -qO - https://download.01.org/intel-sgx/sgx_repo/ubuntu/intel-sgx-deb.key | sudo apt-key add
    sudo apt update 
    sudo apt install -y libsgx-epid libsgx-quote-ex libsgx-dcap-ql libsgx-urts libsgx-uae-service libsgx-dcap-default-qpl 

Verify the Intel Architectural Enclave Service Manager is running:

.. code-block:: shell

    service aesmd status

.. code-block:: text

    aesmd.service - Intel(R) Architectural Enclave Service Manager
        Loaded: loaded (/lib/systemd/system/aesmd.service; enabled; vendor preset: enabled)
        Active: active (running) since Mon 2023-01-16 21:08:30 UTC; 2 weeks 0 days ago
        Process: 19616 ExecStartPre=/opt/intel/sgx-aesm-service/aesm/linksgx.sh (code=exited, status=0/SUCCESS)
        Process: 19625 ExecStartPre=/bin/mkdir -p /var/run/aesmd/ (code=exited, status=0/SUCCESS)
        Process: 19626 ExecStartPre=/bin/chown -R aesmd:aesmd /var/run/aesmd/ (code=exited, status=0/SUCCESS)
        Process: 19627 ExecStartPre=/bin/chmod 0755 /var/run/aesmd/ (code=exited, status=0/SUCCESS)
        Process: 19628 ExecStartPre=/bin/chown -R aesmd:aesmd /var/opt/aesmd/ (code=exited, status=0/SUCCESS)
        Process: 19629 ExecStartPre=/bin/chmod 0750 /var/opt/aesmd/ (code=exited, status=0/SUCCESS)
        Process: 19630 ExecStart=/opt/intel/sgx-aesm-service/aesm/aesm_service (code=exited, status=0/SUCCESS)
    Main PID: 19631 (aesm_service)
        Tasks: 4 (limit: 9530)
        Memory: 14.6M
        CGroup: /system.slice/aesmd.service
                └─19631 /opt/intel/sgx-aesm-service/aesm/aesm_service

    Jan 16 21:08:30 Puffer-Dev systemd[1]: Starting Intel(R) Architectural Enclave Service Manager...
    Jan 16 21:08:30 Puffer-Dev aesm_service[19630]: aesm_service: warning: Turn to daemon. Use "--no-daemon" option to execute in foregroun>
    Jan 16 21:08:30 Puffer-Dev systemd[1]: Started Intel(R) Architectural Enclave Service Manager.
    Jan 16 21:08:30 Puffer-Dev aesm_service[19631]: The server sock is 0x5590971d3720
    Jan 21 05:03:23 Puffer-Dev aesm_service[19631]: [ADMIN]EPID Provisioning initiated
    Jan 21 05:03:24 Puffer-Dev aesm_service[19631]: The Request ID is 138bcd8af688471f885ae583772ce00b
    Jan 21 05:03:24 Puffer-Dev aesm_service[19631]: The Request ID is 80565f6a94be471aadd70d5d44d20e78
    Jan 21 05:03:25 Puffer-Dev aesm_service[19631]: [ADMIN]EPID Provisioning successful

Download the docker container:

.. code-block:: shell

    docker pull pufferfinance/secure_signer
