# llvm-linux-5.8.5


## 1. Install LLVM 10

### 1.1 install llvm 10.0 from git repo
```
sudo apt-get install build-essential gcc-9-plugin-dev clang ninja-build cmake libncurses5-dev libelf-dev libssl-dev flex bison bc git pigz
// git clone https://github.com/llvm/llvm-project.git
cd llvm-project
git checkout release/10.x
mkdir build
cd build

```
Using Ninja
```

# cmake -G Ninja -DLLVM_ENABLE_PROJECTS='clang;lld;compiler-rt' \
-DCMAKE_BUILD_TYPE=Release -DLLVM_ENABLE_WARNINGS=OFF \
-DCMAKE_INSTALL_PREFIX=/usr/local/llvm-10 ../llvm

cmake -G Ninja -DLLVM_ENABLE_PROJECTS='clang;lld;compiler-rt' -DCMAKE_BUILD_TYPE=Debug -DLLVM_ENABLE_WARNINGS=OFF -DCMAKE_INSTALL_PREFIX=/usr/local/llvm-10 ../llvm

ninja
sudo ninja install
```


Using Cmake and Make
```
cmake -DLLVM_ENABLE_PROJECTS='clang;lld;compiler-rt' -DCMAKE_BUILD_TYPE=Debug -DLLVM_ENABLE_WARNINGS=OFF -DCMAKE_INSTALL_PREFIX=/usr/local/llvm-10 ../llvm
cmake --build .
mkdir  ./docs/ocamldoc
mkdir  ./docs/ocamldoc/html
make 
sudo make install
```

```
export PATH=/usr/local/llvm-10/bin:$PATH

OR

export PATH=/home/wenhui/llvm-10.0.0.src/build/bin:$PATH
```

## 2. Compile Linux 5.8.5 with LLVM 10

### 2.1 Download tar ball 5.8.5 

https://www.kernel.org/
`
tar -xvf linux-5.8.5.tar.xz
`
### 2.2. Compile kernel with LLVM

```
// cp .config 
make menuconfig LLVM=1
make -j4 LLVM=1
sudo make modules_install LLVM=1
sudo make install LLVM=1
sudo update-grub2
sudo reboot
```


