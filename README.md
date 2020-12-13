# SdkAPI

The SdkAPI is a CMake super project starter template for Stratify OS and API framework applications.

The sample `CMakeLists.txt` file uses an ad hoc method of cloning repositories from Github and building them. The template only includes libraries which can be pulled and installed in the local SDK. You could also add an application as a subproject and link directly to the static libs built inside `SdkAPI` rather than installing to the local SDK.

# Getting Started

## Building for Stratify OS

Use `sl` to install a Stratify OS SDK.

```
git clone https://github.com/StratifyLabs/CMakeSDK.git
git clone https://github.com/StratifyLabs/SdkAPI.git
cd SdkAPI
mkdir cmake_arm
cd cmake_arm
cmake ..
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
