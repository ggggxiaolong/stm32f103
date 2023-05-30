# VSCode + STM32CUBEMX + CMSIS-DAP

1. 添加 rules 文件
    ```
    # CMSIS-DAP compatible adapters
    ATTRS{product}=="*CMSIS-DAP*", MODE="660", GROUP="plugdev", TAG+="uaccess"
    ```

2. `.vscode/c_cpp_properties.json` 增加定义

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

3. 添加`flash` 指令: 在 `MakeFile` clean之后添加

    ```makefile
    #######################################
    # flash
    #######################################
    flash:
    	-openocd -f interface/cmsis-dap.cfg -f target/stm32f1x.cfg -c "program $(BUILD_DIR)/${TARGET}.bin exit 0x08000000"
    ```

4. 编译: `make` , 下载: `make flash`