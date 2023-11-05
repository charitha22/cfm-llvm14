This repository contains the source code for Control-flow Melding (CFM). CFM is a compiler transformation that melds (i.e. merges) isomorphic control-flow regions contained within `if` and `else` sections of a conditional branch. CFM transformation is useful for reducing control-flow divergence in GPU programs and reduce code size in CPU programs. This version of CFM is implemented on top of `LLVM-14.0.0`.

# Dependencies

The default apt packages should be enough for Ubuntu >= 19.10. Default packages plus a pre-built cmake should work for Ubuntu >= 18.04. For older systems, you might have to satisfy the dependencies manually.

## Building LLVM:
* cmake (>= 3.13.4 : If your cmake is older than that, install a newer version maually and add it to your path.
* build-essential : This will pull the rest of the dependencies

For more information about LLVM dependencies check the [LLVM project page](https://llvm.org/docs/GettingStarted.html#software).

# Installation Instructions

Download the code
```
git clone git@github.com:charitha22/cfm-llvm14.git
git clone git@github.com:llvm/llvm-project.git
```

Checkout the LLVM-14.0.0 release.
```
cd llvm-project
git checkout $(cat ../cfm-llvm14/llvm_version.txt)
```

Apply the patch containing CFM source code changes on top of llvm-14
```
git apply ../cfm-llvm14/control-flow-melding-pass-with-llvm-14.patch
```

Build LLVM
```
bash scripts/run_cmake.sh 
bash scripts/build_install.sh
```

Run examples
```
export LLVM_HOME=$(pwd)/build
cd cfm_tests/cfg/
make && make test
```


