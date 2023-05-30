# VSCode + STM32CUBEMX + CMSIS-DAP

1. 添加 rules 文件
    ```
    # CMSIS-DAP compatible adapters
    ATTRS{product}=="*CMSIS-DAP*", MODE="660", GROUP="plugdev", TAG+="uaccess"
    ```
2.  `.vscode/c_cpp_properties.json` 增加定义

    ```
    {
        "configurations": [
            {
                "name": "Linux",
                "includePath": [
                    "${workspaceFolder}/**"
                ],
                "defines": [
                    "STM32F103xB",
                    "USE_HAL_DRIVER"
                ],
                "compilerPath": "/usr/bin/arm-none-eabi-gcc",
                "cStandard": "c17",
                "cppStandard": "c++14",
                "intelliSenseMode": "linux-gcc-arm",
                "configurationProvider": "ms-vscode.makefile-tools"
            }
        ],
        "version": 4
    }
    ```

    