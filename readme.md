# Raspberry Pi Pico C++ SDK Docker DevContainer
[![Build and Upload Artifact](https://github.com/AppacYazilim/PicoDevEnv/actions/workflows/build.yml/badge.svg)](https://github.com/AppacYazilim/PicoDevEnv/actions/workflows/build.yml)
Welcome to **PicoDevEnv**, a simplified Raspberry Pi Pico C++ SDK setup using Docker DevContainers. This repository provides a complete development environment for Raspberry Pi Pico that operates within a Docker container. 

## Why is this method better?

Using Docker DevContainers for your development environment has several benefits:

1. **Consistency**: Docker containers ensure that the environment remains the same across different machines. This eliminates the "it works on my machine" problem.

2. **Portability**: With Docker, you can easily share your development environment. Anyone can clone your repository and get the exact same environment.

3. **Isolation**: Docker isolates your development environment from your local system, protecting your local machine from potential conflicts with system libraries or resources.

4. **Versatility**: Docker makes it easy to set up complex environments, which can be particularly useful when working with hardware-focused programming like the Raspberry Pi Pico.

## Getting Started

Make sure you have Visual Studio Code, Docker, and the Remote - Containers extension installed on your machine.

Follow these steps to get your environment set up:

1. Clone this repository to your local machine.

2. Open the cloned repository with Visual Studio Code.

3. At the bottom-left corner of the VSCode window, you will find the "Remote Window" button (it looks like "><" ). Click it and choose the "Reopen in Container" option. VSCode will then start building the Docker container which may take some time during the first run.

4. Once the container is built and the folder is reopened in the container, the development environment is ready to use.

## Building Your Project

To build your project:

1. Open a terminal in VSCode (which will be within the Docker environment).

2. Navigate to the `build` directory in your project.

3. Run the `make` command. This will compile your code and produce a `.uf2` file.

4. Once the build process is complete, you can find the `.uf2` file in the `build` directory. This file can be copied to a Raspberry Pi Pico in boot select mode to run the program.

Happy coding with your Raspberry Pi Pico!

## Configuring Your Board

This development environment is set up to use the `pico_w` board by default. The board configuration is specified in the `devcontainer.json` file with the `postCreateCommand`:

```json
"postCreateCommand": "mkdir -p build && cd build && cmake .. -DPICO_BOARD=pico_w"
```

If you're using a different board, you can easily update this configuration:

1. Open the `devcontainer.json` file in the root directory of your project.

2. Look for the `postCreateCommand` property. 

3. Replace `pico_w` in the `cmake` command with the name of your board. For example, if you're using the Raspberry Pi Pico, change the `cmake` command to:

```json
"postCreateCommand": "mkdir -p build && cd build && cmake .. -DPICO_BOARD=pico"
```

4. Save the `devcontainer.json` file.

5. Rebuild your Docker container. In VS Code, you can use the "Remote Containers: Rebuild Container" command.

After the container is rebuilt, the new board configuration will be used when building your project.

Remember, the board name must match one of the boards defined in the SDK. You can find the list of boards in the `pico/boards/include/boards` directory in the SDK.

# How to update the SDK

1. Rebuild the Docker Image: After updating the SDK, you'll need to rebuild your Docker image to include the latest changes. Go back to the root directory of your project and rebuild the Docker image. In VS Code, you can use the "Remote Containers: Rebuild Container" command.

2. Recompile Your Project: After updating the SDK, you should recompile your project to ensure it works with the updated SDK. Navigate to your build directory and run make.
```bash
cd /workspace/build
make
```