# 安装GStreamer

## 版本

|文档版本|修改人|修改内容简介|
|-|-|-|
|0_0_0|郑必城|初步完成文档编写|
|0_0_1|郑必城|更新gstreamer的rkmmp插件安装过程|


## 安装Gstreamer

输入以下命令安装GStreamer以及基础的插件

```Bash
sudo apt-get install libgstreamer1.0-0 \
                      gstreamer1.0-plugins-base \
                      gstreamer1.0-plugins-good \
                      gstreamer1.0-plugins-bad \
                      gstreamer1.0-plugins-ugly \
                      gstreamer1.0-libav \
                      gstreamer1.0-tools \
                      gstreamer1.0-x \
                      gstreamer1.0-alsa \
                      gstreamer1.0-gl \
                      gstreamer1.0-gtk3 \
                      gstreamer1.0-qt5 \
                      gstreamer1.0-pulseaudio \
                      libgstreamer1.0-dev \
                      libgstreamer-plugins-base1.0-dev \
                      gstreamer1.0-tools
```

输入以下命令测试是否安装成功

```Bash
gst-launch-1.0 -v v4l2src device=/dev/video9 !  glimagesink
```

## 安装GStreamer rkmpp插件

首先需要安装依赖库

```Bash
sudo apt-get install build-essential
sudo apt-get install libgl1-mesa-dev
sudo apt-get install meson
sudo apt-get install rockchip-mpp
sudo apt-get install rockchip-mpp-dev
sudo apt-get install librga-dev
sudo apt-get install rockchip-rga
sudo apt-get install rockchip-rga-dev
sudo apt-get install librga2

```

然后再编译插件

```Bash
cd gstreamer-rgaconvert-main
ninja -C build
```

最后拷贝动态库到gstreamer插件目录

```Bash
cd build/gst
sudo cp rkximage/libgstrkximage.so /lib/aarch64-linux-gnu/gstreamer-1.0/
sudo cp rockchipmpp/libgstrockchipmpp.so /lib/aarch64-linux-gnu/gstreamer-1.0/
```

输入以下命令查看是否成功安装插件

```Bash
gst-inspect-1.0 | grep rockchipmpp
```