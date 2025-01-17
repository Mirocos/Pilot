# Pilot Engine

**this is a fork repo from [Pilot](https://github.com/BoomingTech/Pilot)**


<p align="center">
  <a href="https://games104.boomingtech.com">
    <img src="engine/source/editor/resource/PilotEngine.png" width="400" alt="Pilot Engine logo">
  </a>
</p>

**Pilot Engine** is a tiny game engine used for the [GAMES104](https://games104.boomingtech.com) course.
## ChangeList (Please first start with the Prerequisites)
- compile in Ubuntu18.04 With Gcc-9 G++-9
  - TBB(Thread Building Blocks) (2018 or newer) dependency requires, solution from [Ask-Ubuntu](https://askubuntu.com/questions/1170054/install-newest-tbb-thread-building-blocks-on-ubuntu-18-04)
  - May need change `cz.archive` mentioned in [Ask-Ubuntu](https://askubuntu.com/questions/1170054/install-newest-tbb-thread-building-blocks-on-ubuntu-18-04) to old-releases
```bash
  echo "deb http://old-releases.ubuntu.com/ubuntu eoan main universe" | sudo tee -a  /etc/apt/sources.list
  sudo apt update
  sudo apt install libtbb-dev
```
- add a linking configuration in `engine/source/editor/CMakeList.txt`
```cmake
target_link_libraries(${TARGET_NAME} tbb) 
```
- include `<algorithm>` in `engine/source/runtime/function/animation`
- change compiler clang/clang++ to gcc-9/g++-9 in `build_linux.sh` 
```shell
#line36
export CC=gcc-9
#line 37
export CXX=g++-9
```


## compilation tips
The easiest way to compile this project is execute the shell scripts `build_linux.sh`,
**Don't forget to get an executable permission to `engine/bin/Linux/meta_parser`** `metaparser` needs `clang-12` dependencies, so you may need to install `clang-12`:
```bash
sudo apt install clang-12 --install-suggests 
```
Then create a symbolic link for `libclang.so.12` that `meta-parser` needs in `/usr/lib/x86_64-linux-gnu/`, you may need **root** permission
```bash
ln -s libclang-12.so.1 libclang.so.12
```

Now finally comes to build the project

```bash
chmod +x build_linux.sh
./build_linux debug/release
```

Or build the project with Cmake command(if your default compiler is gcc-9 and g++-9）
```bash
cmake -S engine -B build -DCMAKE_BUILD_TYPE=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
cmake --build $pwd/build
```
If you are using Clion IDE like me, just use Clion to open the project directory and configure CMake Settings in `File | Settings | Build, Execution, Deployment | CMake | Cmake Options`


## Prerequisites

To build Pilot, you must first install the following tools.

### Windows 10/11
- Visual Studio 2019 (or more recent)
- CMake 3.19 (or more recent)
- Git 2.1 (or more recent)

### macOS >= 10.15 (x86_64)
- Xcode 12.3 (or more recent)
- CMake 3.19 (or more recent)
- Git 2.1 (or more recent)

### Ubuntu 20.04
 - apt install the following packages
```
sudo apt install git
sudo apt install cmake
sudo apt install clang
sudo apt install libxcb1-dev
sudo apt install libvulkan-dev
sudo apt install vulkan-validationlayers
sudo apt install mesa-vulkan-drivers
```  
- [NVIDIA driver](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile) (The AMD and Intel driver is open-source, and thus is installed automatically by mesa-vulkan-drivers)

## Build Pilot

### Build on Windows
You may execute the **build_windows.bat**. This batch file will generate the projects, and build the **Release** config of **Pilot Engine** automatically. After successful build, you can find the PilotEditor.exe at the **bin** directory.

Or you can use the following command to generate the **Visual Studio** project firstly, then open the solution in the build directory and build it manually.
```
cmake -S engine/ -B build
```

### Build on macOS

> The following build instructions only tested on specific hardware of x86_64, and do not support M1 chips. For M1 compatible, we will release later.

To compile Pilot, you must have the most recent version of Xcode installed.
Then run 'cmake' from the project's root directory, to generate a project of Xcode.

```
cmake -S engine/ -B build -G "Xcode"
```
and you can build the project with 
```
cmake --build build --config Release
```

### Build on Ubuntu 20.04 
You can execute the **build_linux.sh** to build the binaries.  
  
