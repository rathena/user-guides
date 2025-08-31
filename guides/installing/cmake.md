# Using CMake

This guide covers how to use cmake to build rAthena.

## Pre-Requisites

### The Code Repository

Before you begin, ensure you have a copy of the rAthena code repository. You can obtain it by cloning the repository from GitHub:

```bash
git clone https://github.com/rathena/rathena.git
```

### Operating System

CMake is supported on most Linux operating systems, as well as Windows.

#### Microsoft Visual Studio

If you're using Visual Studio, Microsoft's [CMake projects in Visual Studio](https://learn.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio) guide is a good place to start.

#### Linux

CMake is available on all major distros. You can install it with your package manager. For example, on Ubuntu, you can use the following command:

```bash
sudo apt install cmake
```

### Other Dependencies

On Linux, you'll also need to install the following packages:

* A C++ compiler (e.g., `g++` on Ubuntu)
* A MySQL development package (e.g., `libmariadbclient-dev` on Ubuntu)
* ZLib (e.g., `zlib1g-dev` on Ubuntu)
* LibPCRE (e.g., `libpcre3-dev` on Ubuntu)

For other distributions, please refer to your package manager's documentation for the equivalent package names.

## Building with CMake

### Visual Studio

Microsoft's [CMake projects in Visual Studio](https://learn.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio) guide will explain how to open a project with a CMakeLists.txt file. Instead of opening a project or solution file, open the `rathena` folder that contains the CMakeLists.txt file, and Visual Studio will automatically configure the project.

### Command Line (Either Windows or Linux)

If you'd rather not use Visual Studio, you can build rAthena from the command line using CMake. Open a command prompt and navigate to the `rathena` directory.

First, run the following command to configure the build. You should only need to do this once.

```bash
cmake -B build
```

This creates a directory called `build` which CMake will use to store all the build-related files.

Then to actually build the project, use the following command:

```bash
cmake --build build
```

Because CMake stores information about the build in the `build` directory, if we add new files to a CMakeLists.txt file or modify existing ones, we can simply re-run the `--build` command to rebuild the project. No re-configuring or `make clean` needed!

## Configuring the build

There are a lot of different options to build rAthena with. Specifying the packet version, using pre-renewal or not, etc, is all configured through CMake.

The list of options can be found in the root directory of the rAthena repository, in the `CMakeLists.txt` file.

Here are a few of the most commonly used options:

Option | Type | Default Value | Comments
-------|------|---------------|---------
`PACKETVER` | String | `20211103` | The packet version to use.
`MAXCONN` | Number | (empty) | The maximum number of connections on Linux. Empty means use default FD_SETSIZE.
`ENABLE_PRERE` | Boolean | `OFF` | Enable pre-renewal features.
`ENABLE_WEB_SERVER` | Boolean | `ON` | Enable the web server.
`ENABLE_RDTSC` | Boolean | `OFF` | Enable RDTSC instruction as a timing source.
`ENABLE_DEBUG` | Boolean | `OFF` | Enable extra debug code.
`ENABLE_MEMMGR` | Boolean | `ON` | Enable memory manager.
`ENABLE_PROFILER` | String | `OFF` | Enable the profiler. Only other valid option is `gprof`.
`ENABLE_BUILDBOT` | Boolean | `OFF` | Enable extra buildbot code.
`ENABLE_SOCKET_EPOLL` | Boolean | `OFF` | Use epoll instead of select.
`ENABLE_VIP` | Boolean | `OFF` | Enable VIP system.

To set these using the command line, pass them as options to the `cmake` command. For example:

```bash
cmake -D PACKETVER=20140806 -D MAXCONN=2048 -D ENABLE_PRERE=ON -D ENABLE_WEB_SERVER=OFF -B build
```

## Using Presets

Instead of having to write the options down in the command line every time, you can use [cmake presets](https://cmake.org/cmake/help/latest/manual/cmake-presets.7.html). We have added our own `CMakePresets.json` file with some basic presets. You can create your own presets and inherit the basic presets to save some time. Create a file named `CMakeUserPresets.json` and place it in the root of your project. Here's an example of what it might look like, importing the `linux` preset and setting your specific options:

```json
{
  "version": 4,
  "configurePresets":[
    {
      "name": "myro",
      "cacheVariables": {
        "ENABLE_PRERE": "ON",
        "PACKETVER": "20200401",
        "ENABLE_MEMMGR": "OFF",
        "ENABLE_SOCKET_EPOLL": "ON"
      }
    },
    {
      "name": "myro-debug",
      "inherits": ["linux", "myro"],
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "Debug",
        "ENABLE_DEBUG": "ON"
      }
    },
    {
      "name": "myro-release",
      "inherits": ["linux", "myro"],
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "RelWithDebInfo",
        "ENABLE_DEBUG": "OFF"
      }
    }
  ],
  "buildPresets": [
    {
      "name": "myro-debug",
      "configurePreset": "myro-debug",
      "targets": ["server"]
    },
    {
      "name": "myro-release",
      "configurePreset": "myro-release",
      "targets": ["server"]
    }
  ]
}
```

You can then use this preset with the following command:

```bash
cmake --preset myro-debug -B build
cmake --preset myro-debug --build build
```

## Running the server

### Running the server on Linux

After building the project, you can run the server using the following command:

```bash
./athena-start.sh start
```

### Running the server on Windows

After building the project, you can run the server using the following command:

```bash
.\runserver.bat start
```
