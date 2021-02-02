# SdkAPI

The SdkAPI is a CMake super project starter template for Stratify OS and API framework applications.

The sample `CMakeLists.txt` file uses an ad hoc method of cloning repositories from Github and building them. The template only includes libraries cloned using git, but you could also add applications as subprojects and link directly to the static libs built inside `SdkAPI` rather than installing to the local SDK.

# Getting Started

## Building for Stratify OS

### Installing `sl` and the Compiler

Use `sl` to install a Stratify OS compiler. To install `sl` use the following commands. Be sure to pay attention to the OS specific comments when setting variables.

```bash
# For MacOS
export SL_LINK=https://stratifylabs.page.link/sl_Darwin_x86_64
# For Windows
export SL_LINK=https://stratifylabs.page.link/sl_windows_x86_64

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
mkdir -p $INSTALL_DIRECTORY/bin
curl -L -o $INSTALL_DIRECTORY/bin/sl $SL_LINK
chmod 755 $INSTALL_DIRECTORY/bin/sl
echo 'export PATH='$INSTALL_DIRECTORY'/bin:$PATH' >> ~/.$PROFILE
echo 'export SOS_SDK_PATH='$INSTALL_DIRECTORY >> ~/.$PROFILE
source ~/.$PROFILE
```

Now you can use `sl` to install the Stratify OS compiler on your computer.

```bash
sl --initialize
sl cloud.login
# paste your credentials from the website in the bash terminal
sl cloud.install:compiler
```

### Building the SDK

```bash 
git clone https://github.com/StratifyLabs/SdkAPI.git
# You can modify the CMakeLists.txt file to include additional libraries if needed
cd SdkAPI
mkdir cmake_arm
cd cmake_arm
# You could also use "Unix Makefiles" and "make" instead of "Ninja"/"ninja"
cmake .. -G Ninja -DIS_PULL=ON
ninja
# if you want to use the same API libraries for multiple projects you can install them
ninja install
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
# You could also use "Unix Makefiles" and "make" instead of "Ninja"/"ninja"
cmake .. -G Ninja
ninja
# if you want to use the API libraries for multiple projects, you can install them
ninja install
```

## Uninstalling `sl` and the Compiler

To completely uninstall the SDK, you need to:

- Delete the `$INSTALL_DIRECTORY` folder that you specified
- Modify the bash `$PROFILE` file to remove the modifications to `$PATH` and `$SOS_SDK_PATH`
