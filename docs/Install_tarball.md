<!--
---

[TOC]
-->
---

**Foreword**

Notes.

---

# Install a Tarball on Linux

Download the tarball; it can have different extensions:

- file.tar.gz
- file.tgz
- file.tar.bz2
- file.tbz2

Unzip the file:

- CLI: `$ tar xvfz sqlite-autoconf-3071502.tar.gz`.
- Double-clicking the triggers an software.

Install the tarball on `/usr/local`:

- Change directory (where the file is located; however, the installation will be in: `/usr/local`).
    - `$ cd sqlite-autoconf-3071502`.
- Open INSTALL or README file for more information (choose).
    - `$ vi INSTALL`.
    - `$ gedit INSTALL`.
    - Or another text editor.
- Configure the software to ensure your system has the necessary functionality and libraries to successfully compile the package.
    - `$ ./configure --prefix=/usr/local`.
- Compile all the source files into executable binaries.
    - `$ make`.
- Install the binaries and any supporting files into the appropriate locations.
    - `$ sudo make install`.
    
# Run an Executive file on Linux

- Run a .sh file in the bash.
    - `$ bash file.sh`.
