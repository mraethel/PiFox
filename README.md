PiFox
=====

Video of the game in action: https://www.youtube.com/watch?v=-5n9IxSQH1M

Developed as an extension to a first year group project at Imperial College London.

Bare Metal 3D rail shooter game

* 5800 lines of ARM assembly (ARMv6 + VFP1)
* Software rasterizer
* 3D objects
* 2D billboards
* Sound using DMA
* NES controller input
* Math & utility library
* GitHub: https://github.com/ICTeam28/PiFox
* Emulator: https://github.com/ICTeam28/PiEmu

Dependencies
-----

Using your favourite Linux package manager, install:

* arm-none-eabi-binutils
* cmake

Build
-----

The project uses CMake and requires an ARM assembler supporting
GNU as syntax. 

    mkdir build
    cd build
    cmake ..
    make
    
Building on a non-Raspbian machine use the `-DCMAKE_TOOLCHAIN_FILE=../toolchains/arm-none-eabi.cmake` argument to cmake.

Emulation
-----

PiEmu (https://github.com/ICTeam28/PiEmu) can run the game without sound. Assuming PiFox and PiEmu have been cloned in the same directory and both are built, PiEmu must be invoked with the following command inside PiFox's build directory:

    ../../PiEmu/build/piemu --graphics --quiet --memory=256M --addr=65536 --nes kernel.img 

A qemu branch can be used to emulate the game at a higher framerate, but sound must be disabled. (https://github.com/Torlus/qemu/tree/rpi)

config.txt
----------

In order to be compatible with qemu, the kernel must be loaded at address 0x10000.

    disable_overscan=1
    disable_pvt=1
    force_turbo=1
    gpu_mem_256=160
    gpu_mem_512=316
    cma_lwm=16
    cma_hwm=32
    kernel_address=65536

Wiring the controller
---------------------

|    NES   |  Raspberry Pi  |
|:--------:|:--------------:|
| GND      | Ground         |
| VCC      | 3v3            |
| CUP      | GPIO 10        |
| OUT 0    | GPIO 11        |
| D1       | GPIO 4         |

![NES Pinout](https://raw.github.com/ICTeam28/PiFox/master/assets/nes-controller-pinout.png)

![Raspberry PI Pinout](https://raw.github.com/ICTeam28/PiFox/master/assets/raspbery-pi-pinout.png)

Authors
-------
Nandor Licker
- Email: nandor.licker13[at]imperial.ac.uk
- Github [@nandor](https://github.com/nandor)

Ilija Radosavovic
- Email: ilija.radosavovic13[at]imperial.ac.uk
- Github [@ir413](https://github.com/ir413)

David Avedissian
- Email: david.avedissian13[at]imperial.ac.uk
- Github [@davedissian](https://github.com/davedissian)
- Twitter [@davedissian](https://twitter.com/davedissian)

Nic Prettejohn
- Email: nicolas.prettejohn13[at]imperial.ac.uk
- Github [@nkp](https://github.com/nkp)
- Twitter [@thisisnkp](https://twitter.com/thisisnkp)

Special thanks
--------------

* https://github.com/dwelch67/raspberrypi
* https://github.com/PeterLemon/RaspberryPi


Special thanks to chpatrick (Patrick Chilton) for his advice.
