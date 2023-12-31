#: Title : PQC and OpenSSH - Remote Server
#: Author : "Caio Abreu Ferreira" <abreuferr_gmail.com>
#: Description : Post-Quantum Cryptography and OpenSSH
#: Options : 

#############################################
#
# doc
#
#############################################

# liboqs
#
# https://github.com/open-quantum-safe/liboqs-go/blob/main/README.md

# openssh
#
# https://developer.ibm.com/tutorials/set-up-a-quantum-safe-ssh-connection/

#############################################
#
# gnu/linux debian
#
#############################################

$ sudo apt update

$ sudo apt -y upgrade

$ sudo apt install autoconf automake cmake gcc libtool libssl-dev make ninja-build zlib1g-dev

$ sudo groupadd sshd

$ sudo useradd -g sshd -c 'sshd privsep' -d /var/empty -s /bin/false sshd

#############################################
#
# liboqs
#
#############################################

$ git clone --depth=1 https://github.com/open-quantum-safe/liboqs

$ cmake -S liboqs -B liboqs/build -DBUILD_SHARED_LIBS=ON

$ cmake --build liboqs/build --parallel 8

$ sudo cmake --build liboqs/build --target install

$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib

$ sudo ldconfig

#############################################
#
# openssh
#
#############################################

$ git clone --depth 1 --branch OQS-v8 https://github.com/open-quantum-safe/openssh.git

$ cd openssh

$ sudo ./oqs-scripts/build_openssh.sh

$ ./oqs-test/run_tests.sh

$ sed -i 's/ListenAddress/#ListenAddress/g' regress/sshd_config