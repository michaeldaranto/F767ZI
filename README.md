# F767ZI
Experiment with Nucleo Board F767ZI

My route to develop stm32F767ZI environment

    1. Buy a nucleo board F767ZI :)
    3. Install GNU Arm Embedded Toolchain from https://developer.arm.com/open-source/gnu-toolchain/gnu-rm
    4. Setup whatever IDE or text editor. I choose Visual Studio Code. https://code.visualstudio.com/
    5. Install stm32cubeMX to generate a Makefile and provide setup libraries. http://www.st.com/en/development-tools/stm32cubemx.html 
    6. Start coding !
    7. This time I'm using LL (Low level) library from Cube.


Note About Visual Studio Code

Script "tasks.json"  :
    make ( to compile,linking, and generate firmware.elf)
    openOCD to flash the chip
    Run Debug server

 {
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Make",
            "type": "shell",
            "command": "make all ",
            "group": {
                "kind": "build",
                "isDefault": true
            }
        },
       
        {
            "label": "OpenOCD-Flash",
            "type": "shell",
            "command": "openocd -f /your/path/scripts.cfg -c 'stm_flash /your/path/firmware.elf'  ",
                 
            "group": {
                "kind": "build",
                "isDefault": true
            }
        },

        {
            "label": "OpenOCD-Debug",
            "type": "shell",
            "command": "openocd -f /your/path/scripts.cfg   ",
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]


}

Script "launch.json"  :
    This script will run native debug.
    Please run "OpenOCD-Debug" first.

{
    "version": "0.2.0",
    "configurations": [

        {
            "cwd": "${workspaceRoot}",
            "name": "Debug-OpenOCD",
            "request": "launch",
            "target": "./yourpath/firmware.elf",
            "type": "gdb",
            "gdbpath" : "/usr/bin/arm-none-eabi-gdb",
            "autorun": [
            "target remote localhost:3333",
            "symbol-file ./yourpath/firmware.elf",
             "monitor reset" 
            ]
        },


    ],
 }

Extension :
Install Native Debug extension. https://github.com/WebFreak001/code-debug
  





 
