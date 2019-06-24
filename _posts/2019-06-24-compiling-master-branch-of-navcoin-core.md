---
layout: post
title: Need to compile Master Branch of NavCoin-Core?
---

Need to compile [NavCoin-Core][navcoin_github] but don't know exactly how?

All you need are the following:

* A linux box
* A tutorial to teach you ( This is that tutorial, LMFAO )

NOTE: For the sake of simplicity, my example will be using an `Ubuntu 18.04 Linux Box`

## Step 1

Install things we need, mainly [Git][git_scm] and `build-essential`.

```shell
sudo apt install git build-essential
```

We need [Git][git_scm] to clone the source and `build-essential` alias package on `Ubuntu` to install our build toolchain.

## Step 2

Clone the code from [NavCoin-Core github repository][navcoin_github].

```shell
# Clone the repo
git clone https://github.com/navcoin/navcoin-core.git

# Move your working directory to the cloned dir
cd navcoin-core

# Checkout the branch/tag/commit you wanna build
git checkout master
```

OR you can update the code if you already have it cloned.

```shell
# Move your working directory to an existing clone
cd navcoin-core

# Checkout the branch/tag/commit you wanna build
git checkout master

# Just pull the code changes
git pull
```

## Step 3

Compile required dependencies

```shell
cd ./depends
make
```

## Step 4

Create and run the `./configure` script

```shell
# Assuming your working directory is still in `./depends` from last commands
cd ..

# Create the `./configure` script
./autogen.sh

# Run the `./configure` script and use the dependencies that we compiled in Step 3
./configure --prefix=`pwd`/`uname -m`-pc-linux-gnu
```

## Step 5

Compile [NavCoin-Core][navcoin_github] itself

```shell
make
```

## Conclusion

Once you have followed this tutorial, you should have a binary in `./src/qt/navcoin-qt` that is the [NavCoin-Core][navcoin_github] `QT` wallet/client

You should also have a binary in `./src/navcoind` which is the [NavCoin-Core][navcoin_github] `daemon` wallet/client

## Things to keep in mind

* You should use `./depends` DIR dependencies to have closest experience to the releases from the offical tagged versions
* You should use `./depends` DIR dependencies if you are not sure what system packages you need
* You can use system dependencies if you want to have less compiling, you can skip `Step 3` if you have required dependencies install system wide
* You can run `make` commands with `-j<number of cpu threads>` ( if you have an eight thread cpu, i7-4790k, you can run `make -j8` to speed up the compile time )

[navcoin_github]: https://github.com/navcoin/navcoin-core
{:target="_blank"}

[git_scm]: https://git-scm.com/
{:target="_blank"}
