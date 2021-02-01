# SdkAPI

The SdkAPI is a CMake super project starter template for Stratify OS and API framework applications.

The sample `CMakeLists.txt` file uses an ad hoc method of cloning repositories from Github and building them. The template only includes libraries cloned using git, but you could also add applications as subprojects and link directly to the static libs built inside `SdkAPI` rather than installing to the local SDK.

# Getting Started

## Building for Stratify OS

Use `sl` to install a Stratify OS SDK.

```bash 
git clone https://github.com/StratifyLabs/SdkAPI.git
# You can modify the CMakeLists.txt file to include additional libraries if needed
cd SdkAPI
mkdir cmake_arm
cd cmake_arm
cmake .. -DIS_PULL=ON
make -j12
```

## Building for the Desktop

Building for the desktop requires cloning a copy of `CMakeSDK` in addition to `SdkAPI`.

```
git clone https://github.com/StratifyLabs/CMakeSDK.git
git clone https://github.com/StratifyLabs/SdkAPI.git
export SOS_SDK_PATH=$CWD/CMakeSDK
cd SdkAPI
mkdir cmake_link
cd cmake_link
cmake ..
make -j12
```
