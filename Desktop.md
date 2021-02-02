# API for Desktop Builds

Building for the desktop (or any non-cross-compiling target) requires cloning a copy of `CMakeSDK` in addition to `SdkAPI`.

## Setting up the Environment

If you have already done these steps as part of a Stratify OS build, you can skip this.

```bash
# Choose a place to install the directory
export INSTALL_DIRECTORY=~/StratifyLabs-SDK

# on Windows you could use something easily accessible
export INSTALL_DIRECTORY=/c/StratifyLabs-SDK

# For MacOS and Windows (Msys)
export PROFILE=bash_profile

# For Linux
export PROFILE=profile
```

```bash
# Copy and paste these
mkdir -p $INSTALL_DIRECTORY
chmod 777 -R $INSTALL_DIRECTORY # if needed to make public
echo 'export SOS_SDK_PATH='$INSTALL_DIRECTORY >> ~/.$PROFILE
source ~/.$PROFILE
```

## Cloning and Building

```
# if you didn't us sl to install the compiler, you need CMakeSDK as well
git clone https://github.com/StratifyLabs/CMakeSDK.git
cd CMakeSDK
mkdir cmake_link && cd cmake_link
cmake .. -G Ninja && ninja install

# Now clone the SdkAPI
git clone https://github.com/StratifyLabs/SdkAPI.git
cd SdkAPI
mkdir cmake_link && cd cmake_link
# You could also use "Unix Makefiles" and "make" instead of "Ninja"/"ninja"
cmake .. -G Ninja && ninja
# if you want to use the API libraries for multiple projects, you can install them
ninja install
```
