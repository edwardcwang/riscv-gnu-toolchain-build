Building riscv-gnu-toolchain
============================

Miscellaneous notes on building `riscv-gnu-toolchain`.

Current riscv-gnu-toolchain revision: `d8243f7`

Environment prep

```
sudo mkdir -p /opt/riscv
sudo chown $(id -u):$(id -g) /opt/riscv
```

Installing tools

```
# From the riscv-gnu-toolchain README
sudo apt-get install -y autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev
```

Repo

```
git clone --recursive https://github.com/riscv/riscv-gnu-toolchain.git
```

Build

```
mkdir build

../configure --prefix=/opt/riscv --target=riscv32-unknown-linux-gnu --with-arch=rv32gc --with-abi=ilp32d

# Multi-lib enables support for multiple ABIs, including important headers
# like gnu/lib-names-ilp32.h
#../configure --prefix=/opt/riscv --target=riscv32-unknown-linux-gnu --with-arch=rv32gc --enable-multilib

# --with-abi does not support multiple options
#../configure --prefix=/opt/riscv --target=riscv32-unknown-linux-gnu --with-arch=rv32gc --with-abi=ilp32,ilp32d,ilp32e,ilp32f,ilp32q

# 64-bit ABIs: lp64,lp64f,lp64d,lp64q
```

```
make linux
```

Package

```
cd ~
tar cjvf toolchain.tar.bz2 -C /opt riscv
```

Tarball formats
===============
Examples:
* `riscv-gnu-toolchain-d8243f7-rv32gc-linux-multilib-ubuntu1910.tar.bz2`
* `riscv-gnu-toolchain-d8243f7-rv32gc-linux-ilp32d-ubuntu1910.tar.bz2`

* `riscv-gnu-toolchain-<revision>-rv32gc-linux-<abi>-ubuntu1910.tar.bz2`

