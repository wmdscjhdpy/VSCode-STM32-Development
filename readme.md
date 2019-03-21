# 在Ubuntu下使用VsCode进行STM32的开发和调试
当前配置信息：使用STM32F405RG系列芯片，使用STM32CubeMX进行代码生成，使用Jlink进行调试。添加对FreeFTOS的支持。如果需要进行其他芯片或工具的开发，请按照说明文档修改参数。

## 准备环境

### 必须环境
1. VSCode 其中需要C/C++,gnu-debugger,ARM 插件
2. arm-none-eabi-gcc 编译器，最好添加到环境变量里
3. Jlink驱动
4. STM32CubeMX+JRE(可选)

### Windows下的准备环境（子系统方向）
1. WSL Windows下的Ubuntu子系统
2. 在WSL中安装make以及arm-none-eabi-gcc(注意不能直接apt-get install 在18.04版本下该编译器对STM32有bug 应在官网下载 下载解压到自定义目录，添加环境变量)
3. 设置WSL为VSCode的默认运行环境,在settings.json中输入
```json
    "terminal.external.windowsExec": "C:\\WINDOWS\\System32\\bash.exe",
    "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\bash.exe"
```

## 使用步骤
1. 在您的工程文件夹中使用STM32CubeMX选择makefile方式生成代码
2. 将本工程的所有文件复制到您的工程文件夹中 如果工程代码中含有C++代码，请使用本仓库的makefile，否则建议使用cube生成的代码
3. 打开makefile文件，将Target的值更改为STM32Target,同时在编译文件目录中添加自己的源文件和包含文件夹，更改芯片型号等操作
4. 使用VSCode打开您的工程文件夹，可以进行编译，下载和调试了

## 直接兼容Keil的方法
1. 需要startup_stm32fxxx.s 文件，因为keil和makefile的startup的注释格式不一样，因此建议备份keil下的.s和gcc下的.s文件以便切换使用(如果需要的话)
2. 需要STM32Fxxx.ld 文件，keil是没有这个文件的


## 当前还未解决的问题
1. 在windows端下的18.04子系统的apt内的arm-none-eabi-gcc不能够进行链接，链接会出现问题，因此需要自行下载最新的编译器
2. 欢迎提交issue反馈问题