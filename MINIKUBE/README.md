#Building without Docker

sudo apt-get install \
    automake \
    bc \
    build-essential \
    cpio \
    gcc-multilib \
    genisoimage \
    git \
    gnupg2 \
    libtool \
    locales \
    p7zip-full \
    python2 \
    unzip \
    wget \
    
IN_DOCKER=1 make minikube-iso-<arch>

$ ./out/minikube start --iso-url=file://$(pwd)/out/minikube-<arch>.iso

cd out/buildroot
make menuconfig
make

make savedefconfig

$ make linux-menuconfig

Adding third-party packages
To add your own package to the minikube ISO, create a package directory under iso/minikube-iso/package. This directory will require at least 3 files:

<package name>.mk - A Makefile describing how to download the source code and build the program
<package name>.hash - Checksums to verify the downloaded source code
Config.in - buildroot configuration

For a relatively simple example to start with, you may want to reference the podman package.

Continuous Integration Builds
We publish CI builds of minikube, built at every Pull Request. Builds are available at (substitute in the relevant PR number):

https://storage.googleapis.com/minikube-builds/PR_NUMBER/minikube-darwin-amd64
https://storage.googleapis.com/minikube-builds/PR_NUMBER/minikube-linux-amd64
https://storage.googleapis.com/minikube-builds/PR_NUMBER/minikube-windows-amd64.exe
Feedback
Was this page helpful?
