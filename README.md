## 简要说明 ##
   以下开发环境的使用内容包括了乐鑫官方 idf 以及 pycom  micropython idf 所需的编译及烧录的全部步骤，请根据自己的选择的idf的不同，正确选择所需的步骤。

# 1. 下载MSYS2环境

可以从乐鑫的官网下载 [MSYS2 all-in-one](https://dl.espressif.com/dl/esp32_win32_msys2_environment_and_toolchain-20170111.zip) 的压缩包，解压缩到C盘的根目录。

# 2. 下载 ESP-IDF 或者 pycom-esp-idf

(1) clone [esp-idf](https://github.com/espressif/esp-idf) 时，用 `git clone --recursive https://github.com/espressif/esp-idf.git`，这样可以把蓝牙协议栈，wifi协议栈等库也同时更新。

(2) (micropython idf 所需) clone [pycom-esp-idf](https://github.com/pycom/pycom-esp-idf) 需要运行

`git clone https://github.com/pycom/pycom-esp-idf`

`git submodule update --init`
目的同样是为了更新蓝牙协议栈，wifi协议栈等其它库文件。

# 3. 配置MYSY2 #

(1) 修改 `msys32\etc\pacman.d` 下的三个下载源的配置。具体可以见文件夹 pacman.d，该修改是把MSYS2一些库的更新源设置为了国内的镜像服务器。

(2) 修改 `C:\msys32\etc\profile.d` 目录下 esp32_toolchain.sh文件，设置esp-idf的路径。例如:

`export IDF_PATH="G:/project/micropython/myan/pycom-esp-idf"`

# 4.下载工程文件 #

(1) esp-idf的工程可以直接使用目录下的examples里面的例子

(2) (micropython idf 所需) clone micropython的工程目录在

`git clone https://github.com/pycom/pycom-micropython`

(3) esp-idf的工程使用  `make menuconfig` 配置串口为 /COMx

(4) (micropython idf 所需) pycom-micropython的工程通过修改 `pycom-micropython\esp32\application.mk` 里面的 ESPPORT的值来配置串口

    ESPPORT ?= /COMx

# 5. 编译及烧录 #

(1) esp-idf的工程使用 `make flash`

(2) (micropython idf 所需) pycom-micropython的工程使用 `make BOARD=WIPY flash`

