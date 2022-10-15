# C++: One Configuration, Many Platforms

![build](https://github.com/jason-m-reich/cpp-one-config-many-platforms/actions/workflows/build-linux.yml/badge.svg)
![build](https://github.com/jason-m-reich/cpp-one-config-many-platforms/actions/workflows/build-mac.yml/badge.svg)
![build](https://github.com/jason-m-reich/cpp-one-config-many-platforms/actions/workflows/build-windows.yml/badge.svg)
![tests](https://github.com/jason-m-reich/cpp-one-config-many-platforms/actions/workflows/run-unit-tests.yml/badge.svg)

## Requirements

There more individualized requirements appear in each platforms' getting started section; the ones here are not listed in any of those sections.

- CMake 3.21 or higher

## Getting Started

### Linux Setup

What follows assumes you have done the following (or equivalent, depending on your Linux distribution):

```
sudo apt-get update
sudo apt-get install build-essential gdb
sudo apt-get install curl zip unzip tar
sudo apt-get install pkg-config
sudo apt-get install ninja-build
```

- Open a terminal and navigate to the directory into which you want to clone this project.

- Set up both the project itself, and the vcpkg submodule that the project uses for package management:

```
git clone --recurse-submodules https://github.com/jason-m-reich/cpp-one-config-many-platforms.git
cd cpp-one-config-many-platforms
./vcpkg/bootstrap-vcpkg.sh -disableMetrics
```

(If you prefer, you can run `.\vcpkg\bootstrap-vcpkg.bat` without "-disableMetrics" and read about the tracking Microsoft would do).

### Linux Development

#### VS Code Users

This section assumes you have the C/C++ extension and CMake Tools extension installed in VS Code.

If you would like to read the VS Code docs on the steps that follow, they are [here](https://github.com/microsoft/vscode-cmake-tools/blob/main/docs/cmake-presets.md#configure-and-build).

- Open the root directory of this project in VS Code

Before moving on, it is worth searching the CMakePresets.json file for "Linux Debug" and "Build Linux Debug". These presets are used in the "Configure Project" and "Build Project" sections that follow.

##### Configure Project

- Go to View &rarr; Command Pallete.
- Start tpying "CMake: Select Configure Preset" until you see it. Click on it.
- From the dropdown that appears, click on "Linux Debug".
- Now the VS Code is ready to configure the project. Open the Command Pallete again, start typing `CMake: Configure` until you see it. Click on it.

##### Build Project

- Go to View &rarr; Command Pallete.
- Start tpying "CMake: Select Build Preset" until you see it. Click on it.
- From the dropdown that appears, click on "Build Linux Debug".
- Now the VS Code is ready to build the project. Open the Command Pallete again, start typing `CMake: Build` until you see it. Click on it.

##### Run Project

Find the run (triangle) icon at the bottom of the screen in the status bar. When you hover over it, it should say "Launch the selected...".

Run the application by clicking on this button.

##### Run Unit Tests

The following steps assume you have done everything up to this point in this "VS Code Users" section.

We will use CMake's [ctest](https://cmake.org/cmake/help/latest/manual/ctest.1.html#ctest-1) executable to run our GoogleTest unit tests.

- Go to View &rarr; Command Pallete.
- Start tping "CMake: Select Test Preset" until you see it. Click on it.
- From the dropdown that appears, click on "all-unit-tests-linux".

"all-unit-tests-linux" can be found in the CMakePresets.json file.

- Go to View &rarr; Command Pallete.
- Start typing "CMake: Run Tests" until you see it. Click on it.

From now on, you might find it is more convenient to use the run button to run both the applicaiton and the unit tests (recall the triangular button mentioned under "Run Project").

To do this, click _to the right_ of the run button to select the "target" you want to run. When you do this, a dropdown will appear at the top of the screen and you can select main (the application target) or unit_tests (the test target).

#### CLion Users

At the time of this writing, CLion only supports CMake Presets versions 2 and 3. And test presets aren't supported yet. More on that in [this CLion doc](https://www.jetbrains.com/help/clion/cmake-presets.html).

Until this changes, you can skip using CMakePresets.json altogether and use the normal CLion workflow for CMake projects... with the one caveat that you will have to manually tell CLion (and CMake) about vcpkg in the following way:

- Open the root directory of this project in CLion
- In the Open Project Wizard window that appears, paste the following in the "CMake options:" field `-DCMAKE_TOOLCHAIN_FILE=vcpkg/scripts/buildsystems/vcpkg.cmake`

You should now be able to use CLion with CMake normally by selecting either main or unit_tests configurations from the dropdown next to the green run icon at the top of the screen.

#### Terminal Users

- Open the root directory of this project in a terminal

##### Configure Project

```
cmake --preset=linux-debug
```

##### Build Project

```
cmake --build --preset=build-linux-debug
```

##### Run Project

```
./linux-debug/main
```

##### Run Unit Tests

```
ctest --preset=all-unit-tests-linux
```

or

```
./linux-debug/tests/unit_tests
```

### Mac Setup

This assumes your machine has a recent Xcode build, and that you have installed the following (it doesn't matter if you use something other than Homebrew for the intsalls so long as the dependencies are properly installed and discoverable):

```
brew install pkg-config
brew install ninja
```

- Open a terminal and navigate to the directory into which you want to clone this project.

Set up both the project itself, and the vcpkg submodule that the project uses for package management:

```
git clone --recurse-submodules https://github.com/jason-m-reich/cpp-one-config-many-platforms.git
cd cpp-one-config-many-platforms
./vcpkg/bootstrap-vcpkg.sh -disableMetrics
```

(If you prefer, you can run `.\vcpkg\bootstrap-vcpkg.bat` without "-disableMetrics" and read about the tracking Microsoft would do).

### Mac Development

#### VS Code Users

See "Build From VS Code" in the Linux section above. Everything (even file names and preset names just needs to have "linux" swapped out for "mac"). _Just be sure to change "linux" to "mac" before pasting any text_.

#### CLion Users

At the time of this writing, CLion only supports CMake Presets versions 2 and 3. And test presets aren't supported yet. More on that in [this CLion doc](https://www.jetbrains.com/help/clion/cmake-presets.html).

Until this changes, you can skip using CMakePresets.json altogether and use the normal CLion workflow for CMake projects... with the one caveat that you will have to manually tell CLion (and CMake) about vcpkg in the following way:

- Open the root directory of this project in CLion
- In the Open Project Wizard window that appears, paste the following in the "CMake options:" field `-DCMAKE_TOOLCHAIN_FILE=vcpkg/scripts/buildsystems/vcpkg.cmake`

You should now be able to use CLion with CMake normally by selecting either main or unit_tests configurations from the dropdown next to the green run icon at the top of the screen.

#### Terminal Users

- Open the root directory of this project in a terminal

##### Configure Project

```
cmake --preset=mac-debug
```

##### Build Project

```
cmake --build --preset=build-mac-debug
```

##### Run Project

```
./mac-debug/main
```

##### Run Unit Tests

```
ctest --preset=all-unit-tests-mac
```

or

```
./mac-debug/tests/unit_tests
```

### Windows Setup

This assumes your machine has a recent Visual Studio (VS) build (the community version of VS is fine),
that your VS copy has "Desktop development with C++" installed from the VS workloads installer,
and that you have git for Windows on your machine.

- Open Windows PowerShell and navigate to the directory into which you want to clone this project.

Set up both the project itself, and the vcpkg submodule that the project uses for package management:

```
git clone --recurse-submodules https://github.com/jason-m-reich/cpp-one-config-many-platforms.git
cd cpp-one-config-many-platforms
.\vcpkg\bootstrap-vcpkg.bat -disableMetrics
```

(If you prefer, you can run `.\vcpkg\bootstrap-vcpkg.bat` without "-disableMetrics" and read about the tracking Microsoft would do).

### Windows Development

#### Visual Studio Users

- Open Visual Studio and select "Open a local folder"
- Navigate to and select the cpp-one-config-many-platforms directory on your machine and select "Select Folder"

##### Configure Project

- Go to Tools &rarr; Options
- Under CMake &rarr; General make sure that either "Use CMake Presets if..." or "Always use CMake Presets" is selected

Wait for the CMake output at the bottom of the screen to say "CMake generation finished."

If you don't see CMake output at the bottom of your screen that (eventually) ends with "CMake generation finished.", then go to the project menu and select "Configure Cache".

##### Build Project

- From the build menu select "Build All"

##### Run Project

- On the toolbar, find the green run button that says "Select Startup Item" and click the down arrow to the right of it
- Select `main.exe`
- Click on the run button

##### Run Unit Tests

- Follow the above steps from "Run Project", except select `unit_tests.exe` from the button's dropdown before clicking on run

#### VS Code Users

See "Build From VS Code" in the Linux section above. Everything (even file names and preset names just needs to have "linux" swapped out for "windows"). _Just be sure to change "linux" to "windows" before pasting any text_.

#### CLion Users

At the time of this writing, CLion only supports CMake Presets versions 2 and 3. And test presets aren't supported yet. More on that in [this CLion doc](https://www.jetbrains.com/help/clion/cmake-presets.html).

Until this changes, you can skip using CMakePresets.json altogether and use the normal CLion workflow for CMake projects... with the one caveat that you will have to manually tell CLion (and CMake) about vcpkg in the following way:

- Open the root directory of this project in CLion
- In the Open Project Wizard window that appears, paste the following in the "CMake options:" field `-DCMAKE_TOOLCHAIN_FILE=vcpkg/scripts/buildsystems/vcpkg.cmake`

You should now be able to use CLion with CMake normally by selecting either main or unit_tests configurations from the dropdown next to the green run icon at the top of the screen.

#### PowerShell Users

- Open Developer PowerShell for VS 2022 (note the "Developer" and the "for VS 2022") and navigate to the root directory of this project

##### Configure Project

```
cmake --preset=windows-debug
```

##### Build Project

```
cmake --build --preset=build-windows-debug
```

##### Run Project

```
.\windows-debug\main.exe
```

##### Run Unit Tests

```
ctest --preset=all-unit-tests-windows
```

or

```
.\windows-debug\tests\unit_tests.exe
```
