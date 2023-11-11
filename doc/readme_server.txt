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

$ sudo apt install astyle cmake gcc ninja-build libssl-dev python3-pytest python3-pytest-xdist unzip xsltproc doxygen graphviz python3-yaml valgrind

$ sudo apt -y install autoconf automake cmake gcc git libtool libssl-dev make ninja-build zlib1g-dev

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

$ sudo vi /etc/group
    sshd:x:74:
     
$ sudo vi /etc/passwd
    sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin

$ git clone --depth 1 --branch OQS-v8 https://github.com/open-quantum-safe/openssh.git

$ cd openssh

$ sudo ./oqs-scripts/build_openssh.sh

$ ./oqs-test/run_tests.sh